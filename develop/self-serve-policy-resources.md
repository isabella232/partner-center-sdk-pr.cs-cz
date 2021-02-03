---
title: Prostředky zásad samoobslužné obsluhy
description: Partner pro zákazníka nastaví zásady samoobslužného poskytování.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766735"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="511aa-103">Prostředek SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="511aa-103">SelfServePolicy resource</span></span>

<span data-ttu-id="511aa-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="511aa-104">**Applies to:**</span></span>

- <span data-ttu-id="511aa-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="511aa-105">Partner Center</span></span>

<span data-ttu-id="511aa-106">Partner pro zákazníka nastaví zásady samoobslužného poskytování.</span><span class="sxs-lookup"><span data-stu-id="511aa-106">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="511aa-107">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="511aa-107">SelfServePolicy</span></span>

<span data-ttu-id="511aa-108">Popisuje košík.</span><span class="sxs-lookup"><span data-stu-id="511aa-108">Describes a cart.</span></span>

| <span data-ttu-id="511aa-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="511aa-109">Property</span></span>              | <span data-ttu-id="511aa-110">Typ</span><span class="sxs-lookup"><span data-stu-id="511aa-110">Type</span></span>             | <span data-ttu-id="511aa-111">Description</span><span class="sxs-lookup"><span data-stu-id="511aa-111">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="511aa-112">id</span><span class="sxs-lookup"><span data-stu-id="511aa-112">id</span></span>                    | <span data-ttu-id="511aa-113">řetězec</span><span class="sxs-lookup"><span data-stu-id="511aa-113">string</span></span>           | <span data-ttu-id="511aa-114">Identifikátor zásady samoobslužné obsluhy, který se poskytne po úspěšném vytvoření zásady samoobslužné obsluhy.</span><span class="sxs-lookup"><span data-stu-id="511aa-114">A self serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="511aa-115">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="511aa-115">SelfServeEntity</span></span>       | <span data-ttu-id="511aa-116">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="511aa-116">SelfServeEntity</span></span>  | <span data-ttu-id="511aa-117">Entita, která má udělen přístup k sobě.</span><span class="sxs-lookup"><span data-stu-id="511aa-117">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="511aa-118">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="511aa-118">Grantor</span></span>               | <span data-ttu-id="511aa-119">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="511aa-119">Grantor</span></span>          | <span data-ttu-id="511aa-120">Uděluje udělení přístupu.</span><span class="sxs-lookup"><span data-stu-id="511aa-120">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="511aa-121">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="511aa-121">Permissions</span></span>           | <span data-ttu-id="511aa-122">Pole oprávnění</span><span class="sxs-lookup"><span data-stu-id="511aa-122">Array of Permission</span></span>| <span data-ttu-id="511aa-123">Pole prostředků [oprávnění](#permission)</span><span class="sxs-lookup"><span data-stu-id="511aa-123">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="511aa-124">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="511aa-124">SelfServeEntity</span></span>

<span data-ttu-id="511aa-125">Představuje entitu udělenou oprávnění.</span><span class="sxs-lookup"><span data-stu-id="511aa-125">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="511aa-126">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="511aa-126">Property</span></span>             | <span data-ttu-id="511aa-127">Typ</span><span class="sxs-lookup"><span data-stu-id="511aa-127">Type</span></span>|<span data-ttu-id="511aa-128">Description</span><span class="sxs-lookup"><span data-stu-id="511aa-128">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="511aa-129">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="511aa-129">SelfServeEntityType</span></span>  | <span data-ttu-id="511aa-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="511aa-130">string</span></span>                           | <span data-ttu-id="511aa-131">Entita, která má udělený přístup, přijaté hodnoty: zákazník</span><span class="sxs-lookup"><span data-stu-id="511aa-131">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="511aa-132">TenantID</span><span class="sxs-lookup"><span data-stu-id="511aa-132">TenantID</span></span>             | <span data-ttu-id="511aa-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="511aa-133">string</span></span>                           | <span data-ttu-id="511aa-134">Identifikátor tenanta entity, která má udělený přístup</span><span class="sxs-lookup"><span data-stu-id="511aa-134">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="511aa-135">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="511aa-135">Grantor</span></span>

<span data-ttu-id="511aa-136">Představuje udělení oprávnění.</span><span class="sxs-lookup"><span data-stu-id="511aa-136">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="511aa-137">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="511aa-137">Property</span></span>             | <span data-ttu-id="511aa-138">Typ</span><span class="sxs-lookup"><span data-stu-id="511aa-138">Type</span></span>|<span data-ttu-id="511aa-139">Description</span><span class="sxs-lookup"><span data-stu-id="511aa-139">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="511aa-140">GrantorType</span><span class="sxs-lookup"><span data-stu-id="511aa-140">GrantorType</span></span>          | <span data-ttu-id="511aa-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="511aa-141">string</span></span>                           | <span data-ttu-id="511aa-142">Uděluje udělení přístupu, přijatelné hodnoty: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="511aa-142">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="511aa-143">TenantID</span><span class="sxs-lookup"><span data-stu-id="511aa-143">TenantID</span></span>             | <span data-ttu-id="511aa-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="511aa-144">string</span></span>                           | <span data-ttu-id="511aa-145">Identifikátor tenanta entity, která uděluje přístup</span><span class="sxs-lookup"><span data-stu-id="511aa-145">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="511aa-146">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="511aa-146">Permission</span></span>

<span data-ttu-id="511aa-147">Představuje oprávnění v zásadách samoobslužné obsluhy.</span><span class="sxs-lookup"><span data-stu-id="511aa-147">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="511aa-148">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="511aa-148">Property</span></span>             | <span data-ttu-id="511aa-149">Typ</span><span class="sxs-lookup"><span data-stu-id="511aa-149">Type</span></span>|<span data-ttu-id="511aa-150">Description</span><span class="sxs-lookup"><span data-stu-id="511aa-150">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="511aa-151">Prostředek</span><span class="sxs-lookup"><span data-stu-id="511aa-151">Resource</span></span>             | <span data-ttu-id="511aa-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="511aa-152">string</span></span>                           | <span data-ttu-id="511aa-153">Přístup k prostředkům se uděluje moc: AzureReservedInstances.</span><span class="sxs-lookup"><span data-stu-id="511aa-153">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="511aa-154">Akce</span><span class="sxs-lookup"><span data-stu-id="511aa-154">Action</span></span>               | <span data-ttu-id="511aa-155">řetězec</span><span class="sxs-lookup"><span data-stu-id="511aa-155">string</span></span>                           | <span data-ttu-id="511aa-156">Přístup k akci je udělován pro: nákup</span><span class="sxs-lookup"><span data-stu-id="511aa-156">The action access is being granted for: Purchase</span></span>                                           |
