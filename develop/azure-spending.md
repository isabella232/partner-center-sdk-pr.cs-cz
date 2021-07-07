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
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="74f9c-103">Prostředky rozhraní API pro útratu v Azure pro správu útraty partnerů nebo zákazníků a využití v rozpočtu</span><span class="sxs-lookup"><span data-stu-id="74f9c-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="74f9c-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="74f9c-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="74f9c-105">Cloud Solution Provider (CSP) mohou zobrazit a spravovat své výdaje za Azure prostřednictvím Partnerské centrum API.</span><span class="sxs-lookup"><span data-stu-id="74f9c-105">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="74f9c-106">Mohou také programově zobrazit útratu zákazníků oproti rozpočtu útraty za Azure.</span><span class="sxs-lookup"><span data-stu-id="74f9c-106">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="74f9c-107">Další informace najdete v situacích, ve kterých zprostředkovatelé CSP mohou pomocí rozhraní API Partnerské centrum ke správě zákaznických a partnerských účtů a [objednávek.](scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="74f9c-107">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="74f9c-108">Správa využití partnerů</span><span class="sxs-lookup"><span data-stu-id="74f9c-108">Partner usage management</span></span>

- <span data-ttu-id="74f9c-109">[Získání souhrnu využití partnera](get-a-partner-usage-summary.md) pomocí prostředku **PartnerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="74f9c-109">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="74f9c-110">[Získání záznamů o využití pro všechny zákazníky](get-a-customer-s-usage-records.md) pomocí prostředku **CustomerMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="74f9c-110">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="74f9c-111">Správa využití zákazníků</span><span class="sxs-lookup"><span data-stu-id="74f9c-111">Customer usage management</span></span>

- <span data-ttu-id="74f9c-112">[Získání souhrnu využití zákazníka pomocí](get-a-customer-usage-summary.md) prostředku **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="74f9c-112">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="74f9c-113">[Získání všech záznamů o využití předplatného pro zákazníka](get-a-customer-subscription-s-usage-records.md) pomocí prostředku **SubscriptionMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="74f9c-113">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="74f9c-114">Správa využití předplatného</span><span class="sxs-lookup"><span data-stu-id="74f9c-114">Subscription usage management</span></span>

- <span data-ttu-id="74f9c-115">[Získání souhrnu využití předplatného](get-a-customer-subscription-usage-summary.md) pomocí prostředku **SubscriptionUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="74f9c-115">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="74f9c-116">[Získání všech záznamů o měsíčním využití předplatného](get-all-monthly-usage-records-for-a-subscription.md) pomocí prostředku **AzureResourceMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="74f9c-116">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="74f9c-117">[Získání dat o využití předplatného podle prostředku](get-a-customer-subscription-resource-usage-records.md) s využitím prostředku **ResourceUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="74f9c-117">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="74f9c-118">[Získání dat o využití pro předplatné podle měřiče](get-a-customer-subscription-meter-usage-records.md) s využitím **prostředku MeterUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="74f9c-118">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="74f9c-119">Správa rozpočtu na útratu v Azure</span><span class="sxs-lookup"><span data-stu-id="74f9c-119">Azure spending budget management</span></span>

- <span data-ttu-id="74f9c-120">[Získání rozpočtu na využití zákazníka pomocí](get-a-customer-s-usage-spending-budget.md) prostředku **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="74f9c-120">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="74f9c-121">[Aktualizace rozpočtu na využití zákazníka pomocí](update-a-customer-s-usage-spending-budget.md) prostředku **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="74f9c-121">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
