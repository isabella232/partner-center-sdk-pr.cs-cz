---
title: Získání výkazů faktur
description: Načítá výpis faktury pomocí ID faktury.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 42e5201919eea5644da463dfe2584c8d55002083
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766756"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="c2b2c-103">Získání výkazů faktur</span><span class="sxs-lookup"><span data-stu-id="c2b2c-103">Get invoice statement</span></span>

<span data-ttu-id="c2b2c-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="c2b2c-104">**Applies To**</span></span>

- <span data-ttu-id="c2b2c-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="c2b2c-105">Partner Center</span></span>
- <span data-ttu-id="c2b2c-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="c2b2c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c2b2c-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="c2b2c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c2b2c-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c2b2c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c2b2c-109">Načítá výpis faktury pomocí ID faktury.</span><span class="sxs-lookup"><span data-stu-id="c2b2c-109">Retrieves an invoice statement using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2b2c-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c2b2c-110">Prerequisites</span></span>

- <span data-ttu-id="c2b2c-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c2b2c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c2b2c-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="c2b2c-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c2b2c-113">Platné ID faktury</span><span class="sxs-lookup"><span data-stu-id="c2b2c-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="c2b2c-114">C\#</span><span class="sxs-lookup"><span data-stu-id="c2b2c-114">C\#</span></span>

<span data-ttu-id="c2b2c-115">Chcete-li získat příkaz faktury podle ID, použijte kolekci **IPartner.** Invoices a zavolejte metodu **ById ()** pomocí ID faktury a pak zavolejte metody **Documents ()** a **Statement ()** pro přístup k výpisu faktury.</span><span class="sxs-lookup"><span data-stu-id="c2b2c-115">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="c2b2c-116">Nakonec zavolejte metody **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="c2b2c-116">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="c2b2c-117">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c2b2c-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c2b2c-118">**Projekt**: PartnerSDK. FeatureSample **Třída**: GetInvoiceStatement.cs</span><span class="sxs-lookup"><span data-stu-id="c2b2c-118">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c2b2c-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="c2b2c-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c2b2c-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="c2b2c-120">Request syntax</span></span>

| <span data-ttu-id="c2b2c-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="c2b2c-121">Method</span></span>  | <span data-ttu-id="c2b2c-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="c2b2c-122">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c2b2c-123">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="c2b2c-123">**GET**</span></span> | <span data-ttu-id="c2b2c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Documents/Statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c2b2c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="c2b2c-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c2b2c-125">URI parameter</span></span>

<span data-ttu-id="c2b2c-126">K získání příkazu faktury použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="c2b2c-126">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="c2b2c-127">Název</span><span class="sxs-lookup"><span data-stu-id="c2b2c-127">Name</span></span>       | <span data-ttu-id="c2b2c-128">Typ</span><span class="sxs-lookup"><span data-stu-id="c2b2c-128">Type</span></span>       | <span data-ttu-id="c2b2c-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="c2b2c-129">Required</span></span> | <span data-ttu-id="c2b2c-130">Popis</span><span class="sxs-lookup"><span data-stu-id="c2b2c-130">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c2b2c-131">ID faktury</span><span class="sxs-lookup"><span data-stu-id="c2b2c-131">invoice-id</span></span> | <span data-ttu-id="c2b2c-132">řetězec</span><span class="sxs-lookup"><span data-stu-id="c2b2c-132">string</span></span>     | <span data-ttu-id="c2b2c-133">Yes</span><span class="sxs-lookup"><span data-stu-id="c2b2c-133">Yes</span></span>      | <span data-ttu-id="c2b2c-134">Hodnota je ID faktury, které prodejci umožňuje filtrovat výsledky dané faktury.</span><span class="sxs-lookup"><span data-stu-id="c2b2c-134">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c2b2c-135">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="c2b2c-135">Request headers</span></span>

<span data-ttu-id="c2b2c-136">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c2b2c-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c2b2c-137">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="c2b2c-137">Request body</span></span>

<span data-ttu-id="c2b2c-138">Žádné</span><span class="sxs-lookup"><span data-stu-id="c2b2c-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="c2b2c-139">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="c2b2c-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="c2b2c-140">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="c2b2c-140">REST response</span></span>

<span data-ttu-id="c2b2c-141">V případě úspěchu tato metoda vrátí prostředek [InvoiceStatement](invoice-resources.md#invoicestatement) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c2b2c-141">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c2b2c-142">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="c2b2c-142">Response success and error codes</span></span>

<span data-ttu-id="c2b2c-143">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="c2b2c-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c2b2c-144">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="c2b2c-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c2b2c-145">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c2b2c-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c2b2c-146">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="c2b2c-146">Response example</span></span>

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
