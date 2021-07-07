---
title: Odstranit nepřímý prodejce v izolovaném prostoru
description: Poskytuje informace o odstranění nepřímých prodejců izolovaného prostoru (sandbox) a povolení komplexního testování pomocí rozhraní API.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba1fd002ac62aba4e414d263b33ecc8153054602
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973005"
---
# <a name="delete-indirect-reseller-in-sandbox"></a>Odstranit nepřímý prodejce v izolovaném prostoru

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo

Tento dokument ukazuje, jak odstranit nepřímé poskytovatele izolovaného prostoru (sandbox) a jak povolit komplexní testování pomocí rozhraní API.

> [!Important]
> Tento dokument popisuje funkce, které jsou povoleny pouze v prostředí izolovaného prostoru pro prostředí nepřímých modelů.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a>Nepřímý poskytovatel izolovaného prostoru – odstranění nepřímého prodejce izolovaného prostoru 

Tato funkce je k dispozici pouze v izolovaném prostoru (sandbox) a poskytuje nepřímým poskytovatelům izolovaného prostoru možnost vytvářet nepřímé prodejce izolovaného prostoru.

1. Předpoklady pro odstranění nepřímého prodejce izolovaného prostoru
    1. Pozastavit odběry pro každého zákazníka nepřímého prodejce izolovaného prostoru
    2. Odstranit všechny zákazníky nepřímého prodejce
2. Limit pěti nepřímých prodejců v izolovaném prostoru (sandbox) povolených pro nepřímý poskytovatel izolovaného prostoru Po odstranění nepřímého prodejce izolovaného prostoru (sandbox) bude kvóta resetována.

## <a name="delete-sandbox-indirect-reseller-through-api"></a>Odstranění nepřímého prodejce izolovaného prostoru prostřednictvím rozhraní API

### <a name="rest-request"></a>Žádost REST

#### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti                                                                             |
|------------|-------------------------------------------------------------------------------------|
| **DSTRANIT** | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId} |

#### <a name="request-headers"></a>Hlavičky požadavku

- Toto rozhraní API se idempotentní (nepřinese se mu jiný výsledek, pokud ho zavoláte víckrát).
- Vyžaduje se ID žádosti a ID korelace.
- Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md) .

### <a name="request-example"></a>Příklad požadavku

DSTRANIT https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

Tato metoda vrací následující stavové kódy a chyby:

| Stavový kód HTTP                     | Kód chyby     | Description                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| 401                                  | 6002           | Neoprávněný token nebo účet poskytovatele tipů |
| 403                                  | 6003           | Odstranění izolovaného prostoru (sandbox) se nepovoluje.                 |
| 403                                  | 6004           | Operace vytvoření izolovaného prostoru (sandbox) není povolená.          |
| 409                                  | 1003           | Konflikt při vytváření tenanta                   |
