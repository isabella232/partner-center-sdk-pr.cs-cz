---
title: Prostředky vztahů
description: Popisuje prostředky vztahující se k relacím.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766710"
---
# <a name="relationships-resources"></a>Prostředky vztahů

**Platí pro**

- Partnerské centrum

Popisuje prostředky vztahující se k relacím.

## <a name="partnerrelationship"></a>PartnerRelationship

Představuje vztah mezi dvěma partnery.

| Vlastnost         | Typ                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | řetězec                                                         | Identifikátor partnera Identifikátor partnera určuje ID tenanta partnera, který je na straně příjemce (od) vztahu. |
| location         | řetězec                                                         | Umístění partnera.                                                                                                                   |
| mpnId            | řetězec                                                         | Identifikátor Microsoft Partner Network (MPN) partnera.                                                                                 |
| name             | řetězec                                                         | Název partnera.                                                                                                                       |
| Element | řetězec                                                         | Typ relace.                                                                                                                      |
| state            | řetězec                                                         | Stav relace (například `active` ).                                                                                                 |
| atributy       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Poskytuje adresu URL, pomocí které může zákazník vytvořit relaci s partnerem.

| Vlastnost   | Typ                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | řetězec                                                         | Adresa URL požadavku vztahu |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat.      |
