---
title: Prostředky relací
description: Popisuje prostředky související s relacemi.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bbbc973679ae80c3ad6b9d67945c6fbcb087789484939b67f8d8a6b538ce7d37
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997086"
---
# <a name="relationships-resources"></a>Prostředky relací

Popisuje prostředky související s relacemi.

## <a name="partnerrelationship"></a>PartnerRelationship

Představuje vztah mezi dvěma partnery.

| Vlastnost         | Typ                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | řetězec                                                         | Identifikátor partnera. Identifikátor partnera určuje ID tenanta partnera, který je na straně příjemce (z) vztahu. |
| location         | řetězec                                                         | Umístění partnera.                                                                                                                   |
| ID mpn            | řetězec                                                         | Identifikátor Microsoft Partner Network (MPN) partnera.                                                                                 |
| name             | řetězec                                                         | Název partnera.                                                                                                                       |
| Relationshiptype | řetězec                                                         | Typ relace                                                                                                                      |
| state            | řetězec                                                         | Stav relace (například `active` ).                                                                                                 |
| atributy       | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.                                                                                                                       |

## <a name="relationshiprequest"></a>Požadavek na vztah

Poskytuje adresu URL, pomocí které může zákazník navázat vztah s partnerem.

| Vlastnost   | Typ                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | řetězec                                                         | Adresa URL žádosti o relaci |
| atributy | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat.      |
