---
title: Získání profilu programu Microsoft Partner Network
description: Získá objekt představující profil MPN partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38c12a9a9755b9838b7742d9f38c5cbd52b81210
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548851"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="be2e5-103">Získání profilu programu Microsoft Partner Network</span><span class="sxs-lookup"><span data-stu-id="be2e5-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="be2e5-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="be2e5-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="be2e5-105">Získá objekt představující profil MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="be2e5-105">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be2e5-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="be2e5-106">Prerequisites</span></span>

- <span data-ttu-id="be2e5-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="be2e5-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="be2e5-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="be2e5-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="be2e5-109">C\#</span><span class="sxs-lookup"><span data-stu-id="be2e5-109">C\#</span></span>

<span data-ttu-id="be2e5-110">Pokud chcete získat profil partnerské sítě, použijte kolekci **IAggregatePartner.Profiles** a zavolejte **vlastnost MpnProfile.**</span><span class="sxs-lookup"><span data-stu-id="be2e5-110">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="be2e5-111">Nakonec zavolejte [**metody Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="be2e5-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="be2e5-112">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="be2e5-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="be2e5-113">**Project**:P artnerCenterSDK.FeaturesSamples – **třída:** GetMPNProfile.cs</span><span class="sxs-lookup"><span data-stu-id="be2e5-113">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="be2e5-114">Java</span><span class="sxs-lookup"><span data-stu-id="be2e5-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="be2e5-115">Pokud chcete získat profil partnerské sítě, použijte funkci **IAggregatePartner.getProfiles** a zavolejte **funkci getMpnProfile.**</span><span class="sxs-lookup"><span data-stu-id="be2e5-115">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="be2e5-116">Nakonec zavolejte **funkci get().**</span><span class="sxs-lookup"><span data-stu-id="be2e5-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="be2e5-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be2e5-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="be2e5-118">Pokud chcete získat profil partnerské sítě, spusťte [**příkaz Get-PartnerMpnProfile.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md)</span><span class="sxs-lookup"><span data-stu-id="be2e5-118">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="be2e5-119">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="be2e5-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="be2e5-120">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="be2e5-120">Request syntax</span></span>

| <span data-ttu-id="be2e5-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="be2e5-121">Method</span></span>  | <span data-ttu-id="be2e5-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="be2e5-122">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="be2e5-123">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="be2e5-123">**GET**</span></span> | <span data-ttu-id="be2e5-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="be2e5-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="be2e5-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="be2e5-125">Request headers</span></span>

<span data-ttu-id="be2e5-126">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="be2e5-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="be2e5-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="be2e5-127">Request body</span></span>

<span data-ttu-id="be2e5-128">Žádné</span><span class="sxs-lookup"><span data-stu-id="be2e5-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="be2e5-129">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="be2e5-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="be2e5-130">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="be2e5-130">REST response</span></span>

<span data-ttu-id="be2e5-131">V případě úspěchu vrátí tato metoda v textu odpovědi objekt **MPNProfile.**</span><span class="sxs-lookup"><span data-stu-id="be2e5-131">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="be2e5-132">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="be2e5-132">Response success and error codes</span></span>

<span data-ttu-id="be2e5-133">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="be2e5-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="be2e5-134">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="be2e5-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="be2e5-135">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="be2e5-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="be2e5-136">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="be2e5-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
Date: Mon, 21 Mar 2016 05:51:29 GMT

{
    "mpnId":"<mpnID>",
    "profileType":"MpnProfile",
    "links":{
        "self":{
            "uri":"/profiles/mpn",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"MpnProfile"
    }
}
```
