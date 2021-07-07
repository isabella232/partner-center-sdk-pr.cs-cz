---
title: Získání všech analytických informací o referencích
description: Jak získat analytické informace o všech referenčních odkazech
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 7deda4098ceb9eb4e1ee75056c53c754618bf3e2
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760602"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="dbc3e-103">Získání všech analytických informací o referencích</span><span class="sxs-lookup"><span data-stu-id="dbc3e-103">Get all referrals analytics information</span></span>

<span data-ttu-id="dbc3e-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="dbc3e-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="dbc3e-105">Jak získat analytické informace o všech referenčních odkazech pro vaše zákazníky.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-105">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbc3e-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="dbc3e-106">Prerequisites</span></span>

- <span data-ttu-id="dbc3e-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="dbc3e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dbc3e-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů uživatele.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="dbc3e-109">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="dbc3e-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dbc3e-110">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="dbc3e-110">Request syntax</span></span>

| <span data-ttu-id="dbc3e-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="dbc3e-111">Method</span></span>  | <span data-ttu-id="dbc3e-112">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="dbc3e-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="dbc3e-113">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="dbc3e-113">**GET**</span></span> | <span data-ttu-id="dbc3e-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="dbc3e-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="dbc3e-115">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="dbc3e-115">URI parameters</span></span>

| <span data-ttu-id="dbc3e-116">Parametr</span><span class="sxs-lookup"><span data-stu-id="dbc3e-116">Parameter</span></span> | <span data-ttu-id="dbc3e-117">Typ</span><span class="sxs-lookup"><span data-stu-id="dbc3e-117">Type</span></span> | <span data-ttu-id="dbc3e-118">Description</span><span class="sxs-lookup"><span data-stu-id="dbc3e-118">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="dbc3e-119">filter</span><span class="sxs-lookup"><span data-stu-id="dbc3e-119">filter</span></span> | <span data-ttu-id="dbc3e-120">řetězec</span><span class="sxs-lookup"><span data-stu-id="dbc3e-120">string</span></span> | <span data-ttu-id="dbc3e-121">Vrátí data odpovídající pod podmínkě filtru.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-121">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="dbc3e-122">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="dbc3e-122">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="dbc3e-123">Groupby</span><span class="sxs-lookup"><span data-stu-id="dbc3e-123">groupby</span></span> | <span data-ttu-id="dbc3e-124">řetězec</span><span class="sxs-lookup"><span data-stu-id="dbc3e-124">string</span></span> | <span data-ttu-id="dbc3e-125">Podporuje termíny i kalendářní data.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-125">Supports both terms and dates.</span></span> <span data-ttu-id="dbc3e-126">Logika krátkého okruhu pro omezení počtu kbelíků</span><span class="sxs-lookup"><span data-stu-id="dbc3e-126">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="dbc3e-127">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="dbc3e-127">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="dbc3e-128">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="dbc3e-128">aggregationLevel</span></span> | <span data-ttu-id="dbc3e-129">řetězec</span><span class="sxs-lookup"><span data-stu-id="dbc3e-129">string</span></span> | <span data-ttu-id="dbc3e-130">Parametr *aggregationLevel* vyžaduje *parametr groupby*.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="dbc3e-131">Parametr *aggregationLevel* se vztahuje na všechna pole data, která jsou v *groupby*.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="dbc3e-132">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="dbc3e-132">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="dbc3e-133">top</span><span class="sxs-lookup"><span data-stu-id="dbc3e-133">top</span></span> | <span data-ttu-id="dbc3e-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="dbc3e-134">string</span></span> | <span data-ttu-id="dbc3e-135">Limit stránky je 10 000.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-135">The page limit is 10000.</span></span> <span data-ttu-id="dbc3e-136">Přebírá libovolnou hodnotu menší než 1 0000.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-136">Takes any value less than 10000.</span></span></br> <span data-ttu-id="dbc3e-137">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="dbc3e-137">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="dbc3e-138">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="dbc3e-138">skip</span></span> | <span data-ttu-id="dbc3e-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="dbc3e-139">string</span></span> | <span data-ttu-id="dbc3e-140">Počet řádků k přeskočení</span><span class="sxs-lookup"><span data-stu-id="dbc3e-140">Number of rows to skip.</span></span></br> <span data-ttu-id="dbc3e-141">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="dbc3e-141">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="dbc3e-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="dbc3e-142">Request headers</span></span>

<span data-ttu-id="dbc3e-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="dbc3e-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dbc3e-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="dbc3e-144">Request body</span></span>

<span data-ttu-id="dbc3e-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="dbc3e-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dbc3e-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="dbc3e-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="dbc3e-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="dbc3e-147">REST response</span></span>

<span data-ttu-id="dbc3e-148">V případě úspěchu bude text odpovědi obsahovat kolekci prostředků [referenčních](partner-center-analytics-resources.md#referrals-resource) seznamů.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-148">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dbc3e-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="dbc3e-149">Response success and error codes</span></span>

<span data-ttu-id="dbc3e-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dbc3e-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="dbc3e-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dbc3e-152">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="dbc3e-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dbc3e-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="dbc3e-153">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="dbc3e-154">Viz také</span><span class="sxs-lookup"><span data-stu-id="dbc3e-154">See also</span></span>

- [<span data-ttu-id="dbc3e-155">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="dbc3e-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
