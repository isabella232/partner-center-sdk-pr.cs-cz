---
title: Získání seznamu kategorií nabídek podle trhu
description: Naučte se, jak získat kolekci, která obsahuje všechny kategorie nabídek v dané zemi nebo oblasti a národním prostředí pro všechny cloudy Microsoftu.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 05aad095c6cb8eaee4cbf7ce976ca1b4b7a408c4
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500052"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="18c9f-103">Získání seznamu kategorií nabídek podle trhu</span><span class="sxs-lookup"><span data-stu-id="18c9f-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="18c9f-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="18c9f-104">**Applies to:**</span></span>

- <span data-ttu-id="18c9f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="18c9f-105">Partner Center</span></span>
- <span data-ttu-id="18c9f-106">Partnerské centrum provozované společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="18c9f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="18c9f-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="18c9f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="18c9f-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="18c9f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="18c9f-109">Tento článek popisuje, jak získat kolekci, která obsahuje všechny kategorie nabídek v dané zemi nebo oblasti a národním prostředí.</span><span class="sxs-lookup"><span data-stu-id="18c9f-109">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18c9f-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="18c9f-110">Prerequisites</span></span>

- <span data-ttu-id="18c9f-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="18c9f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="18c9f-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="18c9f-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="18c9f-113">C\#</span><span class="sxs-lookup"><span data-stu-id="18c9f-113">C\#</span></span>

<span data-ttu-id="18c9f-114">Postup získání seznamu kategorií nabídek v dané zemi nebo oblasti a národním prostředí:</span><span class="sxs-lookup"><span data-stu-id="18c9f-114">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="18c9f-115">K volání metody [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) v daném kontextu použijte kolekci [**IAggregatePartner. Operations.**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner)</span><span class="sxs-lookup"><span data-stu-id="18c9f-115">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="18c9f-116">Zkontrolujte vlastnost [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) výsledného objektu.</span><span class="sxs-lookup"><span data-stu-id="18c9f-116">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="18c9f-117">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="18c9f-117">For an example, see the following:</span></span>

- <span data-ttu-id="18c9f-118">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="18c9f-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="18c9f-119">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="18c9f-119">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="18c9f-120">Třída: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="18c9f-120">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="18c9f-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="18c9f-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="18c9f-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="18c9f-122">Request syntax</span></span>

| <span data-ttu-id="18c9f-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="18c9f-123">Method</span></span>  | <span data-ttu-id="18c9f-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="18c9f-124">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="18c9f-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="18c9f-125">**GET**</span></span> | <span data-ttu-id="18c9f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories? Country = {Country-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="18c9f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="18c9f-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="18c9f-127">URI parameter</span></span>

<span data-ttu-id="18c9f-128">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání kategorií nabídek.</span><span class="sxs-lookup"><span data-stu-id="18c9f-128">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="18c9f-129">Název</span><span class="sxs-lookup"><span data-stu-id="18c9f-129">Name</span></span>           | <span data-ttu-id="18c9f-130">Typ</span><span class="sxs-lookup"><span data-stu-id="18c9f-130">Type</span></span>       | <span data-ttu-id="18c9f-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="18c9f-131">Required</span></span> | <span data-ttu-id="18c9f-132">Popis</span><span class="sxs-lookup"><span data-stu-id="18c9f-132">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="18c9f-133">**ID země**</span><span class="sxs-lookup"><span data-stu-id="18c9f-133">**country-id**</span></span> | <span data-ttu-id="18c9f-134">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="18c9f-134">**string**</span></span> | <span data-ttu-id="18c9f-135">Y</span><span class="sxs-lookup"><span data-stu-id="18c9f-135">Y</span></span>        | <span data-ttu-id="18c9f-136">ID země nebo oblasti</span><span class="sxs-lookup"><span data-stu-id="18c9f-136">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="18c9f-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="18c9f-137">Request headers</span></span>

<span data-ttu-id="18c9f-138">Je vyžadováno **ID národního prostředí** naformátovaného jako řetězec.</span><span class="sxs-lookup"><span data-stu-id="18c9f-138">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="18c9f-139">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="18c9f-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="18c9f-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="18c9f-140">Request body</span></span>

<span data-ttu-id="18c9f-141">Žádné</span><span class="sxs-lookup"><span data-stu-id="18c9f-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="18c9f-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="18c9f-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="18c9f-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="18c9f-143">REST response</span></span>

<span data-ttu-id="18c9f-144">V případě úspěchu tato metoda vrátí kolekci prostředků **OfferCategory** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="18c9f-144">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="18c9f-145">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="18c9f-145">Response success and error codes</span></span>

<span data-ttu-id="18c9f-146">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="18c9f-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="18c9f-147">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="18c9f-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="18c9f-148">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="18c9f-148">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="18c9f-149">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="18c9f-149">Response example</span></span>

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
