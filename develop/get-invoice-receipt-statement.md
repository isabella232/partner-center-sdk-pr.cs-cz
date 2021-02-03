---
title: Získání příjmových výkazů faktur
description: Načte výpis účtenky faktury pomocí ID faktury a ID účtenky.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766655"
---
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="1945e-103">Získání příjmových výkazů faktur</span><span class="sxs-lookup"><span data-stu-id="1945e-103">Get invoice receipt statement</span></span>

<span data-ttu-id="1945e-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="1945e-104">**Applies To**</span></span>

- <span data-ttu-id="1945e-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="1945e-105">Partner Center</span></span>

<span data-ttu-id="1945e-106">Načte výpis účtenky faktury pomocí ID faktury a ID účtenky.</span><span class="sxs-lookup"><span data-stu-id="1945e-106">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1945e-107">Tato funkce se vztahuje pouze na příjem daně z Tchaj-wanu.</span><span class="sxs-lookup"><span data-stu-id="1945e-107">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1945e-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1945e-108">Prerequisites</span></span>

- <span data-ttu-id="1945e-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1945e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1945e-110">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="1945e-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1945e-111">Platné ID faktury a odpovídající ID účtenky.</span><span class="sxs-lookup"><span data-stu-id="1945e-111">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="1945e-112">C\#</span><span class="sxs-lookup"><span data-stu-id="1945e-112">C\#</span></span>

<span data-ttu-id="1945e-113">Chcete-li získat příkaz pro příjem faktury podle ID počínaje partnerským centrem SDK v 1.12.0, použijte svou kolekci **IPartner.** Invoices a zavolejte metodu **ById ()** s použitím ID faktury, potom zavolejte shromažďování **příjemek** a zavolejte **ById ()** a zavolejte metody **Documents ()** a **Statement ()** pro přístup k příkazu pro příjem faktury.</span><span class="sxs-lookup"><span data-stu-id="1945e-113">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="1945e-114">Nakonec zavolejte metody **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="1945e-114">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="1945e-115">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1945e-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1945e-116">**Projekt**: PartnerSDK. FeatureSample **Třída**: GetInvoiceReceiptStatement.cs</span><span class="sxs-lookup"><span data-stu-id="1945e-116">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1945e-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1945e-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1945e-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="1945e-118">Request syntax</span></span>

| <span data-ttu-id="1945e-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="1945e-119">Method</span></span>  | <span data-ttu-id="1945e-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1945e-120">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1945e-121">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="1945e-121">**GET**</span></span> | <span data-ttu-id="1945e-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Receipts/{Receipt-ID}/Documents/Statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1945e-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1945e-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1945e-123">URI parameter</span></span>

<span data-ttu-id="1945e-124">K získání příkazu pro příjem faktury použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="1945e-124">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="1945e-125">Název</span><span class="sxs-lookup"><span data-stu-id="1945e-125">Name</span></span>       | <span data-ttu-id="1945e-126">Typ</span><span class="sxs-lookup"><span data-stu-id="1945e-126">Type</span></span>   | <span data-ttu-id="1945e-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1945e-127">Required</span></span> | <span data-ttu-id="1945e-128">Popis</span><span class="sxs-lookup"><span data-stu-id="1945e-128">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1945e-129">ID faktury</span><span class="sxs-lookup"><span data-stu-id="1945e-129">invoice-id</span></span> | <span data-ttu-id="1945e-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="1945e-130">string</span></span> | <span data-ttu-id="1945e-131">Yes</span><span class="sxs-lookup"><span data-stu-id="1945e-131">Yes</span></span>      | <span data-ttu-id="1945e-132">Hodnota je ID faktury, které prodejci umožňuje filtrovat výsledky dané faktury.</span><span class="sxs-lookup"><span data-stu-id="1945e-132">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="1945e-133">ID účtenky</span><span class="sxs-lookup"><span data-stu-id="1945e-133">receipt-id</span></span> | <span data-ttu-id="1945e-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="1945e-134">string</span></span> | <span data-ttu-id="1945e-135">Yes</span><span class="sxs-lookup"><span data-stu-id="1945e-135">Yes</span></span>      | <span data-ttu-id="1945e-136">Hodnota je ID příjemky, které umožňuje prodejci filtrovat účtenky pro danou fakturu.</span><span class="sxs-lookup"><span data-stu-id="1945e-136">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1945e-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1945e-137">Request headers</span></span>

<span data-ttu-id="1945e-138">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1945e-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1945e-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1945e-139">Request body</span></span>

<span data-ttu-id="1945e-140">Žádné</span><span class="sxs-lookup"><span data-stu-id="1945e-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="1945e-141">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1945e-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="1945e-142">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1945e-142">REST response</span></span>

<span data-ttu-id="1945e-143">V případě úspěchu tato metoda vrátí datový proud PDF v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="1945e-143">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1945e-144">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="1945e-144">Response success and error codes</span></span>

<span data-ttu-id="1945e-145">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1945e-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1945e-146">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="1945e-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1945e-147">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1945e-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1945e-148">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1945e-148">Response example</span></span>

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
