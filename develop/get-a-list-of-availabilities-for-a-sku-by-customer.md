---
title: Získání seznamu dostupností pro skladovou položku (podle zákazníka)
description: Můžete získat kolekci dostupnosti pro určitý produkt a SKU podle zákazníka pomocí identifikátorů zákazníka, produktu a SKU.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 5f4067916fea911963182954eed77f4e230e79d6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766793"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="caa6e-103">Získání seznamu dostupností pro skladovou položku (podle zákazníka)</span><span class="sxs-lookup"><span data-stu-id="caa6e-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="caa6e-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="caa6e-104">**Applies to:**</span></span>

- <span data-ttu-id="caa6e-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="caa6e-105">Partner Center</span></span>
- <span data-ttu-id="caa6e-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="caa6e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="caa6e-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="caa6e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="caa6e-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="caa6e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="caa6e-109">Následující metody můžete použít k získání kolekce dostupnosti pro určitý produkt a SKU k dispozici konkrétnímu zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="caa6e-109">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caa6e-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="caa6e-110">Prerequisites</span></span>

- <span data-ttu-id="caa6e-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="caa6e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="caa6e-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="caa6e-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="caa6e-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="caa6e-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="caa6e-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="caa6e-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="caa6e-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="caa6e-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="caa6e-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="caa6e-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="caa6e-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="caa6e-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="caa6e-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="caa6e-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="caa6e-119">Identifikátor produktu (**ID produktu**).</span><span class="sxs-lookup"><span data-stu-id="caa6e-119">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="caa6e-120">Identifikátor SKU (**SKU-ID**).</span><span class="sxs-lookup"><span data-stu-id="caa6e-120">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="caa6e-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="caa6e-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="caa6e-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="caa6e-122">Request syntax</span></span>

| <span data-ttu-id="caa6e-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="caa6e-123">Method</span></span> | <span data-ttu-id="caa6e-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="caa6e-124">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="caa6e-125">POST</span><span class="sxs-lookup"><span data-stu-id="caa6e-125">POST</span></span>   | <span data-ttu-id="caa6e-126">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/skus/{SKU-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="caa6e-126">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="caa6e-127">Parametry identifikátoru URI žádosti</span><span class="sxs-lookup"><span data-stu-id="caa6e-127">Request URI parameters</span></span>

| <span data-ttu-id="caa6e-128">Název</span><span class="sxs-lookup"><span data-stu-id="caa6e-128">Name</span></span>               | <span data-ttu-id="caa6e-129">Typ</span><span class="sxs-lookup"><span data-stu-id="caa6e-129">Type</span></span> | <span data-ttu-id="caa6e-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="caa6e-130">Required</span></span> | <span data-ttu-id="caa6e-131">Popis</span><span class="sxs-lookup"><span data-stu-id="caa6e-131">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="caa6e-132">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="caa6e-132">customer-tenant-id</span></span> | <span data-ttu-id="caa6e-133">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="caa6e-133">GUID</span></span> | <span data-ttu-id="caa6e-134">Yes</span><span class="sxs-lookup"><span data-stu-id="caa6e-134">Yes</span></span> | <span data-ttu-id="caa6e-135">Hodnota je **číslo zákazníka**, který je ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="caa6e-135">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="caa6e-136">ID produktu</span><span class="sxs-lookup"><span data-stu-id="caa6e-136">product-id</span></span> | <span data-ttu-id="caa6e-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="caa6e-137">string</span></span> | <span data-ttu-id="caa6e-138">Yes</span><span class="sxs-lookup"><span data-stu-id="caa6e-138">Yes</span></span> | <span data-ttu-id="caa6e-139">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="caa6e-139">A string that identifies the product.</span></span> |
| <span data-ttu-id="caa6e-140">SKU – ID</span><span class="sxs-lookup"><span data-stu-id="caa6e-140">sku-id</span></span> | <span data-ttu-id="caa6e-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="caa6e-141">string</span></span> | <span data-ttu-id="caa6e-142">Yes</span><span class="sxs-lookup"><span data-stu-id="caa6e-142">Yes</span></span> | <span data-ttu-id="caa6e-143">Řetězec, který identifikuje SKU.</span><span class="sxs-lookup"><span data-stu-id="caa6e-143">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="caa6e-144">Hlavička požadavku</span><span class="sxs-lookup"><span data-stu-id="caa6e-144">Request header</span></span>

<span data-ttu-id="caa6e-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="caa6e-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="caa6e-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="caa6e-146">Request body</span></span>

<span data-ttu-id="caa6e-147">Žádné</span><span class="sxs-lookup"><span data-stu-id="caa6e-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="caa6e-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="caa6e-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="caa6e-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="caa6e-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="caa6e-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="caa6e-150">Response success and error codes</span></span>

<span data-ttu-id="caa6e-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="caa6e-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="caa6e-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="caa6e-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="caa6e-153">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="caa6e-153">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="caa6e-154">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="caa6e-154">This method returns the following error codes:</span></span>

| <span data-ttu-id="caa6e-155">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="caa6e-155">HTTP Status Code</span></span> | <span data-ttu-id="caa6e-156">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="caa6e-156">Error code</span></span> | <span data-ttu-id="caa6e-157">Description</span><span class="sxs-lookup"><span data-stu-id="caa6e-157">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="caa6e-158">404</span><span class="sxs-lookup"><span data-stu-id="caa6e-158">404</span></span> | <span data-ttu-id="caa6e-159">400013</span><span class="sxs-lookup"><span data-stu-id="caa6e-159">400013</span></span> | <span data-ttu-id="caa6e-160">Nadřazený produkt nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="caa6e-160">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="caa6e-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="caa6e-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Microsoft Azure plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
