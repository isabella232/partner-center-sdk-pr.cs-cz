---
title: Prostředky zásad samoobslužné obsluhy
description: Partner pro zákazníka nastaví zásady samoobslužného poskytování.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffca78481572e201d3ef9f488e7d594a9c1176249b4415a347b488f4b9b81c51
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996763"
---
# <a name="selfservepolicy-resource"></a>Prostředek SelfServePolicy

Partner pro zákazníka nastaví zásady samoobslužného poskytování.

## <a name="selfservepolicy"></a>SelfServePolicy

Popisuje košík.

| Vlastnost              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | Identifikátor zásady, který se poskytuje po úspěšném vytvoření zásady samoobslužné obsluhy.     |
| SelfServeEntity       | SelfServeEntity  | Entita, která má udělen přístup k sobě.                                                     |
| Udělovatel               | Udělovatel          | Uděluje udělení přístupu.                                                                    |
| Oprávnění           | Pole oprávnění| Pole prostředků [oprávnění](#permission)                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Představuje entitu udělenou oprávnění.

| Vlastnost             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | řetězec                           | Entita, která má udělený přístup, přijaté hodnoty: zákazník                                 |
| TenantID             | řetězec                           | Identifikátor tenanta entity, která má udělený přístup                                   |

## <a name="grantor"></a>Udělovatel

Představuje udělení oprávnění.

| Vlastnost             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | řetězec                           | Uděluje udělení přístupu, přijatelné hodnoty: BillToPartner.                               |
| TenantID             | řetězec                           | Identifikátor tenanta entity, která uděluje přístup                                       |


## <a name="permission"></a>Oprávnění

Představuje oprávnění v zásadách samoobslužné obsluhy.

| Vlastnost             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Prostředek             | řetězec                           | Přístup k prostředkům se uděluje moc: AzureReservedInstances.                          |
| Akce               | řetězec                           | Přístup k akci je udělován pro: nákup                                           |
