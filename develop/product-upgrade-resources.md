---
title: Prostředky pro upgrade produktů
description: K plánu Azure můžete použít více prostředků souvisejících s upgrady produktu partnerského centra. Patří mezi ně ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct a ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8975f0a135c88796a21f8abab944e53181f591e
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274610"
---
# <a name="product-upgrade-resources"></a>Prostředky pro upgrade produktů

**Platí pro:**

- Partnerské centrum

Následující prostředky vám pomůžou získat informace o upgradech na produktech partnerského centra z předplatného Microsoft Azure (MS-AZR-0145P) do plánu Azure.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

Prostředek **ProductUpgradesRequest** poskytuje informace o objektu žádosti o upgrade produktu.

| Vlastnost      | Typ                                                          | Description                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | řetězec                                                        | Řetězec ve formátu GUID, který identifikuje zákazníka.      |
| Produktová řada | řetězec                                                        | Produktová řada, pro kterou je upgrade požadován. |
| atributy    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

Prostředek **ProductUpgradesEligibility** poskytuje informace o nároku zákazníka na upgrade produktu.

| Vlastnost      | Typ                                                          | Description                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | řetězec                                                        | Řetězec ve formátu GUID, který identifikuje zákazníka.                            |
| Produktová řada | řetězec                                                        | Produktová řada, pro kterou je upgrade požadován.                       |
| Oprávněné    | bool                                                          | Hodnota bool označuje, jestli má zákazník nárok na požadovaný upgrade. |
| upgradeId     | řetězec                                                        | ID upgradu v případě, že je již provedena aktualizace produktu pro danou rodinu.        |
| reason        | řetězec                                                        | Důvod, proč zákazník nemá nárok na upgrade produktu.                |
| Produktová řada | řetězec                                                        | Produktová řada, pro kterou je upgrade požadován.                       |
| atributy    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                                         |

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

Prostředek **ProductUpgradesStatus** poskytuje informace o stavu upgradu produktu.

| Vlastnost | Typ   | Description                                          |
|----------|--------|------------------------------------------------------|
| Id       | řetězec | Řetězec ve formátu GUID, který identifikuje upgrade. |
| Produktová řada       | řetězec                                                         | Produktová řada, pro kterou je upgrade požadován.
| status              | řetězec                                                         | Stav upgradu produktu.
| Položky řádku           | pole prostředků [UpgradesLineItem](#upgradeslineitem)       | Pole objektů, které poskytuje informace o podrobnostech o upgradu pro jednotlivé položky řádku, které byly součástí textu žádosti.
| errorDetails        | Prostředek [ErrorDetails](#errordetails)                         | Podrobnosti o chybě pro požadovaný upgrade
| atributy          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atributy metadat. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

Prostředek **UpgradesLineItem** popisuje stav detailů upgradu produktu pro každou položku řádku požadavku.

| Vlastnost      | Typ                                                          | Description                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct | Objekt [UpgradeProduct](#upgradeproduct)                      | Informace o upgradovaném zdrojovém produktu. |
| targetProduct | Objekt [UpgradeProduct](#upgradeproduct)                      | Informace o cílovém upgradu produktu.   |
| upgradedDate  | řetězec ve formátu data a času standardu UTC                                | Datum, kdy bylo předplatné upgradováno.           |
| status        | řetězec                                                        | Stav upgradu produktu.                |
| errorDetails  | Prostředek [ErrorDetails](#errordetails)                        | Podrobnosti o chybě pro požadovaný upgrade          |
| atributy    | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                          |

## <a name="upgradeproduct"></a>UpgradeProduct

Prostředek **UpgradeProduct** poskytuje informace o upgradovaném produktu.

| Vlastnost   | Typ                                                          | Description                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| id         | řetězec                                                        | Řetězec ve formátu GUID, který identifikuje produkt. |
| name       | řetězec                                                        | Popisný název produktu, který se má upgradovat         |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                             |

## <a name="errordetails"></a>ErrorDetails

Prostředek **ErrorDetails** poskytuje podrobnosti o chybách během procesu upgradu.

| Vlastnost   | Typ                                                          | Description                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| kód       | řetězec                                                        | Kód chyby v případě, že upgrade produktu se nezdařil.      |
| zpráva    | řetězec                                                        | Chybová zpráva při neúspěšném upgradu produktu |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                          |
