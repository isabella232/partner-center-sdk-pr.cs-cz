---
title: Získat fakturu podle ID
description: Načte danou fakturu pomocí ID faktury.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c888786a6b6ca941629bb7aac95227021c37a7fc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549157"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="8538d-103">Získat fakturu podle ID</span><span class="sxs-lookup"><span data-stu-id="8538d-103">Get invoice by ID</span></span>

<span data-ttu-id="8538d-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8538d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8538d-105">Načte danou fakturu pomocí ID faktury.</span><span class="sxs-lookup"><span data-stu-id="8538d-105">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8538d-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8538d-106">Prerequisites</span></span>

- <span data-ttu-id="8538d-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8538d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8538d-108">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="8538d-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="8538d-109">Platné ID faktury</span><span class="sxs-lookup"><span data-stu-id="8538d-109">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="8538d-110">C\#</span><span class="sxs-lookup"><span data-stu-id="8538d-110">C\#</span></span>

<span data-ttu-id="8538d-111">Získání faktury podle ID:</span><span class="sxs-lookup"><span data-stu-id="8538d-111">To get an invoice by ID:</span></span>

1. <span data-ttu-id="8538d-112">Použijte svou kolekci **IPartner. faktur** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="8538d-112">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="8538d-113">Zavolejte metody **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="8538d-113">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="8538d-114">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8538d-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8538d-115">**Project**: PartnerSDK. FeatureSample **třída**: getinvoice. cs</span><span class="sxs-lookup"><span data-stu-id="8538d-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8538d-116">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="8538d-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8538d-117">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="8538d-117">Request syntax</span></span>

| <span data-ttu-id="8538d-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="8538d-118">Method</span></span>  | <span data-ttu-id="8538d-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8538d-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="8538d-120">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="8538d-120">**GET**</span></span> | <span data-ttu-id="8538d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8538d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="8538d-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8538d-122">URI parameter</span></span>

<span data-ttu-id="8538d-123">K získání faktury použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="8538d-123">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="8538d-124">Název</span><span class="sxs-lookup"><span data-stu-id="8538d-124">Name</span></span>           | <span data-ttu-id="8538d-125">Typ</span><span class="sxs-lookup"><span data-stu-id="8538d-125">Type</span></span>       | <span data-ttu-id="8538d-126">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8538d-126">Required</span></span> | <span data-ttu-id="8538d-127">Popis</span><span class="sxs-lookup"><span data-stu-id="8538d-127">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8538d-128">**ID faktury**</span><span class="sxs-lookup"><span data-stu-id="8538d-128">**invoice-id**</span></span> | <span data-ttu-id="8538d-129">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="8538d-129">**string**</span></span> | <span data-ttu-id="8538d-130">Yes</span><span class="sxs-lookup"><span data-stu-id="8538d-130">Yes</span></span>      | <span data-ttu-id="8538d-131">Hodnota je **ID faktury** , které prodejci umožňuje filtrovat výsledky dané faktury.</span><span class="sxs-lookup"><span data-stu-id="8538d-131">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8538d-132">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8538d-132">Request headers</span></span>

<span data-ttu-id="8538d-133">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8538d-133">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8538d-134">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8538d-134">Request body</span></span>

<span data-ttu-id="8538d-135">Žádná</span><span class="sxs-lookup"><span data-stu-id="8538d-135">None</span></span>

### <a name="request-example"></a><span data-ttu-id="8538d-136">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8538d-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="8538d-137">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8538d-137">REST response</span></span>

<span data-ttu-id="8538d-138">V případě úspěchu tato metoda vrátí prostředek [faktury](invoice-resources.md#invoice) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="8538d-138">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8538d-139">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="8538d-139">Response success and error codes</span></span>

<span data-ttu-id="8538d-140">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8538d-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8538d-141">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="8538d-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8538d-142">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8538d-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8538d-143">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8538d-143">Response example</span></span>

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
