---
title: Zdroje informací o licencích
description: Popisuje prostředky související s licencemi.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e6d91110dcec8a873e77cb02bdb77f6335e27989201ea68eebf904c5159964c5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996576"
---
# <a name="license-resources"></a>Zdroje informací o licencích

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Popisuje prostředky související s licencemi.

## <a name="license"></a>Licence

Popisuje uživatelskou licenci.

>[!NOTE]
>Nepodporované Partnerské centrum provozované společností 21Vianet.

| Vlastnost     | Typ                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | pole prostředků serviceplan                                 | Kolekce plánů služeb, které odpovídají licenci |
| productSKU   | ProductSku                                                     | SKU produktu, který odpovídá licenci.        |
| atributy   | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající licenci.          |

## <a name="licenseupdate"></a>LicenseUpdate

Poskytuje informace, které se používají k přiřazení nebo odebrání licencí uživateli.

| Vlastnost         | Typ                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | pole objektů                                               | Pole objektů [LicenseAssignment](#licenseassignment) |
| licensesToRemove | pole řetězců                                               | Identifikátory SKU produktu licencí, které se odeberou.    |
| LicenseWarnings  | pole objektů                                               | Pole objektů [LicenseWarning](#licensewarning)       |
| atributy       | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.                                  |

## <a name="licenseassignment"></a>LicenseAssignment

Poskytuje informace potřebné pro operaci aktualizace licence.

| Vlastnost      | Typ             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | pole řetězců | Identifikátory plánu služby, které mají být vyloučeny z dostupnosti pro uživatele. |
| ID SKU         | řetězec           | Identifikátor SKU produktu pro licenci.                                |

## <a name="licensewarning"></a>LicenseWarning

Obsahuje informace o upozornění, ke kterým došlo během operace aktualizace licence.

| Vlastnost     | Typ             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| kód         | řetězec           | Kód upozornění                                   |
| zpráva      | řetězec           | Upozornění                                |
| servicePlans | pole řetězců | Názvy plánu služby přidružené k upozornění. |

## <a name="productsku"></a>ProductSku

Popisuje podrobnosti o produktu.

| Vlastnost       | Typ             | Description                                         |
|----------------|------------------|-----------------------------------------------------|
| id             | řetězec           | Identifikátor produktu.                             |
| name           | řetězec           | Identifikátor objektu zabezpečení uživatele.                      |
| skuPartNumber  | řetězec           | Název čísla části SKU pro produkt. Například pro plán Office 365 E3 je tato hodnota `EnterprisePack` . Pokud ID není k dispozici, můžete tuto vlastnost použít místo ID.                |
| Targettype     | řetězec           | Cílový typ produktu. Tato vlastnost určuje, jestli se produkt vztahuje na `User` nebo `Tenant` .                                                                    |
| ID skupiny licencí | řetězec           | Identifikuje prostřednictvím identifikátoru skupiny autoritu nebo službu, která spravuje licenci productSku. Pro lepší správu jsou produkty oddělené v rámci skupin licencí.<br/><br/>                                                                                     `group1`– Všechny produkty, jejichž licence může spravovat Azure Active Directory (AAD).<br/><br/>                                            `group2`– Minecraft licence na produkty.                                         |

## <a name="serviceplan"></a>ServicePlan

Identifikuje nasaditelné služby v rámci SKU produktu. Produkt může mít mnoho plánů služeb.

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
