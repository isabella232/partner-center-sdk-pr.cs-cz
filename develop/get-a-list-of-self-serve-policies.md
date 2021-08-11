---
title: Získat seznam zásad pro samoobslužné zpracování
description: Jak získat kolekci prostředků představujících samoobslužné zásady zákazníka.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ce217e34090d589c07a49cd51abef3f5cfc010631088890324a63bdef1480f65
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995522"
---
# <a name="get-a-list-of-self-serve-policies"></a>Získat seznam zásad pro samoobslužné zpracování

Získá kolekci prostředků, které představují samoobslužné zásady pro entitu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="c"></a>C\#

Získání seznamu všech samoobslužných zásad:

1. Voláním metody [**IAggregatePartner. SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) s identifikátorem entity načtěte rozhraní pro operace s těmito zásadami.

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

Příklad naleznete v následujících tématech:

- Ukázka: [aplikace testů konzoly](console-test-app.md)
- Project: **PartnerSDK. FeatureSamples**
- Třída: **GetSelfServePolicies. cs**

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy? entity_id = {ENTITY_ID} HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Chcete-li získat seznam zákazníků, použijte následující parametr dotazu.

| Název          | Typ       | Vyžadováno | Popis                                        |
|---------------|------------|----------|----------------------------------------------------|
| **entity_id** | **řetězec** | Y        | Identifikátor entity požadující přístup pro. Toto bude ID tenanta zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace naleznete v části [Headers](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí kolekci prostředků [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 1,
    "items": [{
        "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
        "selfServeEntity": {
            "selfServeEntityType": "customer",
            "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
        },
        "grantor": {
            "grantorType": "billToPartner",
            "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
        },
        "permissions": [{
            "resource": "AzureReservedInstances",
            "action": "Purchase"
        }],
        "attributes": {
            "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
            "objectType": "SelfServePolicy"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
