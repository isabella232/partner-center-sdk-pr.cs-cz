---
title: Získání informací o využití licencí
description: Jak získat informace o využití licencí na úrovni úloh pro Office a Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea3658089ce7eb5c1ad7cc65c3db34f9b6353cdd
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445969"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="9af24-103">Získání informací o využití licencí</span><span class="sxs-lookup"><span data-stu-id="9af24-103">Get licenses usage information</span></span>

<span data-ttu-id="9af24-104">Jak získat informace o využití licencí na úrovni úloh pro Office a Dynamics.</span><span class="sxs-lookup"><span data-stu-id="9af24-104">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9af24-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9af24-105">Prerequisites</span></span>

<span data-ttu-id="9af24-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9af24-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9af24-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="9af24-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="9af24-108">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="9af24-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9af24-109">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="9af24-109">Request syntax</span></span>

| <span data-ttu-id="9af24-110">Metoda</span><span class="sxs-lookup"><span data-stu-id="9af24-110">Method</span></span>  | <span data-ttu-id="9af24-111">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9af24-111">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="9af24-112">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="9af24-112">**GET**</span></span> | <span data-ttu-id="9af24-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9af24-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9af24-114">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9af24-114">Request headers</span></span>

<span data-ttu-id="9af24-115">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9af24-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="9af24-116">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="9af24-116">URI parameters</span></span>

