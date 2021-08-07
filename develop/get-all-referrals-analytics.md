---
title: Získání všech analytických informací o referencích
description: Jak získat analytické informace o všech referenčních odkazech
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 8fded9cc9d540fa1f7f3fcb38620c26b85c1c6032ef0176e9bd043943a425f65
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992717"
---
# <a name="get-all-referrals-analytics-information"></a>Získání všech analytických informací o referencích

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat analytické informace o všech referenčních odkazech pro vaše zákazníky.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů uživatele.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti |
|---------|-------------|
| **Dostat** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Parametr | Typ | Description |
|-----------|------|-------------|
| filter | řetězec | Vrátí data odpovídající pod podmínkě filtru.</br> **Příklad:**</br>  `.../referrals?filter=field eq 'value'` |
| Groupby | řetězec | Podporuje termíny i kalendářní data. Logika krátkého okruhu pro omezení počtu kbelíků</br> **Příklad:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | řetězec | Parametr *aggregationLevel* vyžaduje *parametr groupby*. Parametr *aggregationLevel* se vztahuje na všechna pole data, která jsou v *groupby*.</br> **Příklad:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | řetězec | Limit stránky je 10 000. Přebírá libovolnou hodnotu menší než 1 0000.</br> **Příklad:**</br> `.../referrals?top=100`</br> |
| Přeskočit | řetězec | Počet řádků k přeskočení</br> **Příklad:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu bude text odpovědi obsahovat kolekci prostředků [referenčních](partner-center-analytics-resources.md#referrals-resource) seznamů.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

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
