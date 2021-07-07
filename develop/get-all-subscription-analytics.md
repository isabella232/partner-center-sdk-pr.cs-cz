---
title: Získání všech analytických informací o předplatných
description: Jak získat všechny analytické informace o předplatném
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e1f16c92569a02bc51c96a85ecb642fbeb76a9a7
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760245"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="18505-103">Získání všech analytických informací o předplatných</span><span class="sxs-lookup"><span data-stu-id="18505-103">Get all subscription analytics information</span></span>

<span data-ttu-id="18505-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="18505-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="18505-105">Tento článek popisuje, jak získat všechny analytické informace o předplatném pro vaše zákazníky.</span><span class="sxs-lookup"><span data-stu-id="18505-105">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18505-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="18505-106">Prerequisites</span></span>

- <span data-ttu-id="18505-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="18505-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="18505-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů uživatele.</span><span class="sxs-lookup"><span data-stu-id="18505-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="18505-109">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="18505-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="18505-110">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="18505-110">Request syntax</span></span>

| <span data-ttu-id="18505-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="18505-111">Method</span></span> | <span data-ttu-id="18505-112">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="18505-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="18505-113">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="18505-113">**GET**</span></span> | <span data-ttu-id="18505-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="18505-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="18505-115">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="18505-115">URI parameters</span></span>

<span data-ttu-id="18505-116">Následující tabulka uvádí volitelné parametry a jejich popisy:</span><span class="sxs-lookup"><span data-stu-id="18505-116">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="18505-117">Parametr</span><span class="sxs-lookup"><span data-stu-id="18505-117">Parameter</span></span> | <span data-ttu-id="18505-118">Typ</span><span class="sxs-lookup"><span data-stu-id="18505-118">Type</span></span> |  <span data-ttu-id="18505-119">Description</span><span class="sxs-lookup"><span data-stu-id="18505-119">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="18505-120">top</span><span class="sxs-lookup"><span data-stu-id="18505-120">top</span></span> | <span data-ttu-id="18505-121">int</span><span class="sxs-lookup"><span data-stu-id="18505-121">int</span></span> | <span data-ttu-id="18505-122">Počet řádků dat, které se v požadavku vrátí.</span><span class="sxs-lookup"><span data-stu-id="18505-122">The number of rows of data to return in the request.</span></span> <span data-ttu-id="18505-123">Pokud hodnota není zadaná, maximální a výchozí hodnota jsou `10000` .</span><span class="sxs-lookup"><span data-stu-id="18505-123">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="18505-124">Pokud dotaz obsahuje více řádků, obsahuje text odpovědi další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="18505-124">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="18505-125">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="18505-125">skip</span></span> | <span data-ttu-id="18505-126">int</span><span class="sxs-lookup"><span data-stu-id="18505-126">int</span></span> | <span data-ttu-id="18505-127">Počet řádků, které se v dotazu přeskočí</span><span class="sxs-lookup"><span data-stu-id="18505-127">The number of rows to skip in the query.</span></span> <span data-ttu-id="18505-128">Tento parametr použijte k stránkování velkých datových sad.</span><span class="sxs-lookup"><span data-stu-id="18505-128">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="18505-129">Například a načte prvních 10 000 řádků dat a načte dalších `top=10000` `skip=0` `top=10000` `skip=10000` 1 0000 řádků dat.</span><span class="sxs-lookup"><span data-stu-id="18505-129">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="18505-130">filter</span><span class="sxs-lookup"><span data-stu-id="18505-130">filter</span></span> | <span data-ttu-id="18505-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="18505-131">string</span></span> | <span data-ttu-id="18505-132">Jeden nebo více příkazů, které filtruje řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="18505-132">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="18505-133">Každý příkaz filtru obsahuje název pole z textu odpovědi a hodnotu přidruženou k operátoru , nebo pro **`eq`** **`ne`** určitá **`contains`** pole.</span><span class="sxs-lookup"><span data-stu-id="18505-133">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="18505-134">Příkazy lze kombinovat pomocí **`and`** nebo **`or`** .</span><span class="sxs-lookup"><span data-stu-id="18505-134">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="18505-135">Řetězcové hodnoty musí být v parametru filtru v jednoduchých **uvozovkách.**</span><span class="sxs-lookup"><span data-stu-id="18505-135">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="18505-136">V následující části najdete seznam polí, která lze filtrovat, a operátory, které jsou u těchto polí podporovány.</span><span class="sxs-lookup"><span data-stu-id="18505-136">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="18505-137">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="18505-137">aggregationLevel</span></span> | <span data-ttu-id="18505-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="18505-138">string</span></span> | <span data-ttu-id="18505-139">Určuje časový rozsah, pro který se mají načíst agregovaná data.</span><span class="sxs-lookup"><span data-stu-id="18505-139">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="18505-140">Může to být jeden z následujících řetězců: **den,** **týden** nebo **měsíc**.</span><span class="sxs-lookup"><span data-stu-id="18505-140">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="18505-141">Pokud hodnota není zadaná, výchozí hodnota je **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="18505-141">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="18505-142">Tento parametr platí pouze v případě, že je pole data předáno jako součást **parametru groupBy.**</span><span class="sxs-lookup"><span data-stu-id="18505-142">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="18505-143">Groupby</span><span class="sxs-lookup"><span data-stu-id="18505-143">groupBy</span></span> | <span data-ttu-id="18505-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="18505-144">string</span></span> | <span data-ttu-id="18505-145">Příkaz, který použije agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="18505-145">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="18505-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="18505-146">Request headers</span></span>

<span data-ttu-id="18505-147">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="18505-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="18505-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="18505-148">Request body</span></span>

<span data-ttu-id="18505-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="18505-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="18505-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="18505-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="18505-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="18505-151">REST response</span></span>

<span data-ttu-id="18505-152">V případě úspěchu bude text odpovědi obsahovat kolekci prostředků [**předplatného.**](partner-center-analytics-resources.md#subscription-resource)</span><span class="sxs-lookup"><span data-stu-id="18505-152">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="18505-153">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="18505-153">Response success and error codes</span></span>

<span data-ttu-id="18505-154">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="18505-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="18505-155">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="18505-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="18505-156">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="18505-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="18505-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="18505-157">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="18505-158">Viz také</span><span class="sxs-lookup"><span data-stu-id="18505-158">See also</span></span>

- [<span data-ttu-id="18505-159">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="18505-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
