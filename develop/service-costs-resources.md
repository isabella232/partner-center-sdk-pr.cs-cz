---
title: Prostředky nákladů na službu
description: Popisuje prostředky související se službami zakoupenými zákazníkem.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c1e3a05be89eee12d708a3a37e008ec7fa42358eaec7e1f020aaa47e44b452c
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996134"
---
# <a name="service-costs-resources"></a>Prostředky nákladů na službu

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
> Následující vlastnosti *platí jenom pro položky s náklady na* službu, u kterých je produkt *jednorázové nákupy*: **ProductID**, **ProductName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **Publisher**, **termAndBillingCycle**, **discountDetails**. Tyto vlastnosti se *nevztahují na* položky řádku služby, ve kterých je produkt *opakovaný nákup*. tyto vlastnosti se například *nevztahují* na Office 365 a Azure na základě předplatného.

| Vlastnost                 | Typ                           | Description                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | řetězec ve formátu data a času standardu UTC | Počáteční datum poplatku.                                       |
| endDate                  | řetězec ve formátu data a času standardu UTC | Koncové datum poplatku.                                         |
| subscriptionFriendlyName | řetězec                         | Popisný název předplatného.                              |
| subscriptionId           | řetězec                         | Identifikátor předplatného.                                         |
| Seskup                  | řetězec                         | Identifikátor objednávky.                                                |
| Hodnotami OfferId                  | řetězec                         | Identifikátor nabídky                                                |
| offerName                | řetězec                         | Název nabídky                                                      |
| resellerMPNId            | řetězec                         | Používá se jenom ve scénářích partnerských partnerů. Odkazuje na identifikátor MPN. |
| chargeType               | řetězec                         | Typ přidruženého účtování                                          |
| quantity                 | číslo                         | Množství použitých nebo zakoupených jednotek.                             |
| unitPrice                | číslo                         | Cena za jednotku                                                  |
| pretaxTotal              | číslo                         | Celkový poplatek za tuto položku před daněmi.                         |
| Daňové                      | číslo                         | Celková daňová poplatek za tuto položku                         |
| afterTaxTotal            | číslo                         | Celkové náklady na tuto položku                                    |
| currencyCode             | řetězec                         | Představuje měnu použitou pro náklady.                          |
| Currencysymbol           | řetězec                         | Symbol měny použitý pro náklady.                              |
| customerId               | řetězec                         | ID zákazníka, který nákup zakoupí.                          |
| customerName             | řetězec                         | Jméno zákazníka, který nákup zakoupí.                        |
| invoiceNumber            | řetězec                         | Číslo faktury, ke které tato řádková položka patří.                   |
| productId                | řetězec                         | Identifikátor produktu.                                              |
| ID SKU                    | řetězec                         | Identifikátor SKU.                                                  |
| ID dostupnosti           | řetězec                         | Identifikátor dostupnosti.                                         |
| Productname              | řetězec                         | Název produktu.                                                    |
| skuName                  | řetězec                         | Název SKU                                                        |
| publisherName            | řetězec                         | Název vydavatele.                                                  |
| ID vydavatele              | řetězec                         | Identifikátor vydavatele.                                            |
| termAndBillingCycle      | řetězec                         | Období a fakturační cyklus.                                          |
| discountDetails          | řetězec                         | Podrobnosti o slevě                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Vlastnost             | Typ                               | Description                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Odkaz](utility-resources.md#link) | Identifikátor URI pro načtení řádkové položky. |
| Vlastní                 | [Odkaz](utility-resources.md#link) | Identifikátor URI sebe sama.                       |
