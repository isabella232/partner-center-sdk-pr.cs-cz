---
title: Získání seznamu kategorií nabídek podle trhu
description: Zjistěte, jak získat kolekci, která obsahuje všechny kategorie nabídek v dané zemi/oblasti a národní prostředí pro všechny cloudy Microsoftu.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e699355f07dda3941eafed32f5f635d94000abd1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874274"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="e1f43-103">Získání seznamu kategorií nabídek podle trhu</span><span class="sxs-lookup"><span data-stu-id="e1f43-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="e1f43-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e1f43-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e1f43-105">Tento článek popisuje, jak získat kolekci, která obsahuje všechny kategorie nabídek v dané zemi/oblasti a národní prostředí.</span><span class="sxs-lookup"><span data-stu-id="e1f43-105">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1f43-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e1f43-106">Prerequisites</span></span>

- <span data-ttu-id="e1f43-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e1f43-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e1f43-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="e1f43-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e1f43-109">C\#</span><span class="sxs-lookup"><span data-stu-id="e1f43-109">C\#</span></span>

<span data-ttu-id="e1f43-110">Získání seznamu kategorií nabídek v dané zemi/oblasti a národního prostředí:</span><span class="sxs-lookup"><span data-stu-id="e1f43-110">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="e1f43-111">Pomocí kolekce [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) zavolejte metodu [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) pro daný kontext.</span><span class="sxs-lookup"><span data-stu-id="e1f43-111">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="e1f43-112">Zkontrolujte vlastnost [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) výsledného objektu.</span><span class="sxs-lookup"><span data-stu-id="e1f43-112">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="e1f43-113">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="e1f43-113">For an example, see the following:</span></span>

- <span data-ttu-id="e1f43-114">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e1f43-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e1f43-115">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="e1f43-115">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="e1f43-116">Třída: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="e1f43-116">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e1f43-117">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="e1f43-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e1f43-118">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="e1f43-118">Request syntax</span></span>

| <span data-ttu-id="e1f43-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="e1f43-119">Method</span></span>  | <span data-ttu-id="e1f43-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e1f43-120">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="e1f43-121">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="e1f43-121">**GET**</span></span> | <span data-ttu-id="e1f43-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e1f43-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e1f43-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e1f43-123">URI parameter</span></span>

<span data-ttu-id="e1f43-124">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání kategorií nabídek.</span><span class="sxs-lookup"><span data-stu-id="e1f43-124">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="e1f43-125">Název</span><span class="sxs-lookup"><span data-stu-id="e1f43-125">Name</span></span>           | <span data-ttu-id="e1f43-126">Typ</span><span class="sxs-lookup"><span data-stu-id="e1f43-126">Type</span></span>       | <span data-ttu-id="e1f43-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e1f43-127">Required</span></span> | <span data-ttu-id="e1f43-128">Popis</span><span class="sxs-lookup"><span data-stu-id="e1f43-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="e1f43-129">**country-id**</span><span class="sxs-lookup"><span data-stu-id="e1f43-129">**country-id**</span></span> | <span data-ttu-id="e1f43-130">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="e1f43-130">**string**</span></span> | <span data-ttu-id="e1f43-131">Y</span><span class="sxs-lookup"><span data-stu-id="e1f43-131">Y</span></span>        | <span data-ttu-id="e1f43-132">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="e1f43-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e1f43-133">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e1f43-133">Request headers</span></span>

<span data-ttu-id="e1f43-134">Vyžaduje **se ID národního** prostředí formátované jako řetězec.</span><span class="sxs-lookup"><span data-stu-id="e1f43-134">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="e1f43-135">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e1f43-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e1f43-136">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e1f43-136">Request body</span></span>

<span data-ttu-id="e1f43-137">Žádné</span><span class="sxs-lookup"><span data-stu-id="e1f43-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e1f43-138">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e1f43-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e1f43-139">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e1f43-139">REST response</span></span>

<span data-ttu-id="e1f43-140">V případě úspěchu tato metoda vrátí kolekci **prostředků OfferCategory** v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e1f43-140">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e1f43-141">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="e1f43-141">Response success and error codes</span></span>

<span data-ttu-id="e1f43-142">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e1f43-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e1f43-143">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="e1f43-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e1f43-144">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e1f43-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e1f43-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e1f43-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
