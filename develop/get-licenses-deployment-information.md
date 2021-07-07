---
title: Získání informací o nasazení licencí
description: jak získat informace o nasazení pro licence Office a Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9eb0dc655affb2216b11635e58e00ed6464d6792
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445659"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="742e3-103">Získání informací o nasazení licencí</span><span class="sxs-lookup"><span data-stu-id="742e3-103">Get licenses deployment information</span></span>

<span data-ttu-id="742e3-104">jak získat informace o nasazení pro licence Office a Dynamics.</span><span class="sxs-lookup"><span data-stu-id="742e3-104">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="742e3-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="742e3-105">Prerequisites</span></span>

<span data-ttu-id="742e3-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="742e3-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="742e3-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="742e3-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="742e3-108">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="742e3-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="742e3-109">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="742e3-109">Request syntax</span></span>

| <span data-ttu-id="742e3-110">Metoda</span><span class="sxs-lookup"><span data-stu-id="742e3-110">Method</span></span>  | <span data-ttu-id="742e3-111">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="742e3-111">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="742e3-112">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="742e3-112">**GET**</span></span> | <span data-ttu-id="742e3-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Deployment/License/HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="742e3-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="742e3-114">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="742e3-114">Request headers</span></span>

<span data-ttu-id="742e3-115">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="742e3-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="742e3-116">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="742e3-116">URI parameters</span></span>

