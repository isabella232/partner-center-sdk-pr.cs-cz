---
title: Ověření předplatného pro migraci
description: Jak ověřit, jestli je předplatné vhodné pro migraci
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d085093b8adc3750d1b8d95963fc9d74c4209e00
ms.sourcegitcommit: 53980dc43fb2277878bf61a15a86013b8b1c2574
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/06/2021
ms.locfileid: "129609992"
---
# <a name="validate-a-subscription-for-migration"></a>Ověření předplatného pro migraci

**Platí pro:** Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Ověření předplatného pro migraci do nového komerčního prostředí

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte ID **Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID aktuálního předplatného

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
|**PŘÍSPĚVEK** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/migrations/nový obchod/ověření HTTP/1.1  |

### <a name="uri-parameter"></a>Parametr URI

Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro ověření předplatného pro migraci.

| Název               | Typ   | Vyžadováno | Popis                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| customer-tenant-id | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [Partnerské centrum hlavičky REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje [vlastnosti předplatného](subscription-resources.md) v textu požadavku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| currentSubscriptionId | řetězec           | Yes             | Identifikátor předplatného, který označuje, které předplatné vyžaduje ověření pro migraci.            |

### <a name="request-example"></a>Příklad požadavku

```http
"currentSubscriptionId" : "9beb6319-6889-4d28-a155-68ca9c783842"
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v textu odpovědi logickou hodnotu "isEligible", která označuje, jestli je aktuální předplatné vhodné pro migraci na nové obchodování.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-examples"></a>Příklady odpovědí

```http
1. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": false,
        "errors": [
            {
                "code": 5,
                "description": "Subscription cannot be migrated to New Commerce because the equivalent offer is not yet available in New Commerce",
            }
        ]
    }
```

```http
2. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": true,
        "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV"
    }
```
