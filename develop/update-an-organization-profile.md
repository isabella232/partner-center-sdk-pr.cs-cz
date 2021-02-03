---
title: Aktualizace profilu organizace
description: Aktualizuje Fakturační profil organizace.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ccf938fff285704f54d4717b2678e1419d857d8d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766749"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="42873-103">Aktualizace profilu organizace</span><span class="sxs-lookup"><span data-stu-id="42873-103">Update an organization profile</span></span>

<span data-ttu-id="42873-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="42873-104">**Applies To**</span></span>

- <span data-ttu-id="42873-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="42873-105">Partner Center</span></span>
- <span data-ttu-id="42873-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="42873-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="42873-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="42873-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="42873-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="42873-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="42873-109">Aktualizuje Fakturační profil partnera.</span><span class="sxs-lookup"><span data-stu-id="42873-109">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42873-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="42873-110">Prerequisites</span></span>

- <span data-ttu-id="42873-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="42873-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="42873-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="42873-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="42873-113">C\#</span><span class="sxs-lookup"><span data-stu-id="42873-113">C\#</span></span>

<span data-ttu-id="42873-114">Pokud chcete aktualizovat profil vaší organizace, načtěte profil a proveďte potřebné změny.</span><span class="sxs-lookup"><span data-stu-id="42873-114">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="42873-115">Pak použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **OrganizationProfile** .</span><span class="sxs-lookup"><span data-stu-id="42873-115">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="42873-116">Nakonec zavolejte metodu **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="42873-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="42873-117">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="42873-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="42873-118">**Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: UpdateOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="42873-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="42873-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="42873-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="42873-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="42873-120">Request syntax</span></span>

| <span data-ttu-id="42873-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="42873-121">Method</span></span>  | <span data-ttu-id="42873-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="42873-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="42873-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="42873-123">**PUT**</span></span> | <span data-ttu-id="42873-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="42873-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="42873-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="42873-125">Request headers</span></span>

<span data-ttu-id="42873-126">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="42873-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="42873-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="42873-127">Request body</span></span>

<span data-ttu-id="42873-128">Žádné</span><span class="sxs-lookup"><span data-stu-id="42873-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="42873-129">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="42873-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="42873-130">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="42873-130">REST response</span></span>

<span data-ttu-id="42873-131">V případě úspěchu tato metoda vrátí objekt **OrganizationProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="42873-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="42873-132">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="42873-132">Response success and error codes</span></span>

<span data-ttu-id="42873-133">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="42873-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="42873-134">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="42873-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="42873-135">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="42873-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="42873-136">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="42873-136">Response example</span></span>

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