| <span data-ttu-id="742e3-117">Parametr</span><span class="sxs-lookup"><span data-stu-id="742e3-117">Parameter</span></span>         | <span data-ttu-id="742e3-118">Typ</span><span class="sxs-lookup"><span data-stu-id="742e3-118">Type</span></span>     | <span data-ttu-id="742e3-119">Popis</span><span class="sxs-lookup"><span data-stu-id="742e3-119">Description</span></span> | <span data-ttu-id="742e3-120">Povinné</span><span class="sxs-lookup"><span data-stu-id="742e3-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="742e3-121">top</span><span class="sxs-lookup"><span data-stu-id="742e3-121">top</span></span>               | <span data-ttu-id="742e3-122">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-122">string</span></span>   | <span data-ttu-id="742e3-123">Počet řádků dat, který má být vrácen v požadavku.</span><span class="sxs-lookup"><span data-stu-id="742e3-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="742e3-124">Maximální hodnota a výchozí hodnota, pokud není zadána, je 10000.</span><span class="sxs-lookup"><span data-stu-id="742e3-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="742e3-125">Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="742e3-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="742e3-126">No</span><span class="sxs-lookup"><span data-stu-id="742e3-126">No</span></span> |
| <span data-ttu-id="742e3-127">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="742e3-127">skip</span></span>              | <span data-ttu-id="742e3-128">int</span><span class="sxs-lookup"><span data-stu-id="742e3-128">int</span></span>      | <span data-ttu-id="742e3-129">Počet řádků, které mají být v dotazu přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="742e3-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="742e3-130">Tento parametr použijte pro stránku s velkými datovými sadami.</span><span class="sxs-lookup"><span data-stu-id="742e3-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="742e3-131">Například Top = 10000 a Skip = 0 načte prvních 10000 řádků dat, Top = 10000 a Skip = 10000 načte další 10000 řádků dat a tak dále.</span><span class="sxs-lookup"><span data-stu-id="742e3-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="742e3-132">No</span><span class="sxs-lookup"><span data-stu-id="742e3-132">No</span></span> |
| <span data-ttu-id="742e3-133">filter</span><span class="sxs-lookup"><span data-stu-id="742e3-133">filter</span></span>            | <span data-ttu-id="742e3-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-134">string</span></span>   | <span data-ttu-id="742e3-135">Parametr *filtru* požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="742e3-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="742e3-136">Každý příkaz obsahuje pole a hodnotu, které jsou spojeny s `eq` `ne` operátory nebo, a příkazy lze kombinovat pomocí operátoru OR `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="742e3-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="742e3-137">Tady je několik příkladů parametrů *filtru* :</span><span class="sxs-lookup"><span data-stu-id="742e3-137">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="742e3-138">*Filter = serviceCode EQ ' O365 '*</span><span class="sxs-lookup"><span data-stu-id="742e3-138">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="742e3-139">*Filter = serviceCode EQ ' O365 '* nebo (*Channel EQ ' prodejce '*)</span><span class="sxs-lookup"><span data-stu-id="742e3-139">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="742e3-140">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="742e3-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="742e3-141">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="742e3-141">**serviceCode**</span></span><br/><span data-ttu-id="742e3-142">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="742e3-142">**serviceName**</span></span><br/><span data-ttu-id="742e3-143">**kanál**</span><span class="sxs-lookup"><span data-stu-id="742e3-143">**channel**</span></span><br/><span data-ttu-id="742e3-144">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="742e3-144">**customerTenantId**</span></span><br/><span data-ttu-id="742e3-145">**customerName**</span><span class="sxs-lookup"><span data-stu-id="742e3-145">**customerName**</span></span><br/><span data-ttu-id="742e3-146">**productId**</span><span class="sxs-lookup"><span data-stu-id="742e3-146">**productId**</span></span><br/><span data-ttu-id="742e3-147">**NázevVýrobku**</span><span class="sxs-lookup"><span data-stu-id="742e3-147">**productName**</span></span>  | <span data-ttu-id="742e3-148">No</span><span class="sxs-lookup"><span data-stu-id="742e3-148">No</span></span> |
| <span data-ttu-id="742e3-149">GroupBy</span><span class="sxs-lookup"><span data-stu-id="742e3-149">groupby</span></span>           | <span data-ttu-id="742e3-150">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-150">string</span></span>   | <span data-ttu-id="742e3-151">Příkaz, který aplikuje agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="742e3-151">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="742e3-152">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="742e3-152">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="742e3-153">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="742e3-153">**serviceCode**</span></span><br/><span data-ttu-id="742e3-154">**serviceName**</span><span class="sxs-lookup"><span data-stu-id="742e3-154">**serviceName**</span></span><br/><span data-ttu-id="742e3-155">**kanál**</span><span class="sxs-lookup"><span data-stu-id="742e3-155">**channel**</span></span><br/><span data-ttu-id="742e3-156">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="742e3-156">**customerTenantId**</span></span><br/><span data-ttu-id="742e3-157">**customerName**</span><span class="sxs-lookup"><span data-stu-id="742e3-157">**customerName**</span></span><br/><span data-ttu-id="742e3-158">**productId**</span><span class="sxs-lookup"><span data-stu-id="742e3-158">**productId**</span></span><br/><span data-ttu-id="742e3-159">**NázevVýrobku**</span><span class="sxs-lookup"><span data-stu-id="742e3-159">**productName**</span></span><br/><br/> <span data-ttu-id="742e3-160">Vrácené řádky dat budou obsahovat pole zadaná v parametru *GroupBy* a následující:</span><span class="sxs-lookup"><span data-stu-id="742e3-160">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="742e3-161">**licensesDeployed**</span><span class="sxs-lookup"><span data-stu-id="742e3-161">**licensesDeployed**</span></span><br/><span data-ttu-id="742e3-162">**licensesSold**</span><span class="sxs-lookup"><span data-stu-id="742e3-162">**licensesSold**</span></span>  | <span data-ttu-id="742e3-163">No</span><span class="sxs-lookup"><span data-stu-id="742e3-163">No</span></span> |
| <span data-ttu-id="742e3-164">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="742e3-164">processedDateTime</span></span> | <span data-ttu-id="742e3-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="742e3-165">DateTime</span></span> | <span data-ttu-id="742e3-166">Jedna z nich může určovat datum, ze kterého byla zpracována data o využití.</span><span class="sxs-lookup"><span data-stu-id="742e3-166">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="742e3-167">Výchozí hodnota je poslední datum, kdy byla data zpracována.</span><span class="sxs-lookup"><span data-stu-id="742e3-167">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="742e3-168">No</span><span class="sxs-lookup"><span data-stu-id="742e3-168">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="742e3-169">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="742e3-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="742e3-170">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="742e3-170">REST response</span></span>

