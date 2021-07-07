---
title: Zdroje informací o využití pro zákazníky
description: Prostředky pro zákazníky s předplatným založeným na využití a měsíčními rozpočty využití (včetně CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary a SpendingBudget).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eae516e2f759dfc2e8f80e946a835d70760c5c9e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973039"
---
# <a name="customer-usage-resources"></a>Zdroje informací o využití pro zákazníky

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Zákazníci s předplatným založenými na využití mohou mít měsíční rozpočet na využití. Tento rozpočet nastavuje limit maximálního využití zákazníka a umožňuje partnerovi sledovat jeho využití v průběhu času.

> [!NOTE]
> Čísla zákaznického využití jsou odhady (ne konečné hodnoty), které by se neměly používat pro účely fakturace.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord představuje** odhadované peněžní náklady na využití zákazníka v aktuálním měsíci.

| Vlastnost         | Typ               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Rozpočet           | ÚtrataRozsádky     | Rozpočet útraty přidělený zákazníkovi                          |
| PercentUsed      | decimal             | Procento využité z přiděleného rozpočtu                        |
| ResourceId       | řetězec             | Jedinečný identifikátor prostředku.                                   |
| ResourceName     | řetězec             | Název prostředku.                                                |
| TotalCost        | decimal             | Odhadované celkové náklady na využití prostředků v předplatném|
| CurrencyLocale   | řetězec             | Národní prostředí měny zákazníka K dispozici Microsoft Azure předplatných (MS-AZR-0145P).            |
| CurrencyCode     | řetězec             | Získá nebo nastaví kód měny. K dispozici pro plány Azure.           |
| USDTotalCost     | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. K dispozici pro plány Azure.                                         |
| Jeupgradovaný       | bool             | Získá nebo nastaví hodnotu určující, jestli je předplatné Azure zákazníka upgradované. Hodnota **true představuje** zákazníky, kteří mají plán Azure.                         |
| LastModifiedDate. | date               | Datum poslední změny dat o využití                               |
| Atributy       | Atributy prostředků | Atributy metadat odpovídající záznamu o využití.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** představuje souhrn využití zákazníka za celé fakturační období.

| Vlastnost         | Typ               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Rozpočet           | ÚtrataRozsádky     | Rozpočet útraty přidělený zákazníkovi                                                                  |
| ResourceId       | řetězec             | Jedinečný identifikátor prostředku. V kontextu CustomerMonthlyUsageRecord je toto ID ID zákazníka. |
| ResourceName     | řetězec             | Název prostředku. V kontextu CustomerMonthlyUsageRecord se jedná o jméno zákazníka.               |
| BillingStartDate | date               | Počáteční datum aktuálního fakturačního období.                                                                    |
| BillingEndDate   | date               | Koncové datum aktuálního fakturačního období.                                                                      |
| TotalCost        | decimal             | Odhadované celkové náklady na využití prostředků v předplatném                                         |
| CurrencyLocale   | řetězec             | Národní prostředí měny zákazníka K dispozici Microsoft Azure předplatných (MS-AZR-0145P).                                         |
| CurrencyCode     | řetězec             | Získá nebo nastaví kód měny. K dispozici pro plány Azure.                                         |
| USDTotalCost     | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. K dispozici pro prostředky předplatného plánu Azure.                                         |
| LastModifiedDate. | date               | Datum poslední změny dat o využití                                                                       |
| Odkazy            | Odkazy na prostředky      | Odkazy na prostředky odpovídající souhrnu využití.                                                           |
| Atributy       | Atributy prostředků | Atributy metadat odpovídající souhrnu využití.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** představuje souhrn využití pro všechny zákazníky na úrovni partnera.

| Vlastnost         | Typ               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | pole řetězců   | Seznam e-mailových adres pro oznámení                                                                   |
| CustomerOverBudget | integer          | Počet zákazníků, kteří jsou nad rozpočtem.                                                                    |
| CustomersTrendingOver | integer       | Počet zákazníků, kteří se blíží rozpočtu.                                                     |
| CustomersWithUsageBasedSubscriptions  | integer | Počet zákazníků s předplatným založeným na využití.                                               |
| ResourceId       | řetězec             | Jedinečný identifikátor prostředku V kontextu CustomerMonthlyUsageRecord je toto ID ID zákazníka. |
| ResourceName     | řetězec             | Název prostředku. V kontextu CustomerMonthlyUsageRecord se jedná o jméno zákazníka.               |
| BillingStartDate | date               | Počáteční datum aktuálního fakturačního období.                                                                    |
| BillingEndDate   | date               | Koncové datum aktuálního fakturačního období.                                                                      |
| TotalCost        | decimal             | Odhadované celkové náklady na využívání zákazníků na základě aktuálního využití od začátku fakturačního období.      |
| CurrencyLocale   | řetězec             | Národní prostředí měny.                                                                                             |
| LastModifiedDate. | date               | Datum, kdy se data o využití naposledy změnila                                                                       |
| Odkazy            | ResourceLinks      | Odkazy na prostředky odpovídající souhrnu využití.                                                           |
| Atributy       | ResourceAttributes | Atributy metadat odpovídající souhrnu využití.                                                      |

## <a name="spendingbudget"></a>SpendingBudget

**SpendingBudget** představuje rozpočet přidělený tomuto zákazníkovi pro odběry založené na využití.

| Vlastnost   | Typ               | Description                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Částka     | decimal             | Přidělený rozpočet. Pokud je hodnota null, k tomuto zákazníkovi se nepřiřazuje žádný rozpočet útraty. |
| Atributy | ResourceAttributes | Atributy metadat odpovídající rozpočtu.                                                |
