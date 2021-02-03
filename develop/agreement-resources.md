---
title: Prostředky smlouvy
description: Prostředek smlouvy představuje smlouvu zákazníka v cloudu Microsoftu s podrobnostmi o certifikaci poskytované partnerem.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2020
ms.locfileid: "97767091"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a><span data-ttu-id="83d3f-103">Prostředky smlouvy, které představují zákaznickou smlouvu o cloudu Microsoftu</span><span class="sxs-lookup"><span data-stu-id="83d3f-103">Agreement resources representing a Microsoft cloud customer agreement</span></span>

<span data-ttu-id="83d3f-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="83d3f-104">**Applies to:**</span></span>

- <span data-ttu-id="83d3f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="83d3f-105">Partner Center</span></span>

<span data-ttu-id="83d3f-106">Prostředek **smlouvy** je aktuálně podporovaný partnerským centrem jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="83d3f-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="83d3f-107">Neplatí pro:</span><span class="sxs-lookup"><span data-stu-id="83d3f-107">It isn't applicable to:</span></span>

- <span data-ttu-id="83d3f-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="83d3f-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="83d3f-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="83d3f-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="83d3f-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="83d3f-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="83d3f-111">Prostředek **smlouvy** představuje zákaznickou smlouvu Microsoftu pro Cloud.</span><span class="sxs-lookup"><span data-stu-id="83d3f-111">The **Agreement** resource represents a Microsoft cloud customer agreement.</span></span>

## <a name="agreement"></a><span data-ttu-id="83d3f-112">Smlouva</span><span class="sxs-lookup"><span data-stu-id="83d3f-112">Agreement</span></span>

<span data-ttu-id="83d3f-113">Prostředek **smlouvy** představuje podrobnosti o certifikaci poskytované partnerem.</span><span class="sxs-lookup"><span data-stu-id="83d3f-113">The **Agreement** resource represents the details of certification provided by the partner.</span></span>

| <span data-ttu-id="83d3f-114">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="83d3f-114">Property</span></span>       | <span data-ttu-id="83d3f-115">Typ</span><span class="sxs-lookup"><span data-stu-id="83d3f-115">Type</span></span>   | <span data-ttu-id="83d3f-116">Description</span><span class="sxs-lookup"><span data-stu-id="83d3f-116">Description</span></span>                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="83d3f-117">userId</span><span class="sxs-lookup"><span data-stu-id="83d3f-117">userId</span></span>         | <span data-ttu-id="83d3f-118">řetězec</span><span class="sxs-lookup"><span data-stu-id="83d3f-118">string</span></span>                         | <span data-ttu-id="83d3f-119">Identifikátor objektu přihlášeného uživatele v partnerském tenantovi, který poskytuje potvrzení jménem partnerské organizace.</span><span class="sxs-lookup"><span data-stu-id="83d3f-119">Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization.</span></span> <span data-ttu-id="83d3f-120">Při použití ověřování aplikací a uživatelů k vytvoření prostředku smlouvy partnerské Centrum automaticky odvozuje hodnotu atributu **userId** z tokenu App + User.</span><span class="sxs-lookup"><span data-stu-id="83d3f-120">When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.</span></span>                                                                             |
| <span data-ttu-id="83d3f-121">primaryContact</span><span class="sxs-lookup"><span data-stu-id="83d3f-121">primaryContact</span></span> | [<span data-ttu-id="83d3f-122">Kontakt</span><span class="sxs-lookup"><span data-stu-id="83d3f-122">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="83d3f-123">Informace o uživateli od organizace zákazníka, která smlouvu přijala, včetně:  **FirstName**, **LastName**, **email** a **phoneNumber** (volitelné).</span><span class="sxs-lookup"><span data-stu-id="83d3f-123">Information about the user from the customer organization that accepted the agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional).</span></span> |
| <span data-ttu-id="83d3f-124">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="83d3f-124">dateAgreed</span></span>     | <span data-ttu-id="83d3f-125">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="83d3f-125">string in UTC date time format</span></span> | <span data-ttu-id="83d3f-126">Datum, kdy zákazník smlouvu přijal.</span><span class="sxs-lookup"><span data-stu-id="83d3f-126">The date when the customer accepted the agreement.</span></span>                                 |
| <span data-ttu-id="83d3f-127">templateId</span><span class="sxs-lookup"><span data-stu-id="83d3f-127">templateId</span></span>     |<span data-ttu-id="83d3f-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="83d3f-128">string</span></span>                          | <span data-ttu-id="83d3f-129">Jedinečný identifikátor smlouvy, kterou zákazník přijal</span><span class="sxs-lookup"><span data-stu-id="83d3f-129">Unique identifier of the agreement that the customer accepted.</span></span> |
| <span data-ttu-id="83d3f-130">typ</span><span class="sxs-lookup"><span data-stu-id="83d3f-130">type</span></span>           |<span data-ttu-id="83d3f-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="83d3f-131">string</span></span>                          | <span data-ttu-id="83d3f-132">Typ smlouvy</span><span class="sxs-lookup"><span data-stu-id="83d3f-132">Agreement type.</span></span> <span data-ttu-id="83d3f-133">V současné době podporované hodnoty zahrnují **MicrosoftCloudAgreement** a **MicrosoftCustomerAgreement**.</span><span class="sxs-lookup"><span data-stu-id="83d3f-133">Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.</span></span>|
| <span data-ttu-id="83d3f-134">agreementLink</span><span class="sxs-lookup"><span data-stu-id="83d3f-134">agreementLink</span></span>  | <span data-ttu-id="83d3f-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="83d3f-135">string</span></span>                         | <span data-ttu-id="83d3f-136">Adresa URL šablony smlouvy</span><span class="sxs-lookup"><span data-stu-id="83d3f-136">URL for the agreement template.</span></span>                                                    |
