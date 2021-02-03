---
title: Prostředky TransferEligibility
description: Partner vytvoří přenos, pokud chce zákazník své předplatné s partnerem přenést na jiného partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766738"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="820bc-103">Prostředky TransferEligibility</span><span class="sxs-lookup"><span data-stu-id="820bc-103">TransferEligibility resources</span></span>

<span data-ttu-id="820bc-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="820bc-104">**Applies to:**</span></span>

- <span data-ttu-id="820bc-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="820bc-105">Partner Center</span></span>

<span data-ttu-id="820bc-106">Partner vytvoří přenos, pokud chce zákazník své předplatné s partnerem přenést na jiného partnera.</span><span class="sxs-lookup"><span data-stu-id="820bc-106">A partner creates a transfer when a customer wants their subscription with the partner to be transferred to another partner.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="820bc-107">TransferEligibility</span><span class="sxs-lookup"><span data-stu-id="820bc-107">TransferEligibility</span></span>

<span data-ttu-id="820bc-108">Popisuje transferEligibility.</span><span class="sxs-lookup"><span data-stu-id="820bc-108">Describes a transferEligibility.</span></span>

| <span data-ttu-id="820bc-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="820bc-109">Property</span></span>              | <span data-ttu-id="820bc-110">Typ</span><span class="sxs-lookup"><span data-stu-id="820bc-110">Type</span></span>             | <span data-ttu-id="820bc-111">Description</span><span class="sxs-lookup"><span data-stu-id="820bc-111">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="820bc-112">id</span><span class="sxs-lookup"><span data-stu-id="820bc-112">id</span></span>                    | <span data-ttu-id="820bc-113">řetězec</span><span class="sxs-lookup"><span data-stu-id="820bc-113">string</span></span>           | <span data-ttu-id="820bc-114">Identifikátor předplatného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="820bc-114">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="820bc-115">Oprávněné</span><span class="sxs-lookup"><span data-stu-id="820bc-115">isEligible</span></span>            | <span data-ttu-id="820bc-116">bool</span><span class="sxs-lookup"><span data-stu-id="820bc-116">bool</span></span>             | <span data-ttu-id="820bc-117">Uvádí, zda má předplatné nárok na přenos.</span><span class="sxs-lookup"><span data-stu-id="820bc-117">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="820bc-118">Důvod</span><span class="sxs-lookup"><span data-stu-id="820bc-118">Reason</span></span>                | <span data-ttu-id="820bc-119">řetězec</span><span class="sxs-lookup"><span data-stu-id="820bc-119">string</span></span>           | <span data-ttu-id="820bc-120">Vlastnost důvod vysvětluje, proč odběr není způsobilý pro přenos.</span><span class="sxs-lookup"><span data-stu-id="820bc-120">The reason property explains why the subscription isn't eligible for transfer.</span></span> |