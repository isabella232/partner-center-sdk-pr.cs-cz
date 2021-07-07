---
title: Získání nabídky podle ID
description: Získá prostředek nabídky, který odpovídá ID nabídky.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: f759cbdeefb4f550c41b41de40e9979e72e4ddeb
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760636"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="20dd0-103">Získání nabídky podle ID</span><span class="sxs-lookup"><span data-stu-id="20dd0-103">Get an offer by ID</span></span>

<span data-ttu-id="20dd0-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="20dd0-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="20dd0-105">Získá prostředek **nabídky** , který odpovídá ID nabídky.</span><span class="sxs-lookup"><span data-stu-id="20dd0-105">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20dd0-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="20dd0-106">Prerequisites</span></span>

- <span data-ttu-id="20dd0-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="20dd0-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="20dd0-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="20dd0-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="20dd0-109">ID nabídky</span><span class="sxs-lookup"><span data-stu-id="20dd0-109">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="20dd0-110">C\#</span><span class="sxs-lookup"><span data-stu-id="20dd0-110">C\#</span></span>

<span data-ttu-id="20dd0-111">Chcete-li najít konkrétní nabídku podle ID, použijte svou kolekci **IAggregatePartner.** offers, vytvořte zemi se voláním **ByCountry ()** a poté zavolejte metodu [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="20dd0-111">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="20dd0-112">Pak zavolejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) nebo [**Get Async ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="20dd0-112">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="20dd0-113">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="20dd0-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="20dd0-114">**Project**: PartnerSDK. FeatureSample **třída**: getoffer. cs</span><span class="sxs-lookup"><span data-stu-id="20dd0-114">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="20dd0-115">Java</span><span class="sxs-lookup"><span data-stu-id="20dd0-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="20dd0-116">Chcete-li najít konkrétní nabídku podle ID, použijte funkci **IAggregatePartner. res** , stanovte zemi voláním funkce **byCountry ()** a potom zavolejte funkci **byID ()** .</span><span class="sxs-lookup"><span data-stu-id="20dd0-116">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="20dd0-117">Pak zavolejte funkci **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="20dd0-117">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="20dd0-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20dd0-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="20dd0-119">Chcete-li najít konkrétní nabídku podle ID, spusťte příkaz [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) a zadejte parametry **CountryCode** a **hodnotami OfferId** .</span><span class="sxs-lookup"><span data-stu-id="20dd0-119">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="20dd0-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="20dd0-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="20dd0-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="20dd0-121">Request syntax</span></span>

| <span data-ttu-id="20dd0-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="20dd0-122">Method</span></span>  | <span data-ttu-id="20dd0-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="20dd0-123">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="20dd0-124">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="20dd0-124">**GET**</span></span> | <span data-ttu-id="20dd0-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{Offer-ID}? Country = {Country-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="20dd0-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="20dd0-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="20dd0-126">URI parameter</span></span>

| <span data-ttu-id="20dd0-127">Název</span><span class="sxs-lookup"><span data-stu-id="20dd0-127">Name</span></span>           | <span data-ttu-id="20dd0-128">Typ</span><span class="sxs-lookup"><span data-stu-id="20dd0-128">Type</span></span>       | <span data-ttu-id="20dd0-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="20dd0-129">Required</span></span> | <span data-ttu-id="20dd0-130">Popis</span><span class="sxs-lookup"><span data-stu-id="20dd0-130">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="20dd0-131">**ID nabídky**</span><span class="sxs-lookup"><span data-stu-id="20dd0-131">**offer-id**</span></span>   | <span data-ttu-id="20dd0-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="20dd0-132">**guid**</span></span>   | <span data-ttu-id="20dd0-133">Y</span><span class="sxs-lookup"><span data-stu-id="20dd0-133">Y</span></span>        | <span data-ttu-id="20dd0-134">Identifikátor GUID, který odpovídá této nabídce</span><span class="sxs-lookup"><span data-stu-id="20dd0-134">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="20dd0-135">**ID země**</span><span class="sxs-lookup"><span data-stu-id="20dd0-135">**country-id**</span></span> | <span data-ttu-id="20dd0-136">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="20dd0-136">**string**</span></span> | <span data-ttu-id="20dd0-137">Y</span><span class="sxs-lookup"><span data-stu-id="20dd0-137">Y</span></span>        | <span data-ttu-id="20dd0-138">ID země nebo oblasti</span><span class="sxs-lookup"><span data-stu-id="20dd0-138">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="20dd0-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="20dd0-139">Request headers</span></span>

- <span data-ttu-id="20dd0-140">Je vyžadováno **ID národního prostředí** naformátovaného jako řetězec.</span><span class="sxs-lookup"><span data-stu-id="20dd0-140">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="20dd0-141">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="20dd0-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="20dd0-142">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="20dd0-142">Request body</span></span>

<span data-ttu-id="20dd0-143">Žádné</span><span class="sxs-lookup"><span data-stu-id="20dd0-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="20dd0-144">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="20dd0-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="20dd0-145">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="20dd0-145">REST response</span></span>

<span data-ttu-id="20dd0-146">V případě úspěchu vrátí tato metoda v těle odpovědi prostředek **nabídky** .</span><span class="sxs-lookup"><span data-stu-id="20dd0-146">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="20dd0-147">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="20dd0-147">Response success and error codes</span></span>

<span data-ttu-id="20dd0-148">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="20dd0-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="20dd0-149">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="20dd0-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="20dd0-150">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="20dd0-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="20dd0-151">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="20dd0-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Mon, 23 Nov 2015 23:13:01 GMT

{
    "id": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "name": "Office 365 Business Premium",
    "description": "For businesses with 1 to 300 users that need the latest desktop version of Office,
                    plus anywhere access to email, filesharing, and online conferencing.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "rank": 56,
    "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/031C9E47-4802-4248-838E-778FB1D2CC05",
    "locale": "en-us",
    "country": "US",
    "category": {
        "id": "SmallBusiness_Key",
        "name": "Small Business",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    "prerequisiteOffers": [],
    "isAddOn": false,
    "isAvailableForPurchase": true,
    "billing": "license",
    "isAutoRenewable": true,
    "product": {
        "id": "f245ecc8-75af-4f8e-b61f-27d8114de5f3",
        "name": "Office 365 Business Premium",
        "unit": "Licenses"
    },
    "unitType": "Licenses",
    "links": {
        "learnMore": {
            "uri": "http: //g.microsoftonline.com/0BXPS00en/909",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Offer"
    }
}
```
