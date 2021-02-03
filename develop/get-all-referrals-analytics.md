---
title: Získání všech analytických informací o referencích
description: Jak získat všechny analytické informace o odkazech.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766778"
---
# <a name="get-all-referrals-analytics-information"></a>Získání všech analytických informací o referencích

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak získat všechny informace o analýze odkazů pro vaše zákazníky.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti |
|---------|-------------|
| **Čtěte** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Referrals HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Parametr | Typ | Description |
|-----------|------|-------------|
| filter | řetězec | Vrátí data, která odpovídají podmínkám filtru.</br> **Příklad:**</br>  `.../referrals?filter=field eq 'value'` |
| GroupBy | řetězec | Podporuje termíny i data. Logika krátkého okruhu pro omezení počtu kontejnerů.</br> **Příklad:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | řetězec | Parametr *aggregationLevel* vyžaduje *GroupBy*. Parametr *aggregationLevel* se vztahuje na všechna pole kalendářních dat přítomná v *GroupBy*.</br> **Příklad:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | řetězec | Limit stránky je 10000. Má libovolnou hodnotu menší než 10000.</br> **Příklad:**</br> `.../referrals?top=100`</br> |
| Přeskočit | řetězec | Počet řádků, které se mají přeskočit</br> **Příklad:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [odkazů](partner-center-analytics-resources.md#referrals-resource) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a>Viz také

- [Analýzy Partnerského centra – prostředky](partner-center-analytics-resources.md)
