---
title: Prostředky metadat smlouvy
description: Kolekce prostředků AgreementMetadata popisuje typy smlouvy, které mohou partneři použít k potvrzení přijetí zákazníkem.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025621"
---
# <a name="agreement-metadata-resources"></a><span data-ttu-id="271e4-103">Prostředky metadat smlouvy</span><span class="sxs-lookup"><span data-stu-id="271e4-103">Agreement metadata resources</span></span>

<span data-ttu-id="271e4-104">**Platí pro:** Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="271e4-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="271e4-105">**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="271e4-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="271e4-106">Prostředek **AgreementMetaData** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="271e4-106">The **AgreementMetaData** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span> 

<span data-ttu-id="271e4-107">Kolekce **AgreementMetaData** poskytuje metadata o všech typech smlouvy.</span><span class="sxs-lookup"><span data-stu-id="271e4-107">The **AgreementMetaData** collection provides metadata about all the agreement types.</span></span> <span data-ttu-id="271e4-108">Partneři mohou tuto kolekci použít k potvrzení přijetí smluv zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="271e4-108">Partners can use this collection to provide confirmation of customer acceptance of agreements.</span></span> <span data-ttu-id="271e4-109">Kolekce **AgreementMetaData** vrací metadata pro oba typy smlouvy (**Smlouva o službách Microsoft Cloud** i **Smlouva se zákazníkem Microsoftu**).</span><span class="sxs-lookup"><span data-stu-id="271e4-109">The **AgreementMetaData** collection returns metadata for both agreement types (**Microsoft Cloud Agreement** and **Microsoft Customer Agreement**).</span></span>

## <a name="agreementmetadata"></a><span data-ttu-id="271e4-110">AgreementMetaData</span><span class="sxs-lookup"><span data-stu-id="271e4-110">AgreementMetaData</span></span>

<span data-ttu-id="271e4-111">Vrácená metadata smlouvy zahrnují následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="271e4-111">Agreement metadata returned includes the following properties:</span></span>

| <span data-ttu-id="271e4-112">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="271e4-112">Property</span></span>      | <span data-ttu-id="271e4-113">Typ</span><span class="sxs-lookup"><span data-stu-id="271e4-113">Type</span></span>               | <span data-ttu-id="271e4-114">Description</span><span class="sxs-lookup"><span data-stu-id="271e4-114">Description</span></span>                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="271e4-115">ID šablony</span><span class="sxs-lookup"><span data-stu-id="271e4-115">templateId</span></span>    | <span data-ttu-id="271e4-116">řetězec</span><span class="sxs-lookup"><span data-stu-id="271e4-116">string</span></span>             | <span data-ttu-id="271e4-117">Jedinečný identifikátor šablony smlouvy</span><span class="sxs-lookup"><span data-stu-id="271e4-117">Unique identifier of an agreement template.</span></span>                                       |
| <span data-ttu-id="271e4-118">typ</span><span class="sxs-lookup"><span data-stu-id="271e4-118">type</span></span>          | <span data-ttu-id="271e4-119">řetězec</span><span class="sxs-lookup"><span data-stu-id="271e4-119">string</span></span>             | <span data-ttu-id="271e4-120">Typ smlouvy.</span><span class="sxs-lookup"><span data-stu-id="271e4-120">Agreement type.</span></span> <span data-ttu-id="271e4-121">V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement** (Preview).</span><span class="sxs-lookup"><span data-stu-id="271e4-121">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview).</span></span> |
| <span data-ttu-id="271e4-122">odkaz na smlouvu</span><span class="sxs-lookup"><span data-stu-id="271e4-122">agreementLink</span></span> | <span data-ttu-id="271e4-123">řetězec</span><span class="sxs-lookup"><span data-stu-id="271e4-123">string</span></span>             | <span data-ttu-id="271e4-124">Adresa URL šablony smlouvy.</span><span class="sxs-lookup"><span data-stu-id="271e4-124">URL for the agreement template.</span></span>                                                    |
