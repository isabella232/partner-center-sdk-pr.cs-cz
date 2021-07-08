---
title: Získání seznamu nabídek pro trh
description: Získá kolekci, která obsahuje všechny nabídky pro určitý trh.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 6f4fd821879545db4e781fe3202c8ee11f167615
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874240"
---
# <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="b965b-103">Získání seznamu nabídek pro trh</span><span class="sxs-lookup"><span data-stu-id="b965b-103">Get a list of offers for a market</span></span>

<span data-ttu-id="b965b-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b965b-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b965b-105">Získá kolekci, která obsahuje všechny nabídky pro určitý trh.</span><span class="sxs-lookup"><span data-stu-id="b965b-105">Gets a collection that contains all the offers for a specific market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b965b-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b965b-106">Prerequisites</span></span>

- <span data-ttu-id="b965b-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b965b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b965b-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="b965b-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="b965b-109">C\#</span><span class="sxs-lookup"><span data-stu-id="b965b-109">C\#</span></span>

<span data-ttu-id="b965b-110">Pokud chcete získat seznam nabídek na daném trhu, použijte svou kolekci **IAggregatePartner. nabídky** , vyberte trh podle země a zavolejte metodu **Get ()** nebo **Get Async ()** .</span><span class="sxs-lookup"><span data-stu-id="b965b-110">To get a list of offers in a given market, use your **IAggregatePartner.Offers** collection, select the market by country, and call the **Get()** or **Get Async()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<Offer> offers = partnerOperations.Offers.ByCountry("US").Get();
```

<span data-ttu-id="b965b-111">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b965b-111">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b965b-112">**Project**: **třída** PartnerSDK. FeatureSample: nabídky. cs</span><span class="sxs-lookup"><span data-stu-id="b965b-112">**Project**: PartnerSDK.FeatureSample **Class**: Offers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b965b-113">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b965b-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b965b-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b965b-114">Request syntax</span></span>

| <span data-ttu-id="b965b-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="b965b-115">Method</span></span>  | <span data-ttu-id="b965b-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b965b-116">Request URI</span></span>                                                                          |
|---------|--------------------------------------------------------------------------------------|
| <span data-ttu-id="b965b-117">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b965b-117">**GET**</span></span> | <span data-ttu-id="b965b-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers? Country = {Country-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b965b-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country-id} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="b965b-119">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b965b-119">URI parameter</span></span>

<span data-ttu-id="b965b-120">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání nabídek.</span><span class="sxs-lookup"><span data-stu-id="b965b-120">This table lists the required query parameters to get the offers.</span></span>

| <span data-ttu-id="b965b-121">Název</span><span class="sxs-lookup"><span data-stu-id="b965b-121">Name</span></span>           | <span data-ttu-id="b965b-122">Typ</span><span class="sxs-lookup"><span data-stu-id="b965b-122">Type</span></span>       | <span data-ttu-id="b965b-123">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b965b-123">Required</span></span> | <span data-ttu-id="b965b-124">Popis</span><span class="sxs-lookup"><span data-stu-id="b965b-124">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="b965b-125">**ID země**</span><span class="sxs-lookup"><span data-stu-id="b965b-125">**country-id**</span></span> | <span data-ttu-id="b965b-126">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="b965b-126">**string**</span></span> | <span data-ttu-id="b965b-127">Y</span><span class="sxs-lookup"><span data-stu-id="b965b-127">Y</span></span>        | <span data-ttu-id="b965b-128">ID země nebo oblasti</span><span class="sxs-lookup"><span data-stu-id="b965b-128">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b965b-129">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b965b-129">Request headers</span></span>

- <span data-ttu-id="b965b-130">Je vyžadováno **ID národního prostředí** naformátovaného jako řetězec.</span><span class="sxs-lookup"><span data-stu-id="b965b-130">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="b965b-131">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b965b-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b965b-132">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b965b-132">Request body</span></span>

<span data-ttu-id="b965b-133">Žádné</span><span class="sxs-lookup"><span data-stu-id="b965b-133">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b965b-134">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b965b-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers?country=<country-id> HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
```

## <a name="rest-response"></a><span data-ttu-id="b965b-135">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b965b-135">REST response</span></span>

<span data-ttu-id="b965b-136">V případě úspěchu tato metoda vrátí kolekci prostředků **nabídky** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b965b-136">If successful, this method returns a collection of **Offer** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b965b-137">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b965b-137">Response success and error codes</span></span>

<span data-ttu-id="b965b-138">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b965b-138">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b965b-139">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b965b-139">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b965b-140">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b965b-140">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b965b-141">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b965b-141">Response example</span></span>

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
