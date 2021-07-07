---
title: Získání všech analytických informací o hledání
description: Jak získat všechny informace o analýze vyhledávání.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e789a013b01fb63a38c72f4fe94864ecf21f7e4b
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760160"
---
# <a name="get-all-search-analytics-information"></a>Získání všech analytických informací o hledání

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat všechny informace o analýze vyhledávání pro vaše zákazníky.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti |
|---------|-------------|
| **Čtěte** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Search HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

|    Parametr     |  Typ  |                                                                                                                   Description                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter      | řetězec |                                                                     Vrátí data, která odpovídají podmínkám filtru. </br> **Příklad:**</br> `.../search?filter=field eq 'value'`                                                                     |
|     GroupBy      | řetězec |                                         Podporuje termíny i data. Logika krátkého okruhu pro omezení počtu kontejnerů. </br> **Příklad:**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | řetězec | Parametr *aggregationLevel* vyžaduje *GroupBy*. Parametr *aggregationLevel* se vztahuje na všechna pole kalendářních dat přítomná v *GroupBy*. </br> **Příklad:**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | řetězec |                                                                     Limit stránky je 10000. Má libovolnou hodnotu menší než 10000.  </br> **Příklad:**</br>  `.../search?top=100`                                                                     |
|       Přeskočit       | řetězec |                                                                                  Počet řádků, které se mají přeskočit </br> **Příklad:**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [vyhledávání](partner-center-analytics-resources.md#search-resource) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a>Viz také

- [Analýzy Partnerského centra – prostředky](partner-center-analytics-resources.md)
