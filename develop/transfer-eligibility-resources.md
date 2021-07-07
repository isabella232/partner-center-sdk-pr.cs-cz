---
title: PřevodSchůdnost prostředků
description: Partner může vytvořit převod, když zákazník požádá o převod předplatného s partnerem na jiného partnera.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530204"
---
# <a name="transfereligibility-resources"></a><span data-ttu-id="fba1c-103">PřevodSchůdnost prostředků</span><span class="sxs-lookup"><span data-stu-id="fba1c-103">TransferEligibility resources</span></span>

<span data-ttu-id="fba1c-104">Partner může vytvořit převod, když zákazník požádá o převod předplatného s partnerem na jiného partnera.</span><span class="sxs-lookup"><span data-stu-id="fba1c-104">A partner can create a transfer when a customer requests their subscription with the partner to be transferred to another partner.</span></span> <span data-ttu-id="fba1c-105">Pomocí možnosti TransferEligibility (Nárok na převod) zkontrolujte, jestli má předplatné nárok na převod.</span><span class="sxs-lookup"><span data-stu-id="fba1c-105">Use TransferEligibility to check whether a subscription is eligible to be transferred.</span></span>

## <a name="transfereligibility"></a><span data-ttu-id="fba1c-106">PřevodOchemiitelnost</span><span class="sxs-lookup"><span data-stu-id="fba1c-106">TransferEligibility</span></span>

<span data-ttu-id="fba1c-107">Popisuje přenositelnost.</span><span class="sxs-lookup"><span data-stu-id="fba1c-107">Describes a transferEligibility.</span></span>

| <span data-ttu-id="fba1c-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fba1c-108">Property</span></span>              | <span data-ttu-id="fba1c-109">Typ</span><span class="sxs-lookup"><span data-stu-id="fba1c-109">Type</span></span>             | <span data-ttu-id="fba1c-110">Description</span><span class="sxs-lookup"><span data-stu-id="fba1c-110">Description</span></span>                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="fba1c-111">id</span><span class="sxs-lookup"><span data-stu-id="fba1c-111">id</span></span>                    | <span data-ttu-id="fba1c-112">řetězec</span><span class="sxs-lookup"><span data-stu-id="fba1c-112">string</span></span>           | <span data-ttu-id="fba1c-113">Identifikátor předplatného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fba1c-113">The customer's subscription identifier.</span></span>                                                  |
| <span data-ttu-id="fba1c-114">isEligible</span><span class="sxs-lookup"><span data-stu-id="fba1c-114">isEligible</span></span>            | <span data-ttu-id="fba1c-115">bool</span><span class="sxs-lookup"><span data-stu-id="fba1c-115">bool</span></span>             | <span data-ttu-id="fba1c-116">Určuje, jestli má předplatné nárok na převod.</span><span class="sxs-lookup"><span data-stu-id="fba1c-116">Indicates whether the subscription is eligible for the transfer.</span></span>                         |
| <span data-ttu-id="fba1c-117">Důvod</span><span class="sxs-lookup"><span data-stu-id="fba1c-117">Reason</span></span>                | <span data-ttu-id="fba1c-118">řetězec</span><span class="sxs-lookup"><span data-stu-id="fba1c-118">string</span></span>           | <span data-ttu-id="fba1c-119">Vlastnost reason vysvětluje, proč předplatné nemá nárok na převod.</span><span class="sxs-lookup"><span data-stu-id="fba1c-119">The reason property explains why the subscription isn't eligible for transfer.</span></span> |