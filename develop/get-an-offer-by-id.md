---
title: Získání nabídky podle ID
description: Získá prostředek nabídky, který odpovídá ID nabídky.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: 9448276e817affb823eddabbcab8757c79615fbd
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767054"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="8850a-103">Získání nabídky podle ID</span><span class="sxs-lookup"><span data-stu-id="8850a-103">Get an offer by ID</span></span>

<span data-ttu-id="8850a-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="8850a-104">**Applies To**</span></span>

- <span data-ttu-id="8850a-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="8850a-105">Partner Center</span></span>
- <span data-ttu-id="8850a-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="8850a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8850a-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="8850a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8850a-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8850a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8850a-109">Získá prostředek **nabídky** , který odpovídá ID nabídky.</span><span class="sxs-lookup"><span data-stu-id="8850a-109">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8850a-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8850a-110">Prerequisites</span></span>

- <span data-ttu-id="8850a-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8850a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8850a-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="8850a-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8850a-113">ID nabídky</span><span class="sxs-lookup"><span data-stu-id="8850a-113">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="8850a-114">C\#</span><span class="sxs-lookup"><span data-stu-id="8850a-114">C\#</span></span>

<span data-ttu-id="8850a-115">Chcete-li najít konkrétní nabídku podle ID, použijte svou kolekci **IAggregatePartner.** offers, vytvořte zemi se voláním **ByCountry ()** a poté zavolejte metodu [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="8850a-115">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="8850a-116">Pak zavolejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) nebo [**Get Async ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="8850a-116">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="8850a-117">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8850a-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8850a-118">**Projekt**: PartnerSDK. FeatureSample **Třída**: GetOffer.cs</span><span class="sxs-lookup"><span data-stu-id="8850a-118">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="8850a-119">Java</span><span class="sxs-lookup"><span data-stu-id="8850a-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="8850a-120">Chcete-li najít konkrétní nabídku podle ID, použijte funkci **IAggregatePartner. res** , stanovte zemi voláním funkce **byCountry ()** a potom zavolejte funkci **byID ()** .</span><span class="sxs-lookup"><span data-stu-id="8850a-120">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="8850a-121">Pak zavolejte funkci **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="8850a-121">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="8850a-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8850a-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="8850a-123">Chcete-li najít konkrétní nabídku podle ID, spusťte příkaz [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) a zadejte parametry **CountryCode** a **hodnotami OfferId** .</span><span class="sxs-lookup"><span data-stu-id="8850a-123">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="8850a-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="8850a-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8850a-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="8850a-125">Request syntax</span></span>

| <span data-ttu-id="8850a-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="8850a-126">Method</span></span>  | <span data-ttu-id="8850a-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8850a-127">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8850a-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="8850a-128">**GET**</span></span> | <span data-ttu-id="8850a-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{Offer-ID}? Country = {Country-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8850a-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8850a-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8850a-130">URI parameter</span></span>

| <span data-ttu-id="8850a-131">Název</span><span class="sxs-lookup"><span data-stu-id="8850a-131">Name</span></span>           | <span data-ttu-id="8850a-132">Typ</span><span class="sxs-lookup"><span data-stu-id="8850a-132">Type</span></span>       | <span data-ttu-id="8850a-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8850a-133">Required</span></span> | <span data-ttu-id="8850a-134">Popis</span><span class="sxs-lookup"><span data-stu-id="8850a-134">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="8850a-135">**ID nabídky**</span><span class="sxs-lookup"><span data-stu-id="8850a-135">**offer-id**</span></span>   | <span data-ttu-id="8850a-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="8850a-136">**guid**</span></span>   | <span data-ttu-id="8850a-137">Y</span><span class="sxs-lookup"><span data-stu-id="8850a-137">Y</span></span>        | <span data-ttu-id="8850a-138">Identifikátor GUID, který odpovídá této nabídce</span><span class="sxs-lookup"><span data-stu-id="8850a-138">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="8850a-139">**ID země**</span><span class="sxs-lookup"><span data-stu-id="8850a-139">**country-id**</span></span> | <span data-ttu-id="8850a-140">**řetezce**</span><span class="sxs-lookup"><span data-stu-id="8850a-140">**string**</span></span> | <span data-ttu-id="8850a-141">Y</span><span class="sxs-lookup"><span data-stu-id="8850a-141">Y</span></span>        | <span data-ttu-id="8850a-142">ID země nebo oblasti</span><span class="sxs-lookup"><span data-stu-id="8850a-142">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="8850a-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8850a-143">Request headers</span></span>

- <span data-ttu-id="8850a-144">Je vyžadováno **ID národního prostředí** naformátovaného jako řetězec.</span><span class="sxs-lookup"><span data-stu-id="8850a-144">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="8850a-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8850a-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8850a-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8850a-146">Request body</span></span>

<span data-ttu-id="8850a-147">Žádné</span><span class="sxs-lookup"><span data-stu-id="8850a-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8850a-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8850a-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="8850a-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8850a-149">REST response</span></span>

<span data-ttu-id="8850a-150">V případě úspěchu vrátí tato metoda v těle odpovědi prostředek **nabídky** .</span><span class="sxs-lookup"><span data-stu-id="8850a-150">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8850a-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="8850a-151">Response success and error codes</span></span>

<span data-ttu-id="8850a-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8850a-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8850a-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="8850a-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8850a-154">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8850a-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8850a-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8850a-155">Response example</span></span>

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
