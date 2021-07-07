---
title: Získání všech analytických informací o využití Azure
description: Jak získat všechny informace o analýze využití Azure
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 7fe987c7dc50d55b26cd72d5aead52963eb1cfbe
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760211"
---
# <a name="get-all-azure-usage-analytics-information"></a>Získání všech analytických informací o využití Azure

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat všechny informace o analýze využití Azure pro vaše zákazníky.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti |
|---------|-------------|
| **Čtěte** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Usage/Azure HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

|Parametr        |Typ                        |Description               |
|:----------------|:---------------------------|:-------------------------|
|top              | řetězec                     | Počet řádků dat, který má být vrácen v požadavku. Maximální hodnota a výchozí hodnota, pokud není zadána, je 10000. Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat.                        |
|Přeskočit             | int                        | Počet řádků, které mají být v dotazu přeskočeny. Tento parametr použijte pro stránku s velkými datovými sadami. Například `top=10000 and skip=0` načte první 10000 řádků dat, `top=10000 and skip=10000` načte další 10000 řádků dat a tak dále.                       |
|filter           | řetězec                     | Parametr *filtru* požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi. Každý příkaz obsahuje pole a hodnotu, které jsou spojeny s `eq` `ne` operátory nebo, a příkazy lze kombinovat pomocí operátoru OR `and` `or` . Můžete zadat následující řetězce:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Příklad:**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Příklad:**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | řetězec                    | Určuje časový rozsah, pro který se mají načíst agregovaná data. Může to být jeden z následujících řetězců: `day` , `week` , nebo `month` . Je-li tento parametr zadán, je použita výchozí hodnota `day` .<br/><br/>                                              `aggregationLevel`Parametr není podporován bez `groupby` . `aggregationLevel`Parametr platí pro všechna pole kalendářních dat přítomná v `groupby` .                                                      |
|OrderBy          |řetězec                     | Příkaz, který seřadí hodnoty výsledných dat pro každou instalaci. Syntaxe je `...&orderby=field [order],field [order],...`. `field`Parametr může být jeden z následujících řetězců:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> Parametr *Order* je volitelný a může být `asc` nebo `desc` určen pro každé pole ve vzestupném nebo sestupném pořadí. Výchozí formát je `asc`.<br/><br/>**Příklad:**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|GroupBy          |řetězec                    | Příkaz, který aplikuje agregaci dat pouze na zadaná pole. Můžete zadat následující pole:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>Vrácené řádky dat budou obsahovat pole zadaná v `groupby`  parametru a *množství*.<br/><br/>`groupby`Parametr lze použít s `aggregationLevel` parametrem.<br/><br/>**Příklad:**<br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [využití Azure](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a>Viz také

- [Analýzy Partnerského centra – prostředky](partner-center-analytics-resources.md)
