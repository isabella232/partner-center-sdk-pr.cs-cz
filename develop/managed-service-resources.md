---
title: Prostředky spravované služby
description: Spravované služby jsou služby, ke kterým má partner delegovaná oprávnění správce. Partneři můžou poskytovat podporu pro žádosti a souborové služby jménem svých spravovaných služeb.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548120"
---
# <a name="managed-service-resources"></a><span data-ttu-id="5203a-104">Prostředky spravované služby</span><span class="sxs-lookup"><span data-stu-id="5203a-104">Managed service resources</span></span>

<span data-ttu-id="5203a-105">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5203a-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5203a-106">Spravované služby jsou služby, ke kterým má partner delegovaná oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="5203a-106">Managed services are services to which a partner has delegated admin privileges.</span></span> <span data-ttu-id="5203a-107">Partneři můžou poskytovat podporu pro žádosti a souborové služby jménem svých spravovaných služeb.</span><span class="sxs-lookup"><span data-stu-id="5203a-107">Partners can provide support for and file service requests on the behalf of their managed services.</span></span>

## <a name="managedservice"></a><span data-ttu-id="5203a-108">ManagedService</span><span class="sxs-lookup"><span data-stu-id="5203a-108">ManagedService</span></span>

<span data-ttu-id="5203a-109">Popisuje spravovanou službu.</span><span class="sxs-lookup"><span data-stu-id="5203a-109">Describes a managed service.</span></span>

| <span data-ttu-id="5203a-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="5203a-110">Property</span></span>   | <span data-ttu-id="5203a-111">Typ</span><span class="sxs-lookup"><span data-stu-id="5203a-111">Type</span></span>                | <span data-ttu-id="5203a-112">Description</span><span class="sxs-lookup"><span data-stu-id="5203a-112">Description</span></span>                                              |
|------------|---------------------|----------------------------------------------------------|
| <span data-ttu-id="5203a-113">Id</span><span class="sxs-lookup"><span data-stu-id="5203a-113">Id</span></span>         | <span data-ttu-id="5203a-114">řetězec</span><span class="sxs-lookup"><span data-stu-id="5203a-114">string</span></span>              | <span data-ttu-id="5203a-115">ID spravované služby</span><span class="sxs-lookup"><span data-stu-id="5203a-115">The managed service ID.</span></span>                                  |
| <span data-ttu-id="5203a-116">Name</span><span class="sxs-lookup"><span data-stu-id="5203a-116">Name</span></span>       | <span data-ttu-id="5203a-117">řetězec</span><span class="sxs-lookup"><span data-stu-id="5203a-117">string</span></span>              | <span data-ttu-id="5203a-118">Název spravované služby.</span><span class="sxs-lookup"><span data-stu-id="5203a-118">The name of the managed service.</span></span>                         |
| <span data-ttu-id="5203a-119">Parametr</span><span class="sxs-lookup"><span data-stu-id="5203a-119">GroupName</span></span>  | <span data-ttu-id="5203a-120">řetězec</span><span class="sxs-lookup"><span data-stu-id="5203a-120">string</span></span>              | <span data-ttu-id="5203a-121">Název skupiny, do které patří služba.</span><span class="sxs-lookup"><span data-stu-id="5203a-121">The name of the group to which the service belongs.</span></span>      |
| <span data-ttu-id="5203a-122">Odkazy</span><span class="sxs-lookup"><span data-stu-id="5203a-122">Links</span></span>      | <span data-ttu-id="5203a-123">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="5203a-123">ManagedServiceLinks</span></span> | <span data-ttu-id="5203a-124">Odkazy na prostředky odpovídající spravované službě.</span><span class="sxs-lookup"><span data-stu-id="5203a-124">The resource links corresponding to the managed service.</span></span> |
| <span data-ttu-id="5203a-125">Atributy</span><span class="sxs-lookup"><span data-stu-id="5203a-125">Attributes</span></span> | <span data-ttu-id="5203a-126">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="5203a-126">ResourceAttributes</span></span>  | <span data-ttu-id="5203a-127">Atributy metadat odpovídající smlouvě.</span><span class="sxs-lookup"><span data-stu-id="5203a-127">The metadata attributes corresponding to the agreement.</span></span>  |

