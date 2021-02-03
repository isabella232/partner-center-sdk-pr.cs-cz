---
title: Prostředky nákladů na službu
description: Popisuje prostředky související se službami zakoupenými zákazníkem.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c0236329d93d8ddc9019a15fb67a81a3af3e7620
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766817"
---
# <a name="service-costs-resources"></a>Prostředky nákladů na službu

**Platí pro:**

- Partnerské centrum

Popisuje prostředky související se službami zakoupenými zákazníkem.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** obsahuje souhrn, který agreguje všechny služby zakoupené zadaným zákazníkem během fakturačního období.

| Vlastnost | Typ | Description |
| -------- | ---- | ----------- |
| zobrazí | pole objektů [ServiceCostsSummaryDetail](#servicecostssummarydetail) | Seznam podrobných informací o nákladech služby, který se odlišuje podle typu faktury|
| odkazy | [ResourceLinks](utility-resources.md#resourcelinks) | Odkazy na prostředky. |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat. |

> [!IMPORTANT]
> **Pole v následující tabulce jsou zastaralá.** Chcete-li načíst periodické a jednorázové souhrny nákladů na službu, použijte místo toho pole **Podrobnosti** . Pole **podrobností** je popsáno v předchozí tabulce. Podívejte se na odpovídající hodnoty dat v poli **Details** , ale ne na pole na úrovni root.

| Vlastnost | Typ | Description |
| -------- | ---- | ----------- |
| billingStartDate | date | Začátek fakturačního období. |
| billingEndDate | date | Konec fakturačního období. |
| pretaxTotal | double | Celkový součet všech nákladů pro zákazníka. |
| daňových  | double | Celková daň vzniklá u všech položek zakoupených zákazníkem. |
| afterTaxTotal | double | Celkové náklady na netto pro všechny položky, které zákazník zakoupil. |
| currencyCode | řetězec | Představuje měnu použitou pro náklady. |
| currencySymbol | řetězec | Symbol měny použitý pro náklady |
| customerId | řetězec | ID zákazníka, který provádí nákup |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** popisuje souhrn nákladů na službu, který agreguje všechny služby zakoupené zadaným zákazníkem během fakturačního období (z buď opakujících se nebo jednorázových faktur).

| Vlastnost | Typ | Description |
| -------- | ---- | ----------- |
| invoiceType | řetězec | InvoiceType, že byly vygenerovány souhrn nákladů služby. |
| shrnutí | [ServiceCostsSummary](#servicecostssummary) | Souhrn nákladů služby agregovaný zákazníkem v rámci jednoho typu faktury. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem** popisuje jednu položku zakoupenou zákazníkem.

> [!IMPORTANT]
> Následující vlastnosti *platí jenom pro položky s náklady na* službu, u kterých je produkt *jednorázové nákupy*: **ProductID**, **ProductName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **Publisher**, **termAndBillingCycle**, **discountDetails**. Tyto vlastnosti se *nevztahují na* položky řádku služby, ve kterých je produkt *opakovaný nákup*. Tyto vlastnosti se například *nevztahují* na sady Office 365 a Azure založené na předplatném.

| Vlastnost                 | Typ                           | Description                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | řetězec ve formátu data a času standardu UTC | Počáteční datum poplatku.                                       |
| endDate                  | řetězec ve formátu data a času standardu UTC | Koncové datum poplatku.                                         |
| subscriptionFriendlyName | řetězec                         | Popisný název předplatného.                              |
| subscriptionId           | řetězec                         | Identifikátor předplatného.                                         |
| Seskup                  | řetězec                         | Identifikátor objednávky.                                                |
| Hodnotami OfferId                  | řetězec                         | Identifikátor nabídky                                                |
| offerName                | řetězec                         | Název nabídky                                                      |
| resellerMPNId            | řetězec                         | Používá se jenom ve dvou partnerských scénářích. Odkazuje na identifikátor MPN. |
| chargeType               | řetězec                         | Typ přidruženého účtování                                          |
| quantity                 | číslo                         | Množství použitých nebo zakoupených jednotek.                             |
| unitPrice                | číslo                         | Cena za jednotku                                                  |
| pretaxTotal              | číslo                         | Celkový poplatek za tuto položku před zdaněním.                         |
| daňových                      | číslo                         | Celkový daňový poplatek vynaložený za tuto položku.                         |
| afterTaxTotal            | číslo                         | Celkové náklady na netto pro tuto položku.                                    |
| currencyCode             | řetězec                         | Představuje měnu použitou pro náklady.                          |
| currencySymbol           | řetězec                         | Symbol měny použitý pro náklady                              |
| customerId               | řetězec                         | ID zákazníka, který provádí nákup                          |
| customerName             | řetězec                         | Jméno zákazníka, který provádí nákup                        |
| invoiceNumber            | řetězec                         | Číslo faktury, ke které patří tato položka řádku                   |
| productId                | řetězec                         | Identifikátor produktu.                                              |
| skuId                    | řetězec                         | Identifikátor SKU.                                                  |
| availabilityId           | řetězec                         | Identifikátor dostupnosti.                                         |
| NázevVýrobku              | řetězec                         | Název produktu                                                    |
| skuName                  | řetězec                         | Název SKU.                                                        |
| publisherName            | řetězec                         | Název vydavatele                                                  |
| publisherId              | řetězec                         | Identifikátor vydavatele                                            |
| termAndBillingCycle      | řetězec                         | Období a fakturační cyklus.                                          |
| discountDetails          | řetězec                         | Podrobnosti o slevě.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Vlastnost             | Typ                               | Description                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Odkaz](utility-resources.md#link) | Identifikátor URI pro načtení položek čáry |
| samorozbalující                 | [Odkaz](utility-resources.md#link) | Identifikátor URI samostatného.                       |
