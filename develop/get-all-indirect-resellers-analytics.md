---
title: Získání všech analytických informací o nepřímých prodejcích
description: Jak získat všechny informace o analýze nepřímých prodejců.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 9f9c030278ba8fef9090f7be89064ac6054129ef
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766899"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Získání všech analytických informací o nepřímých prodejcích

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak získat všechny nepřímé informace o proprodejci pro vaše zákazníky.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti |
|---------|-------------|
| **Čtěte** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/indirectresellers HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Parametr                             | Typ     | Description                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | řetězec   | ID tenanta partnera, pro který chcete načíst data nepřímých prodejců. |
| id                                    | řetězec   | ID nepřímého prodejce                                                                 |
| name                                  | řetězec   | Název partnera, pro který chcete načíst data nepřímých prodejců.      |
| uvádět                                | řetězec   | Trh partnera, pro který chcete načíst data nepřímých prodejců.    |
| firstSubscriptionCreationDate         | řetězec ve formátu data a času UTC  | Datum vytvoření prvního předplatného, na základě kterého chcete načíst data nepřímých prodejců.  |
| latestSubscriptionCreationDate        | řetězec ve formátu data a času UTC  | Datum vytvoření posledního předplatného.                 |
| firstSubscriptionEndDate              | řetězec ve formátu data a času UTC  | První ukončení předplatného.                        |
| latestSubscriptionEndDate             | řetězec ve formátu data a času UTC  | Poslední datum, kdy bylo ukončeno nějaké předplatné.                  |
| firstSubscriptionSuspendedDate        | řetězec v hodnotě data a času UTC         | Při prvním pozastavení předplatného.                    |
| latestSubscriptionSuspendedDate       | řetězec ve formátu data a času UTC  | Poslední datum, kdy se nějaké předplatné pozastavilo.              |
| firstSubscriptionDeprovisionedDate    | řetězec ve formátu data a času UTC  | Při prvním zrušení zřízení předplatného.                |
| latestSubscriptionDeprovisionedDate   | řetězec ve formátu data a času UTC  | Poslední datum, kdy bylo zrušeno zřízení nějakého předplatného.          |
| subscriptionCount                     | double   | Počet předplatných pro všechny přidané hodnoty pro prodejce                                     |
| licenseCount                          | double   | Počet licencí pro všechny přidané hodnoty pro prodejce.                                         |
| indirectResellerCount                 | double   | Počet nepřímých prodejců                                                             |
|  top                                  | řetězec   | Počet řádků dat, který má být vrácen v požadavku. Maximální hodnota a výchozí hodnota, pokud není zadána, je 10000. Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat.  |
| Přeskočit                                  | int      | Počet řádků, které mají být v dotazu přeskočeny. Tento parametr použijte pro stránku s velkými datovými sadami. Například **`top=10000 and skip=0`** načte první 10000 řádků dat, **`top=10000 and skip=10000`** načte další 10000 řádků dat a tak dále.              |
| filter                                | řetězec   | Parametr *filtru* požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi. Každý příkaz obsahuje pole a hodnotu, které jsou spojeny s **`eq`** **`ne`** operátory nebo, a příkazy lze kombinovat pomocí operátoru OR **`and`** **`or`** . Můžete zadat následující pole:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Název*<br/>                *uvádět*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Příklad:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Příklad:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | řetězec    | Určuje časový rozsah, pro který se mají načíst agregovaná data. Může to být jeden z následujících řetězců: &quot; den &quot; , &quot; týden &quot; nebo &quot; měsíc &quot; . Je-li tento parametr zadán, výchozí hodnota je &quot; Day &quot; .<br/><br/>                                 `aggregationLevel` není podporován bez `aggregationLevel` . `aggregationLevel` platí pro všechny **datefields** přítomné v `aggregationLevel`                         |
| OrderBy                              | řetězec    | Příkaz, který seřadí hodnoty výsledných dat pro každou instalaci. Syntaxe je `...&orderby=field[order],field [order],...`. Parametr Field může být jeden z následujících řetězců:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;Jméno&quot;<br/>                &quot;uvádět&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   Parametr *Order* je volitelný a může být `asc` nebo `desc` ; k určení vzestupného nebo sestupného pořadí pro každé pole. Výchozí formát je `asc`.<br/><br/>    **Příklad:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| GroupBy                              | řetězec    | Příkaz, který aplikuje agregaci dat pouze na zadaná pole. Můžete zadat následující pole:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Název*<br/>                *uvádět*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 Vrácené řádky dat obsahují pole zadaná v `groupby` klauzuli a následující pole:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            `groupby`Parametr lze použít s `aggregationLevel` parametrem.<br/><br/>            **Příklad:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci [nepřímých prodejců](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) prostředků.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## <a name="see-also"></a>Viz také

- [Analýzy Partnerského centra – prostředky](partner-center-analytics-resources.md)
