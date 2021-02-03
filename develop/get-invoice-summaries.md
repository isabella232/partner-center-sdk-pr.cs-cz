---
title: Získání přehledu faktur
description: K zobrazení zůstatku a celkovému počtu poplatků za periodické i jednorázové poplatky můžete použít prostředek souhrnu faktury pro každý typ měny.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 82cd669117db72e1819d941f48f8ea69b2eddaec
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766656"
---
# <a name="get-invoice-summaries"></a>Získání přehledu faktur

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Můžete použít **InvoiceSummaries** k načtení souhrnu faktury, který ukazuje zůstatek a celkové poplatky za periodické i jednorázové poplatky. Prostředek **InvoiceSummaries** obsahuje souhrn faktury pro každý typ měny.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- Platný identifikátor faktury

## <a name="c"></a>C\#

Načtení kolekce [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) obsahující [**InvoiceSummary**](invoice-resources.md#invoicesummary) pro každý typ měny:

1. Pomocí kolekce **IAggregatePartner. faktur** volejte vlastnost **souhrny** .

2. Zavolejte metodu **Get ()** .
3. Chcete-li získat rovnováhu jednotlivého [**InvoiceSummary**](invoice-resources.md#invoicesummary), přístup k vlastnosti **BalanceAmount** pro daného člena kolekce.

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

Další informace naleznete v následujícím ukázkovém kódu:

- Ukázka: [aplikace testů konzoly](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSample**
- Třída: **GetInvoiceSummaries.cs**

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/summaries HTTP/1.1     |

#### <a name="uri-parameter"></a>Parametr URI

Žádné

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "totalCount": 3,
    "items": [
        {
            "balanceAmount": 751094.39,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
            "lastPaymentDate": "2017-01-01T12:00:00Z",
            "lastPaymentAmount": 1000,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "Recurring",
                    "summary": {
                        "balanceAmount": 202955.87,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2017-02-27T00:00:00Z",
                        "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
                        "lastPaymentDate": "2017-01-01T12:00:00Z",
                        "lastPaymentAmount": 1000,
                        "latestInvoiceDate": "0001-01-01T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                },
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 548138.52,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1230.33,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1230.33,
                        "currencyCode": "CHF",
                        "currencySymbol": "CHF",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1001.12,
            "currencyCode": "EUR",
            "currencySymbol": "€",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1001.12,
                        "currencyCode": "EUR",
                        "currencySymbol": "€",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/summaries",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
