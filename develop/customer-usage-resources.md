---
title: Zdroje využívání zákaznických prostředků
description: Prostředky pro zákazníky s předplatnými na základě využití a měsíční rozpočty využití (včetně CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary a SpendingBudget).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ec82fcfe6c08a8ad55dd1fb48984859b954dd3c8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766682"
---
# <a name="customer-usage-resources"></a>Zdroje využívání zákaznických prostředků

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Zákazníci s předplatnými na základě využití můžou mít měsíční rozpočet na používání. Tato hodnota rozpočtu stanoví omezení maximálního využití zákazníka a umožňuje partnerovi sledovat jejich využití v průběhu času.

> [!NOTE]
> Čísla zákaznického používání jsou odhady (ne konečné hodnoty), které by se neměly používat pro účely fakturace.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** představuje odhadované peněžní náklady na využití zákazníka v aktuálním měsíci.

| Vlastnost         | Typ               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Rozpočet           | SpendingBudget     | Rozpočet útraty přidělený pro zákazníka.                          |
| PercentUsed      | decimal             | Procento využité z přiděleného rozpočtu.                        |
| ResourceId       | řetězec             | Jedinečný identifikátor prostředku                                   |
| ResourceName     | řetězec             | Název prostředku.                                                |
| TotalCost        | decimal             | Odhadované celkové náklady na využití prostředků v rámci předplatného.|
| CurrencyLocale   | řetězec             | Národní prostředí měny zákazníka. K dispozici pro předplatná Microsoft Azure (MS-AZR-0145P).            |
| CurrencyCode     | řetězec             | Získá nebo nastaví kód měny. K dispozici pro plány Azure.           |
| USDTotalCost     | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. K dispozici pro plány Azure.                                         |
| Upgradované       | bool             | Získá nebo nastaví hodnotu označující, jestli se má upgradovat předplatné Azure zákazníka. Hodnota **true** představuje zákazníky, kteří mají plán Azure.                         |
| LastModifiedDate. | date               | Datum, kdy se data o využití naposledy změnila                               |
| Atributy       | ResourceAttributes | Atributy metadat odpovídající záznamu o využití.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** představuje souhrn využití zákazníka pro celé fakturační období.

| Vlastnost         | Typ               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Rozpočet           | SpendingBudget     | Rozpočet útraty přidělený pro zákazníka.                                                                  |
| ResourceId       | řetězec             | Jedinečný identifikátor prostředku V kontextu CustomerMonthlyUsageRecord je toto ID ID zákazníka. |
| ResourceName     | řetězec             | Název prostředku. V kontextu CustomerMonthlyUsageRecord se jedná o jméno zákazníka.               |
| BillingStartDate | date               | Počáteční datum aktuálního fakturačního období.                                                                    |
| BillingEndDate   | date               | Koncové datum aktuálního fakturačního období.                                                                      |
| TotalCost        | decimal             | Odhadované celkové náklady na využití prostředků v rámci předplatného.                                         |
| CurrencyLocale   | řetězec             | Národní prostředí měny zákazníka. K dispozici pro předplatná Microsoft Azure (MS-AZR-0145P).                                         |
| CurrencyCode     | řetězec             | Získá nebo nastaví kód měny. K dispozici pro plány Azure.                                         |
| USDTotalCost     | decimal             | Získá nebo nastaví odhadované celkové náklady v USD. K dispozici pro prostředky předplatného Azure Plan.                                         |
| LastModifiedDate. | date               | Datum, kdy se data o využití naposledy změnila                                                                       |
| Odkazy            | ResourceLinks      | Odkazy na prostředky odpovídající souhrnu využití.                                                           |
| Atributy       | ResourceAttributes | Atributy metadat odpovídající souhrnu využití.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** představuje souhrn rozpočtu využití na úrovni partnera pro všechny zákazníky.

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
