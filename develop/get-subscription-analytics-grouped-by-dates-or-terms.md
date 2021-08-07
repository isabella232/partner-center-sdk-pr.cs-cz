---
title: Získání analýz předplatného seskupených podle kalendářních dat nebo termínů
description: Jak získat analytické informace předplatného seskupené podle kalendářních dat nebo termínů
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66336d3e5573598eb4810853ad2704bc8d2c76680292a4f5b4a3da9bb50936b8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989674"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Získání analýz předplatného seskupených podle kalendářních dat nebo termínů

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat analytické informace o předplatném pro zákazníky seskupené podle kalendářních dat nebo podmínek.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů uživatele.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti |
|--------|-------------|
| **Dostat** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries} |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

Pomocí následujících požadovaných parametrů cesty identifikujte svou organizaci a seskupte výsledky.

| Název | Typ | Vyžadováno | Popis |
|------|------|----------|-------------|
| groupby_queries | dvojice řetězců a dateTime | Yes | Termíny a kalendářní data pro filtrování výsledku. |

### <a name="groupby-syntax"></a>Syntaxe GroupBy

Parametr seskupit podle se musí skládat jako řada hodnot polí oddělených čárkami.

Nekódovaný příklad vypadá jako tento:

```http
?groupby=termField1,dateField1,termField2
```

Následující tabulka obsahuje seznam podporovaných polí pro seskupení podle.

| Pole | Typ | Description |
|-------|------|-------------|
| customerTenantId | řetězec | Řetězec ve formátu GUID, který identifikuje tenanta zákazníka. |
| customerName | řetězec | Jméno zákazníka. |
| customerMarket | řetězec | Země nebo oblast, ve které zákazník obchoduje. |
| id | řetězec | Řetězec formátovaný identifikátorem GUID, který identifikuje odběr. |
| status | řetězec | Stav předplatného Podporované hodnoty: AKTIVNÍ, POZASTAVENO nebo ZRUŠENO ZŘÍZENÍ. |
| Productname | řetězec | Název produktu. |
| typ předplatného | řetězec | Typ předplatného. Poznámka: V tomto poli se rozlišují velká a malá písmena. Podporované hodnoty: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Logická hodnota | Hodnota, která určuje, jestli se předplatné obnovuje automaticky. |
| ID partnera  | řetězec | ID MPN. Pro přímého prodejce bude tento parametr ID MPN partnera. Pro nepřímého prodejce bude tento parametr ID MPN nepřímého prodejce. |
| Friendlyname | řetězec | Název předplatného. |
| název partnera | řetězec | Název partnera, pro kterého bylo předplatné zakoupeno |
| Providername | řetězec | Pokud je transakce předplatného zprostředkovatelem nepřímého prodejce, název poskytovatele je nepřímý poskytovatel, který předplatné zakoupil.
| datum vytvoření | řetězec ve formátu data a času UTC | Datum vytvoření předplatného |
| effectiveStartDate | řetězec ve formátu data a času UTC | Datum zahájení odběru |
| datum ukončení závazku | řetězec ve formátu data a času UTC | Datum, kdy odběr skončí. |
| currentStateEndDate | řetězec ve formátu data a času UTC | Datum, kdy se změní aktuální stav předplatného. |
| trialToPaidConversionDate | řetězec ve formátu data a času UTC | Datum převodu předplatného ze zkušební verze na placenou verzi. Výchozí hodnotou je hodnota null. |
| trialStartDate | řetězec ve formátu data a času UTC | Datum zahájení zkušebního období předplatného Výchozí hodnotou je hodnota null. |
| lastUsageDate | řetězec ve formátu data a času UTC | Datum posledního použití předplatného Výchozí hodnotou je hodnota null. |
| deprovisionedDate | řetězec ve formátu data a času UTC | Datum, kdy bylo zrušeno zřízení předplatného. Výchozí hodnotou je hodnota null. |
| lastRenewalDate | řetězec ve formátu data a času UTC | Datum poslední obnovy odběru Výchozí hodnotou je hodnota null. |

### <a name="filter-fields"></a>Filtrovat pole

V následující tabulce jsou uvedena volitelná pole filtru a jejich popisy:

| Pole | Typ |  Description |
|-------|------|--------------|
| top | int | Počet řádků dat, který má být vrácen v požadavku. Pokud hodnota není zadaná, maximální hodnota a výchozí hodnota jsou 10000. Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat. |
| Přeskočit | int | Počet řádků, které mají být v dotazu přeskočeny. Tento parametr použijte pro stránku s velkými datovými sadami. Například Top = 10000 a Skip = 0 načte prvních 10000 řádků dat, Top = 10000 a Skip = 10000 načte další 10000 řádků dat. |
| filter | řetězec | Jeden nebo více příkazů, které filtrují řádky v odpovědi. Každý příkaz filtru obsahuje název pole z textu odpovědi a hodnotu, která je přidružena k **`eq`** , **`ne`** nebo pro určitá pole **`contains`** operátor. Příkazy lze kombinovat pomocí operátoru **`and`** OR **`or`** . Řetězcové hodnoty musí být obklopeny jednoduchými uvozovkami v parametru Filter. Seznam polí, která lze filtrovat, a operátory, které jsou s těmito poli podporovány, naleznete v následující části. |
| aggregationLevel | řetězec | Určuje časový rozsah, pro který se mají načíst agregovaná data. Může to být jeden z následujících řetězců: **den**, **týden** nebo **měsíc**. Pokud hodnota není zadaná, výchozí hodnota je **DateRange**. **Poznámka**: Tento parametr platí pouze v případě, že je pole data předáno jako součást parametru GroupBy. |
| groupBy | řetězec | Příkaz, který aplikuje agregaci dat pouze na zadaná pole. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [předplatného](partner-center-analytics-resources.md#subscription-resource) seskupených podle zadaných podmínek a dat.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a>Viz také

[Analýzy Partnerského centra – prostředky](partner-center-analytics-resources.md)
