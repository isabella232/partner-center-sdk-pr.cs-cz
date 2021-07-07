---
title: Načtení seznamu nepřímých prodejců
description: Jak načíst seznam nepřímých prodejců přihlášených partnerů.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 58f5c3378b5b941fdc9dafcf28f5efbc58c29c7c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446560"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Načtení seznamu nepřímých prodejců

Jak načíst seznam nepřímých prodejců přihlášených partnerů.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

## <a name="c"></a>C\#

Pokud chcete načíst seznam nepřímých prodejců, se kterými má přihlášený partner vztah, nejprve z vlastnosti [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) získejte rozhraní pro operace shromažďování relací. Potom zavolejte [**metodu Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) nebo [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) a předáte člena výčtu [**PartnerRelationshipType,**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) abyste identifikovali typ vztahu. Pokud chcete načíst nepřímé prodejce, musíte použít IsIndirectCloudSolutionProviderOf.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md)**Project:** SDK pro Partnerské centrum Samples **Class:** GetIndirectResellers.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship \_ type=IsIndirectCloudSolutionProviderOf HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Pomocí následujícího parametru dotazu identifikujte typ relace.

| Název               | Typ    | Vyžadováno  | Popis                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | řetězec  | Yes       | Hodnota je řetězcová reprezentace jednoho z názvů členů nalezených v [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).<br/><br/> Pokud je partner přihlášený jako poskytovatel a chcete získat seznam nepřímých prodejců, se kterými navázal vztah, použijte IsIndirectCloudSolutionProviderOf.<br/><br/> Pokud je partner přihlášený jako prodejce a chcete získat seznam nepřímých poskytovatelů, se kterými se na navázat vztah, použijte IsIndirectResellerOf.    |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu obsahuje text odpovědi kolekci prostředků [PartnerRelationship,](relationships-resources.md) které identifikují prodejce.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

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