---
title: Získání požadavků na portál bez MFA
description: Seznam uživatelských požadavků bez vícefaktorového ověřování (MFA) získáte pomocí partnerského REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: d7d901bc78f889593612f64d28e465737f764ba711e49419444de6971c56d404
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995777"
---
# <a name="get-portal-requests-without-mfa"></a>Získání požadavků na portál bez MFA

Tento článek vysvětluje, jak získat seznam nejnovějších požadavků od uživatelů, kteří přistupují k portálu Partnerské centrum, aniž by se dokončilo vícefaktorové ověřování (MFA).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                  |
|---------|--------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals |

### <a name="request-headers"></a>Hlavičky požadavku

- Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí kolekci prostředků [požadavku portálu](mfa-resources.md#portal-request-without-mfa) v textu odpovědi.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

``` http
HTTP/1.1 200 OK
Content-Length: 296
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 23 Apr 2020 22:10:30 GMT
{
    "totalCount": 1,
    "items": [
        {
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "lastNonMfaCompliantRequestDateTime": "2020-04-21T22:09:53.051"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
