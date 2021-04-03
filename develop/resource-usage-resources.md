---
title: Prostředky záznamu využití prostředků
description: Pomocí prostředku ResourceUsageRecord můžete popsat odhadované peněžní náklady na využití na úrovni prostředků předplatného v aktuálním fakturačním cyklu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b0a28620eec86e86630aef93b13f26c9dd675a5d
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274559"
---
# <a name="resource-usage-record-resources"></a>Prostředky záznamu využití prostředků

**Platí pro:**

- Partnerské centrum

Pomocí prostředku **ResourceUsageRecord** můžete popsat odhadované peněžní náklady na využití na úrovni prostředků předplatného v aktuálním fakturačním cyklu.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Vlastnost          | Typ               | Description                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | řetězec             | Získá nebo nastaví identifikátor předplatného. Pro předplatná Microsoft Azure (MS-AZR-0145P) je tato hodnota identifikátorem předplatného pro obchod. V případě plánů Azure je tato hodnota identifikátor plánu Azure). |
| ResourceUri       | řetězec             | Získá nebo nastaví identifikátor URI prostředku.                                                                                                                                                                            |
| ResourceType      | řetězec             | Získá nebo nastaví typ prostředku.                                                                                                                                                                            |
| EntitlementId     | řetězec             | Získá nebo nastaví identifikátor nároku (identifikátor předplatného Azure).                                                                                                                               |
| EntitlementName   | řetězec             | Získá nebo nastaví název nároku.                                                                                                                                                                         |
| ResourceGroupName | double             | Získá nebo nastaví název skupiny prostředků.                                                                                                                                                                      |
| Name              | řetězec             | Název prostředku.                                                                                                                                                                                  |
| ResourceName      | řetězec             | Získá nebo nastaví název prostředku.                                                                                                                                                                     |
| TotalCost         | decimal            | Získá nebo nastaví odhadované celkové využití nákladů.                                                                                                                                                               |
| CurrencyCode      | řetězec             | Získá nebo nastaví kód měny.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Získá nebo nastaví odhadované celkové náklady v USD.                                                                                                                                                              |
| LastModifiedDate.  | řetězec             | Den (ve formátu data a času), kdy se tento záznam naposledy změnil                                                                                                                                          |
| Atributy        | ResourceAttributes | Atributy metadat odpovídající prostředku.                                                                                                                                                     |
