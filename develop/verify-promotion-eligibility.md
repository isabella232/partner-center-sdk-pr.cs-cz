---
title: Ověření způsobilosti pro propagační akci
description: Ověří, jestli je transakce zákazníka způsobilá pro dané povýšení.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: ad3346ddca0438c0011e2c6fd03c3ec00b1a1fe3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715976"
---
# <a name="verify-promotion-eligibility"></a>Ověření způsobilosti pro povýšení

**Platí pro**

- Partnerské centrum

**Odpovídající role**

- Globální správce
- Agent pro správu

> [!Note] 
> Nové obchodní změny jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí Microsoft 365 Dynamics 365 a dynamics 365 technical preview.

Parters can verify whether a customer transaction is eligible for a given promotion. Tato metoda vrátí *hodnotu True,* pokud má transakce zákazníka nárok na dané povýšení. Partneři mohou před odesláním transakce ověřit způsobilost, aby se zajistilo, že se propagační akce použije.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- Nárok zahrnuje zakoupenou dostupnost skladové položky produktu, vyhodnocované ID povýšení, množství, dobu trvání období a fakturační cyklus transakce.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **PŘÍSPĚVEK**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/promotionEligibilities HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K vrácení dostupných propagačních akcí použijte následující parametry dotazu.

| Název                    | Typ     | Vyžadováno | Popis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Kódzákazníka**  | **řetězec** | Y        | Hodnota je ID tenanta zákazníka ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka.          |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [Partnerské centrum hlavičky REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tělo obsahuje kolekci PromotionEligibilitiesRequestItems. Tato tabulka popisuje vlastnosti [pro PromotionEligibilitiesRequestItem](promotion-resources.md#promotioneligibilitiesrequestitem).

| Vlastnost        | Typ             | Vyžadováno        | Popis                                                                                               |
|-----------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| catalogItemId   | řetězec           | Ano             | Identifikátor položky katalogu.                         |
| quantity        | int | Ano        | Počet licencí nebo instancí                 |
| termDuration    | DateTime         | Ano             | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou P1M (jeden měsíc), P1Y (jeden rok) a P3Y (tři roky).   |
| billingCycle    | řetězec | Ano     | Hodnota, která označuje typ fakturačního období.   |
| ID povýšení     | řetězec           | Ano             | Identifikátor položky povýšení.                       | 

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/46632f71-f052-4384-8f84-4cdb6c12c2a1/promotionEligibilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "promotionId": " CFQ7TTC0HL8W:0001:CFQ7TTC0K59M"
        }
    ]
}

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda kolekci výsledků způsobilosti.

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
    "totalCount": 1,
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "eligibilities": [
                {
                    "promotionId": "CFQ9TTC0HH4R:0001:CFQ8HGC0K77G",
                    "isEligible": false,
                    "errors": [
                        {
                            "type": "SeatCount",
                            "minRequiredSeats": 25,
                            "maxRequiredSeats": 500
                        },
                        {
                            "type": "Term",
                            "eligibleTerms": [
                                {
                                    "duration": "P3Y",
                                    "billingCycle": "Monthly"
                                }
                            ]
                        },
                        {
                            "type": "FirstPurchase"
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "PromotionEligibilities"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