## <a name="managedservicelinks"></a><span data-ttu-id="5203a-128">ManagedServiceLinks</span><span class="sxs-lookup"><span data-stu-id="5203a-128">ManagedServiceLinks</span></span>

<span data-ttu-id="5203a-129">Obsahuje odkazy, které umožňují partnerovi s delegovaným oprávněním správce poskytovat podporu pro službu.</span><span class="sxs-lookup"><span data-stu-id="5203a-129">Contains the links that allow the partner with delegated admin permissions to provide support for the service.</span></span>

| <span data-ttu-id="5203a-130">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="5203a-130">Property</span></span>      | <span data-ttu-id="5203a-131">Typ</span><span class="sxs-lookup"><span data-stu-id="5203a-131">Type</span></span> | <span data-ttu-id="5203a-132">Description</span><span class="sxs-lookup"><span data-stu-id="5203a-132">Description</span></span>                 |
|---------------|------|-----------------------------|
| <span data-ttu-id="5203a-133">AdminService</span><span class="sxs-lookup"><span data-stu-id="5203a-133">AdminService</span></span>  | <span data-ttu-id="5203a-134">Odkaz</span><span class="sxs-lookup"><span data-stu-id="5203a-134">Link</span></span> | <span data-ttu-id="5203a-135">Identifikátor URI služby pro správu</span><span class="sxs-lookup"><span data-stu-id="5203a-135">The admin service URI.</span></span>      |
| <span data-ttu-id="5203a-136">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="5203a-136">ServiceHealth</span></span> | <span data-ttu-id="5203a-137">Odkaz</span><span class="sxs-lookup"><span data-stu-id="5203a-137">Link</span></span> | <span data-ttu-id="5203a-138">Identifikátor URI stavu služby.</span><span class="sxs-lookup"><span data-stu-id="5203a-138">The service health URI.</span></span>     |
| <span data-ttu-id="5203a-139">ServiceTicket</span><span class="sxs-lookup"><span data-stu-id="5203a-139">ServiceTicket</span></span> | <span data-ttu-id="5203a-140">Odkaz</span><span class="sxs-lookup"><span data-stu-id="5203a-140">Link</span></span> | <span data-ttu-id="5203a-141">Identifikátor URI lístku služby.</span><span class="sxs-lookup"><span data-stu-id="5203a-141">The service ticket URI.</span></span>     |
| <span data-ttu-id="5203a-142">Self</span><span class="sxs-lookup"><span data-stu-id="5203a-142">Self</span></span>          | <span data-ttu-id="5203a-143">Odkaz</span><span class="sxs-lookup"><span data-stu-id="5203a-143">Link</span></span> | <span data-ttu-id="5203a-144">Identifikátor URI pro sebe.</span><span class="sxs-lookup"><span data-stu-id="5203a-144">The self-URI.</span></span>               |
| <span data-ttu-id="5203a-145">Další</span><span class="sxs-lookup"><span data-stu-id="5203a-145">Next</span></span>          | <span data-ttu-id="5203a-146">Odkaz</span><span class="sxs-lookup"><span data-stu-id="5203a-146">Link</span></span> | <span data-ttu-id="5203a-147">Další stránka položek</span><span class="sxs-lookup"><span data-stu-id="5203a-147">The next page of items.</span></span>     |
| <span data-ttu-id="5203a-148">Předchozí</span><span class="sxs-lookup"><span data-stu-id="5203a-148">Previous</span></span>      | <span data-ttu-id="5203a-149">Odkaz</span><span class="sxs-lookup"><span data-stu-id="5203a-149">Link</span></span> | <span data-ttu-id="5203a-150">Předchozí stránka položek</span><span class="sxs-lookup"><span data-stu-id="5203a-150">The previous page of items.</span></span> |

