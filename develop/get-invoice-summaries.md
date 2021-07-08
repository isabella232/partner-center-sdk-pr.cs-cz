---
title: Získání přehledu faktur
description: K zobrazení zůstatku a celkovému počtu poplatků za periodické i jednorázové poplatky můžete použít prostředek souhrnu faktury pro každý typ měny.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: fb6ff839c56c7b0b77a9904abf05d95ca0500b00
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549106"
---
# <a name="get-invoice-summaries"></a><span data-ttu-id="a9fb5-103">Získání přehledu faktur</span><span class="sxs-lookup"><span data-stu-id="a9fb5-103">Get invoice summaries</span></span>

<span data-ttu-id="a9fb5-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a9fb5-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a9fb5-105">Můžete použít **InvoiceSummaries** k načtení souhrnu faktury, který ukazuje zůstatek a celkové poplatky za periodické i jednorázové poplatky.</span><span class="sxs-lookup"><span data-stu-id="a9fb5-105">You can use the **InvoiceSummaries** to retrieve an invoice summary that shows the balance and total charges of both recurring and one-time charges.</span></span> <span data-ttu-id="a9fb5-106">Prostředek **InvoiceSummaries** obsahuje souhrn faktury pro každý typ měny.</span><span class="sxs-lookup"><span data-stu-id="a9fb5-106">The **InvoiceSummaries** resource contains an invoice summary for each currency type.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9fb5-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a9fb5-107">Prerequisites</span></span>

- <span data-ttu-id="a9fb5-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a9fb5-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a9fb5-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="a9fb5-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="a9fb5-110">Platný identifikátor faktury</span><span class="sxs-lookup"><span data-stu-id="a9fb5-110">A valid invoice identifier.</span></span>

## <a name="c"></a><span data-ttu-id="a9fb5-111">C\#</span><span class="sxs-lookup"><span data-stu-id="a9fb5-111">C\#</span></span>

<span data-ttu-id="a9fb5-112">Načtení kolekce [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) obsahující [**InvoiceSummary**](invoice-resources.md#invoicesummary) pro každý typ měny:</span><span class="sxs-lookup"><span data-stu-id="a9fb5-112">To retrieve an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) collection that contains an [**InvoiceSummary**](invoice-resources.md#invoicesummary) for each currency type:</span></span>

1. <span data-ttu-id="a9fb5-113">Pomocí kolekce **IAggregatePartner. faktur** volejte vlastnost **souhrny** .</span><span class="sxs-lookup"><span data-stu-id="a9fb5-113">Use your **IAggregatePartner.Invoices** collection to call the **Summaries** property.</span></span>

2. <span data-ttu-id="a9fb5-114">Zavolejte metodu **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="a9fb5-114">Call the **Get()** method.</span></span>
3. <span data-ttu-id="a9fb5-115">Chcete-li získat rovnováhu jednotlivého [**InvoiceSummary**](invoice-resources.md#invoicesummary), přístup k vlastnosti **BalanceAmount** pro daného člena kolekce.</span><span class="sxs-lookup"><span data-stu-id="a9fb5-115">To get the balance of an individual [**InvoiceSummary**](invoice-resources.md#invoicesummary), access the **BalanceAmount** property for that member of the collection.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

<span data-ttu-id="a9fb5-116">Další informace naleznete v následujícím ukázkovém kódu:</span><span class="sxs-lookup"><span data-stu-id="a9fb5-116">For more information, see the following example code:</span></span>

- <span data-ttu-id="a9fb5-117">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a9fb5-117">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a9fb5-118">Project: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="a9fb5-118">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="a9fb5-119">Třída: **GetInvoiceSummaries. cs**</span><span class="sxs-lookup"><span data-stu-id="a9fb5-119">Class: **GetInvoiceSummaries.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="a9fb5-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="a9fb5-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a9fb5-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="a9fb5-121">Request syntax</span></span>

| <span data-ttu-id="a9fb5-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="a9fb5-122">Method</span></span>  | <span data-ttu-id="a9fb5-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a9fb5-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="a9fb5-124">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="a9fb5-124">**GET**</span></span> | <span data-ttu-id="a9fb5-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/summaries HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a9fb5-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span></span>     |

#### <a name="uri-parameter"></a><span data-ttu-id="a9fb5-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a9fb5-126">URI parameter</span></span>

<span data-ttu-id="a9fb5-127">Žádné</span><span class="sxs-lookup"><span data-stu-id="a9fb5-127">None.</span></span>

### <a name="request-headers"></a><span data-ttu-id="a9fb5-128">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a9fb5-128">Request headers</span></span>

<span data-ttu-id="a9fb5-129">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a9fb5-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a9fb5-130">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a9fb5-130">Request body</span></span>

<span data-ttu-id="a9fb5-131">Žádné</span><span class="sxs-lookup"><span data-stu-id="a9fb5-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a9fb5-132">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a9fb5-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a9fb5-133">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a9fb5-133">REST response</span></span>

<span data-ttu-id="a9fb5-134">V případě úspěchu tato metoda vrátí prostředek [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="a9fb5-134">If successful, this method returns an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a9fb5-135">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="a9fb5-135">Response success and error codes</span></span>

<span data-ttu-id="a9fb5-136">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a9fb5-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a9fb5-137">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="a9fb5-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a9fb5-138">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a9fb5-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a9fb5-139">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a9fb5-139">Response example</span></span>

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
