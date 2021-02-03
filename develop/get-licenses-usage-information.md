---
title: Získání informací o využití licencí
description: Jak získat informace o využití licencí na úrovni úloh pro Office a Dynamics
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766894"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="86260-103">Získání informací o využití licencí</span><span class="sxs-lookup"><span data-stu-id="86260-103">Get licenses usage information</span></span>

<span data-ttu-id="86260-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="86260-104">**Applies To**</span></span>

- <span data-ttu-id="86260-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="86260-105">Partner Center</span></span>

<span data-ttu-id="86260-106">Jak získat informace o využití licencí na úrovni úloh pro Office a Dynamics</span><span class="sxs-lookup"><span data-stu-id="86260-106">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86260-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="86260-107">Prerequisites</span></span>

<span data-ttu-id="86260-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="86260-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="86260-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="86260-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="86260-110">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="86260-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="86260-111">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="86260-111">Request syntax</span></span>

| <span data-ttu-id="86260-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="86260-112">Method</span></span>  | <span data-ttu-id="86260-113">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="86260-113">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="86260-114">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="86260-114">**GET**</span></span> | <span data-ttu-id="86260-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Usage/License/HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="86260-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="86260-116">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="86260-116">Request headers</span></span>

<span data-ttu-id="86260-117">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="86260-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="86260-118">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="86260-118">URI parameters</span></span>

