---
title: Ověření ID MPN partnera
description: Zjistěte, jak ověřit identifikátor Microsoft Partner Network MPN (MPN ID) partnera tím, že prostřednictvím C nebo Partnerské centrum REST API požádáte o profil MPN \# partnera.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bd51850c7bc5a099a34f9c028a58e247c2600a3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548817"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="d728a-103">Ověření ID MPN partnera prostřednictvím jazyka C \# nebo Partnerské centrum REST API</span><span class="sxs-lookup"><span data-stu-id="d728a-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="d728a-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d728a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d728a-105">Ověření identifikátoru MPN (MICROSOFT PARTNER NETWORK partnera)</span><span class="sxs-lookup"><span data-stu-id="d728a-105">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="d728a-106">Zde zobrazená technika ověří identifikátor Microsoft Partner Network tím, že si z Partnerského centra vyžádá profil MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="d728a-106">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="d728a-107">Identifikátor se považuje za platný, pokud je požadavek úspěšný.</span><span class="sxs-lookup"><span data-stu-id="d728a-107">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d728a-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d728a-108">Prerequisites</span></span>

- <span data-ttu-id="d728a-109">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d728a-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d728a-110">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d728a-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d728a-111">ID MPN partnera, které chcete ověřit.</span><span class="sxs-lookup"><span data-stu-id="d728a-111">The partner MPN ID to verify.</span></span> <span data-ttu-id="d728a-112">Pokud tuto hodnotu vynecháte, požadavek načte profil MPN přihlášených partnerů.</span><span class="sxs-lookup"><span data-stu-id="d728a-112">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="d728a-113">C\#</span><span class="sxs-lookup"><span data-stu-id="d728a-113">C\#</span></span>

<span data-ttu-id="d728a-114">Pokud chcete ověřit ID MPN partnera, nejprve načtěte rozhraní pro operace shromažďování profilů partnerů z [**vlastnosti IAggregatePartner.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)</span><span class="sxs-lookup"><span data-stu-id="d728a-114">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="d728a-115">Pak z vlastnosti [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) získejte rozhraní operací profilu MPN.</span><span class="sxs-lookup"><span data-stu-id="d728a-115">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="d728a-116">Nakonec zavolejte metody [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) s ID MPN a načtěte profil MPN.</span><span class="sxs-lookup"><span data-stu-id="d728a-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="d728a-117">Pokud vynecháte ID MPN z volání Get nebo GetAsync, požadavek se pokusí načíst profil MPN přihlášený partner.</span><span class="sxs-lookup"><span data-stu-id="d728a-117">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="d728a-118">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d728a-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d728a-119">**Project:** SDK pro Partnerské centrum Samples **:** VerifyPartnerMpnId.cs</span><span class="sxs-lookup"><span data-stu-id="d728a-119">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d728a-120">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="d728a-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d728a-121">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="d728a-121">Request syntax</span></span>

| <span data-ttu-id="d728a-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="d728a-122">Method</span></span>  | <span data-ttu-id="d728a-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d728a-123">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="d728a-124">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="d728a-124">**GET**</span></span> | <span data-ttu-id="d728a-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d728a-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d728a-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d728a-126">URI parameter</span></span>

<span data-ttu-id="d728a-127">Zadejte následující parametr dotazu pro identifikaci partnera.</span><span class="sxs-lookup"><span data-stu-id="d728a-127">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="d728a-128">Pokud tento parametr dotazu vynecháte, požadavek vrátí profil MPN přihlášených partnerů.</span><span class="sxs-lookup"><span data-stu-id="d728a-128">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="d728a-129">Název</span><span class="sxs-lookup"><span data-stu-id="d728a-129">Name</span></span>   | <span data-ttu-id="d728a-130">Typ</span><span class="sxs-lookup"><span data-stu-id="d728a-130">Type</span></span> | <span data-ttu-id="d728a-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d728a-131">Required</span></span> | <span data-ttu-id="d728a-132">Popis</span><span class="sxs-lookup"><span data-stu-id="d728a-132">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="d728a-133">id mpn</span><span class="sxs-lookup"><span data-stu-id="d728a-133">mpn-id</span></span> | <span data-ttu-id="d728a-134">int</span><span class="sxs-lookup"><span data-stu-id="d728a-134">int</span></span>  | <span data-ttu-id="d728a-135">No</span><span class="sxs-lookup"><span data-stu-id="d728a-135">No</span></span>       | <span data-ttu-id="d728a-136">Id Microsoft Partner Network, které identifikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="d728a-136">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d728a-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d728a-137">Request headers</span></span>

<span data-ttu-id="d728a-138">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d728a-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d728a-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d728a-139">Request body</span></span>

<span data-ttu-id="d728a-140">Žádné</span><span class="sxs-lookup"><span data-stu-id="d728a-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d728a-141">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d728a-141">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d728a-142">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d728a-142">REST response</span></span>

<span data-ttu-id="d728a-143">V případě úspěchu bude tělo odpovědi obsahovat prostředek [MpnProfile](profile-resources.md#mpnprofile) pro partnera.</span><span class="sxs-lookup"><span data-stu-id="d728a-143">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d728a-144">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="d728a-144">Response success and error codes</span></span>

<span data-ttu-id="d728a-145">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d728a-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d728a-146">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="d728a-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d728a-147">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d728a-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="d728a-148">Příklad odpovědi (úspěch)</span><span class="sxs-lookup"><span data-stu-id="d728a-148">Response example (success)</span></span>

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

### <a name="response-example-failure"></a><span data-ttu-id="d728a-149">Příklad odpovědi (selhání)</span><span class="sxs-lookup"><span data-stu-id="d728a-149">Response example (failure)</span></span>

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
