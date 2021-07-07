---
title: Prostředky použití předplatného
description: Prostředky použití předplatného popisují předplatné s fakturací na základě využití. Tato předplatná mají záznamy denního a měsíčního využití společně se souhrnem využití pro každé období platby.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcb24dcf5ca8165ec23c4b187def38d05772e1de
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547372"
---
# <a name="subscription-usage-resources"></a>Prostředky použití předplatného

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Pomocí následujících prostředků použití předplatného můžete získat informace o využití určitého předplatného s fakturací na základě využití. Tato předplatná mají záznamy denního a měsíčního využití společně se souhrnem využití pro každé období platby.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*Prostředek **SubscriptionDailyUsageRecord** je zastaralý a může způsobit nepřesné výsledky. doporučujeme aktualizovat aplikace tak, aby používaly rozhraní api popsané v tématu [získání záznamů o využití zákazníka pro Azure](get-a-customer-s-utilization-record-for-azure.md) a místo toho [získat ceny pro Microsoft Azure](get-prices-for-microsoft-azure.md) .*

Prostředek **SubscriptionDailyUsageRecord** popisuje, kolik předplatných se používá v jednom dni.

| Vlastnost         | Typ               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | řetězec             | Den, ve formátu data a času, který bylo použito v předplatném.                                 |
| ResourceId       | řetězec             | Hlavních. Jedinečné ID prostředku                                                          |
| ResourceName     | řetězec             | Název prostředku.                                                                     |
| TotalCost        | decimal             | Odhadované celkové náklady na používání prostředků v předplatném v zadaném dni.     |
| CurrencyLocale   | řetězec             | Národní prostředí, ve kterém bylo použito předplatné, určuje měnu, která se má použít na faktuře. |
| LastModifiedDate. | řetězec             | Den v formátu data a času, který tento záznam naposledy změnil.                             |
| Atributy       | ResourceAttributes | Atributy metadat odpovídající prostředku.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

Prostředek **SubscriptionMonthlyUsageRecord** popisuje, kolik předplatných se používá v jednom měsíci.

| Vlastnost         | Typ               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Status           | řetězec             | Stav předplatného: "none", "Active", "Suspended" nebo "Deleted".                  |
| PartnerOnRecord  | řetězec             | "ID MPN partnera na záznamu"                                                        |
| Hodnotami OfferId          | řetězec             | Hlavních. ID nabídky, která se vztahuje k tomuto předplatnému.                                       |
| Id               | řetězec             | Hlavních. ID předplatného nebo prostředku.                                                 |
| Name             | řetězec             | Název předplatného nebo prostředku.                                                     |
| TotalCost        | decimal             | Odhadované celkové náklady na používání prostředků v předplatném v zadaném měsíci.   |
| CurrencyLocale   | řetězec             | Národní prostředí, ve kterém bylo použito předplatné, určuje měnu, která se má použít na faktuře. k dispozici pro předplatná Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode     | řetězec             | Získá nebo nastaví kód měny. K dispozici pro prostředky předplatného Azure Plan.                                         |
| USDTotalCost     | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. K dispozici pro plány Azure.                                         |
| LastModifiedDate. | řetězec             | Den v formátu data a času, který tento záznam naposledy změnil.                             |
| Atributy       | ResourceAttributes | Atributy metadat odpovídající prostředku.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

Prostředek **SubscriptionUsageSummary** popisuje, kolik určitého předplatného bylo použito v aktuálním fakturačním období.

| Vlastnost         | Typ               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | řetězec             | Hlavních. ID předplatného nebo prostředku. V kontextu CustomerMonthlyUsageRecord je toto ID ID zákazníka. |
| ResourceName     | řetězec             | Název předplatného nebo prostředku. V kontextu CustomerMonthlyUsageRecord je tímto názvem jméno zákazníka. |
| BillingStartDate | date               | Počáteční datum aktuálního fakturačního období ve formátu data a času.                                                     |
| BillingEndDate   | date               | Koncové datum aktuálního fakturačního období ve formátu data a času.                                                       |
| TotalCost        | double             | Odhadované celkové náklady na používání prostředků v předplatném během zadaného fakturačního období.               |
| CurrencyLocale   | řetězec             | Národní prostředí, ve kterém bylo předplatné použito, určuje měnu, která se má na faktuře použít. K dispozici Microsoft Azure předplatných (MS-AZR-0145P). |
| CurrencyCode   | řetězec             | Získá nebo nastaví kód měny. K dispozici pro plány Azure.                                         |
| USDTotalCost   | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. K dispozici pro prostředky předplatného plánu Azure.                                         |
| LastModifiedDate. | řetězec             | Den ve formátu data a času, kdy se tento záznam naposledy změnil.                                                      |
| Odkazy            | Odkazy na prostředky      | Propojení prostředků odpovídající předplatnému SubscriptionUsageSummary.                                                      |
| Atributy       | Atributy prostředků | Atributy metadat odpovídající vlastnosti SubscriptionUsageSummary.                                                 |