| <span data-ttu-id="86260-119">Parametr</span><span class="sxs-lookup"><span data-stu-id="86260-119">Parameter</span></span>         | <span data-ttu-id="86260-120">Typ</span><span class="sxs-lookup"><span data-stu-id="86260-120">Type</span></span>     | <span data-ttu-id="86260-121">Popis</span><span class="sxs-lookup"><span data-stu-id="86260-121">Description</span></span> | <span data-ttu-id="86260-122">Povinné</span><span class="sxs-lookup"><span data-stu-id="86260-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="86260-123">top</span><span class="sxs-lookup"><span data-stu-id="86260-123">top</span></span>               | <span data-ttu-id="86260-124">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-124">string</span></span>   | <span data-ttu-id="86260-125">Počet řádků dat, který má být vrácen v požadavku.</span><span class="sxs-lookup"><span data-stu-id="86260-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="86260-126">Maximální hodnota a výchozí hodnota, pokud není zadána, je 10000.</span><span class="sxs-lookup"><span data-stu-id="86260-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="86260-127">Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="86260-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="86260-128">No</span><span class="sxs-lookup"><span data-stu-id="86260-128">No</span></span> |
| <span data-ttu-id="86260-129">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="86260-129">skip</span></span>              | <span data-ttu-id="86260-130">int</span><span class="sxs-lookup"><span data-stu-id="86260-130">int</span></span>      | <span data-ttu-id="86260-131">Počet řádků, které mají být v dotazu přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="86260-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="86260-132">Tento parametr použijte pro stránku s velkými datovými sadami.</span><span class="sxs-lookup"><span data-stu-id="86260-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="86260-133">Například Top = 10000 a Skip = 0 načte prvních 10000 řádků dat, Top = 10000 a Skip = 10000 načte další 10000 řádků dat a tak dále.</span><span class="sxs-lookup"><span data-stu-id="86260-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="86260-134">No</span><span class="sxs-lookup"><span data-stu-id="86260-134">No</span></span> |
| <span data-ttu-id="86260-135">filter</span><span class="sxs-lookup"><span data-stu-id="86260-135">filter</span></span>            | <span data-ttu-id="86260-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-136">string</span></span>   | <span data-ttu-id="86260-137">Parametr *filtru* požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="86260-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="86260-138">Každý příkaz obsahuje pole a hodnotu, které jsou spojeny s **`eq`** **`ne`** operátory nebo, a příkazy lze kombinovat pomocí operátoru OR **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="86260-138">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="86260-139">Tady je několik příkladů parametrů *filtru* :</span><span class="sxs-lookup"><span data-stu-id="86260-139">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="86260-140">*Filter = workloadCode EQ ' SFB '*</span><span class="sxs-lookup"><span data-stu-id="86260-140">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="86260-141">*Filter = workloadCode EQ ' SFB '* or (*Channel EQ ' prodejce '*)</span><span class="sxs-lookup"><span data-stu-id="86260-141">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="86260-142">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="86260-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="86260-143">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="86260-143">**workloadCode**</span></span><br/><span data-ttu-id="86260-144">**úloha úlohy**</span><span class="sxs-lookup"><span data-stu-id="86260-144">**workloadName**</span></span><br/><span data-ttu-id="86260-145">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="86260-145">**serviceCode**</span></span><br/><span data-ttu-id="86260-146">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="86260-146">**serviceName**</span></span><br/><span data-ttu-id="86260-147">**kanál**</span><span class="sxs-lookup"><span data-stu-id="86260-147">**channel**</span></span><br/><span data-ttu-id="86260-148">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="86260-148">**customerTenantId**</span></span><br/><span data-ttu-id="86260-149">**customerName**</span><span class="sxs-lookup"><span data-stu-id="86260-149">**customerName**</span></span><br/><span data-ttu-id="86260-150">**productId**</span><span class="sxs-lookup"><span data-stu-id="86260-150">**productId**</span></span><br/><span data-ttu-id="86260-151">**NázevVýrobku**</span><span class="sxs-lookup"><span data-stu-id="86260-151">**productName**</span></span> | <span data-ttu-id="86260-152">No</span><span class="sxs-lookup"><span data-stu-id="86260-152">No</span></span> |
| <span data-ttu-id="86260-153">GroupBy</span><span class="sxs-lookup"><span data-stu-id="86260-153">groupby</span></span>           | <span data-ttu-id="86260-154">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-154">string</span></span>   | <span data-ttu-id="86260-155">Příkaz, který aplikuje agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="86260-155">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="86260-156">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="86260-156">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="86260-157">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="86260-157">**workloadCode**</span></span><br/><span data-ttu-id="86260-158">**úloha úlohy**</span><span class="sxs-lookup"><span data-stu-id="86260-158">**workloadName**</span></span><br/><span data-ttu-id="86260-159">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="86260-159">**serviceCode**</span></span><br/><span data-ttu-id="86260-160">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="86260-160">**serviceName**</span></span><br/><span data-ttu-id="86260-161">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="86260-161">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="86260-162">**customerName**</span><span class="sxs-lookup"><span data-stu-id="86260-162">**customerName**</span></span><br/><span data-ttu-id="86260-163">**productId**</span><span class="sxs-lookup"><span data-stu-id="86260-163">**productId**</span></span><br/><span data-ttu-id="86260-164">**NázevVýrobku**</span><span class="sxs-lookup"><span data-stu-id="86260-164">**productName**</span></span><br/><br/><span data-ttu-id="86260-165">Vrácené řádky dat budou obsahovat pole zadaná v parametru *GroupBy* a také následující:</span><span class="sxs-lookup"><span data-stu-id="86260-165">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="86260-166">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="86260-166">**licensesActive**</span></span><br/><span data-ttu-id="86260-167">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="86260-167">**licensesQualified**</span></span> | <span data-ttu-id="86260-168">No</span><span class="sxs-lookup"><span data-stu-id="86260-168">No</span></span> |
| <span data-ttu-id="86260-169">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="86260-169">processedDateTime</span></span> | <span data-ttu-id="86260-170">DateTime</span><span class="sxs-lookup"><span data-stu-id="86260-170">DateTime</span></span> | <span data-ttu-id="86260-171">Jedna z nich může určovat datum, ze kterého byla zpracována data o využití.</span><span class="sxs-lookup"><span data-stu-id="86260-171">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="86260-172">Výchozí hodnota je poslední datum, kdy byla data zpracována.</span><span class="sxs-lookup"><span data-stu-id="86260-172">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="86260-173">No</span><span class="sxs-lookup"><span data-stu-id="86260-173">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="86260-174">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="86260-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="86260-175">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="86260-175">REST response</span></span>

