---
title: Načtení seznamu nepřímých prodejců
description: Jak načíst seznam nepřímých prodejců partnera, který je přihlášený.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e53237b97fa26d3a987f0ee7de491084b596af4a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767013"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Načtení seznamu nepřímých prodejců

**Platí pro**

- Partnerské centrum

Jak načíst seznam nepřímých prodejců partnera, který je přihlášený.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="c"></a>C\#

Chcete-li načíst seznam nepřímých prodejců, se kterými má přihlášený partner relaci, nejprve získejte rozhraní pro operace shromažďování relací z vlastnosti [**partnerOperations. relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) . Pak zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) nebo [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) , předáním členu výčtu [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) Identifikujte typ vztahu. K načtení nepřímých prodejců musíte použít IsIndirectCloudSolutionProviderOf.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Ukázka**:**projekt** [aplikace testů konzoly](console-test-app.md): ukázkové **třídy** SDK pro partnerských Center: GetIndirectResellers.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Relationships? \_ typ vztahu = IsIndirectCloudSolutionProviderOf HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci typu vztahu použijte následující parametr dotazu.

| Název               | Typ    | Vyžadováno  | Popis                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | řetězec  | Yes       | Hodnota je řetězcová reprezentace jednoho z názvů členů nalezených v [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).<br/><br/> Pokud je partner přihlášený jako poskytovatel a chcete získat seznam nepřímých prodejců, se kterými navázali relaci, použijte IsIndirectCloudSolutionProviderOf.<br/><br/> Pokud je partner přihlášený jako prodejce a chcete získat seznam nepřímých zprostředkovatelů, se kterými navázali relaci, použijte IsIndirectResellerOf.    |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [PartnerRelationship](relationships-resources.md) k identifikaci prodejců.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```