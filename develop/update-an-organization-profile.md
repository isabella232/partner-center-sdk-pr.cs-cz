---
title: Aktualizace profilu organizace
description: Aktualizuje fakturační profil organizace.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0ef736a722cde16f95ed6dfdbdab278c98fcf738
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530051"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="bb09d-103">Aktualizace profilu organizace</span><span class="sxs-lookup"><span data-stu-id="bb09d-103">Update an organization profile</span></span>

<span data-ttu-id="bb09d-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bb09d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bb09d-105">Aktualizuje fakturační profil partnera.</span><span class="sxs-lookup"><span data-stu-id="bb09d-105">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb09d-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bb09d-106">Prerequisites</span></span>

- <span data-ttu-id="bb09d-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="bb09d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bb09d-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="bb09d-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="bb09d-109">C\#</span><span class="sxs-lookup"><span data-stu-id="bb09d-109">C\#</span></span>

<span data-ttu-id="bb09d-110">Pokud chcete aktualizovat profil organizace, načtěte profil a proveďte potřebné změny.</span><span class="sxs-lookup"><span data-stu-id="bb09d-110">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="bb09d-111">Pak použijte kolekci **IAggregatePartner.Profiles** a zavolejte **vlastnost OrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="bb09d-111">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="bb09d-112">Nakonec zavolejte **metodu Update().**</span><span class="sxs-lookup"><span data-stu-id="bb09d-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="bb09d-113">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bb09d-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bb09d-114">**Project:** PartnerCenterSDK.FeaturesSamples **– třída:** UpdateOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="bb09d-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="bb09d-115">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="bb09d-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bb09d-116">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="bb09d-116">Request syntax</span></span>

| <span data-ttu-id="bb09d-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="bb09d-117">Method</span></span>  | <span data-ttu-id="bb09d-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="bb09d-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="bb09d-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="bb09d-119">**PUT**</span></span> | <span data-ttu-id="bb09d-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bb09d-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bb09d-121">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="bb09d-121">Request headers</span></span>

<span data-ttu-id="bb09d-122">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bb09d-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bb09d-123">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="bb09d-123">Request body</span></span>

<span data-ttu-id="bb09d-124">Žádné</span><span class="sxs-lookup"><span data-stu-id="bb09d-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bb09d-125">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bb09d-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 624
Expect: 100-continue

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="bb09d-126">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="bb09d-126">REST response</span></span>

<span data-ttu-id="bb09d-127">V případě úspěchu vrátí tato metoda v textu odpovědi objekt **OrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="bb09d-127">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bb09d-128">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="bb09d-128">Response success and error codes</span></span>

<span data-ttu-id="bb09d-129">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="bb09d-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bb09d-130">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="bb09d-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bb09d-131">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="bb09d-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bb09d-132">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bb09d-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
Date: Mon, 21 Mar 2016 05:48:41 GMT

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "profileType":"OrganizationProfile",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```
