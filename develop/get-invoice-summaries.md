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
# <a name="get-invoice-summaries"></a><span data-ttu-id="5c40e-103">Získání přehledu faktur</span><span class="sxs-lookup"><span data-stu-id="5c40e-103">Get invoice summaries</span></span>

<span data-ttu-id="5c40e-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="5c40e-104">**Applies to:**</span></span>

- <span data-ttu-id="5c40e-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="5c40e-105">Partner Center</span></span>
- <span data-ttu-id="5c40e-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="5c40e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5c40e-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="5c40e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5c40e-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5c40e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5c40e-109">Můžete použít **InvoiceSummaries** k načtení souhrnu faktury, který ukazuje zůstatek a celkové poplatky za periodické i jednorázové poplatky.</span><span class="sxs-lookup"><span data-stu-id="5c40e-109">You can use the **InvoiceSummaries** to retrieve an invoice summary which shows the balance and total charges of both recurring and one-time charges.</span></span> <span data-ttu-id="5c40e-110">Prostředek **InvoiceSummaries** obsahuje souhrn faktury pro každý typ měny.</span><span class="sxs-lookup"><span data-stu-id="5c40e-110">The **InvoiceSummaries** resource contains an invoice summary for each currency type.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c40e-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5c40e-111">Prerequisites</span></span>

- <span data-ttu-id="5c40e-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5c40e-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5c40e-113">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="5c40e-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5c40e-114">Platný identifikátor faktury</span><span class="sxs-lookup"><span data-stu-id="5c40e-114">A valid invoice identifier.</span></span>

## <a name="c"></a><span data-ttu-id="5c40e-115">C\#</span><span class="sxs-lookup"><span data-stu-id="5c40e-115">C\#</span></span>

<span data-ttu-id="5c40e-116">Načtení kolekce [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) obsahující [**InvoiceSummary**](invoice-resources.md#invoicesummary) pro každý typ měny:</span><span class="sxs-lookup"><span data-stu-id="5c40e-116">To retrieve an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) collection that contains an [**InvoiceSummary**](invoice-resources.md#invoicesummary) for each currency type:</span></span>

1. <span data-ttu-id="5c40e-117">Pomocí kolekce **IAggregatePartner. faktur** volejte vlastnost **souhrny** .</span><span class="sxs-lookup"><span data-stu-id="5c40e-117">Use your **IAggregatePartner.Invoices** collection to call the **Summaries** property.</span></span>

2. <span data-ttu-id="5c40e-118">Zavolejte metodu **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="5c40e-118">Call the **Get()** method.</span></span>
3. <span data-ttu-id="5c40e-119">Chcete-li získat rovnováhu jednotlivého [**InvoiceSummary**](invoice-resources.md#invoicesummary), přístup k vlastnosti **BalanceAmount** pro daného člena kolekce.</span><span class="sxs-lookup"><span data-stu-id="5c40e-119">To get the balance of an individual [**InvoiceSummary**](invoice-resources.md#invoicesummary), access the **BalanceAmount** property for that member of the collection.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

<span data-ttu-id="5c40e-120">Další informace naleznete v následujícím ukázkovém kódu:</span><span class="sxs-lookup"><span data-stu-id="5c40e-120">For more information, see the following example code:</span></span>

- <span data-ttu-id="5c40e-121">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5c40e-121">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="5c40e-122">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="5c40e-122">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="5c40e-123">Třída: **GetInvoiceSummaries.cs**</span><span class="sxs-lookup"><span data-stu-id="5c40e-123">Class: **GetInvoiceSummaries.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="5c40e-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="5c40e-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5c40e-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="5c40e-125">Request syntax</span></span>

| <span data-ttu-id="5c40e-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="5c40e-126">Method</span></span>  | <span data-ttu-id="5c40e-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5c40e-127">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="5c40e-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="5c40e-128">**GET**</span></span> | <span data-ttu-id="5c40e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/summaries HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5c40e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span></span>     |

#### <a name="uri-parameter"></a><span data-ttu-id="5c40e-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5c40e-130">URI parameter</span></span>

<span data-ttu-id="5c40e-131">Žádné</span><span class="sxs-lookup"><span data-stu-id="5c40e-131">None.</span></span>

### <a name="request-headers"></a><span data-ttu-id="5c40e-132">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5c40e-132">Request headers</span></span>

<span data-ttu-id="5c40e-133">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5c40e-133">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5c40e-134">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="5c40e-134">Request body</span></span>

<span data-ttu-id="5c40e-135">Žádné</span><span class="sxs-lookup"><span data-stu-id="5c40e-135">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5c40e-136">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="5c40e-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="5c40e-137">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5c40e-137">REST response</span></span>

<span data-ttu-id="5c40e-138">V případě úspěchu tato metoda vrátí prostředek [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="5c40e-138">If successful, this method returns an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5c40e-139">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="5c40e-139">Response success and error codes</span></span>

<span data-ttu-id="5c40e-140">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5c40e-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5c40e-141">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="5c40e-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5c40e-142">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5c40e-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5c40e-143">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="5c40e-143">Response example</span></span>

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
