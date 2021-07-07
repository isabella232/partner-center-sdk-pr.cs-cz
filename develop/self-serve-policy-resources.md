---
title: Zdroje informací o samoobslužných zásadách
description: Partner pro zákazníka nastaví samoobslužné zásady.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446713"
---
# <a name="selfservepolicy-resource"></a><span data-ttu-id="cca8e-103">Prostředek SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="cca8e-103">SelfServePolicy resource</span></span>

<span data-ttu-id="cca8e-104">Partner pro zákazníka nastaví samoobslužné zásady.</span><span class="sxs-lookup"><span data-stu-id="cca8e-104">A partner sets self serve policies for a customer.</span></span>

## <a name="selfservepolicy"></a><span data-ttu-id="cca8e-105">Samoobslužné zásady</span><span class="sxs-lookup"><span data-stu-id="cca8e-105">SelfServePolicy</span></span>

<span data-ttu-id="cca8e-106">Popisuje košík.</span><span class="sxs-lookup"><span data-stu-id="cca8e-106">Describes a cart.</span></span>

| <span data-ttu-id="cca8e-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="cca8e-107">Property</span></span>              | <span data-ttu-id="cca8e-108">Typ</span><span class="sxs-lookup"><span data-stu-id="cca8e-108">Type</span></span>             | <span data-ttu-id="cca8e-109">Description</span><span class="sxs-lookup"><span data-stu-id="cca8e-109">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cca8e-110">id</span><span class="sxs-lookup"><span data-stu-id="cca8e-110">id</span></span>                    | <span data-ttu-id="cca8e-111">řetězec</span><span class="sxs-lookup"><span data-stu-id="cca8e-111">string</span></span>           | <span data-ttu-id="cca8e-112">Identifikátor samoobslužné zásady, který se dodá po úspěšném vytvoření samoobslužných zásad.</span><span class="sxs-lookup"><span data-stu-id="cca8e-112">A self-serve policy identifier that is supplied upon successful creation of the self serve policy.</span></span>     |
| <span data-ttu-id="cca8e-113">Samoobslužná rezervace</span><span class="sxs-lookup"><span data-stu-id="cca8e-113">SelfServeEntity</span></span>       | <span data-ttu-id="cca8e-114">Samoobslužná rezervace</span><span class="sxs-lookup"><span data-stu-id="cca8e-114">SelfServeEntity</span></span>  | <span data-ttu-id="cca8e-115">Samoobslužná entita, které je udělen přístup.</span><span class="sxs-lookup"><span data-stu-id="cca8e-115">The self serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="cca8e-116">Grantor</span><span class="sxs-lookup"><span data-stu-id="cca8e-116">Grantor</span></span>               | <span data-ttu-id="cca8e-117">Grantor</span><span class="sxs-lookup"><span data-stu-id="cca8e-117">Grantor</span></span>          | <span data-ttu-id="cca8e-118">Grantor, který uděluje přístup.</span><span class="sxs-lookup"><span data-stu-id="cca8e-118">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="cca8e-119">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="cca8e-119">Permissions</span></span>           | <span data-ttu-id="cca8e-120">Pole oprávnění</span><span class="sxs-lookup"><span data-stu-id="cca8e-120">Array of Permission</span></span>| <span data-ttu-id="cca8e-121">Pole prostředků [oprávnění.](#permission)</span><span class="sxs-lookup"><span data-stu-id="cca8e-121">An Array of [Permission](#permission) resources.</span></span>                                                                     |

## <a name="selfserveentity"></a><span data-ttu-id="cca8e-122">Samoobslužná rezervace</span><span class="sxs-lookup"><span data-stu-id="cca8e-122">SelfServeEntity</span></span>

<span data-ttu-id="cca8e-123">Představuje entitu s udělenou oprávněními.</span><span class="sxs-lookup"><span data-stu-id="cca8e-123">Represents the entity being granted permissions.</span></span>

| <span data-ttu-id="cca8e-124">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="cca8e-124">Property</span></span>             | <span data-ttu-id="cca8e-125">Typ</span><span class="sxs-lookup"><span data-stu-id="cca8e-125">Type</span></span>|<span data-ttu-id="cca8e-126">Description</span><span class="sxs-lookup"><span data-stu-id="cca8e-126">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="cca8e-127">SelfServeEntityType</span><span class="sxs-lookup"><span data-stu-id="cca8e-127">SelfServeEntityType</span></span>  | <span data-ttu-id="cca8e-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="cca8e-128">string</span></span>                           | <span data-ttu-id="cca8e-129">Entita, ke které se uděluje přístup, přijaté hodnoty: Zákazník.</span><span class="sxs-lookup"><span data-stu-id="cca8e-129">The entity being granted access, accepted values: Customer.</span></span>                                 |
| <span data-ttu-id="cca8e-130">ID tenanta</span><span class="sxs-lookup"><span data-stu-id="cca8e-130">TenantID</span></span>             | <span data-ttu-id="cca8e-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="cca8e-131">string</span></span>                           | <span data-ttu-id="cca8e-132">Identifikátor tenanta entity, ke které se uděluje přístup.</span><span class="sxs-lookup"><span data-stu-id="cca8e-132">The tenant identifier of the entity being granted access.</span></span>                                   |

## <a name="grantor"></a><span data-ttu-id="cca8e-133">Grantor</span><span class="sxs-lookup"><span data-stu-id="cca8e-133">Grantor</span></span>

<span data-ttu-id="cca8e-134">Představuje udělení oprávnění.</span><span class="sxs-lookup"><span data-stu-id="cca8e-134">Represents the grantor granting the permissions.</span></span>

| <span data-ttu-id="cca8e-135">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="cca8e-135">Property</span></span>             | <span data-ttu-id="cca8e-136">Typ</span><span class="sxs-lookup"><span data-stu-id="cca8e-136">Type</span></span>|<span data-ttu-id="cca8e-137">Description</span><span class="sxs-lookup"><span data-stu-id="cca8e-137">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="cca8e-138">Typ grantoru</span><span class="sxs-lookup"><span data-stu-id="cca8e-138">GrantorType</span></span>          | <span data-ttu-id="cca8e-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="cca8e-139">string</span></span>                           | <span data-ttu-id="cca8e-140">Udělení přístupu, přijaté hodnoty: BillToPartner.</span><span class="sxs-lookup"><span data-stu-id="cca8e-140">The grantor granting access, accepted values: BillToPartner.</span></span>                               |
| <span data-ttu-id="cca8e-141">ID tenanta</span><span class="sxs-lookup"><span data-stu-id="cca8e-141">TenantID</span></span>             | <span data-ttu-id="cca8e-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="cca8e-142">string</span></span>                           | <span data-ttu-id="cca8e-143">Identifikátor tenanta entity udělující přístup.</span><span class="sxs-lookup"><span data-stu-id="cca8e-143">The tenant identifier of the entity granting access.</span></span>                                       |


## <a name="permission"></a><span data-ttu-id="cca8e-144">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="cca8e-144">Permission</span></span>

<span data-ttu-id="cca8e-145">Představuje oprávnění v zásadách samoobslužné služby.</span><span class="sxs-lookup"><span data-stu-id="cca8e-145">Represents a permission in the self serve policy.</span></span>

| <span data-ttu-id="cca8e-146">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="cca8e-146">Property</span></span>             | <span data-ttu-id="cca8e-147">Typ</span><span class="sxs-lookup"><span data-stu-id="cca8e-147">Type</span></span>|<span data-ttu-id="cca8e-148">Description</span><span class="sxs-lookup"><span data-stu-id="cca8e-148">Description</span></span>|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="cca8e-149">Prostředek</span><span class="sxs-lookup"><span data-stu-id="cca8e-149">Resource</span></span>             | <span data-ttu-id="cca8e-150">řetězec</span><span class="sxs-lookup"><span data-stu-id="cca8e-150">string</span></span>                           | <span data-ttu-id="cca8e-151">Uděluje se také přístup k prostředkům: AzureReservedInstances.</span><span class="sxs-lookup"><span data-stu-id="cca8e-151">The resource access is being granted too: AzureReservedInstances.</span></span>                          |
| <span data-ttu-id="cca8e-152">Akce</span><span class="sxs-lookup"><span data-stu-id="cca8e-152">Action</span></span>               | <span data-ttu-id="cca8e-153">řetězec</span><span class="sxs-lookup"><span data-stu-id="cca8e-153">string</span></span>                           | <span data-ttu-id="cca8e-154">Přístup k akci se uděluje pro: Koupit</span><span class="sxs-lookup"><span data-stu-id="cca8e-154">The action access is being granted for: Purchase</span></span>                                           |
