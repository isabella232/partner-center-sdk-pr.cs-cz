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
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>Ověření ID MPN partnera prostřednictvím jazyka C \# nebo partnerského centra REST API

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak ověřit identifikátor Microsoft Partner Network partnera (ID MPN)

Zde uvedená technika ověří identifikátor Microsoft Partner Network partnera tím, že požádá o profil MPN partnera z partnerského centra. Identifikátor se považuje za platný, pokud je požadavek úspěšný.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID MPN partnera, který se má ověřit Pokud tuto hodnotu vynecháte, požadavek načte profil MPN pro přihlášeného partnera.

## <a name="c"></a>C\#

Pokud chcete ověřit ID MPN partnera, nejdřív načtěte rozhraní pro operace shromažďování profilů partnerů z vlastnosti [**IAggregatePartner. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) . Pak z vlastnosti [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) Získejte rozhraní pro operace s profilem MPN. Nakonec voláním metod [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) nebo [**GETASYNC**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) s ID MPN načtěte profil MPN. Pokud z volání Get nebo GetAsync vynecháte ID MPN, požadavek se pokusí načíst profil MPN přihlášeného partnera.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: VerifyPartnerMpnId.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN? mpnId = {MPN-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Zadejte následující parametr dotazu pro identifikaci partnera. Pokud tento parametr dotazu vynecháte, požadavek vrátí profil MPN pro přihlášeného partnera.

| Název   | Typ | Vyžadováno | Popis                                                 |
|--------|------|----------|-------------------------------------------------------------|
| MPN – ID | int  | No       | ID Microsoft Partner Network, které identifikuje partnera. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

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

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi prostředek [MpnProfile](profile-resources.md#mpnprofile) pro partnera.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example-success"></a>Příklad odpovědi (úspěch)

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

### <a name="response-example-failure"></a>Příklad odpovědi (neúspěch)

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
