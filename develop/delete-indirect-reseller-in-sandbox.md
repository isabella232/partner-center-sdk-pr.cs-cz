---
title: Odstranění nepřímého prodejce v Sandboxu
description: Poskytuje informace o odstraňování nepřímých prodejců sandboxu a povolení koncového testování pomocí rozhraní API.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 708fedd4e34b2242aae6e6e0ac673ce77524d448dcee4a05877d37b5266e44c8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994927"
---
# <a name="delete-indirect-reseller-in-sandbox"></a>Odstranění nepřímého prodejce v Sandboxu

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud (Německo)

Tento dokument ukazuje, jak odstranit nepřímé poskytovatele sandboxu a povolit koncové testování pomocí rozhraní API.

> [!Important]
> Tento dokument popisuje funkce, které jsou povolené jenom v prostředí sandboxu pro prostředí nepřímých modelů.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a>Nepřímý poskytovatel sandboxu – Odstranění nepřímého prodejce sandboxu 

Tato funkce je dostupná jenom v sandboxu a dává nepřímým poskytovatelům sandboxu možnost vytvářet nepřímé prodejce sandboxu.

1. Požadavky na odstranění nepřímého prodejce sandboxu
    1. Pozastavení předplatných pro každého zákazníka nepřímého prodejce sandboxu
    2. Odstranění všech zákazníků nepřímého prodejce
2. Povolený limit pěti nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu. Po odstranění nepřímého prodejce sandboxu se kvóta resetuje.

## <a name="delete-sandbox-indirect-reseller-through-api"></a>Odstranění nepřímého prodejce sandboxu prostřednictvím rozhraní API

### <a name="rest-request"></a>Požadavek REST

#### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti                                                                             |
|------------|-------------------------------------------------------------------------------------|
| **Odstranit** | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId} |

#### <a name="request-headers"></a>Hlavičky požadavku

- Toto rozhraní API je idempotentní (pokud ho zavoláte vícekrát, nepřidá jiný výsledek).
- Vyžaduje se ID požadavku a ID korelace.
- Další informace najdete v tématu [Partnerské centrum hlavičky REST.](headers.md)

### <a name="request-example"></a>Příklad požadavku

Odstranit https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}

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

#### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď obsahuje stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

Tato metoda vrátí následující stavové kódy úspěchů a chyb:

| Stavový kód HTTP                     | Kód chyby     | Description                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| 401                                  | 6002           | Neautorizovaný token nebo účet poskytovatele tipů |
| 403                                  | 6003           | Odstranění sandboxu IR není povolené                 |
| 403                                  | 6004           | Operace vytvoření sandboxu IR není povolená          |
| 409                                  | 1003           | Konflikt při vytváření tenanta                   |
