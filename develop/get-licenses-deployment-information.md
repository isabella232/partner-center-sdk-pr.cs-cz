---
title: Získání informací o nasazení licencí
description: Jak získat informace o nasazení pro licence na Office a Dynamics
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef0e5d73d34bc51e4cc58143db6c9fc49cb58fcb
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766896"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="72e07-103">Získání informací o nasazení licencí</span><span class="sxs-lookup"><span data-stu-id="72e07-103">Get licenses deployment information</span></span>

<span data-ttu-id="72e07-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="72e07-104">**Applies To**</span></span>

- <span data-ttu-id="72e07-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="72e07-105">Partner Center</span></span>

<span data-ttu-id="72e07-106">Jak získat informace o nasazení pro licence na Office a Dynamics</span><span class="sxs-lookup"><span data-stu-id="72e07-106">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72e07-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="72e07-107">Prerequisites</span></span>

<span data-ttu-id="72e07-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="72e07-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="72e07-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="72e07-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="72e07-110">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="72e07-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="72e07-111">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="72e07-111">Request syntax</span></span>

| <span data-ttu-id="72e07-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="72e07-112">Method</span></span>  | <span data-ttu-id="72e07-113">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="72e07-113">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72e07-114">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="72e07-114">**GET**</span></span> | <span data-ttu-id="72e07-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Deployment/License/HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="72e07-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="72e07-116">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="72e07-116">Request headers</span></span>

<span data-ttu-id="72e07-117">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="72e07-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="72e07-118">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="72e07-118">URI parameters</span></span>

