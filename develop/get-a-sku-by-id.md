---
title: Získání skladové položky podle ID
description: Získá SKU pro zadaný produkt pomocí zadaného ID SKU.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9516a87a438a0a84a6f6069c1f9b2a2e97e90fba
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873849"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="d7fa2-103">Získání skladové položky podle ID</span><span class="sxs-lookup"><span data-stu-id="d7fa2-103">Get a SKU by ID</span></span>

<span data-ttu-id="d7fa2-104">Získá SKU pro zadaný produkt pomocí zadaného ID SKU.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-104">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7fa2-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d7fa2-105">Prerequisites</span></span>

- <span data-ttu-id="d7fa2-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d7fa2-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d7fa2-107">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d7fa2-108">ID produktu.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-108">A product ID.</span></span>

- <span data-ttu-id="d7fa2-109">ID SKU.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-109">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="d7fa2-110">C\#</span><span class="sxs-lookup"><span data-stu-id="d7fa2-110">C\#</span></span>

<span data-ttu-id="d7fa2-111">Pokud chcete získat podrobnosti o konkrétní SKU, začněte podle kroků v části [získání produktu podle ID](get-a-product-by-id.md) a získejte rozhraní pro konkrétní operace produktu.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-111">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="d7fa2-112">Z výsledného rozhraní vyberte vlastnost **SKU** a získejte rozhraní s dostupnými operacemi SKU.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-112">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="d7fa2-113">Předejte ID skladové položky metodě **ById ()** a voláním metody **Get ()** nebo **GetAsync ()** načtěte podrobnosti SKU.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-113">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="d7fa2-114">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d7fa2-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d7fa2-115">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d7fa2-115">Request syntax</span></span>

| <span data-ttu-id="d7fa2-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="d7fa2-116">Method</span></span>  | <span data-ttu-id="d7fa2-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d7fa2-117">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d7fa2-118">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="d7fa2-118">**GET**</span></span> | <span data-ttu-id="d7fa2-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/skus/{SKU-ID}? Country = {Country-Code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d7fa2-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="d7fa2-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d7fa2-120">URI parameter</span></span>

<span data-ttu-id="d7fa2-121">K získání SKU pro zadaný produkt pomocí zadaného ID SKU použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-121">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="d7fa2-122">Název</span><span class="sxs-lookup"><span data-stu-id="d7fa2-122">Name</span></span>                   | <span data-ttu-id="d7fa2-123">Typ</span><span class="sxs-lookup"><span data-stu-id="d7fa2-123">Type</span></span>     | <span data-ttu-id="d7fa2-124">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d7fa2-124">Required</span></span> | <span data-ttu-id="d7fa2-125">Popis</span><span class="sxs-lookup"><span data-stu-id="d7fa2-125">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="d7fa2-126">ID produktu</span><span class="sxs-lookup"><span data-stu-id="d7fa2-126">product-id</span></span>             | <span data-ttu-id="d7fa2-127">řetězec</span><span class="sxs-lookup"><span data-stu-id="d7fa2-127">string</span></span>   | <span data-ttu-id="d7fa2-128">Yes</span><span class="sxs-lookup"><span data-stu-id="d7fa2-128">Yes</span></span>      | <span data-ttu-id="d7fa2-129">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-129">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="d7fa2-130">SKU – ID</span><span class="sxs-lookup"><span data-stu-id="d7fa2-130">sku-id</span></span>                 | <span data-ttu-id="d7fa2-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="d7fa2-131">string</span></span>   | <span data-ttu-id="d7fa2-132">Yes</span><span class="sxs-lookup"><span data-stu-id="d7fa2-132">Yes</span></span>      | <span data-ttu-id="d7fa2-133">Řetězec, který identifikuje SKU.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-133">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="d7fa2-134">kód země</span><span class="sxs-lookup"><span data-stu-id="d7fa2-134">country-code</span></span>           | <span data-ttu-id="d7fa2-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="d7fa2-135">string</span></span>   | <span data-ttu-id="d7fa2-136">Yes</span><span class="sxs-lookup"><span data-stu-id="d7fa2-136">Yes</span></span>      | <span data-ttu-id="d7fa2-137">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="d7fa2-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d7fa2-138">Request headers</span></span>

<span data-ttu-id="d7fa2-139">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d7fa2-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d7fa2-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d7fa2-140">Request body</span></span>

<span data-ttu-id="d7fa2-141">Žádné</span><span class="sxs-lookup"><span data-stu-id="d7fa2-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d7fa2-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d7fa2-142">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d7fa2-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d7fa2-143">REST response</span></span>

<span data-ttu-id="d7fa2-144">V případě úspěchu obsahuje tělo odpovědi prostředek [SKU](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="d7fa2-144">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d7fa2-145">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d7fa2-145">Response success and error codes</span></span>

<span data-ttu-id="d7fa2-146">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d7fa2-147">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d7fa2-148">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d7fa2-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="d7fa2-149">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="d7fa2-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="d7fa2-150">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="d7fa2-150">HTTP Status Code</span></span>     | <span data-ttu-id="d7fa2-151">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="d7fa2-151">Error code</span></span>   | <span data-ttu-id="d7fa2-152">Description</span><span class="sxs-lookup"><span data-stu-id="d7fa2-152">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d7fa2-153">404</span><span class="sxs-lookup"><span data-stu-id="d7fa2-153">404</span></span>                  | <span data-ttu-id="d7fa2-154">400013</span><span class="sxs-lookup"><span data-stu-id="d7fa2-154">400013</span></span>       | <span data-ttu-id="d7fa2-155">Produkt nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-155">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="d7fa2-156">404</span><span class="sxs-lookup"><span data-stu-id="d7fa2-156">404</span></span>                  | <span data-ttu-id="d7fa2-157">400018</span><span class="sxs-lookup"><span data-stu-id="d7fa2-157">400018</span></span>       | <span data-ttu-id="d7fa2-158">SKU se nepovedlo najít.</span><span class="sxs-lookup"><span data-stu-id="d7fa2-158">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="d7fa2-159">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d7fa2-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
    "minimumQuantity": 1,
    "maximumQuantity": 999999999,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "AzureSubscriptionRegistration",
        "InventoryCheck"
    ],
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
    }
}
```
