---
title: Získá seznam aktuálních propagačních akcí pro segment nabídky a trh.
description: Získá seznam aktuálních propagačních akcí pro segment give a market.
ms.date: 09/24/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 0b9cc6ccdebbd641ab8b7dcd6cc5932c191d85ad
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715975"
---
# <a name="get-promotions"></a>Získání propagačních akcí

**Platí pro**

- Partnerské centrum

**Odpovídající role**

- Globální správce
- Agent pro správu

> [!Note] 
> Nové obchodní změny jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí Microsoft 365 Dynamics 365 a dynamics 365 technical preview.

Partneři mohou získat seznam aktivních nových propagačních akcí pro daný trh (zemi) a segment. Tato metoda vrátí dostupné aktuální propagační akce na základě dostupných počátečních a koncových dat propagačních akcí.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- Segment představuje typ zákazníka, pro který jsou propagační akce povolené. V současné době podporuje pouze komerční.

- Země představuje propagační akce zákazníků v jednotlivých zemích, pro které jsou k dispozici. Země je reprezentována kódem země se dvěma znaky.

## <a name="rest-request"></a>Požadavek REST
[GET] /v1/productpromotions?country={country-code}&segment={segment}

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **DOSTAT**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions?country={country-code}&segment={segment} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K vrácení dostupných propagačních akcí použijte následující parametry dotazu.

| Název                    | Typ     | Vyžadováno | Popis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Segmentu**  | **řetězec** | Y        | Řetězec, který určuje, která povýšení jsou k dispozici pro daný segment.           |
| **Země** | **řetězec** | Y        | Dvou písmeno kódu země určující, pro které propagační akce v zemi zákazníka jsou k dispozici. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [Partnerské centrum hlavičky REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions?country=US&segment=commercial HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí seznam povýšení.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď obsahuje stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. Ke čtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT


{
    "totalCount": 2,
    "items": [
        {
            "id": "39NFJQT1PJQB:0001:39NFJQT1Q5KN",
            "name": "Visio Plan 1",
            "description": "Visio Plan 1",
            "startDate": "2021-09-23T00:00:00+00:00",
            "endDate": "2021-10-14T23:59:59+00:00",
            "properties": {
                "isAutoApplicable": true
            },
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0HD33",
                    "skuId": "0003",
                    "term": {
                        "duration": "P1Y",
                        "billingCycle": "Annual"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.05"
                        }
                    ]
                }
            ]
        },
        {
            "id": "39NFJQT1PJQC:0001:39NFJQT1Q5KM",
            "name": "Vision Plan 1",
            "description": "Vision Plan 1",
            "startDate": "2021-09-23T00:00:00+00:00",
            "endDate": "2021-10-14T23:59:59+00:00",
            "properties": {
                "isAutoApplicable": true
            },
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0HD33",
                    "skuId": "0003",
                    "term": {
                        "duration": "P1Y",
                        "billingCycle": "Monthly"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.167"
                        }
                    ]
                }
            ]
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
