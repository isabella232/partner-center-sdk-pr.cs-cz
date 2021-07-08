---
title: Získání seznamu dostupností pro skladovou položku (podle zákazníka)
description: Pomocí identifikátorů zákazníka, produktu a SKU můžete získat kolekci dostupnosti pro zadaný produkt a SKU zákazníka.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b237bbd17a6108bbcb4e23529cf476a6b8306f68
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874546"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="8625d-103">Získání seznamu dostupností pro skladovou položku (podle zákazníka)</span><span class="sxs-lookup"><span data-stu-id="8625d-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="8625d-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8625d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8625d-105">Následující metody můžete použít k získání kolekce dostupnosti pro zadaný produkt a SKU, které jsou k dispozici pro konkrétního zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8625d-105">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8625d-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8625d-106">Prerequisites</span></span>

- <span data-ttu-id="8625d-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8625d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8625d-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="8625d-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8625d-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8625d-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8625d-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8625d-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8625d-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="8625d-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8625d-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="8625d-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8625d-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8625d-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8625d-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8625d-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8625d-115">Identifikátor produktu (**product-id**).</span><span class="sxs-lookup"><span data-stu-id="8625d-115">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="8625d-116">Identifikátor skladové položky **(sku-id).**</span><span class="sxs-lookup"><span data-stu-id="8625d-116">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="8625d-117">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="8625d-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8625d-118">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="8625d-118">Request syntax</span></span>

| <span data-ttu-id="8625d-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="8625d-119">Method</span></span> | <span data-ttu-id="8625d-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8625d-120">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8625d-121">POST</span><span class="sxs-lookup"><span data-stu-id="8625d-121">POST</span></span>   | <span data-ttu-id="8625d-122">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/products/{ID_produktu}/skus/{ID_SKU} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8625d-122">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="8625d-123">Parametry identifikátoru URI požadavku</span><span class="sxs-lookup"><span data-stu-id="8625d-123">Request URI parameters</span></span>

| <span data-ttu-id="8625d-124">Název</span><span class="sxs-lookup"><span data-stu-id="8625d-124">Name</span></span>               | <span data-ttu-id="8625d-125">Typ</span><span class="sxs-lookup"><span data-stu-id="8625d-125">Type</span></span> | <span data-ttu-id="8625d-126">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8625d-126">Required</span></span> | <span data-ttu-id="8625d-127">Popis</span><span class="sxs-lookup"><span data-stu-id="8625d-127">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="8625d-128">customer-tenant-id</span><span class="sxs-lookup"><span data-stu-id="8625d-128">customer-tenant-id</span></span> | <span data-ttu-id="8625d-129">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="8625d-129">GUID</span></span> | <span data-ttu-id="8625d-130">Yes</span><span class="sxs-lookup"><span data-stu-id="8625d-130">Yes</span></span> | <span data-ttu-id="8625d-131">Hodnota je id tenanta zákazníka ve **formátu** GUID, což je identifikátor, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8625d-131">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="8625d-132">id produktu</span><span class="sxs-lookup"><span data-stu-id="8625d-132">product-id</span></span> | <span data-ttu-id="8625d-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="8625d-133">string</span></span> | <span data-ttu-id="8625d-134">Yes</span><span class="sxs-lookup"><span data-stu-id="8625d-134">Yes</span></span> | <span data-ttu-id="8625d-135">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="8625d-135">A string that identifies the product.</span></span> |
| <span data-ttu-id="8625d-136">sku-id</span><span class="sxs-lookup"><span data-stu-id="8625d-136">sku-id</span></span> | <span data-ttu-id="8625d-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="8625d-137">string</span></span> | <span data-ttu-id="8625d-138">Yes</span><span class="sxs-lookup"><span data-stu-id="8625d-138">Yes</span></span> | <span data-ttu-id="8625d-139">Řetězec, který identifikuje SKU.</span><span class="sxs-lookup"><span data-stu-id="8625d-139">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="8625d-140">Hlavička požadavku</span><span class="sxs-lookup"><span data-stu-id="8625d-140">Request header</span></span>

<span data-ttu-id="8625d-141">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8625d-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8625d-142">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8625d-142">Request body</span></span>

<span data-ttu-id="8625d-143">Žádné</span><span class="sxs-lookup"><span data-stu-id="8625d-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8625d-144">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8625d-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="8625d-145">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8625d-145">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8625d-146">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="8625d-146">Response success and error codes</span></span>

<span data-ttu-id="8625d-147">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8625d-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8625d-148">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="8625d-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8625d-149">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8625d-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="8625d-150">Tato metoda vrátí následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="8625d-150">This method returns the following error codes:</span></span>

| <span data-ttu-id="8625d-151">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="8625d-151">HTTP Status Code</span></span> | <span data-ttu-id="8625d-152">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="8625d-152">Error code</span></span> | <span data-ttu-id="8625d-153">Description</span><span class="sxs-lookup"><span data-stu-id="8625d-153">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="8625d-154">404</span><span class="sxs-lookup"><span data-stu-id="8625d-154">404</span></span> | <span data-ttu-id="8625d-155">400013</span><span class="sxs-lookup"><span data-stu-id="8625d-155">400013</span></span> | <span data-ttu-id="8625d-156">Nadřazený produkt se nenašel.</span><span class="sxs-lookup"><span data-stu-id="8625d-156">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="8625d-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8625d-157">Response example</span></span>

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
