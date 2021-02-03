---
title: Získání seznamu nabídek pro trh
description: Získá kolekci, která obsahuje všechny nabídky pro určitý trh.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 3a004f6f8f8de8cd398d82c300793e4f196efaaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766787"
---
# <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="45276-103">Získání seznamu nabídek pro trh</span><span class="sxs-lookup"><span data-stu-id="45276-103">Get a list of offers for a market</span></span>

<span data-ttu-id="45276-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="45276-104">**Applies To**</span></span>

- <span data-ttu-id="45276-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="45276-105">Partner Center</span></span>
- <span data-ttu-id="45276-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="45276-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="45276-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="45276-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="45276-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="45276-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="45276-109">Získá kolekci, která obsahuje všechny nabídky pro určitý trh.</span><span class="sxs-lookup"><span data-stu-id="45276-109">Gets a collection that contains all the offers for a specific market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45276-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="45276-110">Prerequisites</span></span>

- <span data-ttu-id="45276-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="45276-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="45276-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="45276-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="45276-113">C\#</span><span class="sxs-lookup"><span data-stu-id="45276-113">C\#</span></span>

<span data-ttu-id="45276-114">Pokud chcete získat seznam nabídek na daném trhu, použijte svou kolekci **IAggregatePartner. nabídky** , vyberte trh podle země a zavolejte metodu **Get ()** nebo **Get Async ()** .</span><span class="sxs-lookup"><span data-stu-id="45276-114">To get a list of offers in a given market, use your **IAggregatePartner.Offers** collection, select the market by country, and call the **Get()** or **Get Async()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<Offer> offers = partnerOperations.Offers.ByCountry("US").Get();
```

<span data-ttu-id="45276-115">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="45276-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="45276-116">**Projekt**: PartnerSDK. FeatureSample **Třída**: offers.cs</span><span class="sxs-lookup"><span data-stu-id="45276-116">**Project**: PartnerSDK.FeatureSample **Class**: Offers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="45276-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="45276-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="45276-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="45276-118">Request syntax</span></span>

| <span data-ttu-id="45276-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="45276-119">Method</span></span>  | <span data-ttu-id="45276-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="45276-120">Request URI</span></span>                                                                          |
|---------|--------------------------------------------------------------------------------------|
| <span data-ttu-id="45276-121">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="45276-121">**GET**</span></span> | <span data-ttu-id="45276-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers? Country = {Country-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="45276-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country-id} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="45276-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="45276-123">URI parameter</span></span>

<span data-ttu-id="45276-124">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání nabídek.</span><span class="sxs-lookup"><span data-stu-id="45276-124">This table lists the required query parameters to get the offers.</span></span>

| <span data-ttu-id="45276-125">Název</span><span class="sxs-lookup"><span data-stu-id="45276-125">Name</span></span>           | <span data-ttu-id="45276-126">Typ</span><span class="sxs-lookup"><span data-stu-id="45276-126">Type</span></span>       | <span data-ttu-id="45276-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="45276-127">Required</span></span> | <span data-ttu-id="45276-128">Popis</span><span class="sxs-lookup"><span data-stu-id="45276-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="45276-129">**ID země**</span><span class="sxs-lookup"><span data-stu-id="45276-129">**country-id**</span></span> | <span data-ttu-id="45276-130">**řetezce**</span><span class="sxs-lookup"><span data-stu-id="45276-130">**string**</span></span> | <span data-ttu-id="45276-131">Y</span><span class="sxs-lookup"><span data-stu-id="45276-131">Y</span></span>        | <span data-ttu-id="45276-132">ID země nebo oblasti</span><span class="sxs-lookup"><span data-stu-id="45276-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="45276-133">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="45276-133">Request headers</span></span>

- <span data-ttu-id="45276-134">Je vyžadováno **ID národního prostředí** naformátovaného jako řetězec.</span><span class="sxs-lookup"><span data-stu-id="45276-134">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="45276-135">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="45276-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="45276-136">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="45276-136">Request body</span></span>

<span data-ttu-id="45276-137">Žádné</span><span class="sxs-lookup"><span data-stu-id="45276-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="45276-138">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="45276-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers?country=<country-id> HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
```

## <a name="rest-response"></a><span data-ttu-id="45276-139">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="45276-139">REST response</span></span>

<span data-ttu-id="45276-140">V případě úspěchu tato metoda vrátí kolekci prostředků **nabídky** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="45276-140">If successful, this method returns a collection of **Offer** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="45276-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="45276-141">Response success and error codes</span></span>

<span data-ttu-id="45276-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="45276-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="45276-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="45276-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="45276-144">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="45276-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="45276-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="45276-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 26584
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
Date: Mon, 23 Nov 2015 23:20:44 GMT

{
    "totalCount":12,"items":[{
        "id":"E60E0348-1710-484B-992A-32B294D4CDE1",
        "name":"Azure Rights Management Premium (Government Pricing)",
        "description":"Microsoft Azure Rights Management Premium helps you protect confidential documents and email with strong encryption.
                       Control the use of your information by specifying who can view, edit, print, save and share your data.
                       Simple to use and integrated with Microsoft Office, SharePoint and Exchange.",
        "minimumQuantity":1,
        "maximumQuantity":10000000,
        "rank":5,
        "uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/E60E0348-1710-484B-992A-32B294D4CDE1",
        "locale":"EN-US",
        "country":"US",
        "category":{
            "id":"Government_Key",
            "name":"Government",
            "rank":40,
            "locale":"en-us",
            "country":"US",
            "attributes":{
                "objectType":"OfferCategory"
            }
        },
        "prerequisiteOffers":[],
        "isAddOn":false,
        "isAvailableForPurchase":true,
        "billing":"license",
        "isAutoRenewable":true,
        "product":{
            "id":"c52ea49f-fe5d-4e95-93ba-1de91d380f89",
            "name":"Azure Rights Management Premium",
            "unit":"Licenses"
        },
        "unitType":"Licenses",
        "links":{
            "learnMore":{
                "uri":"http://g.microsoftonline.com/0BXPS00en/0000",
                "method":"GET",
                "headers":[]
            },
            "self":{
                "uri":"/offers/E60E0348-1710-484B-992A-32B294D4CDE1",
                "method":"GET",
                "headers":[]
            }
        },
        "attributes":{
            "objectType":"Offer"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        },
        "previous":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
