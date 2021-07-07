---
title: Zdroje informací o smlouvě
description: Prostředek smlouvy představuje smlouvu se zákazníkem Microsoftu pro cloud s podrobnostmi o certifikaci poskytovanou partnerem.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025612"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="bfaa6-103">Prostředky smlouvy představující smlouvu se zákazníkem Microsoftu pro cloud</span><span class="sxs-lookup"><span data-stu-id="bfaa6-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="bfaa6-104">**Platí pro:** Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="bfaa6-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="bfaa6-105">**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bfaa6-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bfaa6-106">Prostředek **smlouvy** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="bfaa6-107">Prostředek **smlouvy** představuje smlouvu se zákazníkem Microsoftu pro cloud.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-107">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="bfaa6-108">Smlouva</span><span class="sxs-lookup"><span data-stu-id="bfaa6-108">Agreement</span></span>

<span data-ttu-id="bfaa6-109">Prostředek **smlouvy** představuje podrobnosti o certifikaci poskytované partnerem.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-109">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="bfaa6-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="bfaa6-110">Property</span></span>       | <span data-ttu-id="bfaa6-111">Typ</span><span class="sxs-lookup"><span data-stu-id="bfaa6-111">Type</span></span>   | <span data-ttu-id="bfaa6-112">Description</span><span class="sxs-lookup"><span data-stu-id="bfaa6-112">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bfaa6-113">userId</span><span class="sxs-lookup"><span data-stu-id="bfaa6-113">userId</span></span>         | <span data-ttu-id="bfaa6-114">řetězec</span><span class="sxs-lookup"><span data-stu-id="bfaa6-114">string</span></span>                         | <span data-ttu-id="bfaa6-115">Identifikátor objektu přihlášeného uživatele v partnerském tenantovi, který poskytuje potvrzení jménem partnerské organizace.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-115">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="bfaa6-116">Při použití ověřování aplikací a uživatelů k vytvoření prostředku smlouvy Partnerské centrum automaticky odvodí hodnotu **atributu userId** z tokenu App+User.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-116">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="bfaa6-117">primaryContact</span><span class="sxs-lookup"><span data-stu-id="bfaa6-117">primaryContact</span></span> | [<span data-ttu-id="bfaa6-118">Kontakt</span><span class="sxs-lookup"><span data-stu-id="bfaa6-118">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="bfaa6-119">Informace o uživateli z organizace zákazníka, který smlouvu přijal, včetně:  **firstName**, **lastName**, **email** a **phoneNumber** (volitelné).</span><span class="sxs-lookup"><span data-stu-id="bfaa6-119">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="bfaa6-120">datum odgreed</span><span class="sxs-lookup"><span data-stu-id="bfaa6-120">dateAgreed</span></span>     | <span data-ttu-id="bfaa6-121">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="bfaa6-121">string in UTC date time format</span></span> | <span data-ttu-id="bfaa6-122">Datum, kdy zákazník smlouvu přijal.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-122">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="bfaa6-123">ID šablony</span><span class="sxs-lookup"><span data-stu-id="bfaa6-123">templateId</span></span>     |<span data-ttu-id="bfaa6-124">řetězec</span><span class="sxs-lookup"><span data-stu-id="bfaa6-124">string</span></span>                          | <span data-ttu-id="bfaa6-125">Jedinečný identifikátor smlouvy, kterou zákazník přijal</span><span class="sxs-lookup"><span data-stu-id="bfaa6-125">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="bfaa6-126">typ</span><span class="sxs-lookup"><span data-stu-id="bfaa6-126">type</span></span>           |<span data-ttu-id="bfaa6-127">řetězec</span><span class="sxs-lookup"><span data-stu-id="bfaa6-127">string</span></span>                          | <span data-ttu-id="bfaa6-128">Typ smlouvy.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-128">Agreement type.</span></span> <span data-ttu-id="bfaa6-129">V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement**.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-129">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="bfaa6-130">odkaz na smlouvu</span><span class="sxs-lookup"><span data-stu-id="bfaa6-130">agreementLink</span></span>  | <span data-ttu-id="bfaa6-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="bfaa6-131">string</span></span>                         | <span data-ttu-id="bfaa6-132">Adresa URL šablony smlouvy.</span><span class="sxs-lookup"><span data-stu-id="bfaa6-132">URL for the agreement template.</span></span>                                                    |
