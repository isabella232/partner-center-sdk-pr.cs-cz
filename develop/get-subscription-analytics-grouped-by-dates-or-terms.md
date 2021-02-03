---
title: Získání analýzy předplatných seskupených podle kalendářních dat nebo podmínek
description: Jak získat informace o analýze předplatného seskupené podle kalendářních dat nebo podmínek.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766768"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Získání analýzy předplatných seskupených podle kalendářních dat nebo podmínek

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak získat informace o analýze předplatných pro vaše zákazníky seskupené podle kalendářních dat nebo podmínek.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti |
|--------|-------------|
| **Čtěte** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? GroupBy = {groupby_queries} |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci vaší organizace a k seskupení výsledků použijte následující požadované parametry cesty.

| Název | Typ | Vyžadováno | Popis |
|------|------|----------|-------------|
| groupby_queries | páry řetězců a data a času | Yes | Termíny a data pro filtrování výsledku. |

### <a name="groupby-syntax"></a>Syntaxe GroupBy

Parametr Group by se musí skládat jako řada hodnot polí oddělených čárkou.

Nekódovaný příklad vypadá takto:

```http
?groupby=termField1,dateField1,termField2
```

V následující tabulce je uveden seznam podporovaných polí pro Group by.

| Pole | Typ | Description |
|-------|------|-------------|
| customerTenantId | řetězec | Řetězec ve formátu GUID, který identifikuje tenanta zákazníka. |
| customerName | řetězec | Jméno zákazníka. |
| customerMarket | řetězec | Země nebo oblast, ve které má zákazník obchodní oddělení |
| id | řetězec | Řetězec ve formátu GUID, který identifikuje odběr. |
| status | řetězec | Stav předplatného. Podporovány jsou následující hodnoty: "aktivní", "pozastaveno" nebo "zrušení zřízení". |
| NázevVýrobku | řetězec | Název produktu. |
| subscriptionType | řetězec | Typ předplatného. Poznámka: Toto pole rozlišuje velká a malá písmena. Podporované hodnoty jsou: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Logická hodnota | Hodnota, která označuje, jestli se předplatné obnovuje automaticky. |
| partnerId  | řetězec | ID MPN U přímého prodejce bude tento parametr ID MPN partnera. Pro nepřímý prodejce tento parametr bude ID MPN nepřímého prodejce. |
| friendlyName | řetězec | Název předplatného. |
| partnerName | řetězec | Název partnera, pro kterého se předplatné zakoupilo |
| providerName | řetězec | Pokud je transakce předplatného určena pro nepřímý prodejce, jméno poskytovatele je nepřímým poskytovatelem, který si zakoupil předplatné.
| creationDate | řetězec ve formátu data a času UTC | Datum vytvoření odběru. |
| effectiveStartDate | řetězec ve formátu data a času UTC | Datum, kdy se předplatné spustí. |
| commitmentEndDate | řetězec ve formátu data a času UTC | Datum ukončení předplatného |
| currentStateEndDate | řetězec ve formátu data a času UTC | Datum, kdy se změní aktuální stav předplatného. |
| trialToPaidConversionDate | řetězec ve formátu data a času UTC | Datum, kdy se předplatné převede ze zkušební verze na placené. Výchozí hodnotou je hodnota null. |
| trialStartDate | řetězec ve formátu data a času UTC | Datum, kdy se začalo zkušební období předplatného. Výchozí hodnotou je hodnota null. |
| lastUsageDate | řetězec ve formátu data a času UTC | Datum posledního použití předplatného Výchozí hodnotou je hodnota null. |
| deprovisionedDate | řetězec ve formátu data a času UTC | Datum zrušení zřízení předplatného. Výchozí hodnotou je hodnota null. |
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
