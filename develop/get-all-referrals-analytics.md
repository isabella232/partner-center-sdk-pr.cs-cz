---
title: Získání všech analytických informací o referencích
description: Jak získat všechny analytické informace o odkazech.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766778"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="ed82f-103">Získání všech analytických informací o referencích</span><span class="sxs-lookup"><span data-stu-id="ed82f-103">Get all referrals analytics information</span></span>

<span data-ttu-id="ed82f-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="ed82f-104">**Applies To**</span></span>

- <span data-ttu-id="ed82f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="ed82f-105">Partner Center</span></span>
- <span data-ttu-id="ed82f-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="ed82f-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ed82f-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ed82f-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ed82f-108">Jak získat všechny informace o analýze odkazů pro vaše zákazníky.</span><span class="sxs-lookup"><span data-stu-id="ed82f-108">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed82f-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ed82f-109">Prerequisites</span></span>

- <span data-ttu-id="ed82f-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ed82f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ed82f-111">Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.</span><span class="sxs-lookup"><span data-stu-id="ed82f-111">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ed82f-112">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ed82f-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ed82f-113">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ed82f-113">Request syntax</span></span>

| <span data-ttu-id="ed82f-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="ed82f-114">Method</span></span>  | <span data-ttu-id="ed82f-115">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ed82f-115">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="ed82f-116">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="ed82f-116">**GET**</span></span> | <span data-ttu-id="ed82f-117">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Referrals HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ed82f-117">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="ed82f-118">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="ed82f-118">URI parameters</span></span>

| <span data-ttu-id="ed82f-119">Parametr</span><span class="sxs-lookup"><span data-stu-id="ed82f-119">Parameter</span></span> | <span data-ttu-id="ed82f-120">Typ</span><span class="sxs-lookup"><span data-stu-id="ed82f-120">Type</span></span> | <span data-ttu-id="ed82f-121">Description</span><span class="sxs-lookup"><span data-stu-id="ed82f-121">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="ed82f-122">filter</span><span class="sxs-lookup"><span data-stu-id="ed82f-122">filter</span></span> | <span data-ttu-id="ed82f-123">řetězec</span><span class="sxs-lookup"><span data-stu-id="ed82f-123">string</span></span> | <span data-ttu-id="ed82f-124">Vrátí data, která odpovídají podmínkám filtru.</span><span class="sxs-lookup"><span data-stu-id="ed82f-124">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="ed82f-125">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="ed82f-125">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="ed82f-126">GroupBy</span><span class="sxs-lookup"><span data-stu-id="ed82f-126">groupby</span></span> | <span data-ttu-id="ed82f-127">řetězec</span><span class="sxs-lookup"><span data-stu-id="ed82f-127">string</span></span> | <span data-ttu-id="ed82f-128">Podporuje termíny i data.</span><span class="sxs-lookup"><span data-stu-id="ed82f-128">Supports both terms and dates.</span></span> <span data-ttu-id="ed82f-129">Logika krátkého okruhu pro omezení počtu kontejnerů.</span><span class="sxs-lookup"><span data-stu-id="ed82f-129">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="ed82f-130">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="ed82f-130">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="ed82f-131">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="ed82f-131">aggregationLevel</span></span> | <span data-ttu-id="ed82f-132">řetězec</span><span class="sxs-lookup"><span data-stu-id="ed82f-132">string</span></span> | <span data-ttu-id="ed82f-133">Parametr *aggregationLevel* vyžaduje *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="ed82f-133">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="ed82f-134">Parametr *aggregationLevel* se vztahuje na všechna pole kalendářních dat přítomná v *GroupBy*.</span><span class="sxs-lookup"><span data-stu-id="ed82f-134">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="ed82f-135">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="ed82f-135">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="ed82f-136">top</span><span class="sxs-lookup"><span data-stu-id="ed82f-136">top</span></span> | <span data-ttu-id="ed82f-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="ed82f-137">string</span></span> | <span data-ttu-id="ed82f-138">Limit stránky je 10000.</span><span class="sxs-lookup"><span data-stu-id="ed82f-138">The page limit is 10000.</span></span> <span data-ttu-id="ed82f-139">Má libovolnou hodnotu menší než 10000.</span><span class="sxs-lookup"><span data-stu-id="ed82f-139">Takes any value less than 10000.</span></span></br> <span data-ttu-id="ed82f-140">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="ed82f-140">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="ed82f-141">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="ed82f-141">skip</span></span> | <span data-ttu-id="ed82f-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="ed82f-142">string</span></span> | <span data-ttu-id="ed82f-143">Počet řádků, které se mají přeskočit</span><span class="sxs-lookup"><span data-stu-id="ed82f-143">Number of rows to skip.</span></span></br> <span data-ttu-id="ed82f-144">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="ed82f-144">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="ed82f-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ed82f-145">Request headers</span></span>

<span data-ttu-id="ed82f-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ed82f-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ed82f-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ed82f-147">Request body</span></span>

<span data-ttu-id="ed82f-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="ed82f-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ed82f-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ed82f-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="ed82f-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ed82f-150">REST response</span></span>

<span data-ttu-id="ed82f-151">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [odkazů](partner-center-analytics-resources.md#referrals-resource) .</span><span class="sxs-lookup"><span data-stu-id="ed82f-151">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ed82f-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ed82f-152">Response success and error codes</span></span>

<span data-ttu-id="ed82f-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ed82f-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ed82f-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ed82f-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ed82f-155">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ed82f-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ed82f-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ed82f-156">Response example</span></span>

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a><span data-ttu-id="ed82f-157">Viz také</span><span class="sxs-lookup"><span data-stu-id="ed82f-157">See also</span></span>

- [<span data-ttu-id="ed82f-158">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="ed82f-158">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
