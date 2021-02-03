---
title: Prostředky spravované služby
description: Spravované služby jsou služby, ke kterým má partner delegovaná oprávnění správce. Partneři můžou poskytovat podporu pro žádosti a souborové služby jménem svých spravovaných služeb.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766705"
---
# <a name="managed-service-resources"></a><span data-ttu-id="28a85-104">Prostředky spravované služby</span><span class="sxs-lookup"><span data-stu-id="28a85-104">Managed service resources</span></span>

<span data-ttu-id="28a85-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="28a85-105">**Applies To**</span></span>

- <span data-ttu-id="28a85-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="28a85-106">Partner Center</span></span>
- <span data-ttu-id="28a85-107">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="28a85-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="28a85-108">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="28a85-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="28a85-109">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="28a85-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="28a85-110">Spravované služby jsou služby, ke kterým má partner delegovaná oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="28a85-110">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="28a85-111">Partneři můžou poskytovat podporu pro žádosti a souborové služby jménem svých spravovaných služeb.</span><span class="sxs-lookup"><span data-stu-id="28a85-111">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="28a85-112">ManagedService</span><span class="sxs-lookup"><span data-stu-id="28a85-112">ManagedService</span></span>

<span data-ttu-id="28a85-113">Popisuje spravovanou službu.</span><span class="sxs-lookup"><span data-stu-id="28a85-113">Describes a managed service.</span></span>

| <span data-ttu-id="28a85-114">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="28a85-114">Property</span></span>   | <span data-ttu-id="28a85-115">Typ</span><span class="sxs-lookup"><span data-stu-id="28a85-115">Type</span></span>                | <span data-ttu-id="28a85-116">Description</span><span class="sxs-lookup"><span data-stu-id="28a85-116">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="28a85-117">Id</span><span class="sxs-lookup"><span data-stu-id="28a85-117">Id</span></span>         | <span data-ttu-id="28a85-118">řetězec</span><span class="sxs-lookup"><span data-stu-id="28a85-118">string</span></span>              | <span data-ttu-id="28a85-119">ID spravované služby</span><span class="sxs-lookup"><span data-stu-id="28a85-119">The managed service id.</span></span>                                  |
| <span data-ttu-id="28a85-120">Name</span><span class="sxs-lookup"><span data-stu-id="28a85-120">Name</span></span>       | <span data-ttu-id="28a85-121">řetězec</span><span class="sxs-lookup"><span data-stu-id="28a85-121">string</span></span>              | <span data-ttu-id="28a85-122">Název spravované služby.</span><span class="sxs-lookup"><span data-stu-id="28a85-122">The name of the managed service.</span></span>                         |
| <span data-ttu-id="28a85-123">Parametr</span><span class="sxs-lookup"><span data-stu-id="28a85-123">GroupName</span></span>  | <span data-ttu-id="28a85-124">řetězec</span><span class="sxs-lookup"><span data-stu-id="28a85-124">string</span></span>              | <span data-ttu-id="28a85-125">Název skupiny, do které patří služba.</span><span class="sxs-lookup"><span data-stu-id="28a85-125">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="28a85-126">Odkazy</span><span class="sxs-lookup"><span data-stu-id="28a85-126">Links</span></span>      | <span data-ttu-id="28a85-127">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="28a85-127">ManagedServiceLinks</span></span> | <span data-ttu-id="28a85-128">Odkazy na prostředky odpovídající spravované službě.</span><span class="sxs-lookup"><span data-stu-id="28a85-128">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="28a85-129">Atributy</span><span class="sxs-lookup"><span data-stu-id="28a85-129">Attributes</span></span> | <span data-ttu-id="28a85-130">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="28a85-130">ResourceAttributes</span></span>  | <span data-ttu-id="28a85-131">Atributy metadat odpovídající smlouvě.</span><span class="sxs-lookup"><span data-stu-id="28a85-131">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="28a85-132">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="28a85-132">ManagedServiceLinks</span></span>

<span data-ttu-id="28a85-133">Obsahuje odkazy, které umožňují partnerovi s delegovaným oprávněním správce poskytovat podporu pro službu.</span><span class="sxs-lookup"><span data-stu-id="28a85-133">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="28a85-134">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="28a85-134">Property</span></span>      | <span data-ttu-id="28a85-135">Typ</span><span class="sxs-lookup"><span data-stu-id="28a85-135">Type</span></span> | <span data-ttu-id="28a85-136">Description</span><span class="sxs-lookup"><span data-stu-id="28a85-136">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="28a85-137">AdminService</span><span class="sxs-lookup"><span data-stu-id="28a85-137">AdminService</span></span>  | <span data-ttu-id="28a85-138">Odkaz</span><span class="sxs-lookup"><span data-stu-id="28a85-138">Link</span></span> | <span data-ttu-id="28a85-139">Identifikátor URI služby pro správu</span><span class="sxs-lookup"><span data-stu-id="28a85-139">The admin service URI.</span></span>      |
| <span data-ttu-id="28a85-140">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="28a85-140">ServiceHealth</span></span> | <span data-ttu-id="28a85-141">Odkaz</span><span class="sxs-lookup"><span data-stu-id="28a85-141">Link</span></span> | <span data-ttu-id="28a85-142">Identifikátor URI stavu služby.</span><span class="sxs-lookup"><span data-stu-id="28a85-142">The service health URI.</span></span>     |
| <span data-ttu-id="28a85-143">ServiceTicket</span><span class="sxs-lookup"><span data-stu-id="28a85-143">ServiceTicket</span></span> | <span data-ttu-id="28a85-144">Odkaz</span><span class="sxs-lookup"><span data-stu-id="28a85-144">Link</span></span> | <span data-ttu-id="28a85-145">Identifikátor URI lístku služby.</span><span class="sxs-lookup"><span data-stu-id="28a85-145">The service ticket URI.</span></span>     |
| <span data-ttu-id="28a85-146">Self</span><span class="sxs-lookup"><span data-stu-id="28a85-146">Self</span></span>          | <span data-ttu-id="28a85-147">Odkaz</span><span class="sxs-lookup"><span data-stu-id="28a85-147">Link</span></span> | <span data-ttu-id="28a85-148">Identifikátor URI samostatného.</span><span class="sxs-lookup"><span data-stu-id="28a85-148">The self URI.</span></span>               |
| <span data-ttu-id="28a85-149">Další</span><span class="sxs-lookup"><span data-stu-id="28a85-149">Next</span></span>          | <span data-ttu-id="28a85-150">Odkaz</span><span class="sxs-lookup"><span data-stu-id="28a85-150">Link</span></span> | <span data-ttu-id="28a85-151">Další stránka položek</span><span class="sxs-lookup"><span data-stu-id="28a85-151">The next page of items.</span></span>     |
| <span data-ttu-id="28a85-152">Předchozí</span><span class="sxs-lookup"><span data-stu-id="28a85-152">Previous</span></span>      | <span data-ttu-id="28a85-153">Odkaz</span><span class="sxs-lookup"><span data-stu-id="28a85-153">Link</span></span> | <span data-ttu-id="28a85-154">Předchozí stránka položek</span><span class="sxs-lookup"><span data-stu-id="28a85-154">The previous page of items.</span></span> |

