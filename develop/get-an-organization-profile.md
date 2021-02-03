---
title: Získání profilu organizace
description: Získá objekt reprezentující Profil organizace partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 132a1e0efa3efea69d4bf649e55b412e300b0685
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767040"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="2d69d-103">Získání profilu organizace</span><span class="sxs-lookup"><span data-stu-id="2d69d-103">Get an organization profile</span></span>

<span data-ttu-id="2d69d-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="2d69d-104">**Applies To**</span></span>

- <span data-ttu-id="2d69d-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="2d69d-105">Partner Center</span></span>
- <span data-ttu-id="2d69d-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="2d69d-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2d69d-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="2d69d-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2d69d-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2d69d-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2d69d-109">Získá objekt reprezentující Profil organizace partnera.</span><span class="sxs-lookup"><span data-stu-id="2d69d-109">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d69d-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2d69d-110">Prerequisites</span></span>

- <span data-ttu-id="2d69d-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2d69d-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2d69d-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="2d69d-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="2d69d-113">C\#</span><span class="sxs-lookup"><span data-stu-id="2d69d-113">C\#</span></span>

<span data-ttu-id="2d69d-114">Pokud chcete získat profil vaší organizace, použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **OrganizationProfile** .</span><span class="sxs-lookup"><span data-stu-id="2d69d-114">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="2d69d-115">Nakonec zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="2d69d-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="2d69d-116">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2d69d-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2d69d-117">**Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: GetOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="2d69d-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="2d69d-118">Java</span><span class="sxs-lookup"><span data-stu-id="2d69d-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="2d69d-119">Chcete-li získat profil vaší organizace, použijte funkci **IAggregatePartner. Getprofiles** a zavolejte funkci **getOrganizationProfile** .</span><span class="sxs-lookup"><span data-stu-id="2d69d-119">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="2d69d-120">Nakonec zavolejte funkci **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="2d69d-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="2d69d-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d69d-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="2d69d-122">Pokud chcete získat profil vaší organizace, spusťte příkaz [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) .</span><span class="sxs-lookup"><span data-stu-id="2d69d-122">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="2d69d-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="2d69d-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2d69d-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="2d69d-124">Request syntax</span></span>

| <span data-ttu-id="2d69d-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="2d69d-125">Method</span></span>  | <span data-ttu-id="2d69d-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2d69d-126">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="2d69d-127">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="2d69d-127">**GET**</span></span> | <span data-ttu-id="2d69d-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2d69d-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2d69d-129">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2d69d-129">Request headers</span></span>

<span data-ttu-id="2d69d-130">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2d69d-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2d69d-131">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2d69d-131">Request body</span></span>

<span data-ttu-id="2d69d-132">Žádné</span><span class="sxs-lookup"><span data-stu-id="2d69d-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2d69d-133">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="2d69d-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="2d69d-134">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2d69d-134">REST response</span></span>

<span data-ttu-id="2d69d-135">V případě úspěchu tato metoda vrátí objekt **OrganizationProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="2d69d-135">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2d69d-136">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="2d69d-136">Response success and error codes</span></span>

<span data-ttu-id="2d69d-137">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2d69d-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2d69d-138">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="2d69d-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2d69d-139">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2d69d-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2d69d-140">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="2d69d-140">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
Date: Tue, 22 Mar 2016 17:11:06 GMT

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
