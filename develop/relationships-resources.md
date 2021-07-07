---
title: Prostředky vztahů
description: Popisuje prostředky vztahující se k relacím.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dba1e99a6c97c759e3c61cde1e7565faa2ef4d1
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445727"
---
# <a name="relationships-resources"></a>Prostředky vztahů

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
