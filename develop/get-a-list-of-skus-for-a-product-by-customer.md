---
title: Získat seznam SKU pro produkt (podle zákazníka)
description: Získá kolekci SKU pro zadaný produkt od zákazníka.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6b9c9bcd52798006d7f686405f059192a722c7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766783"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="e7b9c-103">Získat seznam SKU pro produkt (podle zákazníka)</span><span class="sxs-lookup"><span data-stu-id="e7b9c-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="e7b9c-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="e7b9c-104">**Applies To**</span></span>

- <span data-ttu-id="e7b9c-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e7b9c-105">Partner Center</span></span>
- <span data-ttu-id="e7b9c-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e7b9c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e7b9c-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="e7b9c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e7b9c-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e7b9c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e7b9c-109">Získá kolekci SKU pro konkrétní produkt, který je k dispozici stávajícímu zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-109">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7b9c-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e7b9c-110">Prerequisites</span></span>

- <span data-ttu-id="e7b9c-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e7b9c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e7b9c-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e7b9c-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e7b9c-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e7b9c-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e7b9c-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e7b9c-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e7b9c-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e7b9c-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e7b9c-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e7b9c-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e7b9c-119">ID produktu (**ID produktu**).</span><span class="sxs-lookup"><span data-stu-id="e7b9c-119">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="e7b9c-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e7b9c-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e7b9c-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e7b9c-121">Request syntax</span></span>

| <span data-ttu-id="e7b9c-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="e7b9c-122">Method</span></span> | <span data-ttu-id="e7b9c-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e7b9c-123">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e7b9c-124">POST</span><span class="sxs-lookup"><span data-stu-id="e7b9c-124">POST</span></span>   | <span data-ttu-id="e7b9c-125">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/skus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e7b9c-125">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="e7b9c-126">Parametr URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e7b9c-126">Request URI parameter</span></span>

| <span data-ttu-id="e7b9c-127">Název</span><span class="sxs-lookup"><span data-stu-id="e7b9c-127">Name</span></span>               | <span data-ttu-id="e7b9c-128">Typ</span><span class="sxs-lookup"><span data-stu-id="e7b9c-128">Type</span></span> | <span data-ttu-id="e7b9c-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e7b9c-129">Required</span></span> | <span data-ttu-id="e7b9c-130">Popis</span><span class="sxs-lookup"><span data-stu-id="e7b9c-130">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="e7b9c-131">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="e7b9c-131">customer-tenant-id</span></span> | <span data-ttu-id="e7b9c-132">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="e7b9c-132">GUID</span></span> | <span data-ttu-id="e7b9c-133">Yes</span><span class="sxs-lookup"><span data-stu-id="e7b9c-133">Yes</span></span> | <span data-ttu-id="e7b9c-134">Hodnota je **číslo zákazníka**, který je ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-134">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="e7b9c-135">ID produktu</span><span class="sxs-lookup"><span data-stu-id="e7b9c-135">product-id</span></span> | <span data-ttu-id="e7b9c-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="e7b9c-136">string</span></span> | <span data-ttu-id="e7b9c-137">Yes</span><span class="sxs-lookup"><span data-stu-id="e7b9c-137">Yes</span></span> | <span data-ttu-id="e7b9c-138">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-138">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="e7b9c-139">Hlavička požadavku</span><span class="sxs-lookup"><span data-stu-id="e7b9c-139">Request header</span></span>

<span data-ttu-id="e7b9c-140">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e7b9c-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e7b9c-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e7b9c-141">Request body</span></span>

<span data-ttu-id="e7b9c-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="e7b9c-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e7b9c-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e7b9c-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="e7b9c-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e7b9c-144">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e7b9c-145">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e7b9c-145">Response success and error codes</span></span>

<span data-ttu-id="e7b9c-146">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e7b9c-147">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e7b9c-148">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e7b9c-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="e7b9c-149">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="e7b9c-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="e7b9c-150">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="e7b9c-150">HTTP Status Code</span></span> | <span data-ttu-id="e7b9c-151">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="e7b9c-151">Error code</span></span> | <span data-ttu-id="e7b9c-152">Description</span><span class="sxs-lookup"><span data-stu-id="e7b9c-152">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="e7b9c-153">404</span><span class="sxs-lookup"><span data-stu-id="e7b9c-153">404</span></span> | <span data-ttu-id="e7b9c-154">400013</span><span class="sxs-lookup"><span data-stu-id="e7b9c-154">400013</span></span> | <span data-ttu-id="e7b9c-155">Nadřazený produkt nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="e7b9c-155">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="e7b9c-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e7b9c-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "id": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Gain access to Azure Services.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "Azure",
            "displayName": "Azure"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BPS6/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "localizedAttributes": [
        {
            "key": "OfferType",
            "value": "OfferType"
        },
        {
            "key": "Standard",
            "value": "Standard"
        },
        {
            "key": "DevTest",
            "value": "Dev/Test"
        }
    ]
}
```
