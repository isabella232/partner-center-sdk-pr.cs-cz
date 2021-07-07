---
title: Aktualizace profilu podpory
description: Aktualizuje profil podpory uživatele.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 143328c5501f525d52911eead805d420f79b78ff
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530340"
---
# <a name="update-support-profile"></a><span data-ttu-id="ab997-103">Aktualizace profilu podpory</span><span class="sxs-lookup"><span data-stu-id="ab997-103">Update support profile</span></span>

<span data-ttu-id="ab997-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ab997-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ab997-105">Aktualizuje profil podpory uživatele.</span><span class="sxs-lookup"><span data-stu-id="ab997-105">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab997-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ab997-106">Prerequisites</span></span>

- <span data-ttu-id="ab997-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ab997-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ab997-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ab997-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="ab997-109">C\#</span><span class="sxs-lookup"><span data-stu-id="ab997-109">C\#</span></span>

<span data-ttu-id="ab997-110">Pokud chcete aktualizovat profil podpory, [nejprve získejte profil podpory](get-support-profile.md) a proveďte požadované změny.</span><span class="sxs-lookup"><span data-stu-id="ab997-110">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="ab997-111">Pak použijte kolekci [**IPartnerOperations.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)</span><span class="sxs-lookup"><span data-stu-id="ab997-111">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="ab997-112">Zavolejte [**vlastnost SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) následovanou metodou [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) nebo [**UpdateAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync)</span><span class="sxs-lookup"><span data-stu-id="ab997-112">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

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

<span data-ttu-id="ab997-113">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ab997-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ab997-114">**Project:** PartnerCenterSDK.FeaturesSamples **– třída:** UpdateSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="ab997-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ab997-115">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="ab997-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ab997-116">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="ab997-116">Request syntax</span></span>

| <span data-ttu-id="ab997-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="ab997-117">Method</span></span>  | <span data-ttu-id="ab997-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ab997-118">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="ab997-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="ab997-119">**PUT**</span></span> | <span data-ttu-id="ab997-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ab997-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ab997-121">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ab997-121">Request headers</span></span>

<span data-ttu-id="ab997-122">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ab997-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ab997-123">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ab997-123">Request body</span></span>

<span data-ttu-id="ab997-124">Úplný prostředek profilu podpory.</span><span class="sxs-lookup"><span data-stu-id="ab997-124">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="ab997-125">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ab997-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ab997-126">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ab997-126">REST response</span></span>

<span data-ttu-id="ab997-127">V případě úspěchu tato metoda vrátí aktualizované vlastnosti objektu **SupportProfile** v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="ab997-127">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ab997-128">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="ab997-128">Response success and error codes</span></span>

<span data-ttu-id="ab997-129">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ab997-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ab997-130">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="ab997-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ab997-131">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ab997-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ab997-132">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ab997-132">Response example</span></span>

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
