---
title: Stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
description: Prostředek DirectSignedCustomerAgreementStatus představuje stav přímého podepisování (přímé přijetí) zákaznické smlouvy.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d4d97667b5fd6b92c85889f1288dd770c2d1c035
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973107"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a><span data-ttu-id="df8bc-103">Stav přímého podepisování (přímé přijetí) pro zákaznickou smlouvu</span><span class="sxs-lookup"><span data-stu-id="df8bc-103">Direct signing (direct acceptance) status of a customer agreement</span></span>

<span data-ttu-id="df8bc-104">**Platí pro**: partnerské Centrum</span><span class="sxs-lookup"><span data-stu-id="df8bc-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="df8bc-105">Nevztahuje **se na**: partnerské Centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="df8bc-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="df8bc-106">Partner Center v současné době podporuje prostředek **DirectSignedCustomerAgreementStatus** jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="df8bc-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="df8bc-107">Prostředek **DirectSignedCustomerAgreementStatus** představuje stav přímého přijetí smlouvy se zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="df8bc-107">The **DirectSignedCustomerAgreementStatus** resource represents the status of the direct acceptance of a customer agreement.</span></span>

## <a name="directsignedcustomeragreementstatus"></a><span data-ttu-id="df8bc-108">DirectSignedCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="df8bc-108">DirectSignedCustomerAgreementStatus</span></span>

<span data-ttu-id="df8bc-109">Prostředek **DirectSignedCustomerAgreementStatus** obsahuje následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="df8bc-109">A **DirectSignedCustomerAgreementStatus** resource includes the following properties:</span></span>

| <span data-ttu-id="df8bc-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="df8bc-110">Property</span></span>       | <span data-ttu-id="df8bc-111">Typ</span><span class="sxs-lookup"><span data-stu-id="df8bc-111">Type</span></span>   | <span data-ttu-id="df8bc-112">Description</span><span class="sxs-lookup"><span data-stu-id="df8bc-112">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="df8bc-113">Podepsaný</span><span class="sxs-lookup"><span data-stu-id="df8bc-113">isSigned</span></span> | <span data-ttu-id="df8bc-114">boolean</span><span class="sxs-lookup"><span data-stu-id="df8bc-114">boolean</span></span> | <span data-ttu-id="df8bc-115">Určuje, jestli je zákazníkská smlouva od zákazníka přímo podepsaná (přijatá).</span><span class="sxs-lookup"><span data-stu-id="df8bc-115">Indicates if the customer agreement has been directly signed (accepted) by the customer.</span></span> |
