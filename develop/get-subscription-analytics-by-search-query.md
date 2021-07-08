---
title: Získat analýzy předplatných pomocí vyhledávacího dotazu
description: Jak získat informace o analýze předplatného filtrované vyhledávacím dotazem.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8df777b9a88206f8b22579f0f445c54d80f7cd64
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548732"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Získání analytických informací o předplatných filtrovaných podle vyhledávacího dotazu

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat informace o analýze předplatných pro zákazníky filtrované pomocí vyhledávacího dotazu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti |
|--------|-------------|
| **Čtěte** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? Filter = {filter_string} |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

Pomocí následujícího parametru cesty Identifikujte vaši organizaci a filtrujte hledání.

| Název | Typ | Vyžadováno | Popis |
|------|------|----------|-------------|
| filter_string | řetězec | Yes | Filtr, který se má použít pro analýzu předplatného Viz část filtru a pole filtru pro syntaxi, pole a operátory pro použití v tomto parametru. |

### <a name="filter-syntax"></a>Syntaxe filtru

Parametr Filter musí být složen jako řada kombinací polí, hodnot a operátorů. Více kombinací lze kombinovat pomocí **`and`** **`or`** operátorů or.

Nekódovaný příklad vypadá takto:

- Řetezce `?filter=Field operator 'Value'`
- Datového `?filter=Field operator Value`
- Zobrazí `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Filtrovat pole

Parametr filtru požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi. Každý příkaz obsahuje pole a hodnotu, která je spojena s **`eq`** **`ne`** operátory OR. Některá pole také podporují **`contains`** operátory, **`gt`** ,, a **`lt`** **`ge`** **`le`** . Příkazy lze kombinovat pomocí **`and`** **`or`** operátorů or.

Následují příklady řetězců filtru:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

V následující tabulce je uveden seznam podporovaných polí a operátorů podpory pro parametr Filter. Řetězcové hodnoty musí být obklopeny jednoduchými uvozovkami.

| Parametr | Podporované operátory | Description |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Hodnota, která označuje, jestli se předplatné obnovuje automaticky. |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Datum ukončení předplatného |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Datum vytvoření odběru. |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum, kdy se změní aktuální stav předplatného. |
| customerMarket | `eq`, `ne` | Země nebo oblast, ve které má zákazník obchodní oddělení |
| customerName | `contains` | Jméno zákazníka. |
| customerTenantId | `eq`, `ne` | Řetězec ve formátu GUID, který identifikuje tenanta zákazníka. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum zrušení zřízení předplatného. Výchozí hodnotou je hodnota null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum, kdy se předplatné spustí. |
| friendlyName | `contains` | Název předplatného. |
| id | `eq`, `ne` | Řetězec ve formátu GUID, který identifikuje odběr. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum poslední obnovy odběru Výchozí hodnotou je hodnota null. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum posledního použití předplatného Výchozí hodnotou je hodnota null. |
| partnerId | `eq`, `ne` | ID MPN U přímého prodejce bude tato hodnota ID MPN partnera. Pro nepřímý prodejce bude tato hodnota ID MPN nepřímého prodejce. |
| partnerName | řetězec | Název partnera, pro kterého se předplatné zakoupilo |
| NázevVýrobku | `contains`, `eq`, `ne` | Název produktu. |
| providerName | řetězec | Pokud je transakce předplatného určena pro nepřímý prodejce, jméno poskytovatele je nepřímým poskytovatelem, který si zakoupil předplatné.|
| status | `eq`, `ne` | Stav předplatného. Podporovány jsou následující hodnoty: "aktivní", "pozastaveno" nebo "zrušení zřízení". |
| subscriptionType | `eq`, `ne` | Typ předplatného. **Poznámka**: Toto pole rozlišuje velká a malá písmena. podporované hodnoty jsou: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Datum, kdy se začalo zkušební období předplatného. Výchozí hodnotou je hodnota null. |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Datum, kdy se předplatné převede ze zkušební verze na placené. Výchozí hodnotou je hodnota null. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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