<span data-ttu-id="742e3-171">V případě úspěchu obsahuje tělo odpovědi následující pole obsahující data o nasazených licencích.</span><span class="sxs-lookup"><span data-stu-id="742e3-171">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="742e3-172">Pole</span><span class="sxs-lookup"><span data-stu-id="742e3-172">Field</span></span>             | <span data-ttu-id="742e3-173">Typ</span><span class="sxs-lookup"><span data-stu-id="742e3-173">Type</span></span>     | <span data-ttu-id="742e3-174">Description</span><span class="sxs-lookup"><span data-stu-id="742e3-174">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="742e3-175">serviceCode</span><span class="sxs-lookup"><span data-stu-id="742e3-175">serviceCode</span></span>       | <span data-ttu-id="742e3-176">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-176">string</span></span>   | <span data-ttu-id="742e3-177">Kód služby</span><span class="sxs-lookup"><span data-stu-id="742e3-177">Service code</span></span>                          |
| <span data-ttu-id="742e3-178">serviceName</span><span class="sxs-lookup"><span data-stu-id="742e3-178">serviceName</span></span>       | <span data-ttu-id="742e3-179">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-179">string</span></span>   | <span data-ttu-id="742e3-180">Název služby</span><span class="sxs-lookup"><span data-stu-id="742e3-180">Service name</span></span>                          |
| <span data-ttu-id="742e3-181">kanál</span><span class="sxs-lookup"><span data-stu-id="742e3-181">channel</span></span>           | <span data-ttu-id="742e3-182">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-182">string</span></span>   | <span data-ttu-id="742e3-183">Název kanálu, prodejce</span><span class="sxs-lookup"><span data-stu-id="742e3-183">Channel name, reseller</span></span>                |
| <span data-ttu-id="742e3-184">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="742e3-184">customerTenantId</span></span>  | <span data-ttu-id="742e3-185">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-185">string</span></span>   | <span data-ttu-id="742e3-186">Jedinečný identifikátor pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="742e3-186">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="742e3-187">customerName</span><span class="sxs-lookup"><span data-stu-id="742e3-187">customerName</span></span>      | <span data-ttu-id="742e3-188">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-188">string</span></span>   | <span data-ttu-id="742e3-189">Jméno zákazníka</span><span class="sxs-lookup"><span data-stu-id="742e3-189">Customer name</span></span>                         |
| <span data-ttu-id="742e3-190">productId</span><span class="sxs-lookup"><span data-stu-id="742e3-190">productId</span></span>         | <span data-ttu-id="742e3-191">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-191">string</span></span>   | <span data-ttu-id="742e3-192">Jedinečný identifikátor produktu</span><span class="sxs-lookup"><span data-stu-id="742e3-192">Unique identifier for the product</span></span>     |
| <span data-ttu-id="742e3-193">NázevVýrobku</span><span class="sxs-lookup"><span data-stu-id="742e3-193">productName</span></span>       | <span data-ttu-id="742e3-194">řetězec</span><span class="sxs-lookup"><span data-stu-id="742e3-194">string</span></span>   | <span data-ttu-id="742e3-195">Název produktu</span><span class="sxs-lookup"><span data-stu-id="742e3-195">Product name</span></span>                          |
| <span data-ttu-id="742e3-196">licensesDeployed</span><span class="sxs-lookup"><span data-stu-id="742e3-196">licensesDeployed</span></span>  | <span data-ttu-id="742e3-197">long</span><span class="sxs-lookup"><span data-stu-id="742e3-197">long</span></span>     | <span data-ttu-id="742e3-198">Počet nasazených licencí</span><span class="sxs-lookup"><span data-stu-id="742e3-198">Number of licenses deployed</span></span>           |
| <span data-ttu-id="742e3-199">licensesSold</span><span class="sxs-lookup"><span data-stu-id="742e3-199">licensesSold</span></span>      | <span data-ttu-id="742e3-200">long</span><span class="sxs-lookup"><span data-stu-id="742e3-200">long</span></span>     | <span data-ttu-id="742e3-201">Počet prodaných licencí</span><span class="sxs-lookup"><span data-stu-id="742e3-201">Number of licenses sold</span></span>               |
| <span data-ttu-id="742e3-202">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="742e3-202">processedDateTime</span></span> | <span data-ttu-id="742e3-203">DateTime</span><span class="sxs-lookup"><span data-stu-id="742e3-203">DateTime</span></span> | <span data-ttu-id="742e3-204">Datum posledního zpracování dat</span><span class="sxs-lookup"><span data-stu-id="742e3-204">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="742e3-205">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="742e3-205">Response success and error codes</span></span>

<span data-ttu-id="742e3-206">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="742e3-206">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="742e3-207">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="742e3-207">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="742e3-208">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="742e3-208">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="742e3-209">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="742e3-209">Response example</span></span>

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
