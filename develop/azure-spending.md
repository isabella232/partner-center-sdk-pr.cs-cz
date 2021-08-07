---
title: Prostředky rozhraní API pro Azure útraty
description: Přečtěte si, jak můžou partneři CSP používat rozhraní API partnerského centra k zobrazení a správě výdajů a využití Azure pro partnery a zákazníky na jejich rozpočet.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b51ccbcdaee18b6d5b3bd1b9531a64b22c8bac5a9d95e6cf94291ee802ed5d9
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992394"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Prostředky rozhraní API pro Azure útraty pro správu využití a výdajů na zákazníky na základě rozpočtu 

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

partneři Cloud Solution Provider (CSP) mohou zobrazit a spravovat své výdaje na Azure prostřednictvím rozhraní api partnerského centra. Můžou také programově zobrazit výdaje svých zákazníků na rozpočet útraty Azure.

Další informace najdete v tématu [scénáře, ve kterých můžou partneři CSP používat rozhraní API partnerského centra ke správě účtů a objednávek zákazníků a partnerů](scenarios.md).

## <a name="partner-usage-management"></a>Správa využití partnerů

- [Získání souhrnu využití partnera](get-a-partner-usage-summary.md) pomocí prostředku **PartnerUsageSummary**
- [Získat záznamy o využití pro všechny zákazníky](get-a-customer-s-usage-records.md) pomocí prostředku **CustomerMonthlyUsageRecord**

## <a name="customer-usage-management"></a>Správa využívání zákazníků

- [Získání souhrnu využití zákazníka](get-a-customer-usage-summary.md) pomocí prostředku **CustomerUsageSummary**
- [Získání všech záznamů o využití předplatných pro zákazníka](get-a-customer-subscription-s-usage-records.md) pomocí prostředku **SubscriptionMonthlyUsageRecord**

## <a name="subscription-usage-management"></a>Správa využití předplatných

- [Získání souhrnu využití předplatného](get-a-customer-subscription-usage-summary.md) pomocí prostředku **SubscriptionUsageSummary**
- [Získání všech měsíčních záznamů o využití pro předplatné](get-all-monthly-usage-records-for-a-subscription.md) pomocí prostředku **AzureResourceMonthlyUsageRecord**
- [Získat data o využití pro předplatné podle prostředku](get-a-customer-subscription-resource-usage-records.md) pomocí prostředku **ResourceUsageRecord**
- [Získat data o využití pro předplatné podle měřiče](get-a-customer-subscription-meter-usage-records.md) pomocí prostředku **MeterUsageRecord**

## <a name="azure-spending-budget-management"></a>Správa rozpočtu útraty Azure

- [Získání rozpočtu využití zákazníka](get-a-customer-s-usage-spending-budget.md) pomocí prostředku **CustomerUsageSummary**
- [Aktualizace rozpočtu využití zákazníka](update-a-customer-s-usage-spending-budget.md) pomocí prostředku **CustomerUsageSummary**
