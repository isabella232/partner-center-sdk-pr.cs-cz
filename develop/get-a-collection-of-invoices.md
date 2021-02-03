---
title: Získání kolekce faktur
description: Jak načíst kolekci faktur partnera.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: f56c3de8dd227f573921e5b969c2217c2f743a21
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766847"
---
# <a name="get-a-collection-of-invoices"></a>Získání kolekce faktur

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak načíst kolekci faktur partnera.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

## <a name="c"></a>C\#

Chcete-li získat kolekci všech dostupných faktur, použijte vlastnost [**faktur**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) k získání rozhraní k fakturaci operace a poté zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) pro načtení kolekce.

Chcete-li získat stránkované kolekce faktur, nejprve zavolejte metodu [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) a předejte jí velikost stránky pro vytvoření objektu [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) . Dále pomocí vlastnosti [**faktury**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) Získejte rozhraní k fakturaci operací a pak předejte objekt IQuery do [**dotazu**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) nebo metody [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) k odeslání požadavku a získání první stránky.

Dále pomocí vlastnosti [**enumerátory**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) Získejte rozhraní pro kolekci podporovaných enumerátorů kolekcí prostředků a potom zavolejte [**faktury. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) k vytvoření enumerátoru pro procházení kolekce faktur. Nakonec použijte enumerátor pro načtení a práci s každou stránkou faktury, jak je znázorněno v následujícím příkladu kódu. Každé volání metody [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) pošle požadavek na další stránku faktury na základě velikosti stránky.

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged)
                 ? partnerOperations.Invoices.Get()
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;

    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}",
            lineCounter++,
            i.Id,
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

Trochu odlišný příklad naleznete v tématu **Ukázka**: [aplikace test Console](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetPagedInvoices.cs

> [!NOTE] 
> Stejné rozhraní API se používá pro všechny moderní komerční nákupy i pro licence na 145p a Office. Velikost a posun se považují jenom za starší faktury. U všech moderních komerčních nákupů se hodnota PageSize & posunu bude ignorovat.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices? size = {size} &posun = {offset} HTTP/1.1  |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

Při vytváření žádosti použijte následující parametry dotazu.

| Název   | Typ | Vyžadováno | Popis                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| size   | int  | No       | Počet fakturovaných prostředků, které se mají vrátit v odpovědi Tento parametr je volitelný. |
| posun | int  | No       | Index založený na nule první faktury, která se má vrátit                                   |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci zdrojů [faktury](invoice-resources.md#invoice) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "taxReceipts": [
                {
                    "id": "123456",
                    "taxReceiptPdfDownloadLink": "/invoices/D02005YFHI/receipts/123456/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "documentType": "invoice",
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "taxReceipts": [
                {
                    "id": "234567",
                    "taxReceiptPdfDownloadLink": "/invoices/G000024130/receipts/234567/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
