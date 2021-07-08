---
title: Získání oficiálního obchodního profilu partnera
description: Naučte se používat rozhraní API k získání vašeho platného obchodního profilu.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0654e364674bc2db129a0904d411c6fb67cbb9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549055"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="6603e-103">Získání oficiálního obchodního profilu partnera</span><span class="sxs-lookup"><span data-stu-id="6603e-103">Get the partner legal business profile</span></span>

<span data-ttu-id="6603e-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6603e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6603e-105">Jak získat oficiální obchodní profil partnera.</span><span class="sxs-lookup"><span data-stu-id="6603e-105">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6603e-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6603e-106">Prerequisites</span></span>

- <span data-ttu-id="6603e-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6603e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6603e-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="6603e-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="6603e-109">C\#</span><span class="sxs-lookup"><span data-stu-id="6603e-109">C\#</span></span>

<span data-ttu-id="6603e-110">Chcete-li získat obchodní profil partnera, nejprve získejte rozhraní pro kolekci operací partnerského profilu z vlastnosti **IAggregatePartner. Profiles** .</span><span class="sxs-lookup"><span data-stu-id="6603e-110">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="6603e-111">Potom Získejte hodnotu vlastnosti **LegalBusinessProfile** , která načte rozhraní k platným obchodním profilům.</span><span class="sxs-lookup"><span data-stu-id="6603e-111">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="6603e-112">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) načtěte profil.</span><span class="sxs-lookup"><span data-stu-id="6603e-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="6603e-113">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6603e-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6603e-114">**Project**: **třída** microsoft Partner SDK samples: GetLegalBusinessProfile. cs</span><span class="sxs-lookup"><span data-stu-id="6603e-114">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6603e-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="6603e-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6603e-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="6603e-116">Request syntax</span></span>

| <span data-ttu-id="6603e-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="6603e-117">Method</span></span>  | <span data-ttu-id="6603e-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="6603e-118">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="6603e-119">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="6603e-119">**GET**</span></span> | <span data-ttu-id="6603e-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6603e-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6603e-121">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="6603e-121">Request headers</span></span>

<span data-ttu-id="6603e-122">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6603e-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6603e-123">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="6603e-123">Request body</span></span>

<span data-ttu-id="6603e-124">Žádné</span><span class="sxs-lookup"><span data-stu-id="6603e-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6603e-125">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="6603e-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6603e-126">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="6603e-126">REST response</span></span>

<span data-ttu-id="6603e-127">V případě úspěchu tato metoda vrátí objekt **LegalBusinessProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="6603e-127">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6603e-128">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="6603e-128">Response success and error codes</span></span>

<span data-ttu-id="6603e-129">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="6603e-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6603e-130">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="6603e-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6603e-131">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6603e-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6603e-132">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="6603e-132">Response example</span></span>

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
