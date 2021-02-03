---
title: Získání seznamu dostupností pro skladovou položku (podle země)
description: Jak získat kolekci dostupnosti pro zadaný produkt a SKU podle země zákazníka.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b97a4ce85b5edd9de1301a577988f8c54096ebeb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766792"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="e49a1-103">Získání seznamu dostupností pro skladovou položku (podle země)</span><span class="sxs-lookup"><span data-stu-id="e49a1-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="e49a1-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="e49a1-104">**Applies to:**</span></span>

- <span data-ttu-id="e49a1-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e49a1-105">Partner Center</span></span>

<span data-ttu-id="e49a1-106">Tento článek popisuje, jak získat kolekci dostupnosti dostupnosti v určité zemi pro určitý produkt a SKU.</span><span class="sxs-lookup"><span data-stu-id="e49a1-106">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e49a1-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e49a1-107">Prerequisites</span></span>

- <span data-ttu-id="e49a1-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e49a1-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e49a1-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e49a1-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e49a1-110">Identifikátor produktu.</span><span class="sxs-lookup"><span data-stu-id="e49a1-110">A product identifier.</span></span>

- <span data-ttu-id="e49a1-111">Identifikátor SKU.</span><span class="sxs-lookup"><span data-stu-id="e49a1-111">A SKU identifier.</span></span>

- <span data-ttu-id="e49a1-112">Země.</span><span class="sxs-lookup"><span data-stu-id="e49a1-112">A country.</span></span>

## <a name="c"></a><span data-ttu-id="e49a1-113">C\#</span><span class="sxs-lookup"><span data-stu-id="e49a1-113">C\#</span></span>

