---
title: Získat fakturu podle ID
description: Načte danou fakturu pomocí ID faktury.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 17880265d06e8e5eaacc5470d83c49defd10ad51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766657"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="27b1e-103">Získat fakturu podle ID</span><span class="sxs-lookup"><span data-stu-id="27b1e-103">Get invoice by ID</span></span>

<span data-ttu-id="27b1e-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="27b1e-104">**Applies to:**</span></span>

- <span data-ttu-id="27b1e-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="27b1e-105">Partner Center</span></span>
- <span data-ttu-id="27b1e-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="27b1e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="27b1e-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="27b1e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="27b1e-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="27b1e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="27b1e-109">Načte danou fakturu pomocí ID faktury.</span><span class="sxs-lookup"><span data-stu-id="27b1e-109">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27b1e-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="27b1e-110">Prerequisites</span></span>

- <span data-ttu-id="27b1e-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="27b1e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="27b1e-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="27b1e-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="27b1e-113">Platné ID faktury</span><span class="sxs-lookup"><span data-stu-id="27b1e-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="27b1e-114">C\#</span><span class="sxs-lookup"><span data-stu-id="27b1e-114">C\#</span></span>

<span data-ttu-id="27b1e-115">Získání faktury podle ID:</span><span class="sxs-lookup"><span data-stu-id="27b1e-115">To get an invoice by ID:</span></span>

1. <span data-ttu-id="27b1e-116">Použijte svou kolekci **IPartner. faktur** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="27b1e-116">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="27b1e-117">Zavolejte metody **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="27b1e-117">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="27b1e-118">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="27b1e-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="27b1e-119">**Projekt**: PartnerSDK. FeatureSample **Třída**: GetInvoice.cs</span><span class="sxs-lookup"><span data-stu-id="27b1e-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="27b1e-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="27b1e-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="27b1e-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="27b1e-121">Request syntax</span></span>

| <span data-ttu-id="27b1e-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="27b1e-122">Method</span></span>  | <span data-ttu-id="27b1e-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="27b1e-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="27b1e-124">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="27b1e-124">**GET**</span></span> | <span data-ttu-id="27b1e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="27b1e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="27b1e-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="27b1e-126">URI parameter</span></span>

<span data-ttu-id="27b1e-127">K získání faktury použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="27b1e-127">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="27b1e-128">Název</span><span class="sxs-lookup"><span data-stu-id="27b1e-128">Name</span></span>           | <span data-ttu-id="27b1e-129">Typ</span><span class="sxs-lookup"><span data-stu-id="27b1e-129">Type</span></span>       | <span data-ttu-id="27b1e-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="27b1e-130">Required</span></span> | <span data-ttu-id="27b1e-131">Popis</span><span class="sxs-lookup"><span data-stu-id="27b1e-131">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="27b1e-132">**ID faktury**</span><span class="sxs-lookup"><span data-stu-id="27b1e-132">**invoice-id**</span></span> | <span data-ttu-id="27b1e-133">**řetezce**</span><span class="sxs-lookup"><span data-stu-id="27b1e-133">**string**</span></span> | <span data-ttu-id="27b1e-134">Yes</span><span class="sxs-lookup"><span data-stu-id="27b1e-134">Yes</span></span>      | <span data-ttu-id="27b1e-135">Hodnota je **ID faktury** , které prodejci umožňuje filtrovat výsledky dané faktury.</span><span class="sxs-lookup"><span data-stu-id="27b1e-135">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="27b1e-136">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="27b1e-136">Request headers</span></span>

<span data-ttu-id="27b1e-137">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="27b1e-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="27b1e-138">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="27b1e-138">Request body</span></span>

<span data-ttu-id="27b1e-139">Žádné</span><span class="sxs-lookup"><span data-stu-id="27b1e-139">None</span></span>

### <a name="request-example"></a><span data-ttu-id="27b1e-140">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="27b1e-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="27b1e-141">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="27b1e-141">REST response</span></span>

<span data-ttu-id="27b1e-142">V případě úspěchu tato metoda vrátí prostředek [faktury](invoice-resources.md#invoice) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="27b1e-142">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="27b1e-143">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="27b1e-143">Response success and error codes</span></span>

<span data-ttu-id="27b1e-144">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="27b1e-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="27b1e-145">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="27b1e-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="27b1e-146">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="27b1e-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="27b1e-147">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="27b1e-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 676
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
Date: Thu, 24 Mar 2016 05:22:14 GMT

{
    "id": "G000024135",
    "invoiceDate": "2018-02-08T22:40:37.5897767Z",
    "billingPeriodStartDate": "2018-02-01T22:40:37.5897767Z",
    "billingPeriodEndDate": "2018-02-28T22:40:37.5897767Z",
    "totalCharges": 2076.63,
    "paidAmount": 0,
    "currencyCode": "USD",
    "currencySymbol": "$",
    "pdfDownloadLink": "/invoices/G000024135/documents/statement",
    "taxReceipts": [
        {
            "id": "123456",
            "taxReceiptPdfDownloadLink": "/invoices/G000024135/receipts/123456/documents/statement"
        }
    ],
    "invoiceDetails": [
        {
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024135/lineitems/OneTime/BillingLineItems",
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
    "invoiceType": "OneTime",
    "links": {
        "self": {
            "uri": "/invoices/OneTime-G000024135",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Invoice"
    }
}
```
