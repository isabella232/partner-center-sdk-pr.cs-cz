---
title: Prostředky záznamů o využití prostředků
description: Prostředek ResourceUsageRecord můžete použít k popisu odhadovaných peněžních nákladů na využití na úrovni prostředků předplatného v aktuálním fakturačním období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b330c49518bc12a63f2be731eef5c57884f5b15b706ce4007bbdf1a7bb8fab0e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996933"
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
