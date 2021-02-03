---
title: Aktualizace profilu podpory
description: Aktualizuje profil podpory uživatele.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 605c509eeb18f301144fec6287c9611d5a5acfe2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766949"
---
# <a name="update-support-profile"></a>Aktualizace profilu podpory

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Aktualizuje profil podpory uživatele.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="c"></a>C\#

Pokud chcete aktualizovat svůj profil podpory, nejdřív [Získejte svůj profil podpory](get-support-profile.md) a proveďte jakékoli změny, které chcete. Pak použijte svou kolekci [**IPartnerOperations. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) . Zavolejte vlastnost [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) , následovanou metodou [**Update ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) nebo [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) .

``` csharp
// IAggregatePartner partnerOperations;

// updated profile
SupportProfile newSupportProfile = new SupportProfile
{
   Email = supportProfile.Email,
   Website = supportProfile.Website,
   Telephone = new Random().Next(10000000, 99999999).ToString(CultureInfo.InvariantCulture)
};

SupportProfile updatedSupportProfile = partnerOperations.Profiles.SupportProfile.Update(newSupportProfile);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: UpdateSupportProfile.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                     |
|---------|---------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/supportprofile HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Prostředek profilu plné podpory.

### <a name="request-example"></a>Příklad požadavku

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/supportprofile HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
Content-Type: application/json
Content-Length: 167
Expect: 100-continue

{
    "Email": "email@sample.com",
    "Telephone": "4255555555",
    "Website": "www.microsoft.com",
    "ProfileType": "support_profile",
    "Attributes": {
        "ObjectType": "PartnerSupportProfile"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí aktualizované vlastnosti objektu **SupportProfile** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
Date: Wed, 25 Nov 2015 07:16:18 GMT

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