| <span data-ttu-id="9af24-117">Parametr</span><span class="sxs-lookup"><span data-stu-id="9af24-117">Parameter</span></span>         | <span data-ttu-id="9af24-118">Typ</span><span class="sxs-lookup"><span data-stu-id="9af24-118">Type</span></span>     | <span data-ttu-id="9af24-119">Popis</span><span class="sxs-lookup"><span data-stu-id="9af24-119">Description</span></span> | <span data-ttu-id="9af24-120">Povinné</span><span class="sxs-lookup"><span data-stu-id="9af24-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="9af24-121">top</span><span class="sxs-lookup"><span data-stu-id="9af24-121">top</span></span>               | <span data-ttu-id="9af24-122">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-122">string</span></span>   | <span data-ttu-id="9af24-123">Počet řádků dat, které se v požadavku vrátí.</span><span class="sxs-lookup"><span data-stu-id="9af24-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="9af24-124">Maximální hodnota a výchozí hodnota, pokud není zadaná, je 10 000.</span><span class="sxs-lookup"><span data-stu-id="9af24-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="9af24-125">Pokud dotaz obsahuje více řádků, obsahuje text odpovědi další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="9af24-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="9af24-126">No</span><span class="sxs-lookup"><span data-stu-id="9af24-126">No</span></span> |
| <span data-ttu-id="9af24-127">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="9af24-127">skip</span></span>              | <span data-ttu-id="9af24-128">int</span><span class="sxs-lookup"><span data-stu-id="9af24-128">int</span></span>      | <span data-ttu-id="9af24-129">Počet řádků, které se v dotazu přeskočí</span><span class="sxs-lookup"><span data-stu-id="9af24-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="9af24-130">Tento parametr použijte k stránkování velkých datových sad.</span><span class="sxs-lookup"><span data-stu-id="9af24-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="9af24-131">Například top=10000 a skip=0 načte prvních 10 000 řádků dat, top=10000 a skip=10000 načte dalších 1 0000 řádků dat atd.</span><span class="sxs-lookup"><span data-stu-id="9af24-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="9af24-132">No</span><span class="sxs-lookup"><span data-stu-id="9af24-132">No</span></span> |
| <span data-ttu-id="9af24-133">filter</span><span class="sxs-lookup"><span data-stu-id="9af24-133">filter</span></span>            | <span data-ttu-id="9af24-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-134">string</span></span>   | <span data-ttu-id="9af24-135">Parametr *filter* požadavku obsahuje jeden nebo více příkazů, které filtruje řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9af24-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="9af24-136">Každý příkaz obsahuje pole a hodnotu, které jsou přidruženy k operátorům nebo , a příkazy **`eq`** **`ne`** lze kombinovat pomocí **`and`** nebo **`or`** .</span><span class="sxs-lookup"><span data-stu-id="9af24-136">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="9af24-137">Tady je několik příkladů *parametrů* filtru:</span><span class="sxs-lookup"><span data-stu-id="9af24-137">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="9af24-138">*filter=workloadCode eq 'SFB'*</span><span class="sxs-lookup"><span data-stu-id="9af24-138">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="9af24-139">*filter=workloadCode eq 'SFB'* nebo (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="9af24-139">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="9af24-140">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="9af24-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="9af24-141">**workloadCode (kód úlohy)**</span><span class="sxs-lookup"><span data-stu-id="9af24-141">**workloadCode**</span></span><br/><span data-ttu-id="9af24-142">**název úlohy**</span><span class="sxs-lookup"><span data-stu-id="9af24-142">**workloadName**</span></span><br/><span data-ttu-id="9af24-143">**serviceCode (kód služby)**</span><span class="sxs-lookup"><span data-stu-id="9af24-143">**serviceCode**</span></span><br/><span data-ttu-id="9af24-144">**Název_služby**</span><span class="sxs-lookup"><span data-stu-id="9af24-144">**serviceName**</span></span><br/><span data-ttu-id="9af24-145">**Kanál**</span><span class="sxs-lookup"><span data-stu-id="9af24-145">**channel**</span></span><br/><span data-ttu-id="9af24-146">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="9af24-146">**customerTenantId**</span></span><br/><span data-ttu-id="9af24-147">**customerName**</span><span class="sxs-lookup"><span data-stu-id="9af24-147">**customerName**</span></span><br/><span data-ttu-id="9af24-148">**Productid**</span><span class="sxs-lookup"><span data-stu-id="9af24-148">**productId**</span></span><br/><span data-ttu-id="9af24-149">**Productname**</span><span class="sxs-lookup"><span data-stu-id="9af24-149">**productName**</span></span> | <span data-ttu-id="9af24-150">No</span><span class="sxs-lookup"><span data-stu-id="9af24-150">No</span></span> |
| <span data-ttu-id="9af24-151">Groupby</span><span class="sxs-lookup"><span data-stu-id="9af24-151">groupby</span></span>           | <span data-ttu-id="9af24-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-152">string</span></span>   | <span data-ttu-id="9af24-153">Příkaz, který použije agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="9af24-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="9af24-154">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="9af24-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="9af24-155">**workloadCode (kód úlohy)**</span><span class="sxs-lookup"><span data-stu-id="9af24-155">**workloadCode**</span></span><br/><span data-ttu-id="9af24-156">**název úlohy**</span><span class="sxs-lookup"><span data-stu-id="9af24-156">**workloadName**</span></span><br/><span data-ttu-id="9af24-157">**serviceCode (kód služby)**</span><span class="sxs-lookup"><span data-stu-id="9af24-157">**serviceCode**</span></span><br/><span data-ttu-id="9af24-158">**Název_služby**</span><span class="sxs-lookup"><span data-stu-id="9af24-158">**serviceName**</span></span><br/><span data-ttu-id="9af24-159">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="9af24-159">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="9af24-160">**customerName**</span><span class="sxs-lookup"><span data-stu-id="9af24-160">**customerName**</span></span><br/><span data-ttu-id="9af24-161">**Productid**</span><span class="sxs-lookup"><span data-stu-id="9af24-161">**productId**</span></span><br/><span data-ttu-id="9af24-162">**Productname**</span><span class="sxs-lookup"><span data-stu-id="9af24-162">**productName**</span></span><br/><br/><span data-ttu-id="9af24-163">Vrácené řádky dat budou obsahovat pole zadaná v *parametru groupby* a následující:</span><span class="sxs-lookup"><span data-stu-id="9af24-163">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="9af24-164">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="9af24-164">**licensesActive**</span></span><br/><span data-ttu-id="9af24-165">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="9af24-165">**licensesQualified**</span></span> | <span data-ttu-id="9af24-166">No</span><span class="sxs-lookup"><span data-stu-id="9af24-166">No</span></span> |
| <span data-ttu-id="9af24-167">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="9af24-167">processedDateTime</span></span> | <span data-ttu-id="9af24-168">DateTime</span><span class="sxs-lookup"><span data-stu-id="9af24-168">DateTime</span></span> | <span data-ttu-id="9af24-169">Můžete zadat datum, od kterého se data o využití zpracují.</span><span class="sxs-lookup"><span data-stu-id="9af24-169">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="9af24-170">Výchozí hodnota je nejnovější datum zpracování dat.</span><span class="sxs-lookup"><span data-stu-id="9af24-170">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="9af24-171">No</span><span class="sxs-lookup"><span data-stu-id="9af24-171">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="9af24-172">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9af24-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="9af24-173">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9af24-173">REST response</span></span>

<span data-ttu-id="9af24-174">V případě úspěchu bude text odpovědi obsahovat následující pole obsahující data o využití licencí.</span><span class="sxs-lookup"><span data-stu-id="9af24-174">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="9af24-175">Pole</span><span class="sxs-lookup"><span data-stu-id="9af24-175">Field</span></span>             | <span data-ttu-id="9af24-176">Typ</span><span class="sxs-lookup"><span data-stu-id="9af24-176">Type</span></span>     | <span data-ttu-id="9af24-177">Description</span><span class="sxs-lookup"><span data-stu-id="9af24-177">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="9af24-178">workloadCode (kód úlohy)</span><span class="sxs-lookup"><span data-stu-id="9af24-178">workloadCode</span></span>      | <span data-ttu-id="9af24-179">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-179">string</span></span>   | <span data-ttu-id="9af24-180">Kód úlohy</span><span class="sxs-lookup"><span data-stu-id="9af24-180">Workload code</span></span>                                 |
| <span data-ttu-id="9af24-181">název úlohy</span><span class="sxs-lookup"><span data-stu-id="9af24-181">workloadName</span></span>      | <span data-ttu-id="9af24-182">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-182">string</span></span>   | <span data-ttu-id="9af24-183">Název úlohy</span><span class="sxs-lookup"><span data-stu-id="9af24-183">Workload name</span></span>                                 |
| <span data-ttu-id="9af24-184">serviceCode (kód služby)</span><span class="sxs-lookup"><span data-stu-id="9af24-184">serviceCode</span></span>       | <span data-ttu-id="9af24-185">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-185">string</span></span>   | <span data-ttu-id="9af24-186">Kód služby</span><span class="sxs-lookup"><span data-stu-id="9af24-186">Service code</span></span>                                  |
| <span data-ttu-id="9af24-187">Název_služby</span><span class="sxs-lookup"><span data-stu-id="9af24-187">serviceName</span></span>       | <span data-ttu-id="9af24-188">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-188">string</span></span>   | <span data-ttu-id="9af24-189">Název služby</span><span class="sxs-lookup"><span data-stu-id="9af24-189">Service name</span></span>                                  |
| <span data-ttu-id="9af24-190">Kanál</span><span class="sxs-lookup"><span data-stu-id="9af24-190">channel</span></span>           | <span data-ttu-id="9af24-191">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-191">string</span></span>   | <span data-ttu-id="9af24-192">Název kanálu, prodejce</span><span class="sxs-lookup"><span data-stu-id="9af24-192">Channel name, reseller</span></span>                        |
| <span data-ttu-id="9af24-193">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="9af24-193">customerTenantId</span></span>  | <span data-ttu-id="9af24-194">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-194">string</span></span>   | <span data-ttu-id="9af24-195">Jedinečný identifikátor zákazníka</span><span class="sxs-lookup"><span data-stu-id="9af24-195">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="9af24-196">customerName</span><span class="sxs-lookup"><span data-stu-id="9af24-196">customerName</span></span>      | <span data-ttu-id="9af24-197">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-197">string</span></span>   | <span data-ttu-id="9af24-198">Jméno zákazníka</span><span class="sxs-lookup"><span data-stu-id="9af24-198">Customer name</span></span>                                 |
| <span data-ttu-id="9af24-199">productId</span><span class="sxs-lookup"><span data-stu-id="9af24-199">productId</span></span>         | <span data-ttu-id="9af24-200">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-200">string</span></span>   | <span data-ttu-id="9af24-201">Jedinečný identifikátor produktu</span><span class="sxs-lookup"><span data-stu-id="9af24-201">Unique identifier for the product</span></span>             |
| <span data-ttu-id="9af24-202">Productname</span><span class="sxs-lookup"><span data-stu-id="9af24-202">productName</span></span>       | <span data-ttu-id="9af24-203">řetězec</span><span class="sxs-lookup"><span data-stu-id="9af24-203">string</span></span>   | <span data-ttu-id="9af24-204">Název produktu</span><span class="sxs-lookup"><span data-stu-id="9af24-204">Product name</span></span>                                  |
| <span data-ttu-id="9af24-205">licensesActive</span><span class="sxs-lookup"><span data-stu-id="9af24-205">licensesActive</span></span>    | <span data-ttu-id="9af24-206">long</span><span class="sxs-lookup"><span data-stu-id="9af24-206">long</span></span>     | <span data-ttu-id="9af24-207">Počet aktivních licencí na úlohu</span><span class="sxs-lookup"><span data-stu-id="9af24-207">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="9af24-208">licensesQualified</span><span class="sxs-lookup"><span data-stu-id="9af24-208">licensesQualified</span></span> | <span data-ttu-id="9af24-209">long</span><span class="sxs-lookup"><span data-stu-id="9af24-209">long</span></span>     | <span data-ttu-id="9af24-210">Počet kvalifikovaných licencí pro úlohu</span><span class="sxs-lookup"><span data-stu-id="9af24-210">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="9af24-211">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="9af24-211">processedDateTime</span></span> | <span data-ttu-id="9af24-212">DateTime</span><span class="sxs-lookup"><span data-stu-id="9af24-212">DateTime</span></span> | <span data-ttu-id="9af24-213">Datum posledního zpracování dat</span><span class="sxs-lookup"><span data-stu-id="9af24-213">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9af24-214">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="9af24-214">Response success and error codes</span></span>

<span data-ttu-id="9af24-215">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9af24-215">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9af24-216">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="9af24-216">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9af24-217">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9af24-217">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9af24-218">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9af24-218">Response example</span></span>

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
