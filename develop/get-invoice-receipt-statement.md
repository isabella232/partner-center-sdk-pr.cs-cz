---
title: Získání příjmových výkazů faktur
description: Načte výpis účtenky faktury pomocí ID faktury a ID účtenky.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac4c8f0b881409dcad3560eefb82d4bb5e877a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446125"
---
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="cc5cc-103">Získání příjmových výkazů faktur</span><span class="sxs-lookup"><span data-stu-id="cc5cc-103">Get invoice receipt statement</span></span>

<span data-ttu-id="cc5cc-104">Načte výpis účtenky faktury pomocí ID faktury a ID účtenky.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-104">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc5cc-105">Tato funkce se vztahuje pouze na příjem daně z Tchaj-wanu.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-105">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc5cc-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="cc5cc-106">Prerequisites</span></span>

- <span data-ttu-id="cc5cc-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cc5cc-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cc5cc-108">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cc5cc-109">Platné ID faktury a odpovídající ID účtenky.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-109">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="cc5cc-110">C\#</span><span class="sxs-lookup"><span data-stu-id="cc5cc-110">C\#</span></span>

<span data-ttu-id="cc5cc-111">Chcete-li získat příkaz pro příjem faktury podle ID počínaje partnerským centrem SDK v 1.12.0, použijte svou kolekci **IPartner.** Invoices a zavolejte metodu **ById ()** s použitím ID faktury, potom zavolejte shromažďování **příjemek** a zavolejte **ById ()** a zavolejte metody **Documents ()** a **Statement ()** pro přístup k příkazu pro příjem faktury.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-111">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="cc5cc-112">Nakonec zavolejte metody **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="cc5cc-112">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="cc5cc-113">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cc5cc-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cc5cc-114">**Project**: PartnerSDK. FeatureSample **třída**: GetInvoiceReceiptStatement. cs</span><span class="sxs-lookup"><span data-stu-id="cc5cc-114">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cc5cc-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="cc5cc-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cc5cc-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="cc5cc-116">Request syntax</span></span>

| <span data-ttu-id="cc5cc-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="cc5cc-117">Method</span></span>  | <span data-ttu-id="cc5cc-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="cc5cc-118">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc5cc-119">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="cc5cc-119">**GET**</span></span> | <span data-ttu-id="cc5cc-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Receipts/{Receipt-ID}/Documents/Statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cc5cc-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cc5cc-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="cc5cc-121">URI parameter</span></span>

<span data-ttu-id="cc5cc-122">K získání příkazu pro příjem faktury použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-122">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="cc5cc-123">Název</span><span class="sxs-lookup"><span data-stu-id="cc5cc-123">Name</span></span>       | <span data-ttu-id="cc5cc-124">Typ</span><span class="sxs-lookup"><span data-stu-id="cc5cc-124">Type</span></span>   | <span data-ttu-id="cc5cc-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="cc5cc-125">Required</span></span> | <span data-ttu-id="cc5cc-126">Popis</span><span class="sxs-lookup"><span data-stu-id="cc5cc-126">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc5cc-127">ID faktury</span><span class="sxs-lookup"><span data-stu-id="cc5cc-127">invoice-id</span></span> | <span data-ttu-id="cc5cc-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="cc5cc-128">string</span></span> | <span data-ttu-id="cc5cc-129">Yes</span><span class="sxs-lookup"><span data-stu-id="cc5cc-129">Yes</span></span>      | <span data-ttu-id="cc5cc-130">Hodnota je ID faktury, které prodejci umožňuje filtrovat výsledky dané faktury.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-130">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="cc5cc-131">ID účtenky</span><span class="sxs-lookup"><span data-stu-id="cc5cc-131">receipt-id</span></span> | <span data-ttu-id="cc5cc-132">řetězec</span><span class="sxs-lookup"><span data-stu-id="cc5cc-132">string</span></span> | <span data-ttu-id="cc5cc-133">Yes</span><span class="sxs-lookup"><span data-stu-id="cc5cc-133">Yes</span></span>      | <span data-ttu-id="cc5cc-134">Hodnota je ID příjemky, které umožňuje prodejci filtrovat účtenky pro danou fakturu.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-134">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cc5cc-135">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="cc5cc-135">Request headers</span></span>

<span data-ttu-id="cc5cc-136">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cc5cc-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cc5cc-137">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="cc5cc-137">Request body</span></span>

<span data-ttu-id="cc5cc-138">Žádná</span><span class="sxs-lookup"><span data-stu-id="cc5cc-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="cc5cc-139">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="cc5cc-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="cc5cc-140">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="cc5cc-140">REST response</span></span>

<span data-ttu-id="cc5cc-141">V případě úspěchu tato metoda vrátí datový proud PDF v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-141">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cc5cc-142">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="cc5cc-142">Response success and error codes</span></span>

<span data-ttu-id="cc5cc-143">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cc5cc-144">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="cc5cc-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cc5cc-145">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cc5cc-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cc5cc-146">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="cc5cc-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
