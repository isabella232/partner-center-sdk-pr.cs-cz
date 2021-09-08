---
title: Vytvoření objednávky zákazníka
description: Naučte se používat Partnerské centrum API k vytvoření objednávky pro zákazníka. Článek obsahuje požadavky, kroky a příklady.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 232888ee798b4579246bbfd787e049f9f6e2e8a3
ms.sourcegitcommit: 5f27733d7c984c29f71c8b9c8ba5f89753eeabc4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2021
ms.locfileid: "123557248"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Vytvoření objednávky pro zákazníka pomocí Partnerské centrum API

**Platí pro:** Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government

Vytvoření objednávky **produktů rezervovaných instancí virtuálních** počítače Azure se *vztahuje pouze* na:

- Partnerské centrum

Informace o tom, co je aktuálně k dispozici k prodeji, najdete v tématu Nabídky partnerů [v Cloud Solution Provider programu](/partner-center/csp-offers).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka nevíte, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor nabídky.

## <a name="c"></a>C\#

Vytvoření objednávky pro zákazníka:

1. Vytvořte instanci objektu [**Order**](order-resources.md) a nastavte vlastnost **ReferenceCustomerID** na ID zákazníka pro zaznamenání zákazníka.

2. Vytvořte seznam objektů [**OrderLineItem**](order-resources.md#orderlineitem) a přiřaďte ho k vlastnosti **LineItems** objednávky. Každá položka řádku objednávky obsahuje informace o nákupu pro jednu nabídku. Musíte mít alespoň jednu řádkovou položku objednávky.

3. Získání rozhraní pro řazení operací. Nejprve zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a identifikujte zákazníka. Dále načtěte rozhraní z [**vlastnosti Orders.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)

4. Zavolejte [**metodu Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) a předejte [**objekt Order.**](order-resources.md)

5. Pokud chcete dokončit ověření a zahrnout další prodejce, projděte si následující ukázky požadavků a odpovědí:

### <a name="request-example"></a>Příklad požadavku

``` csharp
{
    "PartnerOnRecordAttestationAccepted":true, 
    "lineItems": [
        {
            "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "quantity": 1,
            "lineItemNumber": 0,
            "PartnerIdOnRecord": "873452",
            "AdditionalPartnerIdsOnRecord":["4847383","873452"]
        }
    ],
    "billingCycle": "monthly"
}
```

### <a name="response-example"></a>Příklad odpovědi

``` csharp
{
    "id": "5cf72f146967",
    "alternateId": "5cf72f146967",
    "referenceCustomerId": "f81d98dd-c2f4-499e-a194-5619e260344e",
    "billingCycle": "monthly",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "subscriptionId": "fcddfa52-1da8-4529-d347-50ea51e1e7be",
            "termDuration": "P1M",
            "transactionType": "New",
            "friendlyName": "AI Builder Capacity add-on",
            "quantity": 1,
            "partnerIdOnRecord": "873452",
            "additionalPartnerIdsOnRecord": [
                "4847383",
                "873452"
            ],
            "links": {
                "product": {
                    "uri": "/products/CFQ7TTC0LH0Z?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/CFQ7TTC0LH0Z/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/CFQ7TTC0LH0Z/skus/0001/availabilities/CFQ7TTC0K18P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2021-08-17T18:13:11.3122226Z",
    "status": "pending",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {},
    "attributes": {
        "objectType": "Order"
    }
}

```

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** CreateOrder.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **PŘÍSPĚVEK** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka použijte následující parametr cesty.

| Název        | Typ   | Vyžadováno | Popis                                                |
|-------------|--------|----------|------------------------------------------------------------|
| id zákazníka | řetězec | Yes      | Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

#### <a name="order"></a>Objednávka

Tato tabulka popisuje [vlastnosti Order](order-resources.md) v textu požadavku.

| Vlastnost             | Typ                        | Vyžadováno                        | Popis                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | řetězec                      | No                              | Identifikátor objednávky zadaný po úspěšném vytvoření objednávky.   |
| referenčníCustomerId  | řetězec                      | No                              | Identifikátor zákazníka. |
| billingCycle         | řetězec                      | No                              | Určuje frekvenci, s jakou se partner účtuje za tuto objednávku. Podporované hodnoty jsou názvy členů, které najdete v [části BillingCycleType](product-resources.md#billingcycletype). Výchozí hodnota je "Měsíčně" nebo "OneTime" při vytváření objednávky. Toto pole se použije při úspěšném vytvoření objednávky. |
| položky řádku            | pole prostředků [OrderLineItem](order-resources.md#orderlineitem) | Yes      | Itemized list of the offers the customer is purchasing including the quantity.        |
| currencyCode         | řetězec                      | No                              | Jen pro čtení. Měna použitá při zadávání objednávky. Použije se při úspěšném vytvoření objednávky.           |
| datum vytvoření         | datetime                    | No                              | Jen pro čtení. Datum vytvoření objednávky ve formátu data a času. Použije se při úspěšném vytvoření objednávky.                                   |
| status               | řetězec                      | No                              | Jen pro čtení. Stav objednávky  Podporované hodnoty jsou názvy členů, které najdete v [OrderStatus](order-resources.md#orderstatus).        |
| Odkazy                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | Propojení prostředků odpovídající objednávce |
| atributy           | [ResourceAttributes](utility-resources.md#resourceattributes) | No                              | Atributy metadat odpovídající pořadí. |
| PartnerOnRecordAttestationAccepted | Logická hodnota | Yes | Potvrdí dokončení ověření identity. |


#### <a name="orderlineitem"></a>OrderLineItem

Tato tabulka popisuje vlastnosti [OrderLineItem](order-resources.md#orderlineitem) v textu požadavku.

>[!NOTE]
>PartnerIdOnRecord by měla být poskytnuta pouze v případě, že nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce. Slouží k ukládání Microsoft Partner Network ID nepřímých prodejců (nikdy ID nepřímého poskytovatele).

| Název                 | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Yes      | Každá položka řádku v kolekci získá jedinečné číslo řádku, počítáno od 0 do Count-1.                                                                                                                                                 |
| Hodnotami OfferId              | řetězec | Yes      | Identifikátor nabídky                                                                                                                                                                                                                      |
| subscriptionId       | řetězec | No       | Identifikátor předplatného.                                                                                                                                                                                                               |
| parentSubscriptionId | řetězec | No       | Nepovinný parametr. ID nadřazeného odběru v nabídce doplňku Platí pouze pro opravu.                                                                                                                                                     |
| friendlyName         | řetězec | No       | Nepovinný parametr. Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost.                                                                                                                                              |
| quantity             | int    | Yes      | Počet licencí pro předplatné založené na licencích.                                                                                                                                                                                   |
| partnerIdOnRecord    | řetězec | No       | Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **nepřímého prodejce** (nikdy ID nepřímého poskytovatele). To zajišťuje správné účetnictví pro motivaci. |
| provisioningContext  | Řetězec<slovníku, řetězec>                | No       |  Informace požadované pro zřizování některých položek v katalogu. Vlastnost provisioningVariables v SKU indikuje, které vlastnosti jsou požadovány pro konkrétní položky v katalogu.                  |
| odkazy                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | No       |  Jen pro čtení. Odkazy na prostředky odpovídající položce řádku objednávky.  |
| atributy           | [ResourceAttributes](utility-resources.md#resourceattributes) | No       | Atributy metadat odpovídající OrderLineItem. |
| renewsTo             | Pole objektů                          | No    |Pole prostředků [RenewsTo](order-resources.md#renewsto)                                                                            |
| AttestationAccepted             | bool                 | No   |  Označuje smlouvu o nabídkách nebo podmínkách SKU. Vyžaduje se jenom pro nabídky nebo skladové položky, kde SkuAttestationProperties nebo OfferAttestationProperties enforceAttestation má hodnotu true.          |
| AdditionalPartnerIdsOnRecord | Řetězec | No | Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **dalšího nepřímého prodejce** (nikdy ID nepřímého poskytovatele). Pro tyto další prodejce nelze použít pobídky. Je možné zadat maximálně 5 nepřímých prodejců. Toto jsou pouze partneři, kteří se týkají v zemích EU/ESVO. |

##### <a name="renewsto"></a>RenewsTo

Tato tabulka popisuje vlastnosti [RenewsTo](order-resources.md#renewsto) v textu požadavku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | ISO 8601 představuje dobu trvání období obnovy. Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok). |

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu metoda vrátí zdroj [objednávky](order-resources.md) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
