---
title: Prostředky licencí
description: Popisuje prostředky související s licencemi.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 681f53ec73122a4861e6f1a2f96560336481a068
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766913"
---
# <a name="license-resources"></a>Prostředky licencí

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

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
| skuPartNumber  | řetězec           | Název dílu SKU pro daný produkt. Například pro sadu Office 365 Plan E3 je tato hodnota `EnterprisePack` . Tuto vlastnost lze použít místo ID, pokud není k dispozici ID.                |
| targetType     | řetězec           | Cílový typ produktu. Tato vlastnost určuje, zda je produkt použitelný pro `User` nebo `Tenant` .                                                                    |
| licenseGroupId | řetězec           | Identifikuje se prostřednictvím identifikátoru skupiny autority nebo služby, které spravují licenci productSku. Produkty jsou oddělené v rámci skupin licencí, aby bylo lépe spravovatelnější.<br/><br/>                                                                                     `group1` – Všechny produkty, jejichž licence je možné spravovat pomocí Azure Active Directory (AAD).<br/><br/>                                            `group2` -Minecraftu licence k produktu.                                         |

## <a name="serviceplan"></a>ServicePlan

Identifikuje nasazovatelné služby v rámci SKU produktu. Produkt může mít spoustu plánů služeb.

| Vlastnost         | Typ   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | řetězec | Identifikátor plánu služby.                                                                                      |
| displayName      | řetězec | Lokalizovaný zobrazovaný název plánu služby.                                                                  |
| serviceName      | řetězec | Název služby                                                                                                 |
| capabilityStatus | řetězec | Stav plánu služby plánu služby.                                                                      |
| targetType       | řetězec | Cílový typ plánu služby. Tato vlastnost určuje, jestli se má produkt použít pro uživatele nebo tenanta. |

## <a name="subscribedsku"></a>SubscribedSku

Popisuje předplatné produktu vlastněné klientem.

| Vlastnost         | Typ                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | integer                                                        | Počet jednotek, které jsou k dispozici pro přiřazení. Tato hodnota se vypočte jako celkový počet jednotek spotřebovaných jednotek. |
| activeUnits      | integer                                                        | Počet jednotek aktivních pro přiřazení.                                                        |
| consumedUnits    | integer                                                        | Počet spotřebovaných jednotek.                                                                     |
| suspendedUnits   | integer                                                        | Počet pozastavených jednotek                                                                    |
| totalUnits       | integer                                                        | Celkový počet jednotek Tato hodnota se vypočítá jako součet aktivních a varovných jednotek.         |
| warningUnits     | integer                                                        | Počet varovných jednotek.                                                                      |
| productSku       | ProductSku                                                     | SKU produktu.                                                                                  |
| servicePlans     | pole prostředků ServicePlan                                 | Kolekce plánů služeb produktu.                                                     |
| capabilityStatus | řetězec                                                         | Stav skladové položky produktu.                                                                      |
| atributy       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající prostředku.                                            |
