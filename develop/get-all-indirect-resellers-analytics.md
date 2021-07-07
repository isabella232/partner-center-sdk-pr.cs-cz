---
title: Získání všech analytických informací o nepřímých prodejcích
description: Jak získat analytické informace o všech nepřímých prodejcích
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 4252f5fcbbcb038f382408074c8fd6ede3fd1f58
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760738"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Získání všech analytických informací o nepřímých prodejcích

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat analytické informace o všech nepřímých prodejcích pro vaše zákazníky

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů uživatele.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti |
|---------|-------------|
| **Dostat** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Parametr                             | Typ     | Description                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | řetězec   | ID tenanta partnera, pro kterého chcete načíst data nepřímých prodejců. |
| id                                    | řetězec   | ID nepřímého prodejce                                                                 |
| name                                  | řetězec   | Název partnera, pro kterého chcete načíst data nepřímých prodejců.      |
| Trhu                                | řetězec   | Trh partnera, pro kterého chcete načíst data nepřímých prodejců.    |
| firstSubscriptionCreationDate         | řetězec ve formátu data a času UTC  | Datum vytvoření prvního předplatného, na základě kterého chcete načíst data nepřímých prodejců.  |
| latestSubscriptionCreationDate        | řetězec ve formátu data a času UTC  | Datum vytvoření nejnovějšího předplatného.                 |
| firstSubscriptionEndDate              | řetězec ve formátu data a času UTC  | Při prvním ukončení předplatného.                        |
| latestSubscriptionEndDate             | řetězec ve formátu data a času UTC  | Nejnovější datum ukončení libovolného předplatného                  |
| firstSubscriptionSuspendedDate        | string in UTC date time         | Při prvním pozastavení libovolného předplatného.                    |
| latestSubscriptionSuspendedDate       | řetězec ve formátu data a času UTC  | Nejnovější datum pozastavení libovolného předplatného              |
| firstSubscriptionDeprovisionedDate    | řetězec ve formátu data a času UTC  | Při prvním rušení zřízení libovolného předplatného.                |
| latestSubscriptionDeprovisionedDate   | řetězec ve formátu data a času UTC  | Nejnovější datum, kdy bylo zrušeno zřízení libovolného předplatného.          |
| subscriptionCount                     | double   | Počet předplatných pro všechny prodejce s přidanou hodnotou                                     |
| licenseCount                          | double   | Počet licencí pro všechny prodejce s přidanou hodnotou.                                         |
| indirectResellerCount                 | double   | Počet nepřímých prodejců                                                             |
|  top                                  | řetězec   | Počet řádků dat, které se v požadavku vrátí. Maximální hodnota a výchozí hodnota, pokud není zadaná, je 10 000. Pokud dotaz obsahuje více řádků, obsahuje text odpovědi další odkaz, který můžete použít k vyžádání další stránky dat.  |
| Přeskočit                                  | int      | Počet řádků, které se v dotazu přeskočí Tento parametr použijte k stránkování velkých datových sad. Například načte **`top=10000 and skip=0`** prvních 1 0000 řádků dat, načte dalších **`top=10000 and skip=10000`** 10 000 řádků dat atd.              |
| filter                                | řetězec   | Parametr *filter* požadavku obsahuje jeden nebo více příkazů, které filtruje řádky v odpovědi. Každý příkaz obsahuje pole a hodnotu, které jsou přidruženy k operátorům nebo , a příkazy **`eq`** **`ne`** lze kombinovat pomocí **`and`** nebo **`or`** . Můžete zadat následující pole:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Název*<br/>                *Trhu*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Příklad:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Příklad:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | řetězec    | Určuje časový rozsah, pro který se mají načíst agregovaná data. Může to být jeden z následujících řetězců: &quot; &quot; den, &quot; týden nebo &quot; měsíc &quot; &quot; . Pokud není zadán, výchozí hodnota je &quot; den &quot; .<br/><br/>                                 `aggregationLevel` se nepodporuje bez `aggregationLevel` . `aggregationLevel` platí pro všechna **pole data, která** jsou v objektu `aggregationLevel`                         |
| Orderby                              | řetězec    | Příkaz, který objednává hodnoty výsledných dat pro každou instalaci. Syntaxe je `...&orderby=field[order],field [order],...`. Parametr pole může být jeden z následujících řetězců:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;Jméno&quot;<br/>                &quot;Trhu&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   Parametr *order* je volitelný a může být nebo , pokud chcete pro každé pole zadat vzestupné nebo `asc` sestupné `desc` pořadí. Výchozí formát je `asc`.<br/><br/>    **Příklad:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| Groupby                              | řetězec    | Příkaz, který použije agregaci dat pouze na zadaná pole. Můžete zadat následující pole:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Název*<br/>                *Trhu*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 Vrácené řádky dat obsahují pole zadaná v `groupby` klauzuli a následující pole:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            Parametr `groupby` lze použít s `aggregationLevel` parametrem .<br/><br/>            **Příklad:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu obsahuje text odpovědi kolekci prostředků [nepřímých prodejců.](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

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
