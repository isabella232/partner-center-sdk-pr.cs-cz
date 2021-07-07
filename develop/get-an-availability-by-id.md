---
title: Získání dostupnosti podle ID
description: Získá dostupnost pro zadaný produkt a SKU pomocí ID dostupnosti.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c31bc12d8d484cc8042f36aa865145600d9e6738
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760194"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="eb4ab-103">Získání dostupnosti podle ID</span><span class="sxs-lookup"><span data-stu-id="eb4ab-103">Get the availability by ID</span></span>

<span data-ttu-id="eb4ab-104">Získá dostupnost pro zadaný produkt a SKU pomocí ID dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-104">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb4ab-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="eb4ab-105">Prerequisites</span></span>

- <span data-ttu-id="eb4ab-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="eb4ab-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="eb4ab-107">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="eb4ab-108">ID produktu.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-108">A product ID.</span></span>

- <span data-ttu-id="eb4ab-109">ID SKU.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-109">A SKU ID.</span></span>

- <span data-ttu-id="eb4ab-110">ID dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-110">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="eb4ab-111">C\#</span><span class="sxs-lookup"><span data-stu-id="eb4ab-111">C\#</span></span>

<span data-ttu-id="eb4ab-112">Pokud chcete získat podrobnosti o konkrétní [dostupnosti,](product-resources.md#availability)začněte postupem v tématu Získání [SKU podle ID](get-a-sku-by-id.md) a získejte rozhraní pro operace [konkrétní SKU.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="eb4ab-112">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="eb4ab-113">Ve výsledném rozhraní vyberte vlastnost **Availabilities** a získejte rozhraní s dostupnými operacemi pro dostupnost.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-113">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="eb4ab-114">Potom předejte ID dostupnosti metodě **ById(),** abyste získali operace pro tuto konkrétní dostupnost, a potom zavoláte **Get()** nebo **GetAsync()** a načtete podrobnosti o dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-114">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="eb4ab-115">Java</span><span class="sxs-lookup"><span data-stu-id="eb4ab-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="eb4ab-116">Pokud chcete získat podrobnosti o konkrétní [dostupnosti,](product-resources.md#availability)začněte postupem v tématu Získání [SKU podle ID](get-a-sku-by-id.md) a získejte rozhraní pro operace [konkrétní SKU.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="eb4ab-116">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="eb4ab-117">Ve výsledném rozhraní vyberte funkci **getAvailabilities** a získejte rozhraní s dostupnými operacemi pro dostupnost.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-117">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="eb4ab-118">Potom předejte ID dostupnosti do funkce **byId(),** abyste získali operace pro tuto konkrétní dostupnost, a potom zavoláte funkci **get(),** která načte podrobnosti o dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-118">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="eb4ab-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb4ab-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="eb4ab-120">Pokud chcete získat podrobnosti o konkrétní [dostupnosti,](product-resources.md#availability)spusťte [**get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) a zadáním parametrů **AvailabilityId**, **CountryCode**, **ProductId** a **SkuId** načtěte podrobnosti o dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-120">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="eb4ab-121">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="eb4ab-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="eb4ab-122">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="eb4ab-122">Request syntax</span></span>

| <span data-ttu-id="eb4ab-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="eb4ab-123">Method</span></span>  | <span data-ttu-id="eb4ab-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="eb4ab-124">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="eb4ab-125">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="eb4ab-125">**GET**</span></span> | <span data-ttu-id="eb4ab-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{ID_produktu}/skus/{ID_SKU}/availabilities/{ID_dostupnosti}?country={kód_země} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="eb4ab-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="eb4ab-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="eb4ab-127">URI parameter</span></span>

<span data-ttu-id="eb4ab-128">Pomocí následující cesty a parametrů dotazu získejte konkrétní dostupnost pomocí ID dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-128">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="eb4ab-129">Název</span><span class="sxs-lookup"><span data-stu-id="eb4ab-129">Name</span></span>                   | <span data-ttu-id="eb4ab-130">Typ</span><span class="sxs-lookup"><span data-stu-id="eb4ab-130">Type</span></span>     | <span data-ttu-id="eb4ab-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="eb4ab-131">Required</span></span> | <span data-ttu-id="eb4ab-132">Popis</span><span class="sxs-lookup"><span data-stu-id="eb4ab-132">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="eb4ab-133">id produktu</span><span class="sxs-lookup"><span data-stu-id="eb4ab-133">product-id</span></span>             | <span data-ttu-id="eb4ab-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="eb4ab-134">string</span></span>   | <span data-ttu-id="eb4ab-135">Yes</span><span class="sxs-lookup"><span data-stu-id="eb4ab-135">Yes</span></span>      | <span data-ttu-id="eb4ab-136">Řetězec formátovaný identifikátorem GUID, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-136">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="eb4ab-137">sku-id</span><span class="sxs-lookup"><span data-stu-id="eb4ab-137">sku-id</span></span>                 | <span data-ttu-id="eb4ab-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="eb4ab-138">string</span></span>   | <span data-ttu-id="eb4ab-139">Yes</span><span class="sxs-lookup"><span data-stu-id="eb4ab-139">Yes</span></span>      | <span data-ttu-id="eb4ab-140">Řetězec formátovaný identifikátorem GUID, který identifikuje SKU.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-140">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="eb4ab-141">ID dostupnosti</span><span class="sxs-lookup"><span data-stu-id="eb4ab-141">availability-id</span></span>        | <span data-ttu-id="eb4ab-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="eb4ab-142">string</span></span>   | <span data-ttu-id="eb4ab-143">Yes</span><span class="sxs-lookup"><span data-stu-id="eb4ab-143">Yes</span></span>      | <span data-ttu-id="eb4ab-144">Řetězec formátovaný identifikátorem GUID, který identifikuje dostupnost.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-144">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="eb4ab-145">kód země</span><span class="sxs-lookup"><span data-stu-id="eb4ab-145">country-code</span></span>           | <span data-ttu-id="eb4ab-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="eb4ab-146">string</span></span>   | <span data-ttu-id="eb4ab-147">Yes</span><span class="sxs-lookup"><span data-stu-id="eb4ab-147">Yes</span></span>      | <span data-ttu-id="eb4ab-148">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-148">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="eb4ab-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="eb4ab-149">Request headers</span></span>

<span data-ttu-id="eb4ab-150">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="eb4ab-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="eb4ab-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="eb4ab-151">Request body</span></span>

<span data-ttu-id="eb4ab-152">Žádné</span><span class="sxs-lookup"><span data-stu-id="eb4ab-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="eb4ab-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="eb4ab-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="eb4ab-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="eb4ab-154">REST response</span></span>

<span data-ttu-id="eb4ab-155">V případě úspěchu bude tělo odpovědi obsahovat [prostředek](product-resources.md#availability) dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-155">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="eb4ab-156">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="eb4ab-156">Response success and error codes</span></span>

<span data-ttu-id="eb4ab-157">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="eb4ab-158">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="eb4ab-159">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="eb4ab-159">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="eb4ab-160">Tato metoda vrátí následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="eb4ab-160">This method returns the following error codes:</span></span>

| <span data-ttu-id="eb4ab-161">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="eb4ab-161">HTTP Status Code</span></span>     | <span data-ttu-id="eb4ab-162">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="eb4ab-162">Error code</span></span>   | <span data-ttu-id="eb4ab-163">Description</span><span class="sxs-lookup"><span data-stu-id="eb4ab-163">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="eb4ab-164">404</span><span class="sxs-lookup"><span data-stu-id="eb4ab-164">404</span></span>                  | <span data-ttu-id="eb4ab-165">400013</span><span class="sxs-lookup"><span data-stu-id="eb4ab-165">400013</span></span>       | <span data-ttu-id="eb4ab-166">Produkt se nenašel.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-166">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="eb4ab-167">404</span><span class="sxs-lookup"><span data-stu-id="eb4ab-167">404</span></span>                  | <span data-ttu-id="eb4ab-168">400018</span><span class="sxs-lookup"><span data-stu-id="eb4ab-168">400018</span></span>       | <span data-ttu-id="eb4ab-169">SKU se nenašla.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-169">SKU was not found.</span></span>                                                                                        |
| <span data-ttu-id="eb4ab-170">404</span><span class="sxs-lookup"><span data-stu-id="eb4ab-170">404</span></span>                  | <span data-ttu-id="eb4ab-171">400019</span><span class="sxs-lookup"><span data-stu-id="eb4ab-171">400019</span></span>       | <span data-ttu-id="eb4ab-172">Dostupnost se nenašla.</span><span class="sxs-lookup"><span data-stu-id="eb4ab-172">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="eb4ab-173">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="eb4ab-173">Response example</span></span>

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
