---
title: Prostředek záznamu využití měřiče
description: Pomocí prostředku MeterUsageRecord můžete v aktuálním fakturačním cyklu popsat odhadované peněžní náklady na využití na úrovni měřičů předplatného.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c02c859d1d8ba3edd236d83d3056cb82533f7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766703"
---
# <a name="meter-usage-record-resource"></a>Prostředek záznamu využití měřiče

**Platí pro:**

- Partnerské centrum

Pomocí prostředku **MeterUsageRecord** můžete v aktuálním fakturačním cyklu popsat odhadované peněžní náklady na využití na úrovni měřičů předplatného.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Vlastnost         | Typ               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | řetězec             | Identifikátor GUID odpovídající identifikátoru [prostředku předplatného](subscription-resources.md#subscription)partnerského centra, který představuje předplatné Microsoft Azure (MS-AZR-0145P) nebo plán Azure. V případě předplatných služby Microsoft Azure (MS-AZR-0145P) je tato hodnota identifikátorem předplatného pro obchod. U prostředků předplatného Azure Plan je tato hodnota identifikátor plánu Azure.                  |
| MeterId  | řetězec             | Získá nebo nastaví identifikátor měřiče.                                                        |
| MeterName          | řetězec             | Získá nebo nastaví název měřiče.                                       |
| Kategorie               | řetězec             | Získá nebo nastaví kategorii prostředku Azure.                                                 |
| Subcategory             | řetězec             |  Získá nebo nastaví podkategorii prostředku Azure.                                                     |
| QuantityUsed        | decimal             | Získá nebo nastaví množství použitého prostředku Azure.   |
| Jednotka   | řetězec             | Získá nebo nastaví měrnou jednotku prostředku Azure. |
| TotalCost   | decimal             | Získá nebo nastaví odhadované celkové náklady na využití. |
| CurrencyLocale   | řetězec             | Národní prostředí, ve kterém se předplatné použilo. Tato vlastnost určuje měnu, která se používá na faktuře. Tato vlastnost je k dispozici pro odběry Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode   | řetězec             | Získá nebo nastaví kód měny. Tato vlastnost je k dispozici pro plány Azure.                                         |
| USDTotalCost   | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. Tato vlastnost je k dispozici pro plány Azure.                                         |
| LastModifiedDate. | řetězec             | Den (ve formátu data a času), kdy se tento záznam naposledy změnil                             |
| Atributy       | ResourceAttributes | Atributy metadat odpovídající prostředku.                                        |                                           |