<span data-ttu-id="86260-176">V případě úspěchu obsahuje tělo odpovědi následující pole obsahující data o využití licencí.</span><span class="sxs-lookup"><span data-stu-id="86260-176">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="86260-177">Pole</span><span class="sxs-lookup"><span data-stu-id="86260-177">Field</span></span>             | <span data-ttu-id="86260-178">Typ</span><span class="sxs-lookup"><span data-stu-id="86260-178">Type</span></span>     | <span data-ttu-id="86260-179">Description</span><span class="sxs-lookup"><span data-stu-id="86260-179">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="86260-180">workloadCode</span><span class="sxs-lookup"><span data-stu-id="86260-180">workloadCode</span></span>      | <span data-ttu-id="86260-181">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-181">string</span></span>   | <span data-ttu-id="86260-182">Kód úlohy</span><span class="sxs-lookup"><span data-stu-id="86260-182">Workload code</span></span>                                 |
| <span data-ttu-id="86260-183">úloha úlohy</span><span class="sxs-lookup"><span data-stu-id="86260-183">workloadName</span></span>      | <span data-ttu-id="86260-184">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-184">string</span></span>   | <span data-ttu-id="86260-185">Název úlohy</span><span class="sxs-lookup"><span data-stu-id="86260-185">Workload name</span></span>                                 |
| <span data-ttu-id="86260-186">serviceCode</span><span class="sxs-lookup"><span data-stu-id="86260-186">serviceCode</span></span>       | <span data-ttu-id="86260-187">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-187">string</span></span>   | <span data-ttu-id="86260-188">Kód služby</span><span class="sxs-lookup"><span data-stu-id="86260-188">Service code</span></span>                                  |
| <span data-ttu-id="86260-189">serviceName</span><span class="sxs-lookup"><span data-stu-id="86260-189">serviceName</span></span>       | <span data-ttu-id="86260-190">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-190">string</span></span>   | <span data-ttu-id="86260-191">Název služby</span><span class="sxs-lookup"><span data-stu-id="86260-191">Service name</span></span>                                  |
| <span data-ttu-id="86260-192">kanál</span><span class="sxs-lookup"><span data-stu-id="86260-192">channel</span></span>           | <span data-ttu-id="86260-193">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-193">string</span></span>   | <span data-ttu-id="86260-194">Název kanálu, prodejce</span><span class="sxs-lookup"><span data-stu-id="86260-194">Channel name, reseller</span></span>                        |
| <span data-ttu-id="86260-195">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="86260-195">customerTenantId</span></span>  | <span data-ttu-id="86260-196">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-196">string</span></span>   | <span data-ttu-id="86260-197">Jedinečný identifikátor pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="86260-197">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="86260-198">customerName</span><span class="sxs-lookup"><span data-stu-id="86260-198">customerName</span></span>      | <span data-ttu-id="86260-199">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-199">string</span></span>   | <span data-ttu-id="86260-200">Jméno zákazníka</span><span class="sxs-lookup"><span data-stu-id="86260-200">Customer name</span></span>                                 |
| <span data-ttu-id="86260-201">productId</span><span class="sxs-lookup"><span data-stu-id="86260-201">productId</span></span>         | <span data-ttu-id="86260-202">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-202">string</span></span>   | <span data-ttu-id="86260-203">Jedinečný identifikátor produktu</span><span class="sxs-lookup"><span data-stu-id="86260-203">Unique identifier for the product</span></span>             |
| <span data-ttu-id="86260-204">NázevVýrobku</span><span class="sxs-lookup"><span data-stu-id="86260-204">productName</span></span>       | <span data-ttu-id="86260-205">řetězec</span><span class="sxs-lookup"><span data-stu-id="86260-205">string</span></span>   | <span data-ttu-id="86260-206">Název produktu</span><span class="sxs-lookup"><span data-stu-id="86260-206">Product name</span></span>                                  |
| <span data-ttu-id="86260-207">licensesActive</span><span class="sxs-lookup"><span data-stu-id="86260-207">licensesActive</span></span>    | <span data-ttu-id="86260-208">long</span><span class="sxs-lookup"><span data-stu-id="86260-208">long</span></span>     | <span data-ttu-id="86260-209">Počet aktivních licencí na úlohu</span><span class="sxs-lookup"><span data-stu-id="86260-209">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="86260-210">licensesQualified</span><span class="sxs-lookup"><span data-stu-id="86260-210">licensesQualified</span></span> | <span data-ttu-id="86260-211">long</span><span class="sxs-lookup"><span data-stu-id="86260-211">long</span></span>     | <span data-ttu-id="86260-212">Počet kvalifikovaných licencí pro zatížení</span><span class="sxs-lookup"><span data-stu-id="86260-212">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="86260-213">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="86260-213">processedDateTime</span></span> | <span data-ttu-id="86260-214">DateTime</span><span class="sxs-lookup"><span data-stu-id="86260-214">DateTime</span></span> | <span data-ttu-id="86260-215">Datum posledního zpracování dat</span><span class="sxs-lookup"><span data-stu-id="86260-215">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="86260-216">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="86260-216">Response success and error codes</span></span>

<span data-ttu-id="86260-217">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="86260-217">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="86260-218">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="86260-218">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="86260-219">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="86260-219">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="86260-220">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="86260-220">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
