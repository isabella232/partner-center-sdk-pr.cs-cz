---
title: Získat dostupnost podle ID
description: Získá dostupnost pro zadaný produkt a SKU pomocí ID dostupnosti.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766671"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="00e62-103">Získat dostupnost podle ID</span><span class="sxs-lookup"><span data-stu-id="00e62-103">Get the availability by ID</span></span>

<span data-ttu-id="00e62-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="00e62-104">**Applies To**</span></span>

- <span data-ttu-id="00e62-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="00e62-105">Partner Center</span></span>

<span data-ttu-id="00e62-106">Získá dostupnost pro zadaný produkt a SKU pomocí ID dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="00e62-106">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00e62-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="00e62-107">Prerequisites</span></span>

- <span data-ttu-id="00e62-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="00e62-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="00e62-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="00e62-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="00e62-110">ID produktu.</span><span class="sxs-lookup"><span data-stu-id="00e62-110">A product ID.</span></span>

- <span data-ttu-id="00e62-111">ID SKU.</span><span class="sxs-lookup"><span data-stu-id="00e62-111">A SKU ID.</span></span>

- <span data-ttu-id="00e62-112">ID dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="00e62-112">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="00e62-113">C\#</span><span class="sxs-lookup"><span data-stu-id="00e62-113">C\#</span></span>

