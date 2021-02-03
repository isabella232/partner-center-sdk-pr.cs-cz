---
title: Získání seznamu skladových položek pro produkt (podle země)
description: Můžete získat a filtrovat kolekci SKU podle země pro produkt pomocí rozhraní API partnerského centra.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9d5ec9172ed92d33e6ff291eafd523cbc13bfbbd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766782"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a><span data-ttu-id="7e748-103">Získání seznamu skladových položek pro produkt (podle země)</span><span class="sxs-lookup"><span data-stu-id="7e748-103">Get a list of SKUs for a product (by country)</span></span>

<span data-ttu-id="7e748-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="7e748-104">**Applies to:**</span></span>

- <span data-ttu-id="7e748-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="7e748-105">Partner Center</span></span>

<span data-ttu-id="7e748-106">Můžete získat kolekci SKU dostupných v zemi pro určitý produkt pomocí rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="7e748-106">You can get a collection of SKUs available in a country for a specific product using Partner Center APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e748-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7e748-107">Prerequisites</span></span>

- <span data-ttu-id="7e748-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7e748-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7e748-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="7e748-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7e748-110">Identifikátor produktu.</span><span class="sxs-lookup"><span data-stu-id="7e748-110">A product identifier.</span></span>

## <a name="c"></a><span data-ttu-id="7e748-111">C\#</span><span class="sxs-lookup"><span data-stu-id="7e748-111">C\#</span></span>

<span data-ttu-id="7e748-112">Získání seznamu SKU pro produkt:</span><span class="sxs-lookup"><span data-stu-id="7e748-112">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="7e748-113">Pomocí postupu v části [získání produktu podle ID](get-a-product-by-id.md)Získejte rozhraní pro konkrétní operace produktu.</span><span class="sxs-lookup"><span data-stu-id="7e748-113">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="7e748-114">Z rozhraní vyberte vlastnost **SKU** a získejte rozhraní s dostupnými operacemi pro skladové položky.</span><span class="sxs-lookup"><span data-stu-id="7e748-114">From the interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="7e748-115">Zavolejte metodu **Get ()** nebo **GetAsync ()** pro načtení kolekce dostupných SKU pro daný produkt.</span><span class="sxs-lookup"><span data-stu-id="7e748-115">Call the **Get()** or **GetAsync()** method to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="7e748-116">Volitelné Vyberte rozsah rezervace pomocí metody **ByReservationScope ()** .</span><span class="sxs-lookup"><span data-stu-id="7e748-116">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

5. <span data-ttu-id="7e748-117">Volitelné Použijte metodu **ByTargetSegment ()** pro filtrování SKU podle cílového segmentu před voláním metody **Get ()** nebo **GetAsync ()**.</span><span class="sxs-lookup"><span data-stu-id="7e748-117">(Optional) Use the **ByTargetSegment()** method to filter the SKUs by target segment before calling **Get()** or **GetAsync()**.</span></span>

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="7e748-118">Java</span><span class="sxs-lookup"><span data-stu-id="7e748-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="7e748-119">Získání seznamu SKU pro produkt:</span><span class="sxs-lookup"><span data-stu-id="7e748-119">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="7e748-120">Pomocí postupu v části [získání produktu podle ID](get-a-product-by-id.md)Získejte rozhraní pro konkrétní operace produktu.</span><span class="sxs-lookup"><span data-stu-id="7e748-120">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="7e748-121">Z rozhraní vyberte funkci **GetSku** pro získání rozhraní s dostupnými operacemi pro skladové položky.</span><span class="sxs-lookup"><span data-stu-id="7e748-121">From the interface, select the **getSkus** function to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="7e748-122">Voláním funkce **Get ()** načtěte kolekci dostupných SKU pro daný produkt.</span><span class="sxs-lookup"><span data-stu-id="7e748-122">Call the **get()** function to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="7e748-123">Volitelné Použijte funkci **byTargetSegment ()** pro filtrování SKU podle cílového segmentu před voláním funkce **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="7e748-123">(Optional) Use the **byTargetSegment()** function to filter the SKUs by target segment before calling the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a><span data-ttu-id="7e748-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e748-124">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="7e748-125">Získání seznamu SKU pro produkt:</span><span class="sxs-lookup"><span data-stu-id="7e748-125">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="7e748-126">Spusťte příkaz [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) .</span><span class="sxs-lookup"><span data-stu-id="7e748-126">Execute the [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) command.</span></span>