| <span data-ttu-id="72e07-119">Parametr</span><span class="sxs-lookup"><span data-stu-id="72e07-119">Parameter</span></span>         | <span data-ttu-id="72e07-120">Typ</span><span class="sxs-lookup"><span data-stu-id="72e07-120">Type</span></span>     | <span data-ttu-id="72e07-121">Popis</span><span class="sxs-lookup"><span data-stu-id="72e07-121">Description</span></span> | <span data-ttu-id="72e07-122">Povinné</span><span class="sxs-lookup"><span data-stu-id="72e07-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="72e07-123">top</span><span class="sxs-lookup"><span data-stu-id="72e07-123">top</span></span>               | <span data-ttu-id="72e07-124">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-124">string</span></span>   | <span data-ttu-id="72e07-125">Počet řádků dat, který má být vrácen v požadavku.</span><span class="sxs-lookup"><span data-stu-id="72e07-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="72e07-126">Maximální hodnota a výchozí hodnota, pokud není zadána, je 10000.</span><span class="sxs-lookup"><span data-stu-id="72e07-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="72e07-127">Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="72e07-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="72e07-128">No</span><span class="sxs-lookup"><span data-stu-id="72e07-128">No</span></span> |
| <span data-ttu-id="72e07-129">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="72e07-129">skip</span></span>              | <span data-ttu-id="72e07-130">int</span><span class="sxs-lookup"><span data-stu-id="72e07-130">int</span></span>      | <span data-ttu-id="72e07-131">Počet řádků, které mají být v dotazu přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="72e07-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="72e07-132">Tento parametr použijte pro stránku s velkými datovými sadami.</span><span class="sxs-lookup"><span data-stu-id="72e07-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="72e07-133">Například Top = 10000 a Skip = 0 načte prvních 10000 řádků dat, Top = 10000 a Skip = 10000 načte další 10000 řádků dat a tak dále.</span><span class="sxs-lookup"><span data-stu-id="72e07-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="72e07-134">No</span><span class="sxs-lookup"><span data-stu-id="72e07-134">No</span></span> |
| <span data-ttu-id="72e07-135">filter</span><span class="sxs-lookup"><span data-stu-id="72e07-135">filter</span></span>            | <span data-ttu-id="72e07-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-136">string</span></span>   | <span data-ttu-id="72e07-137">Parametr *filtru* požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="72e07-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="72e07-138">Každý příkaz obsahuje pole a hodnotu, které jsou spojeny s `eq` `ne` operátory nebo, a příkazy lze kombinovat pomocí operátoru OR `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="72e07-138">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="72e07-139">Tady je několik příkladů parametrů *filtru* :</span><span class="sxs-lookup"><span data-stu-id="72e07-139">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="72e07-140">*Filter = serviceCode EQ ' O365 '*</span><span class="sxs-lookup"><span data-stu-id="72e07-140">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="72e07-141">*Filter = serviceCode EQ ' O365 '* nebo (*Channel EQ ' prodejce '*)</span><span class="sxs-lookup"><span data-stu-id="72e07-141">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="72e07-142">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="72e07-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="72e07-143">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="72e07-143">**serviceCode**</span></span><br/><span data-ttu-id="72e07-144">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="72e07-144">**serviceName**</span></span><br/><span data-ttu-id="72e07-145">**kanál**</span><span class="sxs-lookup"><span data-stu-id="72e07-145">**channel**</span></span><br/><span data-ttu-id="72e07-146">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="72e07-146">**customerTenantId**</span></span><br/><span data-ttu-id="72e07-147">**customerName**</span><span class="sxs-lookup"><span data-stu-id="72e07-147">**customerName**</span></span><br/><span data-ttu-id="72e07-148">**productId**</span><span class="sxs-lookup"><span data-stu-id="72e07-148">**productId**</span></span><br/><span data-ttu-id="72e07-149">**NázevVýrobku**</span><span class="sxs-lookup"><span data-stu-id="72e07-149">**productName**</span></span>  | <span data-ttu-id="72e07-150">No</span><span class="sxs-lookup"><span data-stu-id="72e07-150">No</span></span> |
| <span data-ttu-id="72e07-151">GroupBy</span><span class="sxs-lookup"><span data-stu-id="72e07-151">groupby</span></span>           | <span data-ttu-id="72e07-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-152">string</span></span>   | <span data-ttu-id="72e07-153">Příkaz, který aplikuje agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="72e07-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="72e07-154">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="72e07-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="72e07-155">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="72e07-155">**serviceCode**</span></span><br/><span data-ttu-id="72e07-156">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="72e07-156">**serviceName**</span></span><br/><span data-ttu-id="72e07-157">**kanál**</span><span class="sxs-lookup"><span data-stu-id="72e07-157">**channel**</span></span><br/><span data-ttu-id="72e07-158">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="72e07-158">**customerTenantId**</span></span><br/><span data-ttu-id="72e07-159">**customerName**</span><span class="sxs-lookup"><span data-stu-id="72e07-159">**customerName**</span></span><br/><span data-ttu-id="72e07-160">**productId**</span><span class="sxs-lookup"><span data-stu-id="72e07-160">**productId**</span></span><br/><span data-ttu-id="72e07-161">**NázevVýrobku**</span><span class="sxs-lookup"><span data-stu-id="72e07-161">**productName**</span></span><br/><br/> <span data-ttu-id="72e07-162">Vrácené řádky dat budou obsahovat pole zadaná v parametru *GroupBy* a také následující:</span><span class="sxs-lookup"><span data-stu-id="72e07-162">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="72e07-163">**licensesDeployed**</span><span class="sxs-lookup"><span data-stu-id="72e07-163">**licensesDeployed**</span></span><br/><span data-ttu-id="72e07-164">**licensesSold**</span><span class="sxs-lookup"><span data-stu-id="72e07-164">**licensesSold**</span></span>  | <span data-ttu-id="72e07-165">No</span><span class="sxs-lookup"><span data-stu-id="72e07-165">No</span></span> |
| <span data-ttu-id="72e07-166">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="72e07-166">processedDateTime</span></span> | <span data-ttu-id="72e07-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="72e07-167">DateTime</span></span> | <span data-ttu-id="72e07-168">Jedna z nich může určovat datum, ze kterého byla zpracována data o využití.</span><span class="sxs-lookup"><span data-stu-id="72e07-168">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="72e07-169">Výchozí hodnota je poslední datum, kdy byla data zpracována.</span><span class="sxs-lookup"><span data-stu-id="72e07-169">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="72e07-170">No</span><span class="sxs-lookup"><span data-stu-id="72e07-170">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="72e07-171">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="72e07-171">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="72e07-172">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="72e07-172">REST response</span></span>

