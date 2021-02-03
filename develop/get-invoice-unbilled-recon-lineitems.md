---
title: Získat neúčtované položky řádku odsouhlasení faktury
description: Pomocí rozhraní API partnerského centra můžete získat souhrn nefakturovaných podrobností o položkách řádků odsouhlasení pro zadané období.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: ff69798ddfd91fca817ec0d047bf407f326066c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767035"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a>Získat neúčtované položky řádku odsouhlasení faktury

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Následující metody můžete použít k získání kolekce podrobností pro nefakturovatelné položky řádku faktury (známé také jako otevřené položky fakturačního řádku).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- Identifikátor faktury Určuje fakturu, pro kterou se mají načíst položky řádku.

## <a name="c"></a>C\#

Chcete-li získat položky řádku pro určenou fakturu, načtěte objekt faktury:

1. Zavolejte metodu [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , která získá rozhraní k fakturaci operace pro zadanou fakturu.

2. Pro načtení objektu faktury zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) .

Objekt faktury obsahuje všechny informace o zadané faktuře:

- **Zprostředkovatel** identifikuje zdroj nefakturovaných podrobných informací (například **jednorázová**).

- **InvoiceLineItemType** určuje typ (například **BillingLineItem**).

Získání kolekce položek řádků, které odpovídají instanci **InvoiceDetail** :

1. Předejte BillingProvider a InvoiceLineItemType instance do metody [**podle**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .

2. Zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) pro načtení přidružených položek řádků.

3. Vytvořte enumerátor pro procházení kolekce. Příklad naleznete v následujícím ukázkovém kódu.

Následující vzorový kód používá smyčku **foreach** ke zpracování kolekce **InvoiceLineItems** . Pro každou **InvoiceLineItemType** se načte samostatná kolekce položek čáry.

``` csharp
// IAggregatePartner partnerOperations;
// string currencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type OneTimeInvoiceLineItem
        if (item is OneTimeInvoiceLineItem)
        {
            Type t = typeof(OneTimeInvoiceLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

Podobný příklad najdete v těchto tématech:

- Ukázka: [aplikace testů konzoly](console-test-app.md)
- Projekt: **ukázky sady SDK pro partnerských Center**
- Třída: **GetUnBilledReconLineItemsPaging.cs**

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

V závislosti na vašem případu použití můžete pro požadavek REST použít následující syntaxe. Další informace najdete v popisech jednotlivých syntaxí.

 | Metoda  | Identifikátor URI žádosti            | Popis případu použití syntaxe                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = jednorázová&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &perioda = {period} HTTP/1.1                              | Pomocí této syntaxe vrátíte úplný seznam všech položek řádku pro danou fakturu. |
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = jednorázová&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} HTTP/1.1  | Pro velké faktury použijte tuto syntaxi se zadanou velikostí a 0 posunem na základě posunutí stránkovaného seznamu položek řádků. |
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = jednorázová&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} &SeekOperation = Next                               | Tuto syntaxi použijte k získání další stránky položek řádku odsouhlasení pomocí `seekOperation = "Next"` . |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Při vytváření žádosti použijte následující identifikátor URI a parametry dotazu.

| Název                   | Typ   | Vyžadováno | Popis                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| ID faktury             | řetězec | Yes      | Řetězec, který identifikuje fakturu. K získání nefakturovaných odhadů použijte příkaz unfakturováno. |
| Zprostředkovatel               | řetězec | Yes      | Zprostředkovatel: "jednorázová".                                                |
| faktura-line-Item-Type | řetězec | Yes      | Typ podrobností o faktuře: "BillingLineItems".               |
| hasPartnerEarnedCredit | bool   | No       | Hodnota, která označuje, zda se mají vracet položky řádku s použitím realizovaného kreditu. Poznámka: Tento parametr bude použit pouze v případě, že typ zprostředkovatele je jednorázová a InvoiceLineItemType je UsageLineItems.
| currencyCode           | řetězec | Yes      | Kód měny pro nefakturovatelné položky řádku                                  |
| period                 | řetězec | Yes      | Období pro nefakturované rekognoskaci. Příklad: Current, Previous.                      |
| size                   | číslo | No       | Maximální počet položek, které se mají vrátit. Výchozí velikost je 2000.                     |
| seekOperation          | řetězec | No       | Nastavte seekOperation = Next pro získání další stránky rekognoskaci položek řádků.                |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje odpověď kolekci podrobností položky řádku.

*Pro položku řádku **ChargeType** je hodnota **Nákup** namapována na hodnotu **New** a **náhrada** hodnoty je namapována na **Canceled**.*

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="request-response-examples"></a>Příklady požadavků a odpovědí

#### <a name="request-response-example-1"></a>Požadavek-odpověď – příklad 1

Následující podrobnosti se vztahují na tento příklad:

- Zprostředkovatel: **jednorázová**
- InvoiceLineItemType: **BillingLineItems**
- Období: **Předchozí**

#### <a name="request-example-1"></a>Příklad žádosti 1

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a>Příklad odpovědi 1

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "HJVtMZMkgQ2miuCiNv0RSr51zQDans0m1",
            "orderDate": "2019-02-04T17:59:52.9460102Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0002",
            "availabilityId": "DZH318Z0BP8B",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Medium Plan",
            "chargeType": "New",
            "unitPrice": 820,
            "effectiveUnitPrice": 820,
            "unitType": "",
            "quantity": 1,
            "subtotal": 820,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-9cf0-4a1f-9514-7fcc7fe9d1fe",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 3.1618,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "883d475b-0000-1234-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a>Požadavek-odpověď – příklad 2

Následující podrobnosti se vztahují na tento příklad:

- Zprostředkovatel: **jednorázová**
- InvoiceLineItemType: **BillingLineItems**
- Období: **Předchozí**
- SeekOperation: **Další**

#### <a name="request-example-2"></a>Příklad žádosti 2

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=billinglineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a>Příklad odpovědi 2

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": ""
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

#### <a name="request-example-3"></a>Příklad žádosti 3

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=OneTime&invoiceLineItemType=UsageLineItems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a>Příklad odpovědi 3

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "PartnerName": "testPartner",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "invoiceNumber": "T11ETHHDDD",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "publisherId": "21223810",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "subscriptionDescription": "sub description",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "UsageDate": "2019-02-07T09:22:34.6455294-08:00",
            "MeterType": "type",
            "MeterCategory": "category",
            "MeterId": "21312312312-fdsfsd",
            "MeterSubCategory": "subcategory",
            "MeterName": "meter name",
            "MeterRegion": "meter region",
            "UnitOfMeasure": "11",
            "skuName": "Test WaaS - Large Plan",
            "publisherName": "Test Networks, Inc.",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "discountDetails": "",
            "providerSource": "All",
            "RateOfPartnerEarnedCredit": 0.15,
            "IsPartnerEarnedCreditApplied": true,
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
