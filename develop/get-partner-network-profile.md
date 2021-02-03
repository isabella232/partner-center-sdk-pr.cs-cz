---
title: Získání profilu programu Microsoft Partner Network
description: Získá objekt reprezentující profil MPN partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8f3e74462da05de0be47964beb34228650b1f53
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767055"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="235dd-103">Získání profilu programu Microsoft Partner Network</span><span class="sxs-lookup"><span data-stu-id="235dd-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="235dd-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="235dd-104">**Applies To**</span></span>

- <span data-ttu-id="235dd-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="235dd-105">Partner Center</span></span>
- <span data-ttu-id="235dd-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="235dd-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="235dd-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="235dd-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="235dd-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="235dd-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="235dd-109">Získá objekt reprezentující profil MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="235dd-109">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="235dd-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="235dd-110">Prerequisites</span></span>

- <span data-ttu-id="235dd-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="235dd-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="235dd-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="235dd-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="235dd-113">C\#</span><span class="sxs-lookup"><span data-stu-id="235dd-113">C\#</span></span>

<span data-ttu-id="235dd-114">Pokud chcete získat profil partnerské sítě, použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **MpnProfile** .</span><span class="sxs-lookup"><span data-stu-id="235dd-114">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="235dd-115">Nakonec zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="235dd-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="235dd-116">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="235dd-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="235dd-117">**Projekt**:P Artnercentersdk. FeaturesSamples **Třída**: GetMPNProfile.cs</span><span class="sxs-lookup"><span data-stu-id="235dd-117">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="235dd-118">Java</span><span class="sxs-lookup"><span data-stu-id="235dd-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="235dd-119">Pokud chcete získat profil partnerské sítě, použijte funkci **IAggregatePartner. Getprofiles** a zavolejte funkci **getMpnProfile** .</span><span class="sxs-lookup"><span data-stu-id="235dd-119">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="235dd-120">Nakonec zavolejte funkci **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="235dd-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="235dd-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="235dd-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="235dd-122">Pokud chcete získat profil partnerské sítě, spusťte příkaz [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) .</span><span class="sxs-lookup"><span data-stu-id="235dd-122">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="235dd-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="235dd-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="235dd-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="235dd-124">Request syntax</span></span>

| <span data-ttu-id="235dd-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="235dd-125">Method</span></span>  | <span data-ttu-id="235dd-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="235dd-126">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="235dd-127">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="235dd-127">**GET**</span></span> | <span data-ttu-id="235dd-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="235dd-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="235dd-129">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="235dd-129">Request headers</span></span>

<span data-ttu-id="235dd-130">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="235dd-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="235dd-131">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="235dd-131">Request body</span></span>

<span data-ttu-id="235dd-132">Žádné</span><span class="sxs-lookup"><span data-stu-id="235dd-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="235dd-133">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="235dd-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="235dd-134">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="235dd-134">REST response</span></span>

<span data-ttu-id="235dd-135">V případě úspěchu tato metoda vrátí objekt **MPNProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="235dd-135">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="235dd-136">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="235dd-136">Response success and error codes</span></span>

<span data-ttu-id="235dd-137">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="235dd-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="235dd-138">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="235dd-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="235dd-139">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="235dd-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="235dd-140">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="235dd-140">Response example</span></span>

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
