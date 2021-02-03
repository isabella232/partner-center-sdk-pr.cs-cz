---
title: Prostředky dokumentu smlouvy
description: Prostředek AgreementDocument je dokument s smlouvou Microsoftu pro náhled a stažení. Podporuje ho Partnerská centra ve veřejném cloudu Microsoftu.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2020
ms.locfileid: "97767094"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a><span data-ttu-id="d2a88-104">Prostředky dokumentů smlouvy podporované partnerským centrem ve veřejném cloudu Microsoftu</span><span class="sxs-lookup"><span data-stu-id="d2a88-104">Agreement document resources supported by Partner Center in the Microsoft public cloud</span></span>

<span data-ttu-id="d2a88-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="d2a88-105">**Applies to:**</span></span>

- <span data-ttu-id="d2a88-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d2a88-106">Partner Center</span></span>

<span data-ttu-id="d2a88-107">Partner Center v současné době podporuje prostředek **AgreementDocument** jenom ve *veřejném cloudu Microsoftu*.</span><span class="sxs-lookup"><span data-stu-id="d2a88-107">The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="d2a88-108">Tento prostředek se nedá použít pro:</span><span class="sxs-lookup"><span data-stu-id="d2a88-108">This resource not applicable to:</span></span>

- <span data-ttu-id="d2a88-109">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d2a88-109">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d2a88-110">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="d2a88-110">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d2a88-111">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d2a88-111">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d2a88-112">Prostředek **AgreementDocument** představuje dokument smlouvy Microsoft, který je k dispozici pro náhled a stažení.</span><span class="sxs-lookup"><span data-stu-id="d2a88-112">The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.</span></span>

## <a name="agreementdocument"></a><span data-ttu-id="d2a88-113">AgreementDocument</span><span class="sxs-lookup"><span data-stu-id="d2a88-113">AgreementDocument</span></span>

<span data-ttu-id="d2a88-114">Prostředek **AgreementDocument** obsahuje následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="d2a88-114">An **AgreementDocument** resource includes the following properties:</span></span>

| <span data-ttu-id="d2a88-115">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="d2a88-115">Property</span></span>       | <span data-ttu-id="d2a88-116">Typ</span><span class="sxs-lookup"><span data-stu-id="d2a88-116">Type</span></span>   | <span data-ttu-id="d2a88-117">Description</span><span class="sxs-lookup"><span data-stu-id="d2a88-117">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2a88-118">country</span><span class="sxs-lookup"><span data-stu-id="d2a88-118">country</span></span> | <span data-ttu-id="d2a88-119">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2a88-119">string</span></span> | <span data-ttu-id="d2a88-120">Země nebo trh, na který se vztahuje tento dokument.</span><span class="sxs-lookup"><span data-stu-id="d2a88-120">The country or market to which this document applies.</span></span> |
| <span data-ttu-id="d2a88-121">language</span><span class="sxs-lookup"><span data-stu-id="d2a88-121">language</span></span> | <span data-ttu-id="d2a88-122">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2a88-122">string</span></span> | <span data-ttu-id="d2a88-123">Jazyk, ve kterém je tento dokument lokalizován.</span><span class="sxs-lookup"><span data-stu-id="d2a88-123">The language in which this document is localized.</span></span> |
| <span data-ttu-id="d2a88-124">displayUri</span><span class="sxs-lookup"><span data-stu-id="d2a88-124">displayUri</span></span> | <span data-ttu-id="d2a88-125">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2a88-125">string</span></span> | <span data-ttu-id="d2a88-126">Odkaz na náhled dokumentu smlouvy v prohlížeči</span><span class="sxs-lookup"><span data-stu-id="d2a88-126">A link to preview the agreement document in a browser.</span></span>  |
| <span data-ttu-id="d2a88-127">downloadUri</span><span class="sxs-lookup"><span data-stu-id="d2a88-127">downloadUri</span></span> |<span data-ttu-id="d2a88-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2a88-128">string</span></span> | <span data-ttu-id="d2a88-129">Odkaz ke stažení dokumentu smlouvy (ve formátu aplikace Microsoft Word).</span><span class="sxs-lookup"><span data-stu-id="d2a88-129">A link to download the agreement document (in Microsoft Word format).</span></span> |
