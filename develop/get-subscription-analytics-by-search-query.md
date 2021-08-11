---
title: Získání analýzy předplatného pomocí vyhledávacího dotazu
description: Jak získat analytické informace o předplatném filtrované podle vyhledávacího dotazu
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dc6ef8d2136c5ffac3278a372980e9a601ef49bb485ef54187865fc9431b3404
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995675"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Získání analytických informací o předplatných filtrovaných podle vyhledávacího dotazu

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat analytické informace o předplatném pro zákazníky filtrované pomocí vyhledávacího dotazu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů uživatele.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti |
|--------|-------------|
| **Dostat** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string} |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

Pomocí následujícího parametru požadované cesty identifikujte svou organizaci a vyfiltrujte hledání.

| Název | Typ | Vyžadováno | Popis |
|------|------|----------|-------------|
| filter_string | řetězec | Yes | Filtr, který se použije pro analýzu předplatného. Syntaxi, pole a operátory, které se mají použít v tomto parametru, najdete v částech Syntaxe filtru a Filtrovat pole. |

### <a name="filter-syntax"></a>Syntaxe filtru

Parametr filter se musí skládat jako řada kombinací polí, hodnot a operátorů. Pomocí operátorů nebo lze kombinovat **`and`** více **`or`** kombinací.

Nekódovaný příklad vypadá jako tento:

- Řetězec: `?filter=Field operator 'Value'`
- Boolean: `?filter=Field operator Value`
- Obsahuje `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Filtrování polí

Parametr filter požadavku obsahuje jeden nebo více příkazů, které filtruje řádky v odpovědi. Každý příkaz obsahuje pole a hodnotu, které jsou přidruženy k **`eq`** operátorům **`ne`** nebo . Některá pole také podporují **`contains`** operátory , **`gt`** , , **`lt`** a **`ge`** **`le`** . Příkazy lze kombinovat pomocí **`and`** operátorů **`or`** nebo .

Tady jsou příklady řetězců filtru:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

Následující tabulka obsahuje seznam podporovaných polí a operátorů podpory pro parametr filtru. Řetězcové hodnoty musí být v jednoduchých uvozovkách.

| Parametr | Podporované operátory | Description |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Hodnota, která určuje, jestli se předplatné obnovuje automaticky. |
| datum ukončení závazku | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Datum, kdy odběr skončí. |
| datum vytvoření | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Datum vytvoření předplatného |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum, kdy se změní aktuální stav předplatného. |
| customerMarket | `eq`, `ne` | Země nebo oblast, ve které zákazník obchoduje. |
| customerName | `contains` | Jméno zákazníka. |
| customerTenantId | `eq`, `ne` | Řetězec ve formátu GUID, který identifikuje tenanta zákazníka. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum, kdy bylo zrušeno zřízení předplatného. Výchozí hodnotou je hodnota null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum zahájení odběru |
| Friendlyname | `contains` | Název předplatného. |
| id | `eq`, `ne` | Řetězec formátovaný identifikátorem GUID, který identifikuje odběr. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum posledního prodloužení platnosti předplatného Výchozí hodnotou je hodnota null. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum posledního použití předplatného Výchozí hodnotou je hodnota null. |
| ID partnera | `eq`, `ne` | ID MPN. Pro přímého prodejce bude tato hodnota ID MPN partnera. Pro nepřímého prodejce bude tato hodnota ID MPN nepřímého prodejce. |
| název partnera | řetězec | Název partnera, pro kterého bylo předplatné zakoupeno |
| Productname | `contains`, `eq`, `ne` | Název produktu. |
| Providername | řetězec | Pokud je transakce předplatného zprostředkovatelem nepřímého prodejce, název poskytovatele je nepřímý poskytovatel, který předplatné zakoupil.|
| status | `eq`, `ne` | Stav předplatného Podporované hodnoty: AKTIVNÍ, POZASTAVENO nebo ZRUŠENO ZŘÍZENÍ. |
| typ předplatného | `eq`, `ne` | Typ předplatného. **Poznámka:** V tomto poli se rozlišují malá a velká písmena. Podporované hodnoty: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum zahájení zkušebního období předplatného Výchozí hodnotou je hodnota null. |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Datum převodu předplatného ze zkušební verze na placenou verzi. Výchozí hodnotou je hodnota null. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [předplatného](partner-center-analytics-resources.md#subscription-resource) , které splňují kritéria filtru.

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
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a>Viz také

- [Analýzy Partnerského centra – prostředky](partner-center-analytics-resources.md)
