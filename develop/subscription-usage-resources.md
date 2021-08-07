---
title: Prostředky využití předplatného
description: Zdroje informací o využití předplatného popisují předplatná s fakturací na základě využití. Tato předplatná mají záznamy o denním a měsíčním využití spolu se souhrnem využití pro každé platební období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8af4e9b8a4660b5bc9d287ece258dca9aa9ba7a749cfdc89e9c9b47e4af61b1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990269"
---
# <a name="subscription-usage-resources"></a>Prostředky využití předplatného

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

K získání informací o využití pro konkrétní předplatné s fakturací na základě využití můžete použít následující prostředky využití předplatného. Tato předplatná mají záznamy o denním a měsíčním využití spolu se souhrnem využití pro každé platební období.

## <a name="subscriptiondailyusagerecord"></a>Záznam PředplatnéDailyUsage

*Prostředek **SubscriptionDailyUsageRecord** je zastaralý a může vést k nepřesným výsledkům. Doporučujeme aktualizovat aplikace tak, aby místo toho používejte rozhraní API popsaná v článcích Získání záznamů o využití Azure [zákazníkem](get-prices-for-microsoft-azure.md) [a](get-a-customer-s-utilization-record-for-azure.md) Získání cen Microsoft Azure dat.*

Prostředek **SubscriptionDailyUsageRecord** popisuje, kolik předplatného se používá za jeden den.

| Vlastnost         | Typ               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | řetězec             | Den ve formátu data a času, kdy bylo předplatné použito.                                 |
| ResourceId       | řetězec             | Identifikátor guid. Jedinečné ID prostředku.                                                          |
| ResourceName     | řetězec             | Název prostředku.                                                                     |
| TotalCost        | decimal             | Odhadované celkové náklady na používání prostředků v předplatném v zadaný den.     |
| CurrencyLocale   | řetězec             | Národní prostředí, ve kterém se předplatné použilo, určuje měnu, která se má na faktuře použít. |
| LastModifiedDate. | řetězec             | Den ve formátu data a času, kdy se tento záznam naposledy změnil.                             |
| Atributy       | Atributy prostředků | Atributy metadat odpovídající prostředku.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

Prostředek **SubscriptionMonthlyUsageRecord** popisuje, kolik předplatného se používá za jeden měsíc.

| Vlastnost         | Typ               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Status           | řetězec             | Stav předplatného: žádné, Aktivní, Pozastaveno nebo Odstraněno.                  |
| Záznam PartnerOn  | řetězec             | ID MPN partnera v záznamu.                                                        |
| ID nabídky          | řetězec             | Identifikátor guid. ID nabídky související s tímto předplatným.                                       |
| Id               | řetězec             | Identifikátor guid. ID předplatného nebo prostředku.                                                 |
| Name             | řetězec             | Název předplatného nebo prostředku.                                                     |
| TotalCost        | decimal             | Odhadované celkové náklady na používání prostředků v předplatném v zadaném měsíci   |
| CurrencyLocale   | řetězec             | Národní prostředí, ve kterém se předplatné použilo, určuje měnu, která se má na faktuře použít. K dispozici Microsoft Azure předplatných (MS-AZR-0145P). |
| CurrencyCode     | řetězec             | Získá nebo nastaví kód měny. K dispozici pro prostředky předplatného plánu Azure.                                         |
| USDTotalCost     | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. K dispozici pro plány Azure.                                         |
| LastModifiedDate. | řetězec             | Den ve formátu data a času, kdy se tento záznam naposledy změnil.                             |
| Atributy       | Atributy prostředků | Atributy metadat odpovídající prostředku.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

Prostředek **SubscriptionUsageSummary** popisuje, kolik konkrétního předplatného bylo použito v aktuálním fakturačním období.

| Vlastnost         | Typ               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | řetězec             | Identifikátor guid. ID předplatného nebo prostředku. V kontextu CustomerMonthlyUsageRecord je toto ID ID zákazníka. |
| ResourceName     | řetězec             | Název předplatného nebo prostředku. V kontextu CustomerMonthlyUsageRecord je tento název jméno zákazníka. |
| BillingStartDate | date               | Počáteční datum aktuálního fakturačního období ve formátu data a času.                                                     |
| BillingEndDate   | date               | Koncové datum aktuálního fakturačního období ve formátu data a času.                                                       |
| TotalCost        | double             | Odhadované celkové náklady na používání prostředků v předplatném během zadaného fakturačního období.               |
| CurrencyLocale   | řetězec             | Národní prostředí, ve kterém se předplatné použilo, určuje měnu, která se má na faktuře použít. K dispozici Microsoft Azure předplatných (MS-AZR-0145P). |
| CurrencyCode   | řetězec             | Získá nebo nastaví kód měny. K dispozici pro plány Azure.                                         |
| USDTotalCost   | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. K dispozici pro prostředky předplatného plánu Azure.                                         |
| LastModifiedDate. | řetězec             | Den ve formátu data a času, kdy se tento záznam naposledy změnil.                                                      |
| Odkazy            | Odkazy na prostředky      | Propojení prostředků odpovídající předplatnému SubscriptionUsageSummary.                                                      |
| Atributy       | Atributy prostředků | Atributy metadat odpovídající vlastnosti SubscriptionUsageSummary.                                                 |
