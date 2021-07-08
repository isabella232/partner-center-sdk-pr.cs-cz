---
title: Získání seznamu dostupností pro skladovou položku (podle země)
description: Jak získat kolekci dostupnosti pro zadaný produkt a SKU podle země zákazníka.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b29c005e74ad8a4da547a888b78e4599e74ebd02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874529"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="274cf-103">Získání seznamu dostupností pro skladovou položku (podle země)</span><span class="sxs-lookup"><span data-stu-id="274cf-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="274cf-104">Tento článek popisuje, jak získat kolekci dostupnosti v konkrétní zemi pro zadaný produkt a SKU.</span><span class="sxs-lookup"><span data-stu-id="274cf-104">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="274cf-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="274cf-105">Prerequisites</span></span>

- <span data-ttu-id="274cf-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="274cf-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="274cf-107">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="274cf-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="274cf-108">Identifikátor produktu.</span><span class="sxs-lookup"><span data-stu-id="274cf-108">A product identifier.</span></span>

- <span data-ttu-id="274cf-109">Identifikátor SKU.</span><span class="sxs-lookup"><span data-stu-id="274cf-109">A SKU identifier.</span></span>

- <span data-ttu-id="274cf-110">Země.</span><span class="sxs-lookup"><span data-stu-id="274cf-110">A country.</span></span>

## <a name="c"></a><span data-ttu-id="274cf-111">C\#</span><span class="sxs-lookup"><span data-stu-id="274cf-111">C\#</span></span>

