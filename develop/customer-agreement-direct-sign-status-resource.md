---
title: Stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
description: Prostředek DirectSignedCustomerAgreementStatus představuje stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766683"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a><span data-ttu-id="0cfad-103">Stav přímého podepisování (přímé přijetí) pro zákaznickou smlouvu</span><span class="sxs-lookup"><span data-stu-id="0cfad-103">Direct signing (direct acceptance) status of a customer agreement</span></span>

<span data-ttu-id="0cfad-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="0cfad-104">**Applies to:**</span></span>

- <span data-ttu-id="0cfad-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0cfad-105">Partner Center</span></span>

<span data-ttu-id="0cfad-106">Partner Center v současné době podporuje prostředek **DirectSignedCustomerAgreementStatus** jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0cfad-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="0cfad-107">Tento prostředek *nelze použít* pro:</span><span class="sxs-lookup"><span data-stu-id="0cfad-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="0cfad-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="0cfad-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0cfad-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="0cfad-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0cfad-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0cfad-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0cfad-111">Prostředek **DirectSignedCustomerAgreementStatus** představuje stav přímého přijetí smlouvy se zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="0cfad-111">The **DirectSignedCustomerAgreementStatus** resource represents the status of the direct acceptance of a customer agreement.</span></span>

## <a name="directsignedcustomeragreementstatus"></a><span data-ttu-id="0cfad-112">DirectSignedCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="0cfad-112">DirectSignedCustomerAgreementStatus</span></span>

<span data-ttu-id="0cfad-113">Prostředek **DirectSignedCustomerAgreementStatus** obsahuje následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="0cfad-113">A **DirectSignedCustomerAgreementStatus** resource includes the following properties:</span></span>

| <span data-ttu-id="0cfad-114">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="0cfad-114">Property</span></span>       | <span data-ttu-id="0cfad-115">Typ</span><span class="sxs-lookup"><span data-stu-id="0cfad-115">Type</span></span>   | <span data-ttu-id="0cfad-116">Description</span><span class="sxs-lookup"><span data-stu-id="0cfad-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0cfad-117">Podepsaný</span><span class="sxs-lookup"><span data-stu-id="0cfad-117">isSigned</span></span> | <span data-ttu-id="0cfad-118">boolean</span><span class="sxs-lookup"><span data-stu-id="0cfad-118">boolean</span></span> | <span data-ttu-id="0cfad-119">Určuje, jestli je zákazníkská smlouva od zákazníka přímo podepsaná (přijatá).</span><span class="sxs-lookup"><span data-stu-id="0cfad-119">Indicates if the customer agreement has been directly signed (accepted) by the customer.</span></span> |
