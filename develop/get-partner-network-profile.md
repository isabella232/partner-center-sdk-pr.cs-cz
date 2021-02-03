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
# <a name="get-microsoft-partner-network-profile"></a>Získání profilu programu Microsoft Partner Network

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Získá objekt reprezentující profil MPN partnera.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="c"></a>C\#

Pokud chcete získat profil partnerské sítě, použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **MpnProfile** . Nakonec zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) .

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**:P Artnercentersdk. FeaturesSamples **Třída**: GetMPNProfile.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pokud chcete získat profil partnerské sítě, použijte funkci **IAggregatePartner. Getprofiles** a zavolejte funkci **getMpnProfile** . Nakonec zavolejte funkci **Get ()** .

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pokud chcete získat profil partnerské sítě, spusťte příkaz [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) .

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                          |
|---------|----------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí objekt **MPNProfile** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

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
