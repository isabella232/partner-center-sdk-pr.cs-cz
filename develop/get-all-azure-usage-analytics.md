---
title: Získání všech analytických informací o využití Azure
description: Jak získat všechny informace o analýze využití Azure
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766898"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="c6575-103">Získání všech analytických informací o využití Azure</span><span class="sxs-lookup"><span data-stu-id="c6575-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="c6575-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="c6575-104">**Applies To**</span></span>

- <span data-ttu-id="c6575-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="c6575-105">Partner Center</span></span>
- <span data-ttu-id="c6575-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="c6575-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c6575-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="c6575-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c6575-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c6575-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c6575-109">Jak získat všechny informace o analýze využití Azure pro vaše zákazníky.</span><span class="sxs-lookup"><span data-stu-id="c6575-109">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6575-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c6575-110">Prerequisites</span></span>

- <span data-ttu-id="c6575-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c6575-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c6575-112">Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.</span><span class="sxs-lookup"><span data-stu-id="c6575-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c6575-113">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="c6575-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c6575-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="c6575-114">Request syntax</span></span>

| <span data-ttu-id="c6575-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="c6575-115">Method</span></span>  | <span data-ttu-id="c6575-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="c6575-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="c6575-117">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="c6575-117">**GET**</span></span> | <span data-ttu-id="c6575-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Usage/Azure HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c6575-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="c6575-119">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="c6575-119">URI parameters</span></span>

