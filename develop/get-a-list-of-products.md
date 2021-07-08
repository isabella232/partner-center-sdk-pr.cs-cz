---
title: Získání seznamu produktů (podle země)
description: Pomocí prostředku Product můžete získat kolekci produktů podle země zákazníka.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1258727ecbe7c5cc332624577fa8a355e28e3717
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874206"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="537e5-103">Získání seznamu produktů (podle země)</span><span class="sxs-lookup"><span data-stu-id="537e5-103">Get a list of products (by country)</span></span>

<span data-ttu-id="537e5-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="537e5-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="537e5-105">Následující metody můžete použít k získání kolekce produktů dostupných v konkrétní zemi.</span><span class="sxs-lookup"><span data-stu-id="537e5-105">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="537e5-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="537e5-106">Prerequisites</span></span>

- <span data-ttu-id="537e5-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="537e5-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="537e5-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="537e5-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="537e5-109">Země.</span><span class="sxs-lookup"><span data-stu-id="537e5-109">A country.</span></span>

## <a name="c"></a><span data-ttu-id="537e5-110">C\#</span><span class="sxs-lookup"><span data-stu-id="537e5-110">C\#</span></span>

<span data-ttu-id="537e5-111">Získání seznamu produktů:</span><span class="sxs-lookup"><span data-stu-id="537e5-111">To get a list of products:</span></span>

1. <span data-ttu-id="537e5-112">Pomocí kolekce **IAggregatePartner.Products** vyberte zemi pomocí metody **ByCountry().**</span><span class="sxs-lookup"><span data-stu-id="537e5-112">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="537e5-113">Vyberte zobrazení katalogu pomocí **metody ByTargetView().**</span><span class="sxs-lookup"><span data-stu-id="537e5-113">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="537e5-114">(Volitelné) Vyberte rozsah rezervace pomocí metody **ByReservationScope().**</span><span class="sxs-lookup"><span data-stu-id="537e5-114">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="537e5-115">(Volitelné) Vyberte cílový segment pomocí metody **ByTargetSegment().**</span><span class="sxs-lookup"><span data-stu-id="537e5-115">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="537e5-116">Voláním **metody Get()** nebo **GetAsync()** vrátíte kolekci.</span><span class="sxs-lookup"><span data-stu-id="537e5-116">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="537e5-117">Java</span><span class="sxs-lookup"><span data-stu-id="537e5-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="537e5-118">Získání seznamu produktů:</span><span class="sxs-lookup"><span data-stu-id="537e5-118">To get a list of products:</span></span>

1. <span data-ttu-id="537e5-119">Pomocí funkce **IAggregatePartner.getProducts** vyberte zemi pomocí funkce **byCountry().**</span><span class="sxs-lookup"><span data-stu-id="537e5-119">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="537e5-120">Vyberte zobrazení katalogu pomocí **funkce byTargetView().**</span><span class="sxs-lookup"><span data-stu-id="537e5-120">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="537e5-121">(Volitelné) Vyberte cílový segment pomocí funkce **byTargetSegment().**</span><span class="sxs-lookup"><span data-stu-id="537e5-121">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="537e5-122">Voláním **funkce get()** vrátíte kolekci.</span><span class="sxs-lookup"><span data-stu-id="537e5-122">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="537e5-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="537e5-123">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="537e5-124">Získání seznamu produktů:</span><span class="sxs-lookup"><span data-stu-id="537e5-124">To get a list of products:</span></span>

1. <span data-ttu-id="537e5-125">Spusťte příkaz [**Get-PartnerProduct.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)</span><span class="sxs-lookup"><span data-stu-id="537e5-125">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="537e5-126">Katalog vyberte zadáním **parametru Catalog.**</span><span class="sxs-lookup"><span data-stu-id="537e5-126">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="537e5-127">(Volitelné) Vyberte cílový segment zadáním **parametru Segment.**</span><span class="sxs-lookup"><span data-stu-id="537e5-127">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="537e5-128">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="537e5-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="537e5-129">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="537e5-129">Request syntax</span></span>

| <span data-ttu-id="537e5-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="537e5-130">Method</span></span>  | <span data-ttu-id="537e5-131">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="537e5-131">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="537e5-132">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="537e5-132">**GET**</span></span> | <span data-ttu-id="537e5-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="537e5-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="537e5-134">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="537e5-134">URI parameters</span></span>

