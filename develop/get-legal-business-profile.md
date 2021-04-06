---
title: Získání oficiálního obchodního profilu partnera
description: Naučte se používat rozhraní API k získání vašeho platného obchodního profilu.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1d488c8deb9f01110e92327035ce0c3c023fcb46
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500018"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="42a53-103">Získání oficiálního obchodního profilu partnera</span><span class="sxs-lookup"><span data-stu-id="42a53-103">Get the partner legal business profile</span></span>

<span data-ttu-id="42a53-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="42a53-104">**Applies To**</span></span>

- <span data-ttu-id="42a53-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="42a53-105">Partner Center</span></span>
- <span data-ttu-id="42a53-106">Partnerské centrum provozované společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="42a53-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="42a53-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="42a53-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="42a53-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="42a53-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="42a53-109">Jak získat oficiální obchodní profil partnera.</span><span class="sxs-lookup"><span data-stu-id="42a53-109">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42a53-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="42a53-110">Prerequisites</span></span>

- <span data-ttu-id="42a53-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="42a53-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="42a53-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="42a53-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="42a53-113">C\#</span><span class="sxs-lookup"><span data-stu-id="42a53-113">C\#</span></span>

<span data-ttu-id="42a53-114">Chcete-li získat obchodní profil partnera, nejprve získejte rozhraní pro kolekci operací partnerského profilu z vlastnosti **IAggregatePartner. Profiles** .</span><span class="sxs-lookup"><span data-stu-id="42a53-114">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="42a53-115">Potom Získejte hodnotu vlastnosti **LegalBusinessProfile** , která načte rozhraní k platným obchodním profilům.</span><span class="sxs-lookup"><span data-stu-id="42a53-115">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="42a53-116">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) načtěte profil.</span><span class="sxs-lookup"><span data-stu-id="42a53-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="42a53-117">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="42a53-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="42a53-118">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetLegalBusinessProfile. cs</span><span class="sxs-lookup"><span data-stu-id="42a53-118">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="42a53-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="42a53-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="42a53-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="42a53-120">Request syntax</span></span>

| <span data-ttu-id="42a53-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="42a53-121">Method</span></span>  | <span data-ttu-id="42a53-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="42a53-122">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="42a53-123">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="42a53-123">**GET**</span></span> | <span data-ttu-id="42a53-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="42a53-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="42a53-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="42a53-125">Request headers</span></span>

<span data-ttu-id="42a53-126">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="42a53-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="42a53-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="42a53-127">Request body</span></span>

<span data-ttu-id="42a53-128">Žádné</span><span class="sxs-lookup"><span data-stu-id="42a53-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="42a53-129">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="42a53-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness?vettingVersion=Current HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="42a53-130">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="42a53-130">REST response</span></span>

<span data-ttu-id="42a53-131">V případě úspěchu tato metoda vrátí objekt **LegalBusinessProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="42a53-131">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="42a53-132">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="42a53-132">Response success and error codes</span></span>

<span data-ttu-id="42a53-133">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="42a53-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="42a53-134">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="42a53-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="42a53-135">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="42a53-135">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="42a53-136">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="42a53-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1151
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CV: MEgCpJUoGUeXG+4a.0
MS-ServerId: 030011719
Date: Tue, 21 Mar 2017 17:29:52 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550100"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550100"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```
