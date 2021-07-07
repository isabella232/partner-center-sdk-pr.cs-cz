---
title: Prostředky rozhraní API pro útratu v Azure
description: Zjistěte, jak mohou partneři CSP pomocí Partnerské centrum API zobrazit a spravovat útraty a využití Azure partnerů a zákazníků v jejich rozpočtech.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 472554de1c354559d5bc4b21959c109467891806
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974314"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a>Prostředky rozhraní API pro útratu v Azure pro správu útraty partnerů nebo zákazníků a využití v rozpočtu 

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Cloud Solution Provider (CSP) mohou zobrazit a spravovat své výdaje za Azure prostřednictvím Partnerské centrum API. Mohou také programově zobrazit útratu zákazníků oproti rozpočtu útraty za Azure.

Další informace najdete v situacích, ve kterých zprostředkovatelé CSP mohou pomocí rozhraní API Partnerské centrum ke správě zákaznických a partnerských účtů a [objednávek.](scenarios.md)

## <a name="partner-usage-management"></a>Správa využití partnerů

- [Získání souhrnu využití partnera](get-a-partner-usage-summary.md) pomocí prostředku **PartnerUsageSummary**
- [Získání záznamů o využití pro všechny zákazníky](get-a-customer-s-usage-records.md) pomocí prostředku **CustomerMonthlyUsageRecord**

## <a name="customer-usage-management"></a>Správa využití zákazníků

- [Získání souhrnu využití zákazníka pomocí](get-a-customer-usage-summary.md) prostředku **CustomerUsageSummary**
- [Získání všech záznamů o využití předplatného pro zákazníka](get-a-customer-subscription-s-usage-records.md) pomocí prostředku **SubscriptionMonthlyUsageRecord**

## <a name="subscription-usage-management"></a>Správa využití předplatného

- [Získání souhrnu využití předplatného](get-a-customer-subscription-usage-summary.md) pomocí prostředku **SubscriptionUsageSummary**
- [Získání všech záznamů o měsíčním využití předplatného](get-all-monthly-usage-records-for-a-subscription.md) pomocí prostředku **AzureResourceMonthlyUsageRecord**
- [Získání dat o využití předplatného podle prostředku](get-a-customer-subscription-resource-usage-records.md) s využitím prostředku **ResourceUsageRecord**
- [Získání dat o využití pro předplatné podle měřiče](get-a-customer-subscription-meter-usage-records.md) s využitím **prostředku MeterUsageRecord**

## <a name="azure-spending-budget-management"></a>Správa rozpočtu na útratu v Azure

- [Získání rozpočtu na využití zákazníka pomocí](get-a-customer-s-usage-spending-budget.md) prostředku **CustomerUsageSummary**
- [Aktualizace rozpočtu na využití zákazníka pomocí](update-a-customer-s-usage-spending-budget.md) prostředku **CustomerUsageSummary**
