---
title: Získání produktu podle ID
description: Získá zadaný prostředek produktu pomocí ID produktu.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 769a4307dc3cebdc7ebbdcf51d9f2b67a9f4b7c2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874019"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="bb44d-103">Získání produktu podle ID</span><span class="sxs-lookup"><span data-stu-id="bb44d-103">Get a product by ID</span></span>

<span data-ttu-id="bb44d-104">Získá zadaný prostředek produktu pomocí ID produktu.</span><span class="sxs-lookup"><span data-stu-id="bb44d-104">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb44d-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bb44d-105">Prerequisites</span></span>

- <span data-ttu-id="bb44d-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bb44d-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bb44d-107">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="bb44d-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="bb44d-108">ID produktu.</span><span class="sxs-lookup"><span data-stu-id="bb44d-108">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="bb44d-109">C\#</span><span class="sxs-lookup"><span data-stu-id="bb44d-109">C\#</span></span>

<span data-ttu-id="bb44d-110">Pokud chcete vyhledat konkrétní produkt podle ID, použijte kolekci **IAggregatePartner.Products,** vyberte zemi pomocí metody **ByCountry()** a pak zavolejte metodu **ById().**</span><span class="sxs-lookup"><span data-stu-id="bb44d-110">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="bb44d-111">Nakonec zavolejte **metodu Get()** nebo **GetAsync(),** která vrátí produkt.</span><span class="sxs-lookup"><span data-stu-id="bb44d-111">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="bb44d-112">Java</span><span class="sxs-lookup"><span data-stu-id="bb44d-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="bb44d-113">Pokud chcete vyhledat konkrétní produkt podle ID, použijte funkci **IAggregatePartner.getProducts,** vyberte zemi pomocí funkce **byCountry()** a potom zavolejte funkci **byId().**</span><span class="sxs-lookup"><span data-stu-id="bb44d-113">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="bb44d-114">Nakonec zavolejte funkci **get(),** která vrátí produkt.</span><span class="sxs-lookup"><span data-stu-id="bb44d-114">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="bb44d-115">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb44d-115">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="bb44d-116">Pokud chcete najít konkrétní produkt podle ID, spusťte příkaz [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) a zadejte parametr **ProductId.**</span><span class="sxs-lookup"><span data-stu-id="bb44d-116">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="bb44d-117">Parametr **CountryCode** je možnost, pokud není zadaný, použije se země přidružená k prodejci.</span><span class="sxs-lookup"><span data-stu-id="bb44d-117">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="bb44d-118">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="bb44d-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bb44d-119">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="bb44d-119">Request syntax</span></span>

| <span data-ttu-id="bb44d-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="bb44d-120">Method</span></span>  | <span data-ttu-id="bb44d-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="bb44d-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="bb44d-122">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="bb44d-122">**GET**</span></span> | <span data-ttu-id="bb44d-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{ID_produktu}?country={země} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bb44d-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="bb44d-124">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="bb44d-124">URI parameter</span></span>

<span data-ttu-id="bb44d-125">K získání zadaného produktu použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="bb44d-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="bb44d-126">Název</span><span class="sxs-lookup"><span data-stu-id="bb44d-126">Name</span></span>                   | <span data-ttu-id="bb44d-127">Typ</span><span class="sxs-lookup"><span data-stu-id="bb44d-127">Type</span></span>     | <span data-ttu-id="bb44d-128">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="bb44d-128">Required</span></span> | <span data-ttu-id="bb44d-129">Popis</span><span class="sxs-lookup"><span data-stu-id="bb44d-129">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="bb44d-130">id produktu</span><span class="sxs-lookup"><span data-stu-id="bb44d-130">product-id</span></span>             | <span data-ttu-id="bb44d-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="bb44d-131">string</span></span>   | <span data-ttu-id="bb44d-132">Yes</span><span class="sxs-lookup"><span data-stu-id="bb44d-132">Yes</span></span>      | <span data-ttu-id="bb44d-133">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="bb44d-133">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="bb44d-134">country</span><span class="sxs-lookup"><span data-stu-id="bb44d-134">country</span></span>                | <span data-ttu-id="bb44d-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="bb44d-135">string</span></span>   | <span data-ttu-id="bb44d-136">Yes</span><span class="sxs-lookup"><span data-stu-id="bb44d-136">Yes</span></span>      | <span data-ttu-id="bb44d-137">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="bb44d-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="bb44d-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="bb44d-138">Request headers</span></span>

<span data-ttu-id="bb44d-139">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bb44d-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bb44d-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="bb44d-140">Request body</span></span>

<span data-ttu-id="bb44d-141">Žádné</span><span class="sxs-lookup"><span data-stu-id="bb44d-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bb44d-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bb44d-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="bb44d-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="bb44d-143">REST response</span></span>

<span data-ttu-id="bb44d-144">V případě úspěchu bude text odpovědi obsahovat [prostředek Product.](product-resources.md#product)</span><span class="sxs-lookup"><span data-stu-id="bb44d-144">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bb44d-145">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="bb44d-145">Response success and error codes</span></span>

<span data-ttu-id="bb44d-146">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="bb44d-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bb44d-147">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="bb44d-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bb44d-148">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="bb44d-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="bb44d-149">Tato metoda vrátí následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="bb44d-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="bb44d-150">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="bb44d-150">HTTP Status Code</span></span>     | <span data-ttu-id="bb44d-151">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="bb44d-151">Error code</span></span>   | <span data-ttu-id="bb44d-152">Description</span><span class="sxs-lookup"><span data-stu-id="bb44d-152">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="bb44d-153">404</span><span class="sxs-lookup"><span data-stu-id="bb44d-153">404</span></span>                  | <span data-ttu-id="bb44d-154">400013</span><span class="sxs-lookup"><span data-stu-id="bb44d-154">400013</span></span>       | <span data-ttu-id="bb44d-155">Produkt se nenašel.</span><span class="sxs-lookup"><span data-stu-id="bb44d-155">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="bb44d-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bb44d-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
