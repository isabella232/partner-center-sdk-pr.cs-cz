---
title: Prostředky rozhraní API pro Azure útraty
description: Přečtěte si, jak můžou partneři CSP používat rozhraní API partnerského centra k zobrazení a správě výdajů a využití Azure pro partnery a zákazníky na jejich rozpočet.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 02a2995a06473cc6990d1234acd522a3b38a03d3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2020
ms.locfileid: "97767083"
---
# <a name="azure-spending-api-resources-to-manage-partner-or-customer-spending-and-usage-against-a-budget"></a><span data-ttu-id="6c5a7-103">Prostředky rozhraní API pro Azure útraty pro správu využití a výdajů na zákazníky na základě rozpočtu</span><span class="sxs-lookup"><span data-stu-id="6c5a7-103">Azure spending API resources to manage partner or customer spending and usage against a budget</span></span> 

<span data-ttu-id="6c5a7-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-104">**Applies to:**</span></span>

- <span data-ttu-id="6c5a7-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="6c5a7-105">Partner Center</span></span>
- <span data-ttu-id="6c5a7-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="6c5a7-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="6c5a7-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="6c5a7-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6c5a7-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6c5a7-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6c5a7-109">Partneři poskytovatele Cloud Solution Provider (CSP) můžou zobrazit a spravovat výdaje na Azure prostřednictvím rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="6c5a7-109">Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs.</span></span> <span data-ttu-id="6c5a7-110">Můžou také programově zobrazit výdaje svých zákazníků na rozpočet útraty Azure.</span><span class="sxs-lookup"><span data-stu-id="6c5a7-110">They can also programmatically view their customers' spending against an Azure spending budget.</span></span>

<span data-ttu-id="6c5a7-111">Další informace najdete v tématu [scénáře, ve kterých můžou partneři CSP používat rozhraní API partnerského centra ke správě účtů a objednávek zákazníků a partnerů](scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="6c5a7-111">For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md).</span></span>

## <a name="partner-usage-management"></a><span data-ttu-id="6c5a7-112">Správa využití partnerů</span><span class="sxs-lookup"><span data-stu-id="6c5a7-112">Partner usage management</span></span>

- <span data-ttu-id="6c5a7-113">[Získání souhrnu využití partnera](get-a-partner-usage-summary.md) pomocí prostředku **PartnerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-113">[Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource</span></span>
- <span data-ttu-id="6c5a7-114">[Získat záznamy o využití pro všechny zákazníky](get-a-customer-s-usage-records.md) pomocí prostředku **CustomerMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-114">[Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource</span></span>

## <a name="customer-usage-management"></a><span data-ttu-id="6c5a7-115">Správa využívání zákazníků</span><span class="sxs-lookup"><span data-stu-id="6c5a7-115">Customer usage management</span></span>

- <span data-ttu-id="6c5a7-116">[Získání souhrnu využití zákazníka](get-a-customer-usage-summary.md) pomocí prostředku **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-116">[Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="6c5a7-117">[Získání všech záznamů o využití předplatných pro zákazníka](get-a-customer-subscription-s-usage-records.md) pomocí prostředku **SubscriptionMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-117">[Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource</span></span>

## <a name="subscription-usage-management"></a><span data-ttu-id="6c5a7-118">Správa využití předplatných</span><span class="sxs-lookup"><span data-stu-id="6c5a7-118">Subscription usage management</span></span>

- <span data-ttu-id="6c5a7-119">[Získání souhrnu využití předplatného](get-a-customer-subscription-usage-summary.md) pomocí prostředku **SubscriptionUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-119">[Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource</span></span>
- <span data-ttu-id="6c5a7-120">[Získání všech měsíčních záznamů o využití pro předplatné](get-all-monthly-usage-records-for-a-subscription.md) pomocí prostředku **AzureResourceMonthlyUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-120">[Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource</span></span>
- <span data-ttu-id="6c5a7-121">[Získat data o využití pro předplatné podle prostředku](get-a-customer-subscription-resource-usage-records.md) pomocí prostředku **ResourceUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-121">[Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource</span></span>
- <span data-ttu-id="6c5a7-122">[Získat data o využití pro předplatné podle měřiče](get-a-customer-subscription-meter-usage-records.md) pomocí prostředku **MeterUsageRecord**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-122">[Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource</span></span>

## <a name="azure-spending-budget-management"></a><span data-ttu-id="6c5a7-123">Správa rozpočtu útraty Azure</span><span class="sxs-lookup"><span data-stu-id="6c5a7-123">Azure spending budget management</span></span>

- <span data-ttu-id="6c5a7-124">[Získání rozpočtu využití zákazníka](get-a-customer-s-usage-spending-budget.md) pomocí prostředku **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-124">[Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
- <span data-ttu-id="6c5a7-125">[Aktualizace rozpočtu využití zákazníka](update-a-customer-s-usage-spending-budget.md) pomocí prostředku **CustomerUsageSummary**</span><span class="sxs-lookup"><span data-stu-id="6c5a7-125">[Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource</span></span>