2. <span data-ttu-id="7e748-127">Volitelné Určete parametr **segmentu** pro filtrování SKU podle cílového segmentu.</span><span class="sxs-lookup"><span data-stu-id="7e748-127">(Optional) Specify the **Segment** parameter to filter the SKUs by target segment.</span></span>

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a><span data-ttu-id="7e748-128">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="7e748-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7e748-129">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="7e748-129">Request syntax</span></span>

| <span data-ttu-id="7e748-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="7e748-130">Method</span></span>  | <span data-ttu-id="7e748-131">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="7e748-131">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7e748-132">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="7e748-132">**GET**</span></span> | <span data-ttu-id="7e748-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/skus? Country = {Country-code} &targetSegment = {Target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7e748-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="7e748-134">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="7e748-134">URI parameters</span></span>

<span data-ttu-id="7e748-135">K získání seznamu SKU pro produkt použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="7e748-135">Use the following path and query parameters to get a list of SKUs for a product.</span></span>

| <span data-ttu-id="7e748-136">Název</span><span class="sxs-lookup"><span data-stu-id="7e748-136">Name</span></span>                   | <span data-ttu-id="7e748-137">Typ</span><span class="sxs-lookup"><span data-stu-id="7e748-137">Type</span></span>     | <span data-ttu-id="7e748-138">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="7e748-138">Required</span></span> | <span data-ttu-id="7e748-139">Popis</span><span class="sxs-lookup"><span data-stu-id="7e748-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="7e748-140">ID produktu</span><span class="sxs-lookup"><span data-stu-id="7e748-140">product-id</span></span>             | <span data-ttu-id="7e748-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="7e748-141">string</span></span>   | <span data-ttu-id="7e748-142">Yes</span><span class="sxs-lookup"><span data-stu-id="7e748-142">Yes</span></span>      | <span data-ttu-id="7e748-143">Řetězec, který identifikuje produkt.</span><span class="sxs-lookup"><span data-stu-id="7e748-143">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="7e748-144">kód země</span><span class="sxs-lookup"><span data-stu-id="7e748-144">country-code</span></span>           | <span data-ttu-id="7e748-145">řetězec</span><span class="sxs-lookup"><span data-stu-id="7e748-145">string</span></span>   | <span data-ttu-id="7e748-146">Yes</span><span class="sxs-lookup"><span data-stu-id="7e748-146">Yes</span></span>      | <span data-ttu-id="7e748-147">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="7e748-147">A country/region ID.</span></span>                                            |
| <span data-ttu-id="7e748-148">cíl – segment</span><span class="sxs-lookup"><span data-stu-id="7e748-148">target-segment</span></span>         | <span data-ttu-id="7e748-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="7e748-149">string</span></span>   | <span data-ttu-id="7e748-150">No</span><span class="sxs-lookup"><span data-stu-id="7e748-150">No</span></span>       | <span data-ttu-id="7e748-151">Řetězec, který identifikuje cílový segment použitý pro filtrování.</span><span class="sxs-lookup"><span data-stu-id="7e748-151">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="7e748-152">reservationScope</span><span class="sxs-lookup"><span data-stu-id="7e748-152">reservationScope</span></span> | <span data-ttu-id="7e748-153">řetězec</span><span class="sxs-lookup"><span data-stu-id="7e748-153">string</span></span>   | <span data-ttu-id="7e748-154">No</span><span class="sxs-lookup"><span data-stu-id="7e748-154">No</span></span> | <span data-ttu-id="7e748-155">Při dotazování na seznam SKU pro produkt rezervované instance Azure určete, `reservationScope=AzurePlan` že se má získat seznam SKU, které platí pro AzurePlan.</span><span class="sxs-lookup"><span data-stu-id="7e748-155">When querying for a list of SKUs for an Azure Reservation product, specify `reservationScope=AzurePlan` to get a list of SKUs which are applicable to AzurePlan.</span></span> <span data-ttu-id="7e748-156">Vyloučením tohoto parametru získáte seznam SKU pro produkty rezervace Azure, které se vztahují na předplatná Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="7e748-156">Exclude this parameter to get a list of SKUs for an Azure Reservation products which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="7e748-157">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="7e748-157">Request headers</span></span>

