---
title: Získání seznamu produktů (podle země)
description: Pomocí prostředku produktu můžete získat kolekci produktů podle země zákazníka.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ea239aa008a5b7c33740e9c4697c3795908415cd
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766900"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="8e7b2-103">Získání seznamu produktů (podle země)</span><span class="sxs-lookup"><span data-stu-id="8e7b2-103">Get a list of products (by country)</span></span>

<span data-ttu-id="8e7b2-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="8e7b2-104">**Applies to:**</span></span>

- <span data-ttu-id="8e7b2-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="8e7b2-105">Partner Center</span></span>
- <span data-ttu-id="8e7b2-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="8e7b2-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8e7b2-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="8e7b2-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8e7b2-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8e7b2-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8e7b2-109">Pomocí následujících metod můžete získat kolekci produktů dostupných v určité zemi.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-109">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e7b2-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8e7b2-110">Prerequisites</span></span>

- <span data-ttu-id="8e7b2-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8e7b2-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8e7b2-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8e7b2-113">Země.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-113">A country.</span></span>

## <a name="c"></a><span data-ttu-id="8e7b2-114">C\#</span><span class="sxs-lookup"><span data-stu-id="8e7b2-114">C\#</span></span>

<span data-ttu-id="8e7b2-115">Získání seznamu produktů:</span><span class="sxs-lookup"><span data-stu-id="8e7b2-115">To get a list of products:</span></span>

1. <span data-ttu-id="8e7b2-116">Pomocí kolekce **IAggregatePartner. Products** vyberte zemi pomocí metody **ByCountry ()** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-116">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="8e7b2-117">Vyberte zobrazení katalogu pomocí metody **ByTargetView ()** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-117">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="8e7b2-118">Volitelné Vyberte rozsah rezervace pomocí metody **ByReservationScope ()** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-118">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="8e7b2-119">Volitelné Vyberte cílový segment pomocí metody **ByTargetSegment ()** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-119">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="8e7b2-120">Volání metody **Get ()** nebo **GetAsync ()** pro vrácení kolekce.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-120">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

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

## <a name="java"></a><span data-ttu-id="8e7b2-121">Java</span><span class="sxs-lookup"><span data-stu-id="8e7b2-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="8e7b2-122">Získání seznamu produktů:</span><span class="sxs-lookup"><span data-stu-id="8e7b2-122">To get a list of products:</span></span>

1. <span data-ttu-id="8e7b2-123">Použijte funkci **IAggregatePartner. GetProducts** k výběru země pomocí funkce **byCountry ()** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-123">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="8e7b2-124">Vyberte zobrazení katalogu pomocí funkce **byTargetView ()** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-124">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="8e7b2-125">Volitelné Vyberte cílový segment pomocí funkce **byTargetSegment ()** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-125">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="8e7b2-126">Zavolejte funkci **Get ()** , která vrátí kolekci.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-126">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="8e7b2-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e7b2-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="8e7b2-128">Získání seznamu produktů:</span><span class="sxs-lookup"><span data-stu-id="8e7b2-128">To get a list of products:</span></span>

