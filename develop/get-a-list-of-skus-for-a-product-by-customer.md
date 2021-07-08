---
title: Získat seznam SKU pro produkt (podle zákazníka)
description: Získá kolekci SKU pro zadaný produkt od zákazníka.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b76526d97ba9027897fc88954ba45186d58aefb8
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874155"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="1f9f6-103">Získat seznam SKU pro produkt (podle zákazníka)</span><span class="sxs-lookup"><span data-stu-id="1f9f6-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="1f9f6-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1f9f6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1f9f6-105">Získá kolekci SKU pro konkrétní produkt, který je k dispozici stávajícímu zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-105">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f9f6-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1f9f6-106">Prerequisites</span></span>

- <span data-ttu-id="1f9f6-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1f9f6-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1f9f6-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1f9f6-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1f9f6-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1f9f6-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1f9f6-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1f9f6-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1f9f6-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="1f9f6-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1f9f6-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1f9f6-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1f9f6-115">ID produktu (**ID produktu**).</span><span class="sxs-lookup"><span data-stu-id="1f9f6-115">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="1f9f6-116">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1f9f6-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1f9f6-117">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="1f9f6-117">Request syntax</span></span>

| <span data-ttu-id="1f9f6-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="1f9f6-118">Method</span></span> | <span data-ttu-id="1f9f6-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1f9f6-119">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1f9f6-120">POST</span><span class="sxs-lookup"><span data-stu-id="1f9f6-120">POST</span></span>   | <span data-ttu-id="1f9f6-121">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/skus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1f9f6-121">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="1f9f6-122">Parametr URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1f9f6-122">Request URI parameter</span></span>

| <span data-ttu-id="1f9f6-123">Název</span><span class="sxs-lookup"><span data-stu-id="1f9f6-123">Name</span></span>               | <span data-ttu-id="1f9f6-124">Typ</span><span class="sxs-lookup"><span data-stu-id="1f9f6-124">Type</span></span> | <span data-ttu-id="1f9f6-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1f9f6-125">Required</span></span> | <span data-ttu-id="1f9f6-126">Popis</span><span class="sxs-lookup"><span data-stu-id="1f9f6-126">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="1f9f6-127">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="1f9f6-127">customer-tenant-id</span></span> | <span data-ttu-id="1f9f6-128">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="1f9f6-128">GUID</span></span> | <span data-ttu-id="1f9f6-129">Yes</span><span class="sxs-lookup"><span data-stu-id="1f9f6-129">Yes</span></span> | <span data-ttu-id="1f9f6-130">Hodnota je **číslo zákazníka**, který je ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-130">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="1f9f6-131">ID produktu</span><span class="sxs-lookup"><span data-stu-id="1f9f6-131">product-id</span></span> | <span data-ttu-id="1f9f6-132">řetězec</span><span class="sxs-lookup"><span data-stu-id="1f9f6-132">string</span></span> | <span data-ttu-id="1f9f6-133">Yes</span><span class="sxs-lookup"><span data-stu-id="1f9f6-133">Yes</span></span> | <span data-ttu-id="1f9f6-134">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-134">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="1f9f6-135">Hlavička požadavku</span><span class="sxs-lookup"><span data-stu-id="1f9f6-135">Request header</span></span>

<span data-ttu-id="1f9f6-136">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1f9f6-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1f9f6-137">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1f9f6-137">Request body</span></span>

<span data-ttu-id="1f9f6-138">Žádné</span><span class="sxs-lookup"><span data-stu-id="1f9f6-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1f9f6-139">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1f9f6-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="1f9f6-140">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1f9f6-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1f9f6-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="1f9f6-141">Response success and error codes</span></span>

<span data-ttu-id="1f9f6-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1f9f6-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1f9f6-144">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1f9f6-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="1f9f6-145">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="1f9f6-145">This method returns the following error codes:</span></span>

| <span data-ttu-id="1f9f6-146">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="1f9f6-146">HTTP Status Code</span></span> | <span data-ttu-id="1f9f6-147">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="1f9f6-147">Error code</span></span> | <span data-ttu-id="1f9f6-148">Description</span><span class="sxs-lookup"><span data-stu-id="1f9f6-148">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="1f9f6-149">404</span><span class="sxs-lookup"><span data-stu-id="1f9f6-149">404</span></span> | <span data-ttu-id="1f9f6-150">400013</span><span class="sxs-lookup"><span data-stu-id="1f9f6-150">400013</span></span> | <span data-ttu-id="1f9f6-151">Nadřazený produkt nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="1f9f6-151">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="1f9f6-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1f9f6-152">Response example</span></span>

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
