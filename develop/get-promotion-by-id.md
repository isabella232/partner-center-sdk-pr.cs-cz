---
title: Získá jedinou promoakci.
description: Získá jednu promoakci pro dané ID povýšení a zemi.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 9ed9171cd7bbe8a6d5202deb7cc6111bb76ec923
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715978"
---
# <a name="get-promotion-by-id"></a>Získat povýšení podle ID

**Platí pro**

- Partnerské centrum

**Příslušné role**

- Globální správce
- Agent správce

> [!Note] 
> nové obchodní změny jsou aktuálně k dispozici pouze partnerům, kteří jsou součástí Microsoft 365 a Dynamics 365 new Commerce experience technical preview.

Partneři můžou získat jednu promoakci pro dané ID povýšení a zemi. Tato metoda vrátí propagační data a ignoruje počáteční a koncové datum povýšení. Tato metoda se primárně používá pro účely odsouhlasení k načtení podrobností o povýšení i po vypršení platnosti povýšení.



## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID povýšení je oddělená sada řetězců, které reprezentují konkrétní povýšení.

- Země představuje propagační akce pro země zákazníka, které jsou k dispozici pro. Země je reprezentovaná pomocí dvou znakových kódů země.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions/{Promotion-ID}? Country = {Country-Code HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K vrácení dostupných propagačních akcí použijte následující parametry dotazu.

| Název                    | Typ     | Vyžadováno | Popis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **povýšení – ID**  | **řetězec** | Y        | Řetězec definující povýšení, která se má načíst           |
| **krajin** | **řetězec** | Y        | Číslo země, které určuje, pro kterou zákaznickou promoakci jsou k dispozici dvě písmena. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions/CFQ7TTC0HD33:0003:CFQ7TTC0K59M?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda jedinou promoakci.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo neúspěch a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 24 Sep 2021 20:42:26 GMT

 
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
        }
```