<span data-ttu-id="72e07-173">V případě úspěchu obsahuje tělo odpovědi následující pole obsahující data o nasazených licencích.</span><span class="sxs-lookup"><span data-stu-id="72e07-173">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="72e07-174">Pole</span><span class="sxs-lookup"><span data-stu-id="72e07-174">Field</span></span>             | <span data-ttu-id="72e07-175">Typ</span><span class="sxs-lookup"><span data-stu-id="72e07-175">Type</span></span>     | <span data-ttu-id="72e07-176">Description</span><span class="sxs-lookup"><span data-stu-id="72e07-176">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="72e07-177">serviceCode</span><span class="sxs-lookup"><span data-stu-id="72e07-177">serviceCode</span></span>       | <span data-ttu-id="72e07-178">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-178">string</span></span>   | <span data-ttu-id="72e07-179">Kód služby</span><span class="sxs-lookup"><span data-stu-id="72e07-179">Service code</span></span>                          |
| <span data-ttu-id="72e07-180">serviceName</span><span class="sxs-lookup"><span data-stu-id="72e07-180">serviceName</span></span>       | <span data-ttu-id="72e07-181">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-181">string</span></span>   | <span data-ttu-id="72e07-182">Název služby</span><span class="sxs-lookup"><span data-stu-id="72e07-182">Service name</span></span>                          |
| <span data-ttu-id="72e07-183">kanál</span><span class="sxs-lookup"><span data-stu-id="72e07-183">channel</span></span>           | <span data-ttu-id="72e07-184">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-184">string</span></span>   | <span data-ttu-id="72e07-185">Název kanálu, prodejce</span><span class="sxs-lookup"><span data-stu-id="72e07-185">Channel name, reseller</span></span>                |
| <span data-ttu-id="72e07-186">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="72e07-186">customerTenantId</span></span>  | <span data-ttu-id="72e07-187">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-187">string</span></span>   | <span data-ttu-id="72e07-188">Jedinečný identifikátor pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="72e07-188">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="72e07-189">customerName</span><span class="sxs-lookup"><span data-stu-id="72e07-189">customerName</span></span>      | <span data-ttu-id="72e07-190">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-190">string</span></span>   | <span data-ttu-id="72e07-191">Jméno zákazníka</span><span class="sxs-lookup"><span data-stu-id="72e07-191">Customer name</span></span>                         |
| <span data-ttu-id="72e07-192">productId</span><span class="sxs-lookup"><span data-stu-id="72e07-192">productId</span></span>         | <span data-ttu-id="72e07-193">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-193">string</span></span>   | <span data-ttu-id="72e07-194">Jedinečný identifikátor produktu</span><span class="sxs-lookup"><span data-stu-id="72e07-194">Unique identifier for the product</span></span>     |
| <span data-ttu-id="72e07-195">NázevVýrobku</span><span class="sxs-lookup"><span data-stu-id="72e07-195">productName</span></span>       | <span data-ttu-id="72e07-196">řetězec</span><span class="sxs-lookup"><span data-stu-id="72e07-196">string</span></span>   | <span data-ttu-id="72e07-197">Název produktu</span><span class="sxs-lookup"><span data-stu-id="72e07-197">Product name</span></span>                          |
| <span data-ttu-id="72e07-198">licensesDeployed</span><span class="sxs-lookup"><span data-stu-id="72e07-198">licensesDeployed</span></span>  | <span data-ttu-id="72e07-199">long</span><span class="sxs-lookup"><span data-stu-id="72e07-199">long</span></span>     | <span data-ttu-id="72e07-200">Počet nasazených licencí</span><span class="sxs-lookup"><span data-stu-id="72e07-200">Number of licenses deployed</span></span>           |
| <span data-ttu-id="72e07-201">licensesSold</span><span class="sxs-lookup"><span data-stu-id="72e07-201">licensesSold</span></span>      | <span data-ttu-id="72e07-202">long</span><span class="sxs-lookup"><span data-stu-id="72e07-202">long</span></span>     | <span data-ttu-id="72e07-203">Počet prodaných licencí</span><span class="sxs-lookup"><span data-stu-id="72e07-203">Number of licenses sold</span></span>               |
| <span data-ttu-id="72e07-204">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="72e07-204">processedDateTime</span></span> | <span data-ttu-id="72e07-205">DateTime</span><span class="sxs-lookup"><span data-stu-id="72e07-205">DateTime</span></span> | <span data-ttu-id="72e07-206">Datum posledního zpracování dat</span><span class="sxs-lookup"><span data-stu-id="72e07-206">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="72e07-207">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="72e07-207">Response success and error codes</span></span>

<span data-ttu-id="72e07-208">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="72e07-208">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="72e07-209">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="72e07-209">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="72e07-210">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="72e07-210">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="72e07-211">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="72e07-211">Response example</span></span>

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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
