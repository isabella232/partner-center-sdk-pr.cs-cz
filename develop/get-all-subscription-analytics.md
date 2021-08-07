---
title: Získání všech analytických informací o předplatných
description: Jak získat všechny informace o analýze předplatných.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 5c93f36491851be11c700388201443f2e951122e4129786abc3e064091605b8d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992598"
---
# <a name="get-all-subscription-analytics-information"></a>Získání všech analytických informací o předplatných

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak získat všechny informace o analýze předplatného pro vaše zákazníky.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti |
|--------|-------------|
| **Čtěte** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

V následující tabulce jsou uvedeny volitelné parametry a jejich popisy:

| Parametr | Typ |  Description |
|-----------|------|--------------|
| top | int | Počet řádků dat, který má být vrácen v požadavku. Pokud hodnota není zadaná, maximální hodnota a výchozí hodnota je `10000` . Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat. |
| Přeskočit | int | Počet řádků, které mají být v dotazu přeskočeny. Tento parametr použijte pro stránku s velkými datovými sadami. Například `top=10000` `skip=0` načte první 10000 řádků dat a `top=10000` `skip=10000` načte další 10000 řádků dat. |
| filter | řetězec | Jeden nebo více příkazů, které filtrují řádky v odpovědi. Každý příkaz filtru obsahuje název pole z textu odpovědi a hodnotu, která je přidružena k **`eq`** , **`ne`** nebo pro určitá pole **`contains`** operátor. Příkazy lze kombinovat pomocí operátoru **`and`** OR **`or`** . Řetězcové hodnoty musí být obklopeny jednoduchými uvozovkami v parametru **Filter** . Seznam polí, která lze filtrovat, a operátory, které jsou s těmito poli podporovány, naleznete v následující části. |
| aggregationLevel | řetězec | Určuje časový rozsah, pro který se mají načíst agregovaná data. Může to být jeden z následujících řetězců: **den**, **týden** nebo **měsíc**. Pokud hodnota není zadaná, výchozí hodnota je **DateRange**. Tento parametr platí pouze v případě, že je pole data předáno jako součást parametru **GroupBy** . |
| groupBy | řetězec | Příkaz, který aplikuje agregaci dat pouze na zadaná pole. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [**předplatného**](partner-center-analytics-resources.md#subscription-resource) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a>Viz také

- [Analýzy Partnerského centra – prostředky](partner-center-analytics-resources.md)
