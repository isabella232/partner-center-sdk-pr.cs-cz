---
title: Získání všech analytických informací o hledání
description: Jak získat všechny informace o analýze vyhledávání.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e789a013b01fb63a38c72f4fe94864ecf21f7e4b
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760160"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="f3a94-103">Získání všech analytických informací o hledání</span><span class="sxs-lookup"><span data-stu-id="f3a94-103">Get all search analytics information</span></span>

<span data-ttu-id="f3a94-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f3a94-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f3a94-105">Jak získat všechny informace o analýze vyhledávání pro vaše zákazníky.</span><span class="sxs-lookup"><span data-stu-id="f3a94-105">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3a94-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f3a94-106">Prerequisites</span></span>

- <span data-ttu-id="f3a94-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f3a94-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f3a94-108">Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.</span><span class="sxs-lookup"><span data-stu-id="f3a94-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="f3a94-109">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f3a94-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f3a94-110">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f3a94-110">Request syntax</span></span>

| <span data-ttu-id="f3a94-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="f3a94-111">Method</span></span>  | <span data-ttu-id="f3a94-112">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f3a94-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="f3a94-113">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="f3a94-113">**GET**</span></span> | <span data-ttu-id="f3a94-114">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Search HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f3a94-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="f3a94-115">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="f3a94-115">URI parameters</span></span>

|    <span data-ttu-id="f3a94-116">Parametr</span><span class="sxs-lookup"><span data-stu-id="f3a94-116">Parameter</span></span>     |  <span data-ttu-id="f3a94-117">Typ</span><span class="sxs-lookup"><span data-stu-id="f3a94-117">Type</span></span>  |                                                                                                                   <span data-ttu-id="f3a94-118">Description</span><span class="sxs-lookup"><span data-stu-id="f3a94-118">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="f3a94-119">filter</span><span class="sxs-lookup"><span data-stu-id="f3a94-119">filter</span></span>      | <span data-ttu-id="f3a94-120">řetězec</span><span class="sxs-lookup"><span data-stu-id="f3a94-120">string</span></span> |                                                                     <span data-ttu-id="f3a94-121">Vrátí data, která odpovídají podmínkám filtru.</span><span class="sxs-lookup"><span data-stu-id="f3a94-121">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="f3a94-122">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="f3a94-122">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="f3a94-123">GroupBy</span><span class="sxs-lookup"><span data-stu-id="f3a94-123">groupby</span></span>      | <span data-ttu-id="f3a94-124">řetězec</span><span class="sxs-lookup"><span data-stu-id="f3a94-124">string</span></span> |                                         <span data-ttu-id="f3a94-125">Podporuje termíny i data.</span><span class="sxs-lookup"><span data-stu-id="f3a94-125">Supports both terms and dates.</span></span> <span data-ttu-id="f3a94-126">Logika krátkého okruhu pro omezení počtu kontejnerů.</span><span class="sxs-lookup"><span data-stu-id="f3a94-126">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="f3a94-127">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="f3a94-127">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="f3a94-128">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="f3a94-128">aggregationLevel</span></span> | <span data-ttu-id="f3a94-129">řetězec</span><span class="sxs-lookup"><span data-stu-id="f3a94-129">string</span></span> | <span data-ttu-id="f3a94-130">Parametr *aggregationLevel* vyžaduje *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="f3a94-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="f3a94-131">Parametr *aggregationLevel* se vztahuje na všechna pole kalendářních dat přítomná v *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="f3a94-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="f3a94-132">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="f3a94-132">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="f3a94-133">top</span><span class="sxs-lookup"><span data-stu-id="f3a94-133">top</span></span>        | <span data-ttu-id="f3a94-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="f3a94-134">string</span></span> |                                                                     <span data-ttu-id="f3a94-135">Limit stránky je 10000.</span><span class="sxs-lookup"><span data-stu-id="f3a94-135">The page limit is 10000.</span></span> <span data-ttu-id="f3a94-136">Má libovolnou hodnotu menší než 10000.</span><span class="sxs-lookup"><span data-stu-id="f3a94-136">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="f3a94-137">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="f3a94-137">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="f3a94-138">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="f3a94-138">skip</span></span>       | <span data-ttu-id="f3a94-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="f3a94-139">string</span></span> |                                                                                  <span data-ttu-id="f3a94-140">Počet řádků, které se mají přeskočit</span><span class="sxs-lookup"><span data-stu-id="f3a94-140">Number of rows to skip.</span></span> </br> <span data-ttu-id="f3a94-141">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="f3a94-141">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="f3a94-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f3a94-142">Request headers</span></span>

<span data-ttu-id="f3a94-143">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f3a94-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f3a94-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f3a94-144">Request body</span></span>

<span data-ttu-id="f3a94-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="f3a94-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f3a94-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f3a94-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="f3a94-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f3a94-147">REST response</span></span>

<span data-ttu-id="f3a94-148">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [vyhledávání](partner-center-analytics-resources.md#search-resource) .</span><span class="sxs-lookup"><span data-stu-id="f3a94-148">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f3a94-149">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f3a94-149">Response success and error codes</span></span>

<span data-ttu-id="f3a94-150">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f3a94-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f3a94-151">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f3a94-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f3a94-152">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f3a94-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f3a94-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f3a94-153">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="f3a94-154">Viz také</span><span class="sxs-lookup"><span data-stu-id="f3a94-154">See also</span></span>

- [<span data-ttu-id="f3a94-155">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="f3a94-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