<span data-ttu-id="537e5-135">K získání seznamu produktů použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="537e5-135">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="537e5-136">Název</span><span class="sxs-lookup"><span data-stu-id="537e5-136">Name</span></span>                   | <span data-ttu-id="537e5-137">Typ</span><span class="sxs-lookup"><span data-stu-id="537e5-137">Type</span></span>     | <span data-ttu-id="537e5-138">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="537e5-138">Required</span></span> | <span data-ttu-id="537e5-139">Popis</span><span class="sxs-lookup"><span data-stu-id="537e5-139">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="537e5-140">country</span><span class="sxs-lookup"><span data-stu-id="537e5-140">country</span></span>                | <span data-ttu-id="537e5-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="537e5-141">string</span></span>   | <span data-ttu-id="537e5-142">Yes</span><span class="sxs-lookup"><span data-stu-id="537e5-142">Yes</span></span>      | <span data-ttu-id="537e5-143">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="537e5-143">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="537e5-144">targetView</span><span class="sxs-lookup"><span data-stu-id="537e5-144">targetView</span></span>             | <span data-ttu-id="537e5-145">řetězec</span><span class="sxs-lookup"><span data-stu-id="537e5-145">string</span></span>   | <span data-ttu-id="537e5-146">Yes</span><span class="sxs-lookup"><span data-stu-id="537e5-146">Yes</span></span>      | <span data-ttu-id="537e5-147">Identifikuje cílové zobrazení katalogu.</span><span class="sxs-lookup"><span data-stu-id="537e5-147">Identifies the target view of the catalog.</span></span> <span data-ttu-id="537e5-148">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="537e5-148">The supported values are:</span></span> <br/><br/><span data-ttu-id="537e5-149">**Azure**, který zahrnuje všechny položky Azure</span><span class="sxs-lookup"><span data-stu-id="537e5-149">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="537e5-150">**AzureReservations**, která zahrnuje všechny položky rezervací Azure</span><span class="sxs-lookup"><span data-stu-id="537e5-150">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="537e5-151">**AzureReservationsVM**, který zahrnuje všechny položky rezervace virtuálních počítačů</span><span class="sxs-lookup"><span data-stu-id="537e5-151">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="537e5-152">**AzureReservationsSQL**, který zahrnuje všechny SQL položek rezervace</span><span class="sxs-lookup"><span data-stu-id="537e5-152">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="537e5-153">**AzureReservationsCosmosDb**, který zahrnuje všechny Cosmos položek rezervace databáze</span><span class="sxs-lookup"><span data-stu-id="537e5-153">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="537e5-154">**MicrosoftAzure**, který obsahuje položky pro Microsoft Azure předplatná (**MS-AZR-0145P)** a plány Azure</span><span class="sxs-lookup"><span data-stu-id="537e5-154">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="537e5-155">**Onlineslužby**, které zahrnují všechny položky online služeb (včetně produktů komerčního marketplace)</span><span class="sxs-lookup"><span data-stu-id="537e5-155">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="537e5-156">**Software**, který zahrnuje všechny softwarové položky</span><span class="sxs-lookup"><span data-stu-id="537e5-156">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="537e5-157">**SoftwareSUSELinux**, který zahrnuje všechny položky softwaru SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="537e5-157">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="537e5-158">**SoftwarePerpetual**, který zahrnuje všechny časově neomezené softwarové položky</span><span class="sxs-lookup"><span data-stu-id="537e5-158">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="537e5-159">**Předplatná softwaru**, která zahrnují všechny položky předplatného softwaru</span><span class="sxs-lookup"><span data-stu-id="537e5-159">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="537e5-160">TargetSegment</span><span class="sxs-lookup"><span data-stu-id="537e5-160">targetSegment</span></span>          | <span data-ttu-id="537e5-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="537e5-161">string</span></span>   | <span data-ttu-id="537e5-162">No</span><span class="sxs-lookup"><span data-stu-id="537e5-162">No</span></span>       | <span data-ttu-id="537e5-163">Identifikuje cílový segment.</span><span class="sxs-lookup"><span data-stu-id="537e5-163">Identifies the target segment.</span></span> <span data-ttu-id="537e5-164">Zobrazení pro různé cílové skupiny</span><span class="sxs-lookup"><span data-stu-id="537e5-164">The view for different target audiences.</span></span> <span data-ttu-id="537e5-165">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="537e5-165">The supported values are:</span></span> <br/><br/><span data-ttu-id="537e5-166">**Obchodní**</span><span class="sxs-lookup"><span data-stu-id="537e5-166">**commercial**</span></span><br/><span data-ttu-id="537e5-167">**Vzdělávání**</span><span class="sxs-lookup"><span data-stu-id="537e5-167">**education**</span></span><br/><span data-ttu-id="537e5-168">**Vláda**</span><span class="sxs-lookup"><span data-stu-id="537e5-168">**government**</span></span><br/><span data-ttu-id="537e5-169">**Neziskové**</span><span class="sxs-lookup"><span data-stu-id="537e5-169">**nonprofit**</span></span>  |
| <span data-ttu-id="537e5-170">reservationScope</span><span class="sxs-lookup"><span data-stu-id="537e5-170">reservationScope</span></span> | <span data-ttu-id="537e5-171">řetězec</span><span class="sxs-lookup"><span data-stu-id="537e5-171">string</span></span>   | <span data-ttu-id="537e5-172">No</span><span class="sxs-lookup"><span data-stu-id="537e5-172">No</span></span> | <span data-ttu-id="537e5-173">Při dotazování na seznam produktů pro rezervace Azure zadejte a získejte seznam produktů, které se `reservationScope=AzurePlan` vztahují k plánům Azure.</span><span class="sxs-lookup"><span data-stu-id="537e5-173">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="537e5-174">Tento parametr vyloučíte, pokud chcete získat seznam produktů pro rezervace Azure, které se vztahují na předplatná Microsoft Azure (**MS-AZR-0145P).**</span><span class="sxs-lookup"><span data-stu-id="537e5-174">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="537e5-175">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="537e5-175">Request headers</span></span>

