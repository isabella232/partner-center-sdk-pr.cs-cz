---
title: Získání profilu podpory
description: Získá objekt reprezentující profil podpory uživatele.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b8b0fa533aaba74418985ea02cbb13bd722cede2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767020"
---
# <a name="get-support-profile"></a><span data-ttu-id="87270-103">Získání profilu podpory</span><span class="sxs-lookup"><span data-stu-id="87270-103">Get support profile</span></span>

<span data-ttu-id="87270-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="87270-104">**Applies To**</span></span>

- <span data-ttu-id="87270-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="87270-105">Partner Center</span></span>
- <span data-ttu-id="87270-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="87270-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="87270-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="87270-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="87270-108">Získá objekt reprezentující profil podpory uživatele.</span><span class="sxs-lookup"><span data-stu-id="87270-108">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87270-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="87270-109">Prerequisites</span></span>

- <span data-ttu-id="87270-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="87270-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="87270-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="87270-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="87270-112">C\#</span><span class="sxs-lookup"><span data-stu-id="87270-112">C\#</span></span>

<span data-ttu-id="87270-113">Profil podpory získáte pomocí kolekce **IAggregatePartner. Profiles** .</span><span class="sxs-lookup"><span data-stu-id="87270-113">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="87270-114">Zavolejte vlastnost [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) , za kterou následují metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="87270-114">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="87270-115">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="87270-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="87270-116">**Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: GetSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="87270-116">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="87270-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="87270-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="87270-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="87270-118">Request syntax</span></span>

| <span data-ttu-id="87270-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="87270-119">Method</span></span>  | <span data-ttu-id="87270-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="87270-120">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="87270-121">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="87270-121">**GET**</span></span> | <span data-ttu-id="87270-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/support HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="87270-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="87270-123">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="87270-123">Request headers</span></span>

<span data-ttu-id="87270-124">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="87270-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="87270-125">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="87270-125">Request body</span></span>

<span data-ttu-id="87270-126">Žádné</span><span class="sxs-lookup"><span data-stu-id="87270-126">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="87270-127">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="87270-127">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="87270-128">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="87270-128">REST response</span></span>

<span data-ttu-id="87270-129">V případě úspěchu tato metoda vrátí objekt **SupportProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="87270-129">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="87270-130">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="87270-130">Response success and error codes</span></span>

<span data-ttu-id="87270-131">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="87270-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="87270-132">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="87270-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="87270-133">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="87270-133">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="87270-134">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="87270-134">Response example</span></span>

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