<span data-ttu-id="274cf-112">Získání seznamu dostupnosti [pro](product-resources.md#availability) [SKU:](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="274cf-112">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="274cf-113">Postupujte podle kroků v [části Získání SKU podle ID](get-a-sku-by-id.md) a získejte rozhraní pro operace konkrétní SKU.</span><span class="sxs-lookup"><span data-stu-id="274cf-113">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="274cf-114">V rozhraní SKU vyberte vlastnost **Availabilities** a získejte rozhraní s operacemi pro dostupnost.</span><span class="sxs-lookup"><span data-stu-id="274cf-114">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="274cf-115">(Volitelné) K filtrování dostupnosti podle cílového segmentu použijte metodu **ByTargetSegment().**</span><span class="sxs-lookup"><span data-stu-id="274cf-115">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="274cf-116">Voláním **metody Get()** nebo **GetAsync()** načtěte kolekci dostupnosti pro tuto skladové číslo.</span><span class="sxs-lookup"><span data-stu-id="274cf-116">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="274cf-117">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="274cf-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="274cf-118">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="274cf-118">Request syntax</span></span>

| <span data-ttu-id="274cf-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="274cf-119">Method</span></span>  | <span data-ttu-id="274cf-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="274cf-120">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="274cf-121">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="274cf-121">**GET**</span></span> | <span data-ttu-id="274cf-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{id_produktu}/skus/{id_SKU}/availabilities?country={kód_země}&targetSegment={target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="274cf-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="274cf-123">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="274cf-123">URI parameters</span></span>

<span data-ttu-id="274cf-124">Pomocí následující cesty a parametrů dotazu získejte seznam dostupnosti pro SKU.</span><span class="sxs-lookup"><span data-stu-id="274cf-124">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="274cf-125">Název</span><span class="sxs-lookup"><span data-stu-id="274cf-125">Name</span></span>                   | <span data-ttu-id="274cf-126">Typ</span><span class="sxs-lookup"><span data-stu-id="274cf-126">Type</span></span>     | <span data-ttu-id="274cf-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="274cf-127">Required</span></span> | <span data-ttu-id="274cf-128">Popis</span><span class="sxs-lookup"><span data-stu-id="274cf-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="274cf-129">id produktu</span><span class="sxs-lookup"><span data-stu-id="274cf-129">product-id</span></span>             | <span data-ttu-id="274cf-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="274cf-130">string</span></span>   | <span data-ttu-id="274cf-131">Yes</span><span class="sxs-lookup"><span data-stu-id="274cf-131">Yes</span></span>      | <span data-ttu-id="274cf-132">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="274cf-132">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="274cf-133">sku-id</span><span class="sxs-lookup"><span data-stu-id="274cf-133">sku-id</span></span>                 | <span data-ttu-id="274cf-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="274cf-134">string</span></span>   | <span data-ttu-id="274cf-135">Yes</span><span class="sxs-lookup"><span data-stu-id="274cf-135">Yes</span></span>      | <span data-ttu-id="274cf-136">Řetězec, který identifikuje SKU.</span><span class="sxs-lookup"><span data-stu-id="274cf-136">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="274cf-137">kód země</span><span class="sxs-lookup"><span data-stu-id="274cf-137">country-code</span></span>           | <span data-ttu-id="274cf-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="274cf-138">string</span></span>   | <span data-ttu-id="274cf-139">Yes</span><span class="sxs-lookup"><span data-stu-id="274cf-139">Yes</span></span>      | <span data-ttu-id="274cf-140">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="274cf-140">A country/region ID.</span></span>                                            |
| <span data-ttu-id="274cf-141">target-segment</span><span class="sxs-lookup"><span data-stu-id="274cf-141">target-segment</span></span>         | <span data-ttu-id="274cf-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="274cf-142">string</span></span>   | <span data-ttu-id="274cf-143">No</span><span class="sxs-lookup"><span data-stu-id="274cf-143">No</span></span>       | <span data-ttu-id="274cf-144">Řetězec, který identifikuje cílový segment použitý k filtrování.</span><span class="sxs-lookup"><span data-stu-id="274cf-144">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="274cf-145">reservationScope</span><span class="sxs-lookup"><span data-stu-id="274cf-145">reservationScope</span></span> | <span data-ttu-id="274cf-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="274cf-146">string</span></span>   | <span data-ttu-id="274cf-147">No</span><span class="sxs-lookup"><span data-stu-id="274cf-147">No</span></span> | <span data-ttu-id="274cf-148">Při dotazování na seznam dostupnosti pro SKU rezervace Azure zadejte , abyste získali seznam dostupnosti, které se vztahují `reservationScope=AzurePlan` na AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="274cf-148">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities that are applicable to AzurePlan.</span></span> <span data-ttu-id="274cf-149">Tento parametr vyloučíte, pokud chcete získat seznam dostupnosti, které se vztahují Microsoft Azure předplatná MS-AZR-0145P.</span><span class="sxs-lookup"><span data-stu-id="274cf-149">Exclude this parameter to get a list of availabilities that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="274cf-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="274cf-150">Request headers</span></span>

<span data-ttu-id="274cf-151">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="274cf-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="274cf-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="274cf-152">Request body</span></span>

<span data-ttu-id="274cf-153">Žádné</span><span class="sxs-lookup"><span data-stu-id="274cf-153">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="274cf-154">Příklady požadavků</span><span class="sxs-lookup"><span data-stu-id="274cf-154">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="274cf-155">Dostupnost SKU podle země</span><span class="sxs-lookup"><span data-stu-id="274cf-155">Availabilities for SKU by country</span></span>

<span data-ttu-id="274cf-156">Pokud chcete získat seznam dostupnosti pro danou SKU podle země, postupujte podle tohoto příkladu:</span><span class="sxs-lookup"><span data-stu-id="274cf-156">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="274cf-157">Dostupnost pro rezervace virtuálních počítače (plán Azure)</span><span class="sxs-lookup"><span data-stu-id="274cf-157">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="274cf-158">Postupujte podle tohoto příkladu a získejte seznam dostupnosti pro skladové položky rezervací virtuálních počítače Azure podle země.</span><span class="sxs-lookup"><span data-stu-id="274cf-158">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="274cf-159">Tento příklad je pro SKU, které se vztahují na plány Azure:</span><span class="sxs-lookup"><span data-stu-id="274cf-159">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="274cf-160">Dostupnost rezervací virtuálních Microsoft Azure předplatných (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="274cf-160">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="274cf-161">Postupujte podle tohoto příkladu a získejte seznam dostupnosti pro rezervace virtuálních počítače Azure podle země, které se vztahují na předplatná Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="274cf-161">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="274cf-162">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="274cf-162">REST response</span></span>

<span data-ttu-id="274cf-163">V případě úspěchu bude tělo odpovědi obsahovat kolekci [**prostředků**](product-resources.md#availability) dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="274cf-163">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="274cf-164">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="274cf-164">Response success and error codes</span></span>

<span data-ttu-id="274cf-165">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="274cf-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="274cf-166">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="274cf-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="274cf-167">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="274cf-167">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="274cf-168">Tato metoda vrátí následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="274cf-168">This method returns the following error codes:</span></span>

| <span data-ttu-id="274cf-169">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="274cf-169">HTTP Status Code</span></span>     | <span data-ttu-id="274cf-170">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="274cf-170">Error code</span></span>   | <span data-ttu-id="274cf-171">Description</span><span class="sxs-lookup"><span data-stu-id="274cf-171">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="274cf-172">403</span><span class="sxs-lookup"><span data-stu-id="274cf-172">403</span></span>                  | <span data-ttu-id="274cf-173">400030</span><span class="sxs-lookup"><span data-stu-id="274cf-173">400030</span></span>       | <span data-ttu-id="274cf-174">Přístup k **požadovanému targetSegment** není povolený.</span><span class="sxs-lookup"><span data-stu-id="274cf-174">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="274cf-175">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="274cf-175">Response example</span></span>

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
