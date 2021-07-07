---
title: Prostředky záznamů o využití prostředků
description: Prostředek ResourceUsageRecord můžete použít k popisu odhadovaných peněžních nákladů na využití na úrovni prostředků předplatného v aktuálním fakturačním období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eb626b9d4cb4c57a07f45bcf7b914f534e62ab68
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446577"
---
# <a name="resource-usage-record-resources"></a>Prostředky záznamů o využití prostředků

Prostředek **ResourceUsageRecord** můžete použít k popisu odhadovaných peněžních nákladů na využití na úrovni prostředků předplatného v aktuálním fakturačním období.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Vlastnost          | Typ               | Description                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | řetězec             | Získá nebo nastaví identifikátor předplatného. U Microsoft Azure předplatného (MS-AZR-0145P) je tato hodnota identifikátor komerčního předplatného. V případě plánů Azure je tato hodnota identifikátor plánu Azure. |
| Identifikátor URI prostředku       | řetězec             | Získá nebo nastaví identifikátor URI prostředku.                                                                                                                                                                            |
| ResourceType      | řetězec             | Získá nebo nastaví typ prostředku.                                                                                                                                                                            |
| EntitlementId (ID nároku)     | řetězec             | Získá nebo nastaví identifikátor nároku (identifikátor předplatného Azure).                                                                                                                               |
| Název nároku   | řetězec             | Získá nebo nastaví název nároku.                                                                                                                                                                         |
| ResourceGroupName | double             | Získá nebo nastaví název skupiny prostředků.                                                                                                                                                                      |
| Name              | řetězec             | Název prostředku.                                                                                                                                                                                  |
| ResourceName      | řetězec             | Získá nebo nastaví název prostředku.                                                                                                                                                                     |
| TotalCost         | decimal            | Získá nebo nastaví odhadované celkové využití nákladů.                                                                                                                                                               |
| CurrencyCode      | řetězec             | Získá nebo nastaví kód měny.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Získá nebo nastaví odhadované celkové náklady v USD.                                                                                                                                                              |
| LastModifiedDate.  | řetězec             | Den (ve formátu data a času), kdy se tento záznam naposledy změnil.                                                                                                                                          |
| Atributy        | Atributy prostředků | Atributy metadat odpovídající prostředku.                                                                                                                                                     |
