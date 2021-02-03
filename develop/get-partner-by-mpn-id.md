---
title: Ověření ID MPN partnera
description: Přečtěte si, jak ověřit identifikátor ID Microsoft Partner Network partnera (MPN ID) vyžádáním profilu MPN partnera prostřednictvím jazyka C \# nebo partnerského centra REST API.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ef7bcb35274a6bcbaddbe0553ca0cb4dc1b2f9c
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/11/2020
ms.locfileid: "97767064"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="79f18-103">Ověření ID MPN partnera prostřednictvím jazyka C \# nebo partnerského centra REST API</span><span class="sxs-lookup"><span data-stu-id="79f18-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="79f18-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="79f18-104">**Applies To**</span></span>

- <span data-ttu-id="79f18-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="79f18-105">Partner Center</span></span>
- <span data-ttu-id="79f18-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="79f18-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="79f18-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="79f18-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="79f18-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="79f18-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="79f18-109">Jak ověřit identifikátor Microsoft Partner Network partnera (ID MPN)</span><span class="sxs-lookup"><span data-stu-id="79f18-109">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="79f18-110">Zde uvedená technika ověří identifikátor Microsoft Partner Network partnera tím, že požádá o profil MPN partnera z partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="79f18-110">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="79f18-111">Identifikátor se považuje za platný, pokud je požadavek úspěšný.</span><span class="sxs-lookup"><span data-stu-id="79f18-111">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79f18-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="79f18-112">Prerequisites</span></span>

- <span data-ttu-id="79f18-113">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="79f18-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="79f18-114">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="79f18-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="79f18-115">ID MPN partnera, který se má ověřit</span><span class="sxs-lookup"><span data-stu-id="79f18-115">The partner MPN ID to verify.</span></span> <span data-ttu-id="79f18-116">Pokud tuto hodnotu vynecháte, požadavek načte profil MPN pro přihlášeného partnera.</span><span class="sxs-lookup"><span data-stu-id="79f18-116">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="79f18-117">C\#</span><span class="sxs-lookup"><span data-stu-id="79f18-117">C\#</span></span>

<span data-ttu-id="79f18-118">Pokud chcete ověřit ID MPN partnera, nejdřív načtěte rozhraní pro operace shromažďování profilů partnerů z vlastnosti [**IAggregatePartner. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) .</span><span class="sxs-lookup"><span data-stu-id="79f18-118">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="79f18-119">Pak z vlastnosti [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) Získejte rozhraní pro operace s profilem MPN.</span><span class="sxs-lookup"><span data-stu-id="79f18-119">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="79f18-120">Nakonec voláním metod [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) nebo [**GETASYNC**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) s ID MPN načtěte profil MPN.</span><span class="sxs-lookup"><span data-stu-id="79f18-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="79f18-121">Pokud z volání Get nebo GetAsync vynecháte ID MPN, požadavek se pokusí načíst profil MPN přihlášeného partnera.</span><span class="sxs-lookup"><span data-stu-id="79f18-121">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="79f18-122">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="79f18-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="79f18-123">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: VerifyPartnerMpnId.cs</span><span class="sxs-lookup"><span data-stu-id="79f18-123">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="79f18-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="79f18-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="79f18-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="79f18-125">Request syntax</span></span>

| <span data-ttu-id="79f18-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="79f18-126">Method</span></span>  | <span data-ttu-id="79f18-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="79f18-127">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="79f18-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="79f18-128">**GET**</span></span> | <span data-ttu-id="79f18-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN? mpnId = {MPN-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="79f18-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="79f18-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="79f18-130">URI parameter</span></span>

<span data-ttu-id="79f18-131">Zadejte následující parametr dotazu pro identifikaci partnera.</span><span class="sxs-lookup"><span data-stu-id="79f18-131">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="79f18-132">Pokud tento parametr dotazu vynecháte, požadavek vrátí profil MPN pro přihlášeného partnera.</span><span class="sxs-lookup"><span data-stu-id="79f18-132">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="79f18-133">Název</span><span class="sxs-lookup"><span data-stu-id="79f18-133">Name</span></span>   | <span data-ttu-id="79f18-134">Typ</span><span class="sxs-lookup"><span data-stu-id="79f18-134">Type</span></span> | <span data-ttu-id="79f18-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="79f18-135">Required</span></span> | <span data-ttu-id="79f18-136">Popis</span><span class="sxs-lookup"><span data-stu-id="79f18-136">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="79f18-137">MPN – ID</span><span class="sxs-lookup"><span data-stu-id="79f18-137">mpn-id</span></span> | <span data-ttu-id="79f18-138">int</span><span class="sxs-lookup"><span data-stu-id="79f18-138">int</span></span>  | <span data-ttu-id="79f18-139">No</span><span class="sxs-lookup"><span data-stu-id="79f18-139">No</span></span>       | <span data-ttu-id="79f18-140">ID Microsoft Partner Network, které identifikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="79f18-140">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="79f18-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="79f18-141">Request headers</span></span>

<span data-ttu-id="79f18-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="79f18-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="79f18-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="79f18-143">Request body</span></span>

<span data-ttu-id="79f18-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="79f18-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="79f18-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="79f18-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="79f18-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="79f18-146">REST response</span></span>

<span data-ttu-id="79f18-147">V případě úspěchu obsahuje tělo odpovědi prostředek [MpnProfile](profile-resources.md#mpnprofile) pro partnera.</span><span class="sxs-lookup"><span data-stu-id="79f18-147">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="79f18-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="79f18-148">Response success and error codes</span></span>

<span data-ttu-id="79f18-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="79f18-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="79f18-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="79f18-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="79f18-151">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="79f18-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="79f18-152">Příklad odpovědi (úspěch)</span><span class="sxs-lookup"><span data-stu-id="79f18-152">Response example (success)</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a><span data-ttu-id="79f18-153">Příklad odpovědi (neúspěch)</span><span class="sxs-lookup"><span data-stu-id="79f18-153">Response example (failure)</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