<span data-ttu-id="00e62-114">Pokud chcete získat podrobnosti o konkrétní [dostupnosti](product-resources.md#availability), začněte pomocí kroků v části [získání skladové položky podle ID](get-a-sku-by-id.md) , abyste získali rozhraní pro konkrétní [skladové](product-resources.md#sku) operace.</span><span class="sxs-lookup"><span data-stu-id="00e62-114">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="00e62-115">Ve výsledném rozhraní vyberte vlastnost **Nákup** a získejte rozhraní s dostupnými operacemi pro nákup dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="00e62-115">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="00e62-116">Potom předejte ID dostupnosti metodě **ById ()** , abyste získali operace pro konkrétní dostupnost a pak volali **Get ()** nebo **GetAsync ()** pro načtení podrobností o dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="00e62-116">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="00e62-117">Java</span><span class="sxs-lookup"><span data-stu-id="00e62-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="00e62-118">Pokud chcete získat podrobnosti o konkrétní [dostupnosti](product-resources.md#availability), začněte pomocí kroků v části [získání skladové položky podle ID](get-a-sku-by-id.md) , abyste získali rozhraní pro konkrétní [skladové](product-resources.md#sku) operace.</span><span class="sxs-lookup"><span data-stu-id="00e62-118">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="00e62-119">Z výsledného rozhraní vyberte funkci **getAvailabilities** , abyste získali rozhraní s dostupnými operacemi pro nákup dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="00e62-119">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="00e62-120">Potom předejte ID dostupnosti funkci **byId ()** , abyste získali operace pro konkrétní dostupnost a pak zavolali funkci **Get ()** pro načtení podrobností o dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="00e62-120">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="00e62-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00e62-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="00e62-122">Chcete-li získat podrobnosti o [konkrétní dostupnosti](product-resources.md#availability), spusťte příkaz [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) a zadejte parametry **AvailabilityId**, **CountryCode**, **ProductID** a **SkuId** pro načtení podrobností o dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="00e62-122">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="00e62-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="00e62-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="00e62-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="00e62-124">Request syntax</span></span>

| <span data-ttu-id="00e62-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="00e62-125">Method</span></span>  | <span data-ttu-id="00e62-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="00e62-126">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00e62-127">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="00e62-127">**GET**</span></span> | <span data-ttu-id="00e62-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/skus/{SKU-ID}/availabilities/{Availability-ID}? Country = {Country-Code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="00e62-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="00e62-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="00e62-129">URI parameter</span></span>

<span data-ttu-id="00e62-130">K získání konkrétní dostupnosti pomocí ID dostupnosti použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="00e62-130">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="00e62-131">Název</span><span class="sxs-lookup"><span data-stu-id="00e62-131">Name</span></span>                   | <span data-ttu-id="00e62-132">Typ</span><span class="sxs-lookup"><span data-stu-id="00e62-132">Type</span></span>     | <span data-ttu-id="00e62-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="00e62-133">Required</span></span> | <span data-ttu-id="00e62-134">Popis</span><span class="sxs-lookup"><span data-stu-id="00e62-134">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="00e62-135">ID produktu</span><span class="sxs-lookup"><span data-stu-id="00e62-135">product-id</span></span>             | <span data-ttu-id="00e62-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="00e62-136">string</span></span>   | <span data-ttu-id="00e62-137">Yes</span><span class="sxs-lookup"><span data-stu-id="00e62-137">Yes</span></span>      | <span data-ttu-id="00e62-138">Řetězec ve formátu GUID, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="00e62-138">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="00e62-139">SKU – ID</span><span class="sxs-lookup"><span data-stu-id="00e62-139">sku-id</span></span>                 | <span data-ttu-id="00e62-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="00e62-140">string</span></span>   | <span data-ttu-id="00e62-141">Yes</span><span class="sxs-lookup"><span data-stu-id="00e62-141">Yes</span></span>      | <span data-ttu-id="00e62-142">Řetězec ve formátu GUID, který identifikuje SKU.</span><span class="sxs-lookup"><span data-stu-id="00e62-142">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="00e62-143">ID dostupnosti</span><span class="sxs-lookup"><span data-stu-id="00e62-143">availability-id</span></span>        | <span data-ttu-id="00e62-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="00e62-144">string</span></span>   | <span data-ttu-id="00e62-145">Yes</span><span class="sxs-lookup"><span data-stu-id="00e62-145">Yes</span></span>      | <span data-ttu-id="00e62-146">Řetězec ve formátu GUID, který identifikuje dostupnost.</span><span class="sxs-lookup"><span data-stu-id="00e62-146">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="00e62-147">kód země</span><span class="sxs-lookup"><span data-stu-id="00e62-147">country-code</span></span>           | <span data-ttu-id="00e62-148">řetězec</span><span class="sxs-lookup"><span data-stu-id="00e62-148">string</span></span>   | <span data-ttu-id="00e62-149">Yes</span><span class="sxs-lookup"><span data-stu-id="00e62-149">Yes</span></span>      | <span data-ttu-id="00e62-150">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="00e62-150">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="00e62-151">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="00e62-151">Request headers</span></span>

<span data-ttu-id="00e62-152">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="00e62-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="00e62-153">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="00e62-153">Request body</span></span>

<span data-ttu-id="00e62-154">Žádné</span><span class="sxs-lookup"><span data-stu-id="00e62-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="00e62-155">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="00e62-155">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="00e62-156">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="00e62-156">REST response</span></span>

<span data-ttu-id="00e62-157">V případě úspěchu obsahuje tělo odpovědi prostředek [dostupnosti](product-resources.md#availability) .</span><span class="sxs-lookup"><span data-stu-id="00e62-157">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="00e62-158">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="00e62-158">Response success and error codes</span></span>

<span data-ttu-id="00e62-159">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="00e62-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="00e62-160">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="00e62-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="00e62-161">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="00e62-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="00e62-162">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="00e62-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="00e62-163">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="00e62-163">HTTP Status Code</span></span>     | <span data-ttu-id="00e62-164">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="00e62-164">Error code</span></span>   | <span data-ttu-id="00e62-165">Description</span><span class="sxs-lookup"><span data-stu-id="00e62-165">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00e62-166">404</span><span class="sxs-lookup"><span data-stu-id="00e62-166">404</span></span>                  | <span data-ttu-id="00e62-167">400013</span><span class="sxs-lookup"><span data-stu-id="00e62-167">400013</span></span>       | <span data-ttu-id="00e62-168">Produkt nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="00e62-168">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="00e62-169">404</span><span class="sxs-lookup"><span data-stu-id="00e62-169">404</span></span>                  | <span data-ttu-id="00e62-170">400018</span><span class="sxs-lookup"><span data-stu-id="00e62-170">400018</span></span>       | <span data-ttu-id="00e62-171">SKU se nepovedlo najít.</span><span class="sxs-lookup"><span data-stu-id="00e62-171">Sku was not found.</span></span>                                                                                        |
| <span data-ttu-id="00e62-172">404</span><span class="sxs-lookup"><span data-stu-id="00e62-172">404</span></span>                  | <span data-ttu-id="00e62-173">400019</span><span class="sxs-lookup"><span data-stu-id="00e62-173">400019</span></span>       | <span data-ttu-id="00e62-174">Dostupnost se nenašla.</span><span class="sxs-lookup"><span data-stu-id="00e62-174">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="00e62-175">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="00e62-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": false,
    "terms": [{
        "duration": "P1Y",
        "description": "1 Year Prepaid"
    }],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