<span data-ttu-id="7e748-158">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7e748-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7e748-159">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="7e748-159">Request body</span></span>

<span data-ttu-id="7e748-160">Žádné</span><span class="sxs-lookup"><span data-stu-id="7e748-160">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="7e748-161">Příklady požadavků</span><span class="sxs-lookup"><span data-stu-id="7e748-161">Request examples</span></span>

<span data-ttu-id="7e748-162">Získat seznam SKU pro daný produkt:</span><span class="sxs-lookup"><span data-stu-id="7e748-162">Get a list of SKUs for a given product:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="7e748-163">Získejte seznam SKU pro produkt rezervované instance Azure.</span><span class="sxs-lookup"><span data-stu-id="7e748-163">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="7e748-164">Zahrnout jenom SKU, které platí pro plány Azure Microsoft Azure a předplatné AZR (MS--0145P):</span><span class="sxs-lookup"><span data-stu-id="7e748-164">Only include the SKUs which are applicable to Azure plans and not Microsoft Azure (MS-AZR-0145P) subscriptions:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="7e748-165">Získejte seznam SKU pro produkt rezervované instance Azure.</span><span class="sxs-lookup"><span data-stu-id="7e748-165">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="7e748-166">Zahrnout jenom SKU, které platí pro předplatná Microsoft Azure (MS-AZR-0145P) a ne plány Azure:</span><span class="sxs-lookup"><span data-stu-id="7e748-166">Only include the SKUs which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions and not Azure plans:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a><span data-ttu-id="7e748-167">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="7e748-167">REST response</span></span>

<span data-ttu-id="7e748-168">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [SKU](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="7e748-168">If successful, the response body contains a collection of [SKU](product-resources.md#sku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7e748-169">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="7e748-169">Response success and error codes</span></span>

<span data-ttu-id="7e748-170">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="7e748-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7e748-171">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="7e748-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7e748-172">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7e748-172">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="7e748-173">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="7e748-173">This method returns the following error codes:</span></span>

| <span data-ttu-id="7e748-174">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="7e748-174">HTTP Status Code</span></span>     | <span data-ttu-id="7e748-175">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="7e748-175">Error code</span></span>   | <span data-ttu-id="7e748-176">Description</span><span class="sxs-lookup"><span data-stu-id="7e748-176">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7e748-177">403</span><span class="sxs-lookup"><span data-stu-id="7e748-177">403</span></span>                  | <span data-ttu-id="7e748-178">400030</span><span class="sxs-lookup"><span data-stu-id="7e748-178">400030</span></span>       | <span data-ttu-id="7e748-179">Přístup k požadovanému targetSegment není povolený.</span><span class="sxs-lookup"><span data-stu-id="7e748-179">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="7e748-180">404</span><span class="sxs-lookup"><span data-stu-id="7e748-180">404</span></span>                  | <span data-ttu-id="7e748-181">400013</span><span class="sxs-lookup"><span data-stu-id="7e748-181">400013</span></span>       | <span data-ttu-id="7e748-182">Nadřazený produkt nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="7e748-182">The parent product was not found.</span></span>                                                                         |

### <a name="response-example"></a><span data-ttu-id="7e748-183">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="7e748-183">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
