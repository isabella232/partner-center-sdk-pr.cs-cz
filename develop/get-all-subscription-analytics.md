---
title: Získání všech analytických informací o předplatných
description: Jak získat všechny analytické informace o předplatném
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e1f16c92569a02bc51c96a85ecb642fbeb76a9a7
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760245"
---
# <a name="get-all-subscription-analytics-information"></a>Získání všech analytických informací o předplatných

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak získat všechny analytické informace o předplatném pro vaše zákazníky.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů uživatele.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti |
|--------|-------------|
| **Dostat** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Následující tabulka uvádí volitelné parametry a jejich popisy:

| Parametr | Typ |  Description |
|-----------|------|--------------|
| top | int | Počet řádků dat, které se v požadavku vrátí. Pokud hodnota není zadaná, maximální a výchozí hodnota jsou `10000` . Pokud dotaz obsahuje více řádků, obsahuje text odpovědi další odkaz, který můžete použít k vyžádání další stránky dat. |
| Přeskočit | int | Počet řádků, které se v dotazu přeskočí Tento parametr použijte k stránkování velkých datových sad. Například a načte prvních 10 000 řádků dat a načte dalších `top=10000` `skip=0` `top=10000` `skip=10000` 1 0000 řádků dat. |
| filter | řetězec | Jeden nebo více příkazů, které filtruje řádky v odpovědi. Každý příkaz filtru obsahuje název pole z textu odpovědi a hodnotu přidruženou k operátoru , nebo pro **`eq`** **`ne`** určitá **`contains`** pole. Příkazy lze kombinovat pomocí **`and`** nebo **`or`** . Řetězcové hodnoty musí být v parametru filtru v jednoduchých **uvozovkách.** V následující části najdete seznam polí, která lze filtrovat, a operátory, které jsou u těchto polí podporovány. |
| aggregationLevel | řetězec | Určuje časový rozsah, pro který se mají načíst agregovaná data. Může to být jeden z následujících řetězců: **den,** **týden** nebo **měsíc**. Pokud hodnota není zadaná, výchozí hodnota je **dateRange**. Tento parametr platí pouze v případě, že je pole data předáno jako součást **parametru groupBy.** |
| Groupby | řetězec | Příkaz, který použije agregaci dat pouze na zadaná pole. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu bude text odpovědi obsahovat kolekci prostředků [**předplatného.**](partner-center-analytics-resources.md#subscription-resource)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

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