<span data-ttu-id="e49a1-114">Získání seznamu [dostupnosti](product-resources.md#availability) pro [SKU](product-resources.md#sku):</span><span class="sxs-lookup"><span data-stu-id="e49a1-114">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="e49a1-115">Postupujte podle kroků v části [získání SKU podle ID](get-a-sku-by-id.md) a získejte rozhraní pro konkrétní operace SKU.</span><span class="sxs-lookup"><span data-stu-id="e49a1-115">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="e49a1-116">V rozhraní SKU vyberte vlastnost **Nákup** a získejte rozhraní s operacemi pro nákup.</span><span class="sxs-lookup"><span data-stu-id="e49a1-116">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="e49a1-117">Volitelné K filtrování dostupnosti podle cílového segmentu použijte metodu **ByTargetSegment ()** .</span><span class="sxs-lookup"><span data-stu-id="e49a1-117">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="e49a1-118">Volání metody **Get ()** nebo **GetAsync ()** pro načtení kolekce dostupnosti pro tuto sku.</span><span class="sxs-lookup"><span data-stu-id="e49a1-118">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a><span data-ttu-id="e49a1-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e49a1-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e49a1-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e49a1-120">Request syntax</span></span>

| <span data-ttu-id="e49a1-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="e49a1-121">Method</span></span>  | <span data-ttu-id="e49a1-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e49a1-122">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e49a1-123">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="e49a1-123">**GET**</span></span> | <span data-ttu-id="e49a1-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/skus/{SKU-ID}/availabilities? Country = {Country-code} &targetSegment = {Target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e49a1-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="e49a1-125">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="e49a1-125">URI parameters</span></span>

<span data-ttu-id="e49a1-126">K získání seznamu dostupnosti pro SKU použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="e49a1-126">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="e49a1-127">Název</span><span class="sxs-lookup"><span data-stu-id="e49a1-127">Name</span></span>                   | <span data-ttu-id="e49a1-128">Typ</span><span class="sxs-lookup"><span data-stu-id="e49a1-128">Type</span></span>     | <span data-ttu-id="e49a1-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e49a1-129">Required</span></span> | <span data-ttu-id="e49a1-130">Popis</span><span class="sxs-lookup"><span data-stu-id="e49a1-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="e49a1-131">ID produktu</span><span class="sxs-lookup"><span data-stu-id="e49a1-131">product-id</span></span>             | <span data-ttu-id="e49a1-132">řetězec</span><span class="sxs-lookup"><span data-stu-id="e49a1-132">string</span></span>   | <span data-ttu-id="e49a1-133">Yes</span><span class="sxs-lookup"><span data-stu-id="e49a1-133">Yes</span></span>      | <span data-ttu-id="e49a1-134">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="e49a1-134">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="e49a1-135">SKU – ID</span><span class="sxs-lookup"><span data-stu-id="e49a1-135">sku-id</span></span>                 | <span data-ttu-id="e49a1-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="e49a1-136">string</span></span>   | <span data-ttu-id="e49a1-137">Yes</span><span class="sxs-lookup"><span data-stu-id="e49a1-137">Yes</span></span>      | <span data-ttu-id="e49a1-138">Řetězec, který identifikuje SKU.</span><span class="sxs-lookup"><span data-stu-id="e49a1-138">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="e49a1-139">kód země</span><span class="sxs-lookup"><span data-stu-id="e49a1-139">country-code</span></span>           | <span data-ttu-id="e49a1-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="e49a1-140">string</span></span>   | <span data-ttu-id="e49a1-141">Yes</span><span class="sxs-lookup"><span data-stu-id="e49a1-141">Yes</span></span>      | <span data-ttu-id="e49a1-142">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="e49a1-142">A country/region ID.</span></span>                                            |
| <span data-ttu-id="e49a1-143">cíl – segment</span><span class="sxs-lookup"><span data-stu-id="e49a1-143">target-segment</span></span>         | <span data-ttu-id="e49a1-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="e49a1-144">string</span></span>   | <span data-ttu-id="e49a1-145">No</span><span class="sxs-lookup"><span data-stu-id="e49a1-145">No</span></span>       | <span data-ttu-id="e49a1-146">Řetězec, který identifikuje cílový segment použitý pro filtrování.</span><span class="sxs-lookup"><span data-stu-id="e49a1-146">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="e49a1-147">reservationScope</span><span class="sxs-lookup"><span data-stu-id="e49a1-147">reservationScope</span></span> | <span data-ttu-id="e49a1-148">řetězec</span><span class="sxs-lookup"><span data-stu-id="e49a1-148">string</span></span>   | <span data-ttu-id="e49a1-149">No</span><span class="sxs-lookup"><span data-stu-id="e49a1-149">No</span></span> | <span data-ttu-id="e49a1-150">Při dotazování na seznam dostupnosti pro SKU Azure rezervované instance zadejte, `reservationScope=AzurePlan` že se má získat seznam dostupnosti, který platí pro AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="e49a1-150">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities which are applicable to AzurePlan.</span></span> <span data-ttu-id="e49a1-151">Vyloučením tohoto parametru získáte seznam dostupnosti, který se vztahuje na předplatná Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="e49a1-151">Exclude this parameter to get a list of availabilities which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="e49a1-152">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e49a1-152">Request headers</span></span>

<span data-ttu-id="e49a1-153">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e49a1-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e49a1-154">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e49a1-154">Request body</span></span>

<span data-ttu-id="e49a1-155">Žádné</span><span class="sxs-lookup"><span data-stu-id="e49a1-155">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="e49a1-156">Příklady požadavků</span><span class="sxs-lookup"><span data-stu-id="e49a1-156">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="e49a1-157">Dostupnosti pro SKU podle země</span><span class="sxs-lookup"><span data-stu-id="e49a1-157">Availabilities for SKU by country</span></span>

<span data-ttu-id="e49a1-158">Podle tohoto příkladu Získejte seznam dostupnosti pro danou skladovou jednotku podle země:</span><span class="sxs-lookup"><span data-stu-id="e49a1-158">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="e49a1-159">Dostupnosti pro rezervace virtuálních počítačů (plán Azure)</span><span class="sxs-lookup"><span data-stu-id="e49a1-159">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="e49a1-160">Podle tohoto příkladu Získejte seznam dostupnosti podle země pro skladové položky rezervace virtuálních počítačů Azure.</span><span class="sxs-lookup"><span data-stu-id="e49a1-160">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="e49a1-161">Tento příklad je pro SKU, které se vztahují na plány Azure:</span><span class="sxs-lookup"><span data-stu-id="e49a1-161">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="e49a1-162">Dostupnosti pro rezervace virtuálních počítačů pro předplatná Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="e49a1-162">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="e49a1-163">Podle tohoto příkladu Získejte seznam dostupnosti v rámci země pro rezervace virtuálních počítačů Azure, které platí pro předplatná Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="e49a1-163">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="e49a1-164">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e49a1-164">REST response</span></span>

<span data-ttu-id="e49a1-165">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [**dostupnosti**](product-resources.md#availability) .</span><span class="sxs-lookup"><span data-stu-id="e49a1-165">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e49a1-166">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e49a1-166">Response success and error codes</span></span>

<span data-ttu-id="e49a1-167">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e49a1-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e49a1-168">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e49a1-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e49a1-169">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e49a1-169">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="e49a1-170">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="e49a1-170">This method returns the following error codes:</span></span>

| <span data-ttu-id="e49a1-171">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="e49a1-171">HTTP Status Code</span></span>     | <span data-ttu-id="e49a1-172">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="e49a1-172">Error code</span></span>   | <span data-ttu-id="e49a1-173">Description</span><span class="sxs-lookup"><span data-stu-id="e49a1-173">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e49a1-174">403</span><span class="sxs-lookup"><span data-stu-id="e49a1-174">403</span></span>                  | <span data-ttu-id="e49a1-175">400030</span><span class="sxs-lookup"><span data-stu-id="e49a1-175">400030</span></span>       | <span data-ttu-id="e49a1-176">Přístup k požadovanému **targetSegment** není povolený.</span><span class="sxs-lookup"><span data-stu-id="e49a1-176">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="e49a1-177">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e49a1-177">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
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
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
