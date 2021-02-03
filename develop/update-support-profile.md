---
title: Aktualizace profilu podpory
description: Aktualizuje profil podpory uživatele.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 605c509eeb18f301144fec6287c9611d5a5acfe2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766949"
---
# <a name="update-support-profile"></a><span data-ttu-id="c421a-103">Aktualizace profilu podpory</span><span class="sxs-lookup"><span data-stu-id="c421a-103">Update support profile</span></span>

<span data-ttu-id="c421a-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="c421a-104">**Applies To**</span></span>

- <span data-ttu-id="c421a-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="c421a-105">Partner Center</span></span>
- <span data-ttu-id="c421a-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="c421a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c421a-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="c421a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c421a-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c421a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c421a-109">Aktualizuje profil podpory uživatele.</span><span class="sxs-lookup"><span data-stu-id="c421a-109">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c421a-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c421a-110">Prerequisites</span></span>

- <span data-ttu-id="c421a-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c421a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c421a-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="c421a-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="c421a-113">C\#</span><span class="sxs-lookup"><span data-stu-id="c421a-113">C\#</span></span>

<span data-ttu-id="c421a-114">Pokud chcete aktualizovat svůj profil podpory, nejdřív [Získejte svůj profil podpory](get-support-profile.md) a proveďte jakékoli změny, které chcete.</span><span class="sxs-lookup"><span data-stu-id="c421a-114">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="c421a-115">Pak použijte svou kolekci [**IPartnerOperations. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) .</span><span class="sxs-lookup"><span data-stu-id="c421a-115">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="c421a-116">Zavolejte vlastnost [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) , následovanou metodou [**Update ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) nebo [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) .</span><span class="sxs-lookup"><span data-stu-id="c421a-116">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// updated profile
SupportProfile newSupportProfile = new SupportProfile
{
   Email = supportProfile.Email,
   Website = supportProfile.Website,
   Telephone = new Random().Next(10000000, 99999999).ToString(CultureInfo.InvariantCulture)
};

SupportProfile updatedSupportProfile = partnerOperations.Profiles.SupportProfile.Update(newSupportProfile);
```

<span data-ttu-id="c421a-117">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c421a-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c421a-118">**Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: UpdateSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="c421a-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c421a-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="c421a-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c421a-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="c421a-120">Request syntax</span></span>

| <span data-ttu-id="c421a-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="c421a-121">Method</span></span>  | <span data-ttu-id="c421a-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="c421a-122">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="c421a-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="c421a-123">**PUT**</span></span> | <span data-ttu-id="c421a-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/supportprofile HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c421a-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c421a-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="c421a-125">Request headers</span></span>

<span data-ttu-id="c421a-126">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c421a-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c421a-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="c421a-127">Request body</span></span>

<span data-ttu-id="c421a-128">Prostředek profilu plné podpory.</span><span class="sxs-lookup"><span data-stu-id="c421a-128">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="c421a-129">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="c421a-129">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/supportprofile HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
Content-Type: application/json
Content-Length: 167
Expect: 100-continue

{
    "Email": "email@sample.com",
    "Telephone": "4255555555",
    "Website": "www.microsoft.com",
    "ProfileType": "support_profile",
    "Attributes": {
        "ObjectType": "PartnerSupportProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="c421a-130">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="c421a-130">REST response</span></span>

<span data-ttu-id="c421a-131">V případě úspěchu tato metoda vrátí aktualizované vlastnosti objektu **SupportProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c421a-131">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c421a-132">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="c421a-132">Response success and error codes</span></span>

<span data-ttu-id="c421a-133">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="c421a-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c421a-134">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="c421a-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c421a-135">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c421a-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c421a-136">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="c421a-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
Date: Wed, 25 Nov 2015 07:16:18 GMT

{
    "email": "email@sample.com",
    "telephone": "4255555555",
    "website": "www.microsoft.com",
    "profileType": "support_profile",
    "links": {
        "self": {
            "uri": "/v1/profiles/support",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerSupportProfile"
    }
}
```