|<span data-ttu-id="c6575-120">Parametr</span><span class="sxs-lookup"><span data-stu-id="c6575-120">Parameter</span></span>        |<span data-ttu-id="c6575-121">Typ</span><span class="sxs-lookup"><span data-stu-id="c6575-121">Type</span></span>                        |<span data-ttu-id="c6575-122">Description</span><span class="sxs-lookup"><span data-stu-id="c6575-122">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="c6575-123">top</span><span class="sxs-lookup"><span data-stu-id="c6575-123">top</span></span>              | <span data-ttu-id="c6575-124">řetězec</span><span class="sxs-lookup"><span data-stu-id="c6575-124">string</span></span>                     | <span data-ttu-id="c6575-125">Počet řádků dat, který má být vrácen v požadavku.</span><span class="sxs-lookup"><span data-stu-id="c6575-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="c6575-126">Maximální hodnota a výchozí hodnota, pokud není zadána, je 10000.</span><span class="sxs-lookup"><span data-stu-id="c6575-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="c6575-127">Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="c6575-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="c6575-128">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="c6575-128">skip</span></span>             | <span data-ttu-id="c6575-129">int</span><span class="sxs-lookup"><span data-stu-id="c6575-129">int</span></span>                        | <span data-ttu-id="c6575-130">Počet řádků, které mají být v dotazu přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="c6575-130">The number of rows to skip in the query.</span></span> <span data-ttu-id="c6575-131">Tento parametr použijte pro stránku s velkými datovými sadami.</span><span class="sxs-lookup"><span data-stu-id="c6575-131">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="c6575-132">Například `top=10000 and skip=0` načte první 10000 řádků dat, `top=10000 and skip=10000` načte další 10000 řádků dat a tak dále.</span><span class="sxs-lookup"><span data-stu-id="c6575-132">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="c6575-133">filter</span><span class="sxs-lookup"><span data-stu-id="c6575-133">filter</span></span>           | <span data-ttu-id="c6575-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="c6575-134">string</span></span>                     | <span data-ttu-id="c6575-135">Parametr *filtru* požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c6575-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="c6575-136">Každý příkaz obsahuje pole a hodnotu, které jsou spojeny s `eq` `ne` operátory nebo, a příkazy lze kombinovat pomocí operátoru OR `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="c6575-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="c6575-137">Můžete zadat následující řetězce:</span><span class="sxs-lookup"><span data-stu-id="c6575-137">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="c6575-138">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="c6575-138">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="c6575-139">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="c6575-139">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="c6575-140">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="c6575-140">aggregationLevel</span></span> | <span data-ttu-id="c6575-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="c6575-141">string</span></span>                    | <span data-ttu-id="c6575-142">Určuje časový rozsah, pro který se mají načíst agregovaná data.</span><span class="sxs-lookup"><span data-stu-id="c6575-142">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="c6575-143">Může to být jeden z následujících řetězců: `day` , `week` , nebo `month` .</span><span class="sxs-lookup"><span data-stu-id="c6575-143">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="c6575-144">Je-li tento parametr zadán, je použita výchozí hodnota `day` .</span><span class="sxs-lookup"><span data-stu-id="c6575-144">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="c6575-145">`aggregationLevel`Parametr není podporován bez `groupby` .</span><span class="sxs-lookup"><span data-stu-id="c6575-145">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="c6575-146">`aggregationLevel`Parametr platí pro všechna pole kalendářních dat přítomná v `groupby` .</span><span class="sxs-lookup"><span data-stu-id="c6575-146">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="c6575-147">OrderBy</span><span class="sxs-lookup"><span data-stu-id="c6575-147">orderby</span></span>          |<span data-ttu-id="c6575-148">řetězec</span><span class="sxs-lookup"><span data-stu-id="c6575-148">string</span></span>                     | <span data-ttu-id="c6575-149">Příkaz, který seřadí hodnoty výsledných dat pro každou instalaci.</span><span class="sxs-lookup"><span data-stu-id="c6575-149">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="c6575-150">Syntaxe je `...&orderby=field [order],field [order],...`.</span><span class="sxs-lookup"><span data-stu-id="c6575-150">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="c6575-151">`field`Parametr může být jeden z následujících řetězců:</span><span class="sxs-lookup"><span data-stu-id="c6575-151">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="c6575-152">Parametr *Order* je volitelný a může být `asc` nebo `desc` určen pro každé pole ve vzestupném nebo sestupném pořadí.</span><span class="sxs-lookup"><span data-stu-id="c6575-152">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="c6575-153">Výchozí formát je `asc`.</span><span class="sxs-lookup"><span data-stu-id="c6575-153">The default is `asc`.</span></span><br/><br/><span data-ttu-id="c6575-154">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="c6575-154">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="c6575-155">GroupBy</span><span class="sxs-lookup"><span data-stu-id="c6575-155">groupby</span></span>          |<span data-ttu-id="c6575-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="c6575-156">string</span></span>                    | <span data-ttu-id="c6575-157">Příkaz, který aplikuje agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="c6575-157">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="c6575-158">Můžete zadat následující pole:</span><span class="sxs-lookup"><span data-stu-id="c6575-158">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="c6575-159">Vrácené řádky dat budou obsahovat pole zadaná v `groupby`  parametru a také *množství*.</span><span class="sxs-lookup"><span data-stu-id="c6575-159">The returned data rows will contain the fields specified in the `groupby`  parameter as well as the *Quantity*.</span></span><br/><br/><span data-ttu-id="c6575-160">`groupby`Parametr lze použít s `aggregationLevel` parametrem.</span><span class="sxs-lookup"><span data-stu-id="c6575-160">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="c6575-161">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="c6575-161">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="c6575-162">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="c6575-162">Request headers</span></span>

<span data-ttu-id="c6575-163">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c6575-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c6575-164">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="c6575-164">Request body</span></span>

<span data-ttu-id="c6575-165">Žádné</span><span class="sxs-lookup"><span data-stu-id="c6575-165">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c6575-166">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="c6575-166">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="c6575-167">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="c6575-167">REST response</span></span>

<span data-ttu-id="c6575-168">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [využití Azure](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) .</span><span class="sxs-lookup"><span data-stu-id="c6575-168">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c6575-169">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="c6575-169">Response success and error codes</span></span>

<span data-ttu-id="c6575-170">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="c6575-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c6575-171">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="c6575-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c6575-172">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c6575-172">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c6575-173">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="c6575-173">Response example</span></span>

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a><span data-ttu-id="c6575-174">Viz také</span><span class="sxs-lookup"><span data-stu-id="c6575-174">See also</span></span>

- [<span data-ttu-id="c6575-175">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="c6575-175">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
