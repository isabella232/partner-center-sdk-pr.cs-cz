---
title: Prostředky zásad samoobslužné obsluhy
description: Partner pro zákazníka nastaví zásady samoobslužného poskytování.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766735"
---
# <a name="selfservepolicy-resource"></a>Prostředek SelfServePolicy

**Platí pro:**

- Partnerské centrum

Partner pro zákazníka nastaví zásady samoobslužného poskytování.

## <a name="selfservepolicy"></a>SelfServePolicy

Popisuje košík.

| Vlastnost              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | Identifikátor zásady samoobslužné obsluhy, který se poskytne po úspěšném vytvoření zásady samoobslužné obsluhy.     |
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
