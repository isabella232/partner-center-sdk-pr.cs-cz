---
title: Získání všech analytických informací o hledání
description: Jak získat všechny informace o analýze vyhledávání.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766670"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="3696a-103">Získání všech analytických informací o hledání</span><span class="sxs-lookup"><span data-stu-id="3696a-103">Get all search analytics information</span></span>

<span data-ttu-id="3696a-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="3696a-104">**Applies To**</span></span>

- <span data-ttu-id="3696a-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="3696a-105">Partner Center</span></span>
- <span data-ttu-id="3696a-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="3696a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3696a-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="3696a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3696a-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3696a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3696a-109">Jak získat všechny informace o analýze vyhledávání pro vaše zákazníky.</span><span class="sxs-lookup"><span data-stu-id="3696a-109">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3696a-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3696a-110">Prerequisites</span></span>

- <span data-ttu-id="3696a-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3696a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3696a-112">Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.</span><span class="sxs-lookup"><span data-stu-id="3696a-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3696a-113">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="3696a-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3696a-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="3696a-114">Request syntax</span></span>

| <span data-ttu-id="3696a-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="3696a-115">Method</span></span>  | <span data-ttu-id="3696a-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3696a-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="3696a-117">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="3696a-117">**GET**</span></span> | <span data-ttu-id="3696a-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Search HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3696a-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3696a-119">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="3696a-119">URI parameters</span></span>

|    <span data-ttu-id="3696a-120">Parametr</span><span class="sxs-lookup"><span data-stu-id="3696a-120">Parameter</span></span>     |  <span data-ttu-id="3696a-121">Typ</span><span class="sxs-lookup"><span data-stu-id="3696a-121">Type</span></span>  |                                                                                                                   <span data-ttu-id="3696a-122">Description</span><span class="sxs-lookup"><span data-stu-id="3696a-122">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="3696a-123">filter</span><span class="sxs-lookup"><span data-stu-id="3696a-123">filter</span></span>      | <span data-ttu-id="3696a-124">řetězec</span><span class="sxs-lookup"><span data-stu-id="3696a-124">string</span></span> |                                                                     <span data-ttu-id="3696a-125">Vrátí data, která odpovídají podmínkám filtru.</span><span class="sxs-lookup"><span data-stu-id="3696a-125">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="3696a-126">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="3696a-126">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="3696a-127">GroupBy</span><span class="sxs-lookup"><span data-stu-id="3696a-127">groupby</span></span>      | <span data-ttu-id="3696a-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="3696a-128">string</span></span> |                                         <span data-ttu-id="3696a-129">Podporuje termíny i data.</span><span class="sxs-lookup"><span data-stu-id="3696a-129">Supports both terms and dates.</span></span> <span data-ttu-id="3696a-130">Logika krátkého okruhu pro omezení počtu kontejnerů.</span><span class="sxs-lookup"><span data-stu-id="3696a-130">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="3696a-131">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="3696a-131">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="3696a-132">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="3696a-132">aggregationLevel</span></span> | <span data-ttu-id="3696a-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="3696a-133">string</span></span> | <span data-ttu-id="3696a-134">Parametr *aggregationLevel* vyžaduje *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="3696a-134">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="3696a-135">Parametr *aggregationLevel* se vztahuje na všechna pole kalendářních dat přítomná v *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="3696a-135">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="3696a-136">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="3696a-136">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="3696a-137">top</span><span class="sxs-lookup"><span data-stu-id="3696a-137">top</span></span>        | <span data-ttu-id="3696a-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="3696a-138">string</span></span> |                                                                     <span data-ttu-id="3696a-139">Limit stránky je 10000.</span><span class="sxs-lookup"><span data-stu-id="3696a-139">The page limit is 10000.</span></span> <span data-ttu-id="3696a-140">Má libovolnou hodnotu menší než 10000.</span><span class="sxs-lookup"><span data-stu-id="3696a-140">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="3696a-141">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="3696a-141">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="3696a-142">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="3696a-142">skip</span></span>       | <span data-ttu-id="3696a-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="3696a-143">string</span></span> |                                                                                  <span data-ttu-id="3696a-144">Počet řádků, které se mají přeskočit</span><span class="sxs-lookup"><span data-stu-id="3696a-144">Number of rows to skip.</span></span> </br> <span data-ttu-id="3696a-145">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="3696a-145">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="3696a-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="3696a-146">Request headers</span></span>

<span data-ttu-id="3696a-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3696a-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3696a-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="3696a-148">Request body</span></span>

<span data-ttu-id="3696a-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="3696a-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3696a-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="3696a-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="3696a-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3696a-151">REST response</span></span>

<span data-ttu-id="3696a-152">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [vyhledávání](partner-center-analytics-resources.md#search-resource) .</span><span class="sxs-lookup"><span data-stu-id="3696a-152">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3696a-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="3696a-153">Response success and error codes</span></span>

<span data-ttu-id="3696a-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="3696a-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3696a-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="3696a-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3696a-156">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3696a-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3696a-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="3696a-157">Response example</span></span>

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a><span data-ttu-id="3696a-158">Viz také</span><span class="sxs-lookup"><span data-stu-id="3696a-158">See also</span></span>

- [<span data-ttu-id="3696a-159">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="3696a-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