<span data-ttu-id="537e5-176">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="537e5-176">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="537e5-177">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="537e5-177">Request body</span></span>

<span data-ttu-id="537e5-178">Žádné</span><span class="sxs-lookup"><span data-stu-id="537e5-178">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="537e5-179">Příklady požadavků</span><span class="sxs-lookup"><span data-stu-id="537e5-179">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="537e5-180">Products by country</span><span class="sxs-lookup"><span data-stu-id="537e5-180">Products by country</span></span>

<span data-ttu-id="537e5-181">V tomto příkladu získáte seznam produktů podle země pro předplatná Microsoft Azure (MS-AZR-0145P) a plány Azure.</span><span class="sxs-lookup"><span data-stu-id="537e5-181">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="537e5-182">Rezervace virtuálních počítače Azure (plán Azure)</span><span class="sxs-lookup"><span data-stu-id="537e5-182">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="537e5-183">V tomto příkladu získáte seznam produktů podle země pro rezervace virtuálních počítače Azure, které se vztahují na plány Azure.</span><span class="sxs-lookup"><span data-stu-id="537e5-183">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="537e5-184">Rezervace virtuálních Microsoft Azure Azure (MS-AZR-0145P) předplatná</span><span class="sxs-lookup"><span data-stu-id="537e5-184">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="537e5-185">Postupujte podle tohoto příkladu a získejte seznam produktů pro rezervace virtuálních počítače Azure podle země, které se vztahují k předplatným Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="537e5-185">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="537e5-186">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="537e5-186">REST response</span></span>

<span data-ttu-id="537e5-187">V případě úspěchu bude tělo odpovědi obsahovat kolekci prostředků [**Product.**](product-resources.md#product)</span><span class="sxs-lookup"><span data-stu-id="537e5-187">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="537e5-188">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="537e5-188">Response success and error codes</span></span>

<span data-ttu-id="537e5-189">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="537e5-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="537e5-190">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="537e5-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="537e5-191">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="537e5-191">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="537e5-192">Tato metoda vrátí následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="537e5-192">This method returns the following error codes:</span></span>

| <span data-ttu-id="537e5-193">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="537e5-193">HTTP Status Code</span></span>     | <span data-ttu-id="537e5-194">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="537e5-194">Error code</span></span>   | <span data-ttu-id="537e5-195">Description</span><span class="sxs-lookup"><span data-stu-id="537e5-195">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="537e5-196">403</span><span class="sxs-lookup"><span data-stu-id="537e5-196">403</span></span>                  | <span data-ttu-id="537e5-197">400030</span><span class="sxs-lookup"><span data-stu-id="537e5-197">400030</span></span>       | <span data-ttu-id="537e5-198">Přístup k požadovanému targetSegment není povolený.</span><span class="sxs-lookup"><span data-stu-id="537e5-198">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="537e5-199">403</span><span class="sxs-lookup"><span data-stu-id="537e5-199">403</span></span>                  | <span data-ttu-id="537e5-200">400036</span><span class="sxs-lookup"><span data-stu-id="537e5-200">400036</span></span>       | <span data-ttu-id="537e5-201">Přístup k požadovanému objektu targetView není povolený.</span><span class="sxs-lookup"><span data-stu-id="537e5-201">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="537e5-202">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="537e5-202">Response example</span></span>

```http
{
    "totalCount": 19,
    "items": [
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
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
