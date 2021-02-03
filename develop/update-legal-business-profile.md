---
title: Aktualizace oficiálního obchodního profilu partnera
description: Jak aktualizovat licenční profil partnerského podniku
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 6c61b51ab0680e36daa99c11dc8e8c3506259d29
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766951"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="148d7-103">Aktualizace oficiálního obchodního profilu partnera</span><span class="sxs-lookup"><span data-stu-id="148d7-103">Update the partner legal business profile</span></span>

<span data-ttu-id="148d7-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="148d7-104">**Applies To**</span></span>

- <span data-ttu-id="148d7-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="148d7-105">Partner Center</span></span>
- <span data-ttu-id="148d7-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="148d7-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="148d7-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="148d7-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="148d7-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="148d7-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="148d7-109">Jak aktualizovat licenční profil partnerského podniku</span><span class="sxs-lookup"><span data-stu-id="148d7-109">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="148d7-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="148d7-110">Prerequisites</span></span>

- <span data-ttu-id="148d7-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="148d7-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="148d7-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="148d7-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="148d7-113">C\#</span><span class="sxs-lookup"><span data-stu-id="148d7-113">C\#</span></span>

<span data-ttu-id="148d7-114">Pokud chcete aktualizovat obchodní profil partnera, nejprve vytvořte instanci objektu **LegalBusinessProfile** a naplňte ji existujícím profilem.</span><span class="sxs-lookup"><span data-stu-id="148d7-114">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="148d7-115">Další informace najdete v tématu [získání licenčního profilu pro partnery](get-legal-business-profile.md).</span><span class="sxs-lookup"><span data-stu-id="148d7-115">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="148d7-116">Pak aktualizujte vlastnosti, které je třeba změnit.</span><span class="sxs-lookup"><span data-stu-id="148d7-116">Then, update the properties that you need to change.</span></span> <span data-ttu-id="148d7-117">Následující příklad kódu ukazuje, jak změnit adresu a primární kontaktní telefonní číslo.</span><span class="sxs-lookup"><span data-stu-id="148d7-117">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="148d7-118">Pak z vlastnosti **IAggregatePartner. Profiles** Získejte rozhraní do kolekce operací partnerského profilu.</span><span class="sxs-lookup"><span data-stu-id="148d7-118">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="148d7-119">Pak načtěte hodnotu vlastnosti **LegalBusinessProfile** a získejte rozhraní pro obchodní operace obchodních profilů.</span><span class="sxs-lookup"><span data-stu-id="148d7-119">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="148d7-120">Nakonec voláním metody [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) nebo [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) změněného objektu aktualizujete profil.</span><span class="sxs-lookup"><span data-stu-id="148d7-120">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="148d7-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="148d7-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="148d7-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="148d7-122">Request syntax</span></span>

| <span data-ttu-id="148d7-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="148d7-123">Method</span></span>  | <span data-ttu-id="148d7-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="148d7-124">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="148d7-125">**PUT**</span><span class="sxs-lookup"><span data-stu-id="148d7-125">**PUT**</span></span> | <span data-ttu-id="148d7-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="148d7-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="148d7-127">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="148d7-127">Request headers</span></span>

<span data-ttu-id="148d7-128">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="148d7-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="148d7-129">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="148d7-129">Request body</span></span>

<span data-ttu-id="148d7-130">Platný prostředek obchodního profilu.</span><span class="sxs-lookup"><span data-stu-id="148d7-130">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="148d7-131">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="148d7-131">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 806
Expect: 100-continue

{
    "CompanyName": "Lucerne Publishing",
    "Address": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": "Gena",
        "LastName": "Soto",
        "PhoneNumber": "4255550110"
    },
    "PrimaryContact": {
        "FirstName": "Gena",
        "LastName": "Soto",
        "Email": "gena@lucernepublishing.com",
        "PhoneNumber": "4255550110"
    },
    "CompanyApproverAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": null,
        "LastName": null,
        "PhoneNumber": null
    },
    "CompanyApproverEmail": "gena@lucernepublishing.com",
    "VettingStatus": "authorized",
    "VettingSubStatus": "none",
    "Links": {
        "Self": {
            "Uri": "/profiles/legalbusiness",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "LegalBusinessProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="148d7-132">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="148d7-132">REST response</span></span>

<span data-ttu-id="148d7-133">V případě úspěchu obsahuje tělo odpovědi aktualizované **LegalBusinessProfile**</span><span class="sxs-lookup"><span data-stu-id="148d7-133">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="148d7-134">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="148d7-134">Response success and error codes</span></span>

<span data-ttu-id="148d7-135">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="148d7-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="148d7-136">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="148d7-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="148d7-137">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="148d7-137">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="148d7-138">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="148d7-138">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1157
Content-Type: application/json; charset=utf-8
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CV: KZLU42qJ4EObO75q.0
MS-ServerId: 030020643
Date: Tue, 21 Mar 2017 22:03:15 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550110"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550110"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
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
