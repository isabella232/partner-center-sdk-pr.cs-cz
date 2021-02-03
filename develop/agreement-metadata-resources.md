---
title: Prostředky metadat smlouvy
description: Kolekce prostředků AgreementMetadata popisuje typy smluv, které mohou partneři použít k potvrzení přijetí zákazníka.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766697"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="8481a-103">Prostředky metadat smlouvy</span><span class="sxs-lookup"><span data-stu-id="8481a-103">Agreement metadata resources</span></span>

<span data-ttu-id="8481a-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="8481a-104">**Applies to:**</span></span>

- <span data-ttu-id="8481a-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="8481a-105">Partner Center</span></span>

<span data-ttu-id="8481a-106">Partner Center v současné době podporuje prostředek **AgreementMetaData** jenom ve *veřejném cloudu Microsoftu*.</span><span class="sxs-lookup"><span data-stu-id="8481a-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="8481a-107">Tento prostředek se nedá použít pro:</span><span class="sxs-lookup"><span data-stu-id="8481a-107">This resource isn't applicable to:</span></span>

- <span data-ttu-id="8481a-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="8481a-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8481a-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="8481a-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8481a-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8481a-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8481a-111">Kolekce **AgreementMetaData** poskytuje metadata o všech typech smluv.</span><span class="sxs-lookup"><span data-stu-id="8481a-111">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="8481a-112">Partneři mohou tuto kolekci použít k potvrzení přijetí smlouvy od zákazníků.</span><span class="sxs-lookup"><span data-stu-id="8481a-112">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="8481a-113">Kolekce **AgreementMetaData** vrací metadata pro oba typy smluv (**Microsoft Cloud smlouva** a **smlouvy o zákaznících Microsoftu**).</span><span class="sxs-lookup"><span data-stu-id="8481a-113">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="8481a-114">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="8481a-114">AgreementMetaData</span></span>

<span data-ttu-id="8481a-115">Vrácená metadata smlouvy obsahují následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="8481a-115">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="8481a-116">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="8481a-116">Property</span></span>      | <span data-ttu-id="8481a-117">Typ</span><span class="sxs-lookup"><span data-stu-id="8481a-117">Type</span></span>               | <span data-ttu-id="8481a-118">Description</span><span class="sxs-lookup"><span data-stu-id="8481a-118">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="8481a-119">templateId</span><span class="sxs-lookup"><span data-stu-id="8481a-119">templateId</span></span>    | <span data-ttu-id="8481a-120">řetězec</span><span class="sxs-lookup"><span data-stu-id="8481a-120">string</span></span>             | <span data-ttu-id="8481a-121">Jedinečný identifikátor šablony smlouvy</span><span class="sxs-lookup"><span data-stu-id="8481a-121">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="8481a-122">typ</span><span class="sxs-lookup"><span data-stu-id="8481a-122">type</span></span>          | <span data-ttu-id="8481a-123">řetězec</span><span class="sxs-lookup"><span data-stu-id="8481a-123">string</span></span>             | <span data-ttu-id="8481a-124">Typ smlouvy</span><span class="sxs-lookup"><span data-stu-id="8481a-124">Agreement type.</span></span> <span data-ttu-id="8481a-125">V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement** (Preview).</span><span class="sxs-lookup"><span data-stu-id="8481a-125">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="8481a-126">agreementLink</span><span class="sxs-lookup"><span data-stu-id="8481a-126">agreementLink</span></span> | <span data-ttu-id="8481a-127">řetězec</span><span class="sxs-lookup"><span data-stu-id="8481a-127">string</span></span>             | <span data-ttu-id="8481a-128">Adresa URL šablony smlouvy</span><span class="sxs-lookup"><span data-stu-id="8481a-128">URL for the agreement template.</span></span>                                                    |
