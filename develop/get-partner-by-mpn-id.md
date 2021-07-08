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
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>Ověření ID MPN partnera prostřednictvím jazyka C \# nebo Partnerské centrum REST API

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Ověření identifikátoru MPN (MICROSOFT PARTNER NETWORK partnera)

Zde zobrazená technika ověří identifikátor Microsoft Partner Network tím, že si z Partnerského centra vyžádá profil MPN partnera. Identifikátor se považuje za platný, pokud je požadavek úspěšný.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID MPN partnera, které chcete ověřit. Pokud tuto hodnotu vynecháte, požadavek načte profil MPN přihlášených partnerů.

## <a name="c"></a>C\#

Pokud chcete ověřit ID MPN partnera, nejprve načtěte rozhraní pro operace shromažďování profilů partnerů z [**vlastnosti IAggregatePartner.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) Pak z vlastnosti [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) získejte rozhraní operací profilu MPN. Nakonec zavolejte metody [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) s ID MPN a načtěte profil MPN. Pokud vynecháte ID MPN z volání Get nebo GetAsync, požadavek se pokusí načíst profil MPN přihlášený partner.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **:** VerifyPartnerMpnId.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Zadejte následující parametr dotazu pro identifikaci partnera. Pokud tento parametr dotazu vynecháte, požadavek vrátí profil MPN přihlášených partnerů.

| Název   | Typ | Vyžadováno | Popis                                                 |
|--------|------|----------|-------------------------------------------------------------|
| id mpn | int  | No       | Id Microsoft Partner Network, které identifikuje partnera. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu bude tělo odpovědi obsahovat prostředek [MpnProfile](profile-resources.md#mpnprofile) pro partnera.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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

### <a name="response-example-failure"></a>Příklad odpovědi (selhání)

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
