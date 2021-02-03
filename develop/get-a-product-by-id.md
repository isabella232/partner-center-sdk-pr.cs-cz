---
title: Získání produktu podle ID
description: Získá zadaný produkt prostředku s použitím ID produktu.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 8aca626597e9ec903ebecca7d55577ba636c518e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766762"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="30e16-103">Získání produktu podle ID</span><span class="sxs-lookup"><span data-stu-id="30e16-103">Get a product by ID</span></span>

<span data-ttu-id="30e16-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="30e16-104">**Applies To**</span></span>

- <span data-ttu-id="30e16-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="30e16-105">Partner Center</span></span>

<span data-ttu-id="30e16-106">Získá zadaný produkt prostředku s použitím ID produktu.</span><span class="sxs-lookup"><span data-stu-id="30e16-106">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30e16-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="30e16-107">Prerequisites</span></span>

- <span data-ttu-id="30e16-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="30e16-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="30e16-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="30e16-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="30e16-110">ID produktu.</span><span class="sxs-lookup"><span data-stu-id="30e16-110">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="30e16-111">C\#</span><span class="sxs-lookup"><span data-stu-id="30e16-111">C\#</span></span>

<span data-ttu-id="30e16-112">Chcete-li najít konkrétní produkt podle ID, použijte kolekci **IAggregatePartner. Products** , vyberte zemi pomocí metody **ByCountry ()** a potom zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="30e16-112">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="30e16-113">Nakonec voláním metody **Get ()** nebo **GetAsync ()** vraťte produkt.</span><span class="sxs-lookup"><span data-stu-id="30e16-113">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="30e16-114">Java</span><span class="sxs-lookup"><span data-stu-id="30e16-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="30e16-115">Chcete-li najít konkrétní produkt podle ID, použijte funkci **IAggregatePartner. GetProducts** , vyberte zemi pomocí funkce **byCountry ()** a potom zavolejte funkci **byId ()** .</span><span class="sxs-lookup"><span data-stu-id="30e16-115">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="30e16-116">Nakonec zavolejte funkci **Get ()** , která vrátí produkt.</span><span class="sxs-lookup"><span data-stu-id="30e16-116">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="30e16-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="30e16-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="30e16-118">Chcete-li najít konkrétní produkt podle ID, spusťte příkaz [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) a zadejte parametr **ProductID** .</span><span class="sxs-lookup"><span data-stu-id="30e16-118">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="30e16-119">Parametr **CountryCode** je možností, pokud není zadaný, použije se země přidružená k prodejci.</span><span class="sxs-lookup"><span data-stu-id="30e16-119">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="30e16-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="30e16-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="30e16-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="30e16-121">Request syntax</span></span>

| <span data-ttu-id="30e16-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="30e16-122">Method</span></span>  | <span data-ttu-id="30e16-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="30e16-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="30e16-124">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="30e16-124">**GET**</span></span> | <span data-ttu-id="30e16-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}? Country = {Country} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="30e16-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="30e16-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="30e16-126">URI parameter</span></span>

<span data-ttu-id="30e16-127">K získání zadaného produktu použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="30e16-127">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="30e16-128">Název</span><span class="sxs-lookup"><span data-stu-id="30e16-128">Name</span></span>                   | <span data-ttu-id="30e16-129">Typ</span><span class="sxs-lookup"><span data-stu-id="30e16-129">Type</span></span>     | <span data-ttu-id="30e16-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="30e16-130">Required</span></span> | <span data-ttu-id="30e16-131">Popis</span><span class="sxs-lookup"><span data-stu-id="30e16-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="30e16-132">ID produktu</span><span class="sxs-lookup"><span data-stu-id="30e16-132">product-id</span></span>             | <span data-ttu-id="30e16-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="30e16-133">string</span></span>   | <span data-ttu-id="30e16-134">Yes</span><span class="sxs-lookup"><span data-stu-id="30e16-134">Yes</span></span>      | <span data-ttu-id="30e16-135">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="30e16-135">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="30e16-136">country</span><span class="sxs-lookup"><span data-stu-id="30e16-136">country</span></span>                | <span data-ttu-id="30e16-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="30e16-137">string</span></span>   | <span data-ttu-id="30e16-138">Yes</span><span class="sxs-lookup"><span data-stu-id="30e16-138">Yes</span></span>      | <span data-ttu-id="30e16-139">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="30e16-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="30e16-140">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="30e16-140">Request headers</span></span>

<span data-ttu-id="30e16-141">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="30e16-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="30e16-142">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="30e16-142">Request body</span></span>

<span data-ttu-id="30e16-143">Žádné</span><span class="sxs-lookup"><span data-stu-id="30e16-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="30e16-144">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="30e16-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="30e16-145">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="30e16-145">REST response</span></span>

<span data-ttu-id="30e16-146">V případě úspěchu obsahuje tělo odpovědi [produktový](product-resources.md#product) prostředek.</span><span class="sxs-lookup"><span data-stu-id="30e16-146">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="30e16-147">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="30e16-147">Response success and error codes</span></span>

<span data-ttu-id="30e16-148">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="30e16-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="30e16-149">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="30e16-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="30e16-150">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="30e16-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="30e16-151">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="30e16-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="30e16-152">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="30e16-152">HTTP Status Code</span></span>     | <span data-ttu-id="30e16-153">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="30e16-153">Error code</span></span>   | <span data-ttu-id="30e16-154">Description</span><span class="sxs-lookup"><span data-stu-id="30e16-154">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="30e16-155">404</span><span class="sxs-lookup"><span data-stu-id="30e16-155">404</span></span>                  | <span data-ttu-id="30e16-156">400013</span><span class="sxs-lookup"><span data-stu-id="30e16-156">400013</span></span>       | <span data-ttu-id="30e16-157">Produkt nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="30e16-157">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="30e16-158">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="30e16-158">Response example</span></span>

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
