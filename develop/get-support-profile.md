---
title: Získání profilu podpory
description: Získá objekt reprezentující profil podpory uživatele.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b8b0fa533aaba74418985ea02cbb13bd722cede2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767020"
---
# <a name="get-support-profile"></a>Získání profilu podpory

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Získá objekt reprezentující profil podpory uživatele.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="c"></a>C\#

Profil podpory získáte pomocí kolekce **IAggregatePartner. Profiles** . Zavolejte vlastnost [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) , za kterou následují metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) .

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: GetSupportProfile.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                              |
|---------|--------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/support HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí objekt **SupportProfile** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
Date: Wed, 25 Nov 2015 07:16:17 GMT

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