1. <span data-ttu-id="8e7b2-129">Spusťte příkaz [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-129">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="8e7b2-130">Vyberte katalog zadáním parametru **Catalog** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-130">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="8e7b2-131">Volitelné Vyberte cílový segment zadáním parametru **segmentu** .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-131">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="8e7b2-132">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="8e7b2-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8e7b2-133">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="8e7b2-133">Request syntax</span></span>

| <span data-ttu-id="8e7b2-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="8e7b2-134">Method</span></span>  | <span data-ttu-id="8e7b2-135">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8e7b2-135">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="8e7b2-136">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="8e7b2-136">**GET**</span></span> | <span data-ttu-id="8e7b2-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Products? Country = {country} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8e7b2-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8e7b2-138">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="8e7b2-138">URI parameters</span></span>

<span data-ttu-id="8e7b2-139">K získání seznamu produktů použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-139">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="8e7b2-140">Název</span><span class="sxs-lookup"><span data-stu-id="8e7b2-140">Name</span></span>                   | <span data-ttu-id="8e7b2-141">Typ</span><span class="sxs-lookup"><span data-stu-id="8e7b2-141">Type</span></span>     | <span data-ttu-id="8e7b2-142">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8e7b2-142">Required</span></span> | <span data-ttu-id="8e7b2-143">Popis</span><span class="sxs-lookup"><span data-stu-id="8e7b2-143">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="8e7b2-144">country</span><span class="sxs-lookup"><span data-stu-id="8e7b2-144">country</span></span>                | <span data-ttu-id="8e7b2-145">řetězec</span><span class="sxs-lookup"><span data-stu-id="8e7b2-145">string</span></span>   | <span data-ttu-id="8e7b2-146">Yes</span><span class="sxs-lookup"><span data-stu-id="8e7b2-146">Yes</span></span>      | <span data-ttu-id="8e7b2-147">ID země nebo oblasti</span><span class="sxs-lookup"><span data-stu-id="8e7b2-147">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="8e7b2-148">targetView</span><span class="sxs-lookup"><span data-stu-id="8e7b2-148">targetView</span></span>             | <span data-ttu-id="8e7b2-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="8e7b2-149">string</span></span>   | <span data-ttu-id="8e7b2-150">Yes</span><span class="sxs-lookup"><span data-stu-id="8e7b2-150">Yes</span></span>      | <span data-ttu-id="8e7b2-151">Určuje cílové zobrazení katalogu.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-151">Identifies the target view of the catalog.</span></span> <span data-ttu-id="8e7b2-152">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="8e7b2-152">The supported values are:</span></span> <br/><br/><span data-ttu-id="8e7b2-153">**Azure**, který zahrnuje všechny položky Azure</span><span class="sxs-lookup"><span data-stu-id="8e7b2-153">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="8e7b2-154">**AzureReservations**, která zahrnuje všechny položky rezervace Azure</span><span class="sxs-lookup"><span data-stu-id="8e7b2-154">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="8e7b2-155">**AzureReservationsVM**, která zahrnuje všechny položky rezervace virtuálních počítačů (VM)</span><span class="sxs-lookup"><span data-stu-id="8e7b2-155">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="8e7b2-156">**AzureReservationsSQL**, která zahrnuje všechny položky rezervace SQL</span><span class="sxs-lookup"><span data-stu-id="8e7b2-156">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="8e7b2-157">**AzureReservationsCosmosDb**, která zahrnuje všechny položky rezervace databáze Cosmos</span><span class="sxs-lookup"><span data-stu-id="8e7b2-157">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="8e7b2-158">**MicrosoftAzure**, která zahrnuje položky pro předplatná Microsoft Azure (**MS-AZR-0145P**) a plány Azure</span><span class="sxs-lookup"><span data-stu-id="8e7b2-158">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="8e7b2-159">**OnlineServices**, která zahrnuje všechny online položky služeb (včetně produktů z komerčního tržiště)</span><span class="sxs-lookup"><span data-stu-id="8e7b2-159">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="8e7b2-160">**Software**, který zahrnuje všechny softwarové položky</span><span class="sxs-lookup"><span data-stu-id="8e7b2-160">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="8e7b2-161">**SoftwareSUSELinux**, která zahrnuje všechny položky softwaru SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="8e7b2-161">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="8e7b2-162">**SoftwarePerpetual**, která zahrnuje všechny trvalé softwarové položky</span><span class="sxs-lookup"><span data-stu-id="8e7b2-162">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="8e7b2-163">**SoftwareSubscriptions**, která zahrnuje všechny položky předplatného softwaru</span><span class="sxs-lookup"><span data-stu-id="8e7b2-163">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="8e7b2-164">targetSegment</span><span class="sxs-lookup"><span data-stu-id="8e7b2-164">targetSegment</span></span>          | <span data-ttu-id="8e7b2-165">řetězec</span><span class="sxs-lookup"><span data-stu-id="8e7b2-165">string</span></span>   | <span data-ttu-id="8e7b2-166">No</span><span class="sxs-lookup"><span data-stu-id="8e7b2-166">No</span></span>       | <span data-ttu-id="8e7b2-167">Identifikuje cílový segment.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-167">Identifies the target segment.</span></span> <span data-ttu-id="8e7b2-168">Zobrazení pro různé cílové skupiny.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-168">The view for different target audiences.</span></span> <span data-ttu-id="8e7b2-169">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="8e7b2-169">The supported values are:</span></span> <br/><br/><span data-ttu-id="8e7b2-170">**prodejn**</span><span class="sxs-lookup"><span data-stu-id="8e7b2-170">**commercial**</span></span><br/><span data-ttu-id="8e7b2-171">**školení**</span><span class="sxs-lookup"><span data-stu-id="8e7b2-171">**education**</span></span><br/><span data-ttu-id="8e7b2-172">**schod**</span><span class="sxs-lookup"><span data-stu-id="8e7b2-172">**government**</span></span><br/><span data-ttu-id="8e7b2-173">**neziskové**</span><span class="sxs-lookup"><span data-stu-id="8e7b2-173">**nonprofit**</span></span>  |
| <span data-ttu-id="8e7b2-174">reservationScope</span><span class="sxs-lookup"><span data-stu-id="8e7b2-174">reservationScope</span></span> | <span data-ttu-id="8e7b2-175">řetězec</span><span class="sxs-lookup"><span data-stu-id="8e7b2-175">string</span></span>   | <span data-ttu-id="8e7b2-176">No</span><span class="sxs-lookup"><span data-stu-id="8e7b2-176">No</span></span> | <span data-ttu-id="8e7b2-177">Při dotazování na seznam produktů pro Azure Reservations určete, že se `reservationScope=AzurePlan` má získat seznam produktů, které se vztahují k plánům Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-177">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="8e7b2-178">Vyloučením tohoto parametru získáte seznam produktů pro rezervace Azure, které se vztahují na předplatná Microsoft Azure (**MS-AZR-0145P**).</span><span class="sxs-lookup"><span data-stu-id="8e7b2-178">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="8e7b2-179">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8e7b2-179">Request headers</span></span>

<span data-ttu-id="8e7b2-180">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8e7b2-180">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8e7b2-181">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8e7b2-181">Request body</span></span>

<span data-ttu-id="8e7b2-182">Žádné</span><span class="sxs-lookup"><span data-stu-id="8e7b2-182">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="8e7b2-183">Příklady požadavků</span><span class="sxs-lookup"><span data-stu-id="8e7b2-183">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="8e7b2-184">Produkty podle země</span><span class="sxs-lookup"><span data-stu-id="8e7b2-184">Products by country</span></span>

<span data-ttu-id="8e7b2-185">Podle tohoto příkladu Získejte seznam produktů podle země pro předplatná Microsoft Azure (MS-AZR-0145P) a plány Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-185">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="8e7b2-186">Rezervace virtuálních počítačů Azure (plán Azure)</span><span class="sxs-lookup"><span data-stu-id="8e7b2-186">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="8e7b2-187">Podle tohoto příkladu Získejte seznam produktů podle zemí pro rezervace virtuálních počítačů Azure, které platí pro plány Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-187">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="8e7b2-188">Rezervace virtuálních počítačů Azure pro předplatná Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="8e7b2-188">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="8e7b2-189">Podle tohoto příkladu Získejte seznam produktů podle zemí pro rezervace virtuálních počítačů Azure, které platí pro odběry služby Microsoft Azure AZR (MS--0145P).</span><span class="sxs-lookup"><span data-stu-id="8e7b2-189">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="8e7b2-190">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8e7b2-190">REST response</span></span>

<span data-ttu-id="8e7b2-191">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [**produktu**](product-resources.md#product) .</span><span class="sxs-lookup"><span data-stu-id="8e7b2-191">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8e7b2-192">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="8e7b2-192">Response success and error codes</span></span>

<span data-ttu-id="8e7b2-193">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-193">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8e7b2-194">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-194">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8e7b2-195">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8e7b2-195">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="8e7b2-196">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="8e7b2-196">This method returns the following error codes:</span></span>

| <span data-ttu-id="8e7b2-197">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="8e7b2-197">HTTP Status Code</span></span>     | <span data-ttu-id="8e7b2-198">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="8e7b2-198">Error code</span></span>   | <span data-ttu-id="8e7b2-199">Description</span><span class="sxs-lookup"><span data-stu-id="8e7b2-199">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8e7b2-200">403</span><span class="sxs-lookup"><span data-stu-id="8e7b2-200">403</span></span>                  | <span data-ttu-id="8e7b2-201">400030</span><span class="sxs-lookup"><span data-stu-id="8e7b2-201">400030</span></span>       | <span data-ttu-id="8e7b2-202">Přístup k požadovanému targetSegment není povolený.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-202">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="8e7b2-203">403</span><span class="sxs-lookup"><span data-stu-id="8e7b2-203">403</span></span>                  | <span data-ttu-id="8e7b2-204">400036</span><span class="sxs-lookup"><span data-stu-id="8e7b2-204">400036</span></span>       | <span data-ttu-id="8e7b2-205">Přístup k požadovanému targetView není povolený.</span><span class="sxs-lookup"><span data-stu-id="8e7b2-205">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="8e7b2-206">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8e7b2-206">Response example</span></span>

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
