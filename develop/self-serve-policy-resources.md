---
title: Zdroje informací o samoobslužných zásadách
description: Partner pro zákazníka nastaví samoobslužné zásady.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446713"
---
# <a name="selfservepolicy-resource"></a>Prostředek SelfServePolicy

Partner pro zákazníka nastaví samoobslužné zásady.

## <a name="selfservepolicy"></a>Samoobslužné zásady

Popisuje košík.

| Vlastnost              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | Identifikátor samoobslužné zásady, který se dodá po úspěšném vytvoření samoobslužných zásad.     |
| Samoobslužná rezervace       | Samoobslužná rezervace  | Samoobslužná entita, které je udělen přístup.                                                     |
| Grantor               | Grantor          | Grantor, který uděluje přístup.                                                                    |
| Oprávnění           | Pole oprávnění| Pole prostředků [oprávnění.](#permission)                                                                     |

## <a name="selfserveentity"></a>Samoobslužná rezervace

Představuje entitu s udělenou oprávněními.

| Vlastnost             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | řetězec                           | Entita, ke které se uděluje přístup, přijaté hodnoty: Zákazník.                                 |
| ID tenanta             | řetězec                           | Identifikátor tenanta entity, ke které se uděluje přístup.                                   |

## <a name="grantor"></a>Grantor

Představuje udělení oprávnění.

| Vlastnost             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Typ grantoru          | řetězec                           | Udělení přístupu, přijaté hodnoty: BillToPartner.                               |
| ID tenanta             | řetězec                           | Identifikátor tenanta entity udělující přístup.                                       |


## <a name="permission"></a>Oprávnění

Představuje oprávnění v zásadách samoobslužné služby.

| Vlastnost             | Typ|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Prostředek             | řetězec                           | Uděluje se také přístup k prostředkům: AzureReservedInstances.                          |
| Akce               | řetězec                           | Přístup k akci se uděluje pro: Koupit                                           |
