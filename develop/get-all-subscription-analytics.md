---
title: Získání všech analytických informací o předplatných
description: Jak získat všechny informace o analýze předplatných.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: f32fb99ad52939ae8e9de26276588d3022f18fbc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766669"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="bfefc-103">Získání všech analytických informací o předplatných</span><span class="sxs-lookup"><span data-stu-id="bfefc-103">Get all subscription analytics information</span></span>

<span data-ttu-id="bfefc-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="bfefc-104">**Applies to:**</span></span>

- <span data-ttu-id="bfefc-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="bfefc-105">Partner Center</span></span>
- <span data-ttu-id="bfefc-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="bfefc-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="bfefc-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="bfefc-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="bfefc-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bfefc-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bfefc-109">Tento článek popisuje, jak získat všechny informace o analýze předplatného pro vaše zákazníky.</span><span class="sxs-lookup"><span data-stu-id="bfefc-109">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfefc-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bfefc-110">Prerequisites</span></span>

- <span data-ttu-id="bfefc-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bfefc-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bfefc-112">Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.</span><span class="sxs-lookup"><span data-stu-id="bfefc-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="bfefc-113">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="bfefc-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bfefc-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="bfefc-114">Request syntax</span></span>

| <span data-ttu-id="bfefc-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="bfefc-115">Method</span></span> | <span data-ttu-id="bfefc-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="bfefc-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="bfefc-117">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="bfefc-117">**GET**</span></span> | <span data-ttu-id="bfefc-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bfefc-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="bfefc-119">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="bfefc-119">URI parameters</span></span>

<span data-ttu-id="bfefc-120">V následující tabulce jsou uvedeny volitelné parametry a jejich popisy:</span><span class="sxs-lookup"><span data-stu-id="bfefc-120">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="bfefc-121">Parametr</span><span class="sxs-lookup"><span data-stu-id="bfefc-121">Parameter</span></span> | <span data-ttu-id="bfefc-122">Typ</span><span class="sxs-lookup"><span data-stu-id="bfefc-122">Type</span></span> |  <span data-ttu-id="bfefc-123">Description</span><span class="sxs-lookup"><span data-stu-id="bfefc-123">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="bfefc-124">top</span><span class="sxs-lookup"><span data-stu-id="bfefc-124">top</span></span> | <span data-ttu-id="bfefc-125">int</span><span class="sxs-lookup"><span data-stu-id="bfefc-125">int</span></span> | <span data-ttu-id="bfefc-126">Počet řádků dat, který má být vrácen v požadavku.</span><span class="sxs-lookup"><span data-stu-id="bfefc-126">The number of rows of data to return in the request.</span></span> <span data-ttu-id="bfefc-127">Pokud hodnota není zadaná, maximální hodnota a výchozí hodnota je `10000` .</span><span class="sxs-lookup"><span data-stu-id="bfefc-127">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="bfefc-128">Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="bfefc-128">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="bfefc-129">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="bfefc-129">skip</span></span> | <span data-ttu-id="bfefc-130">int</span><span class="sxs-lookup"><span data-stu-id="bfefc-130">int</span></span> | <span data-ttu-id="bfefc-131">Počet řádků, které mají být v dotazu přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="bfefc-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="bfefc-132">Tento parametr použijte pro stránku s velkými datovými sadami.</span><span class="sxs-lookup"><span data-stu-id="bfefc-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="bfefc-133">Například `top=10000` `skip=0` načte první 10000 řádků dat a `top=10000` `skip=10000` načte další 10000 řádků dat.</span><span class="sxs-lookup"><span data-stu-id="bfefc-133">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="bfefc-134">filter</span><span class="sxs-lookup"><span data-stu-id="bfefc-134">filter</span></span> | <span data-ttu-id="bfefc-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="bfefc-135">string</span></span> | <span data-ttu-id="bfefc-136">Jeden nebo více příkazů, které filtrují řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="bfefc-136">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="bfefc-137">Každý příkaz filtru obsahuje název pole z textu odpovědi a hodnotu, která je přidružena k **`eq`** , **`ne`** nebo pro určitá pole **`contains`** operátor.</span><span class="sxs-lookup"><span data-stu-id="bfefc-137">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="bfefc-138">Příkazy lze kombinovat pomocí operátoru **`and`** OR **`or`** .</span><span class="sxs-lookup"><span data-stu-id="bfefc-138">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="bfefc-139">Řetězcové hodnoty musí být obklopeny jednoduchými uvozovkami v parametru **Filter** .</span><span class="sxs-lookup"><span data-stu-id="bfefc-139">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="bfefc-140">Seznam polí, která lze filtrovat, a operátory, které jsou s těmito poli podporovány, naleznete v následující části.</span><span class="sxs-lookup"><span data-stu-id="bfefc-140">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="bfefc-141">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="bfefc-141">aggregationLevel</span></span> | <span data-ttu-id="bfefc-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="bfefc-142">string</span></span> | <span data-ttu-id="bfefc-143">Určuje časový rozsah, pro který se mají načíst agregovaná data.</span><span class="sxs-lookup"><span data-stu-id="bfefc-143">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="bfefc-144">Může to být jeden z následujících řetězců: **den**, **týden** nebo **měsíc**.</span><span class="sxs-lookup"><span data-stu-id="bfefc-144">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="bfefc-145">Pokud hodnota není zadaná, výchozí hodnota je **DateRange**.</span><span class="sxs-lookup"><span data-stu-id="bfefc-145">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="bfefc-146">Tento parametr platí pouze v případě, že je pole data předáno jako součást parametru **GroupBy** .</span><span class="sxs-lookup"><span data-stu-id="bfefc-146">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="bfefc-147">groupBy</span><span class="sxs-lookup"><span data-stu-id="bfefc-147">groupBy</span></span> | <span data-ttu-id="bfefc-148">řetězec</span><span class="sxs-lookup"><span data-stu-id="bfefc-148">string</span></span> | <span data-ttu-id="bfefc-149">Příkaz, který aplikuje agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="bfefc-149">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bfefc-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="bfefc-150">Request headers</span></span>

<span data-ttu-id="bfefc-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bfefc-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bfefc-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="bfefc-152">Request body</span></span>

<span data-ttu-id="bfefc-153">Žádné</span><span class="sxs-lookup"><span data-stu-id="bfefc-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bfefc-154">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bfefc-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="bfefc-155">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="bfefc-155">REST response</span></span>

<span data-ttu-id="bfefc-156">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [**předplatného**](partner-center-analytics-resources.md#subscription-resource) .</span><span class="sxs-lookup"><span data-stu-id="bfefc-156">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bfefc-157">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="bfefc-157">Response success and error codes</span></span>

<span data-ttu-id="bfefc-158">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="bfefc-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bfefc-159">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="bfefc-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bfefc-160">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bfefc-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bfefc-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bfefc-161">Response example</span></span>

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a><span data-ttu-id="bfefc-162">Viz také</span><span class="sxs-lookup"><span data-stu-id="bfefc-162">See also</span></span>

- [<span data-ttu-id="bfefc-163">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="bfefc-163">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
