---
title: Prostředky licencí
description: Popisuje prostředky související s licencemi.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 27d44f89ac89f365e77e073c425ca45ab3638c68
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548392"
---
# <a name="license-resources"></a>Prostředky licencí

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Popisuje prostředky související s licencemi.

## <a name="license"></a>Licence

Popisuje uživatelskou licenci.

>[!NOTE]
>Nepodporováno v partnerském centru provozovaném společností 21Vianet.

| Vlastnost     | Typ                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | pole prostředků ServicePlan                                 | Kolekce plánů služeb, které odpovídají licenci |
| productSKU   | ProductSku                                                     | SKU produktu, který odpovídá licenci.        |
| atributy   | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající licenci.          |

## <a name="licenseupdate"></a>LicenseUpdate

Poskytuje informace, které slouží k přiřazení nebo odebrání licencí uživateli.

| Vlastnost         | Typ                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | pole objektů                                               | Pole objektů [LicenseAssignment](#licenseassignment) |
| licensesToRemove | pole řetězců                                               | Identifikátory SKU licencí, které mají být odebrány.    |
| licenseWarnings  | pole objektů                                               | Pole objektů [LicenseWarning](#licensewarning)       |
| atributy       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                  |

## <a name="licenseassignment"></a>LicenseAssignment

Poskytuje informace potřebné pro operaci aktualizace licencí.

| Vlastnost      | Typ             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | pole řetězců | Identifikátory plánu služby, které mají být vyloučeny z dostupnosti uživateli. |
| skuId         | řetězec           | Identifikátor SKU produktu pro licenci.                                |

## <a name="licensewarning"></a>LicenseWarning

Obsahuje informace o upozorněních, k nimž došlo během operace aktualizace licencí.

| Vlastnost     | Typ             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| kód         | řetězec           | Kód upozornění                                   |
| zpráva      | řetězec           | Upozornění                                |
| servicePlans | pole řetězců | Názvy plánů služby spojené s upozorněním. |

## <a name="productsku"></a>ProductSku

Popisuje podrobnosti o produktu.

| Vlastnost       | Typ             | Description                                         |
|----------------|------------------|-----------------------------------------------------|
| id             | řetězec           | Identifikátor produktu.                             |
| name           | řetězec           | Identifikátor zabezpečení uživatele                      |
| skuPartNumber  | řetězec           | Název dílu SKU pro daný produkt. například pro Office 365 Plan E3 je tato hodnota `EnterprisePack` . Tuto vlastnost lze použít místo ID, pokud není k dispozici ID.                |
| targetType     | řetězec           | Cílový typ produktu. Tato vlastnost určuje, zda je produkt použitelný pro `User` nebo `Tenant` .                                                                    |
| licenseGroupId | řetězec           | Identifikuje se prostřednictvím identifikátoru skupiny autority nebo služby, které spravují licenci productSku. Produkty jsou oddělené v rámci skupin licencí, aby bylo lépe spravovatelnější.<br/><br/>                                                                                     `group1`– Všechny produkty, jejichž licence je možné spravovat pomocí Azure Active Directory (AAD).<br/><br/>                                            `group2`-Minecraft licence k produktu.                                         |

## <a name="serviceplan"></a>ServicePlan

Identifikuje nasazovatelné služby v rámci SKU produktu. Produkt může mít spoustu plánů služeb.

| Vlastnost         | Typ   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | řetězec | Identifikátor plánu služby.                                                                                      |
| displayName      | řetězec | Lokalizovaný zobrazovaný název plánu služby.                                                                  |
| Název_služby      | řetězec | Název služby.                                                                                                 |
| capabilityStatus | řetězec | Stav plánu služby pro plán služby.                                                                      |
| Targettype       | řetězec | Cílový typ plánu služby. Tato vlastnost určuje, jestli se produkt vztahuje na uživatele nebo tenanta. |

## <a name="subscribedsku"></a>SubscribedSku

Popisuje předplacený produkt vlastněný tenantem.

| Vlastnost         | Typ                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | integer                                                        | Počet jednotek dostupných pro přiřazení Tato hodnota se vypočítá jako celkový počet jednotek – spotřebované jednotky. |
| activeUnits      | integer                                                        | Počet aktivních jednotek pro přiřazení                                                        |
| consumedUnits    | integer                                                        | Počet spotřebovaných jednotek                                                                     |
| suspendedUnits (pozastavené jednotky)   | integer                                                        | Počet pozastavených jednotek                                                                    |
| totalUnits       | integer                                                        | Celkový počet jednotek Tato hodnota se vypočítá jako součet aktivních jednotek a jednotek upozornění.         |
| warningUnits (jednotky upozornění)     | integer                                                        | Počet jednotek upozornění                                                                      |
| productSku       | ProductSku                                                     | SKU produktu                                                                                  |
| servicePlans     | pole prostředků serviceplan                                 | Kolekce plánů služeb produktu                                                     |
| capabilityStatus | řetězec                                                         | Stav SKU produktu                                                                      |
| atributy       | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající prostředku.                                            |
