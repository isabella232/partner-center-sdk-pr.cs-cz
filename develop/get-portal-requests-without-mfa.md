---
title: Získání požadavků na portál bez MFA
description: Získejte seznam uživatelských požadavků bez vícefaktorového ověřování (MFA) pomocí REST API partnera.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: fd350aa3301f00926942ae6c6af359b0d0edc423
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766776"
---
# <a name="get-portal-requests-without-mfa"></a>Získání požadavků na portál bez MFA

Platí pro:

- Rozhraní API partnerského centra

Tento článek vysvětluje, jak získat seznam nejaktuálnějších požadavků od uživatelů, kteří přistupují k portálu partnerského centra bez dokončení vícefaktorového ověřování (MFA).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                  |
|---------|--------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals |

### <a name="request-headers"></a>Hlavičky požadavku

- Další informace najdete v tématu [záhlaví REST v partnerském centru](headers.md) .

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

V případě úspěchu tato metoda vrátí kolekci prostředků [žádosti portálu](mfa-resources.md#portal-request-without-mfa) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

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
