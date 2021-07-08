---
title: Získání profilu organizace
description: Získá objekt představující profil organizace partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 1c7272761612e573388d4facea1a78808a5bad52
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760551"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="005d8-103">Získání profilu organizace</span><span class="sxs-lookup"><span data-stu-id="005d8-103">Get an organization profile</span></span>

<span data-ttu-id="005d8-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="005d8-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="005d8-105">Získá objekt představující profil organizace partnera.</span><span class="sxs-lookup"><span data-stu-id="005d8-105">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="005d8-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="005d8-106">Prerequisites</span></span>

- <span data-ttu-id="005d8-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="005d8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="005d8-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="005d8-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="005d8-109">C\#</span><span class="sxs-lookup"><span data-stu-id="005d8-109">C\#</span></span>

<span data-ttu-id="005d8-110">Pokud chcete získat profil organizace, použijte kolekci **IAggregatePartner.Profiles** a zavolejte **vlastnost OrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="005d8-110">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="005d8-111">Nakonec zavolejte [**metody Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="005d8-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="005d8-112">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="005d8-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="005d8-113">**Project:** PartnerCenterSDK.FeaturesSamples – **třída:** GetOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="005d8-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="005d8-114">Java</span><span class="sxs-lookup"><span data-stu-id="005d8-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="005d8-115">Pokud chcete získat profil organizace, použijte **funkci IAggregatePartner.getProfiles** a zavolejte **funkci getOrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="005d8-115">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="005d8-116">Nakonec zavolejte **funkci get().**</span><span class="sxs-lookup"><span data-stu-id="005d8-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="005d8-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="005d8-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="005d8-118">Pokud chcete získat profil organizace, spusťte příkaz [**Get-PartnerOrganizationProfile.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md)</span><span class="sxs-lookup"><span data-stu-id="005d8-118">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="005d8-119">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="005d8-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="005d8-120">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="005d8-120">Request syntax</span></span>

| <span data-ttu-id="005d8-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="005d8-121">Method</span></span>  | <span data-ttu-id="005d8-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="005d8-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="005d8-123">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="005d8-123">**GET**</span></span> | <span data-ttu-id="005d8-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="005d8-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="005d8-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="005d8-125">Request headers</span></span>

<span data-ttu-id="005d8-126">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="005d8-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="005d8-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="005d8-127">Request body</span></span>

<span data-ttu-id="005d8-128">Žádné</span><span class="sxs-lookup"><span data-stu-id="005d8-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="005d8-129">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="005d8-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="005d8-130">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="005d8-130">REST response</span></span>

<span data-ttu-id="005d8-131">V případě úspěchu vrátí tato metoda v textu odpovědi objekt **OrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="005d8-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="005d8-132">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="005d8-132">Response success and error codes</span></span>

<span data-ttu-id="005d8-133">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="005d8-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="005d8-134">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="005d8-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="005d8-135">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="005d8-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="005d8-136">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="005d8-136">Response example</span></span>

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
