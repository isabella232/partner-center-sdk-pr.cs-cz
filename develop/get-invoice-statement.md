---
title: Získání výkazů faktur
description: Načítá výpis faktury pomocí ID faktury.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f0324916eb2efd9244530a53b1d7bb4abc0c8e6e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549123"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="b59db-103">Získání výkazů faktur</span><span class="sxs-lookup"><span data-stu-id="b59db-103">Get invoice statement</span></span>

<span data-ttu-id="b59db-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b59db-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b59db-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b59db-105">Prerequisites</span></span>

- <span data-ttu-id="b59db-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b59db-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b59db-107">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b59db-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b59db-108">Platné ID faktury</span><span class="sxs-lookup"><span data-stu-id="b59db-108">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="b59db-109">C\#</span><span class="sxs-lookup"><span data-stu-id="b59db-109">C\#</span></span>

<span data-ttu-id="b59db-110">Chcete-li získat příkaz faktury podle ID, použijte kolekci **IPartner.** Invoices a zavolejte metodu **ById ()** pomocí ID faktury a pak zavolejte metody **Documents ()** a **Statement ()** pro přístup k výpisu faktury.</span><span class="sxs-lookup"><span data-stu-id="b59db-110">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="b59db-111">Nakonec zavolejte metody **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="b59db-111">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="b59db-112">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b59db-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b59db-113">**Project**: PartnerSDK. FeatureSample **třída**: GetInvoiceStatement. cs</span><span class="sxs-lookup"><span data-stu-id="b59db-113">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b59db-114">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b59db-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b59db-115">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b59db-115">Request syntax</span></span>

| <span data-ttu-id="b59db-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="b59db-116">Method</span></span>  | <span data-ttu-id="b59db-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b59db-117">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b59db-118">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b59db-118">**GET**</span></span> | <span data-ttu-id="b59db-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Documents/Statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b59db-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="b59db-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b59db-120">URI parameter</span></span>

<span data-ttu-id="b59db-121">K získání příkazu faktury použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="b59db-121">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="b59db-122">Název</span><span class="sxs-lookup"><span data-stu-id="b59db-122">Name</span></span>       | <span data-ttu-id="b59db-123">Typ</span><span class="sxs-lookup"><span data-stu-id="b59db-123">Type</span></span>       | <span data-ttu-id="b59db-124">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b59db-124">Required</span></span> | <span data-ttu-id="b59db-125">Popis</span><span class="sxs-lookup"><span data-stu-id="b59db-125">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b59db-126">ID faktury</span><span class="sxs-lookup"><span data-stu-id="b59db-126">invoice-id</span></span> | <span data-ttu-id="b59db-127">řetězec</span><span class="sxs-lookup"><span data-stu-id="b59db-127">string</span></span>     | <span data-ttu-id="b59db-128">Yes</span><span class="sxs-lookup"><span data-stu-id="b59db-128">Yes</span></span>      | <span data-ttu-id="b59db-129">Hodnota je ID faktury, které prodejci umožňuje filtrovat výsledky dané faktury.</span><span class="sxs-lookup"><span data-stu-id="b59db-129">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b59db-130">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b59db-130">Request headers</span></span>

<span data-ttu-id="b59db-131">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b59db-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b59db-132">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b59db-132">Request body</span></span>

<span data-ttu-id="b59db-133">Žádná</span><span class="sxs-lookup"><span data-stu-id="b59db-133">None</span></span>

### <a name="request-example"></a><span data-ttu-id="b59db-134">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b59db-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="b59db-135">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b59db-135">REST response</span></span>

<span data-ttu-id="b59db-136">V případě úspěchu tato metoda vrátí prostředek [InvoiceStatement](invoice-resources.md#invoicestatement) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b59db-136">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b59db-137">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b59db-137">Response success and error codes</span></span>

<span data-ttu-id="b59db-138">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b59db-138">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b59db-139">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b59db-139">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b59db-140">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b59db-140">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b59db-141">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b59db-141">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
