---
title: Prostředky pro upgrade produktů
description: Můžete použít více prostředků souvisejících s Partnerské centrum upgradu produktů na plán Azure. Patří mezi ně ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct a ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c995ac44dbe22000f7bc86991cb973ed31a5c018
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445336"
---
# <a name="product-upgrade-resources"></a>Prostředky pro upgrade produktů

Následující zdroje informací o upgradech produktů Partnerské centrum z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure najdete v následujících zdrojích informací.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

Prostředek **ProductUpgradesRequest** poskytuje informace o objektu požadavku upgradů produktů.

| Vlastnost      | Typ                                                          | Description                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | řetězec                                                        | Řetězec ve formátu GUID, který identifikuje zákazníka.      |
| productFamily | řetězec                                                        | Produktová skupina, pro kterou se upgrade požaduje. |
| atributy    | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

Prostředek **ProductUpgradesEligibility** poskytuje informace o způsobilosti zákazníka k upgradu produktu.

| Vlastnost      | Typ                                                          | Description                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | řetězec                                                        | Řetězec ve formátu GUID, který identifikuje zákazníka.                            |
| productFamily | řetězec                                                        | Produktová skupina, pro kterou se upgrade požaduje.                       |
| isEligible    | bool                                                          | Hodnota bool určuje, jestli má zákazník nárok na požadovaný upgrade. |
| ID upgradu     | řetězec                                                        | ID upgradu, pokud již existuje upgrade produktu pro danou rodinu.        |
| reason        | řetězec                                                        | Důvod, proč zákazník nemá nárok na upgrade produktu.                |
| productFamily | řetězec                                                        | Produktová skupina, pro kterou se upgrade požaduje.                       |
| atributy    | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.                                                         |

## <a name="productupgradesstatus"></a>Stav ProductUpgrades

Prostředek **ProductUpgradesStatus** poskytuje informace o stavu upgradu produktu.

| Vlastnost | Typ   | Description                                          |
|----------|--------|------------------------------------------------------|
| Id       | řetězec | Řetězec formátovaný identifikátorem GUID, který identifikuje upgrade. |
| productFamily       | řetězec                                                         | Produktová skupina, pro kterou se upgrade požaduje.
| status              | řetězec                                                         | Stav upgradu produktu
| položky řádku           | pole [prostředků UpgradesLineItem](#upgradeslineitem)       | Pole objektů, které poskytuje informace o podrobnostech upgradu pro každou položku řádku, která byla součástí textu požadavku.
| errorDetails        | [Prostředek ErrorDetails](#errordetails)                         | Podrobnosti o chybě pro požadovaný upgrade.
| atributy          | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

Prostředek **UpgradesLineItem** popisuje stav podrobností o upgradu produktu pro každou položku řádku žádosti.

| Vlastnost      | Typ                                                          | Description                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct | [Objekt UpgradeProduct](#upgradeproduct)                      | Informace o upgradovaném zdrojovém produktu. |
| targetProduct | [Objekt UpgradeProduct](#upgradeproduct)                      | Informace o cílovém produktu po upgradu.   |
| datum upgradu  | řetězec ve formátu data a času UTC                                | Datum upgradu předplatného           |
| status        | řetězec                                                        | Stav upgradu produktu                |
| errorDetails  | [Prostředek ErrorDetails](#errordetails)                        | Podrobnosti o chybě pro požadovaný upgrade.          |
| atributy    | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.                          |

## <a name="upgradeproduct"></a>UpgradeProduct

Prostředek **UpgradeProduct** poskytuje informace o upgradovaném produktu.

| Vlastnost   | Typ                                                          | Description                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| id         | řetězec                                                        | Řetězec formátovaný identifikátorem GUID, který identifikuje produkt. |
| name       | řetězec                                                        | Popisný název produktu, který se má upgradovat         |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                             |

## <a name="errordetails"></a>ErrorDetails

Prostředek **ErrorDetails** poskytuje podrobnosti o chybách během procesu upgradu.

| Vlastnost   | Typ                                                          | Description                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| kód       | řetězec                                                        | Kód chyby v případě, že upgrade produktu se nezdařil.      |
| zpráva    | řetězec                                                        | Chybová zpráva při neúspěšném upgradu produktu |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                          |
