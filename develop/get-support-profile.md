---
title: Získání profilu podpory
description: Získá objekt představující profil podpory uživatele.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b112ccbbff731795c21f95845a08be9e9dfb6775
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548630"
---
# <a name="get-support-profile"></a><span data-ttu-id="00724-103">Získání profilu podpory</span><span class="sxs-lookup"><span data-stu-id="00724-103">Get support profile</span></span>

<span data-ttu-id="00724-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="00724-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="00724-105">Získá objekt představující profil podpory uživatele.</span><span class="sxs-lookup"><span data-stu-id="00724-105">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00724-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="00724-106">Prerequisites</span></span>

- <span data-ttu-id="00724-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="00724-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="00724-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="00724-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="00724-109">C\#</span><span class="sxs-lookup"><span data-stu-id="00724-109">C\#</span></span>

<span data-ttu-id="00724-110">Pokud chcete získat profil podpory, použijte kolekci **IAggregatePartner.Profiles.**</span><span class="sxs-lookup"><span data-stu-id="00724-110">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="00724-111">Zavolejte [**vlastnost SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) následovanou [**metodami Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="00724-111">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="00724-112">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="00724-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="00724-113">**Project:** PartnerCenterSDK.FeaturesSamples **– třída:** GetSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="00724-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="00724-114">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="00724-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="00724-115">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="00724-115">Request syntax</span></span>

| <span data-ttu-id="00724-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="00724-116">Method</span></span>  | <span data-ttu-id="00724-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="00724-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="00724-118">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="00724-118">**GET**</span></span> | <span data-ttu-id="00724-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="00724-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="00724-120">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="00724-120">Request headers</span></span>

<span data-ttu-id="00724-121">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="00724-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="00724-122">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="00724-122">Request body</span></span>

<span data-ttu-id="00724-123">Žádné</span><span class="sxs-lookup"><span data-stu-id="00724-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="00724-124">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="00724-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="00724-125">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="00724-125">REST response</span></span>

<span data-ttu-id="00724-126">V případě úspěchu vrátí tato metoda v textu odpovědi objekt **SupportProfile.**</span><span class="sxs-lookup"><span data-stu-id="00724-126">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="00724-127">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="00724-127">Response success and error codes</span></span>

<span data-ttu-id="00724-128">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="00724-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="00724-129">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="00724-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="00724-130">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="00724-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="00724-131">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="00724-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
Date: Wed, 25 Nov 2015 07:16:17 GMT

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
