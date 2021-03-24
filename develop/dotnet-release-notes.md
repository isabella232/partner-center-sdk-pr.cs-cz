---
title: Zpráva k vydání verze pro partnerský Center .NET SDK
description: Poznámky k verzi pro nejnovější verzi sady SDK partnerského centra .NET.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2fe309500cc80e962c101ad97f0712bef7e11eb3
ms.sourcegitcommit: f7fce0b35ab1579e59136abc357b71cf768b81b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104895529"
---
# <a name="net-sdk-release-notes"></a><span data-ttu-id="53165-103">Poznámky k verzi sady .NET SDK</span><span class="sxs-lookup"><span data-stu-id="53165-103">.NET SDK release notes</span></span>

<span data-ttu-id="53165-104">Následující poznámky k verzi jsou k dispozici pro nové verze [sady Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span><span class="sxs-lookup"><span data-stu-id="53165-104">The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span></span> <span data-ttu-id="53165-105">[Ukázky sady .NET SDK](https://github.com/Microsoft/Partner-Center-DotNet-Samples) najdete na GitHubu.</span><span class="sxs-lookup"><span data-stu-id="53165-105">You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub.</span></span> <span data-ttu-id="53165-106">Reference k rozhraní [.NET API partnerského centra](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) najdete v prohlížeči rozhraní .NET API.</span><span class="sxs-lookup"><span data-stu-id="53165-106">You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.</span></span>

## <a name="version-1170"></a><span data-ttu-id="53165-107">1.17.0 verze</span><span class="sxs-lookup"><span data-stu-id="53165-107">Version 1.17.0</span></span>

<span data-ttu-id="53165-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v 1.17.0 je teď obecně dostupný.</span><span class="sxs-lookup"><span data-stu-id="53165-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability.</span></span> <span data-ttu-id="53165-109">K dispozici jsou také aktualizované [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) .</span><span class="sxs-lookup"><span data-stu-id="53165-109">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="53165-110">V této verzi jsou zahrnuté tyto změny:</span><span class="sxs-lookup"><span data-stu-id="53165-110">The following changes are included in this version:</span></span>

* <span data-ttu-id="53165-111">Aktualizované audit – byly přidány nové typy operací pro znalost, kdy zákazník schválil a ukončil příznak DAP.</span><span class="sxs-lookup"><span data-stu-id="53165-111">Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP</span></span>
  * [<span data-ttu-id="53165-112">DapAdminRelationshipApproved</span><span class="sxs-lookup"><span data-stu-id="53165-112">DapAdminRelationshipApproved</span></span>](auditing-resources.md)
  * [<span data-ttu-id="53165-113">DapAdminRelationshipTerminated</span><span class="sxs-lookup"><span data-stu-id="53165-113">DapAdminRelationshipTerminated</span></span>](auditing-resources.md)

* <span data-ttu-id="53165-114">Audit byl aktualizován – byly přidány nové typy prostředků a operací pro podporu scénáře pro roli adresáře zákazníka.</span><span class="sxs-lookup"><span data-stu-id="53165-114">Audit Updated – Added new resource and operation types for supporting the customer directory role scenario</span></span>
  * <span data-ttu-id="53165-115">Typ prostředku "[CustomerDirectoryRole](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="53165-115">Resource type "[CustomerDirectoryRole](auditing-resources.md)"</span></span>
  * <span data-ttu-id="53165-116">Typy operací "[AddUserMember](auditing-resources.md)" a "[RemoveUserMember](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="53165-116">Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"</span></span>

* <span data-ttu-id="53165-117">Aktualizace sady SDK na účet Customers – podpora pro následující rozhraní API</span><span class="sxs-lookup"><span data-stu-id="53165-117">SDK Updates to Customers Account - Support for following API's</span></span>
  * <span data-ttu-id="53165-118">ZÍSKAT/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="53165-118">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span></span>
  * <span data-ttu-id="53165-119">ZÍSKAT/Customers/{Customer-tenant-ID}/Qualifications</span><span class="sxs-lookup"><span data-stu-id="53165-119">GET /customers/{customer-tenant-id}/qualifications</span></span> 
  * <span data-ttu-id="53165-120">POST/Customers/{customer_id}/Qualifications? Code = {validationCode}</span><span class="sxs-lookup"><span data-stu-id="53165-120">POST /customers/{customer_id}/qualifications?code={validationCode}</span></span>

* <span data-ttu-id="53165-121">**Po změnách zavedených v rámci nového obchodování, které jsou aktuálně k dispozici na základě pozvánky jenom pro partnery, kteří jsou součástí M365/D365 New Commerce Experience Technical Preview.**</span><span class="sxs-lookup"><span data-stu-id="53165-121">**Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.**</span></span> <span data-ttu-id="53165-122">Partneři, kteří nejsou součástí nového obchodní privátní verze Preview, by neměli poznamenat dopady a měly by být zpětně kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="53165-122">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>
  * <span data-ttu-id="53165-123">Změny katalogu:</span><span class="sxs-lookup"><span data-stu-id="53165-123">Catalog Changes:</span></span>
    * <span data-ttu-id="53165-124">ZÍSKAT/Products/{Product-ID}/skus/{SKU-ID}</span><span class="sxs-lookup"><span data-stu-id="53165-124">GET /products/{product-id}/skus/{sku-id}</span></span>
  * <span data-ttu-id="53165-125">Nákup a správa:</span><span class="sxs-lookup"><span data-stu-id="53165-125">Purchase and Manage:</span></span>
    * <span data-ttu-id="53165-126">ZÍSKAT/customers/{customerId}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="53165-126">GET /customers/{customerId}/subscriptions</span></span>
    * <span data-ttu-id="53165-127">ZÍSKAT/customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="53165-127">GET /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="53165-128">/Customers/{customerId}/subscriptions/{subscriptionId} opravy</span><span class="sxs-lookup"><span data-stu-id="53165-128">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="53165-129">ZÍSKAT/customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span><span class="sxs-lookup"><span data-stu-id="53165-129">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span></span>
    * <span data-ttu-id="53165-130">ZÍSKAT/customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="53165-130">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>
    * <span data-ttu-id="53165-131">PŘÍSPĚVEK/customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="53165-131">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>


## <a name="version-1163"></a><span data-ttu-id="53165-132">1.16.3 verze</span><span class="sxs-lookup"><span data-stu-id="53165-132">Version 1.16.3</span></span>

<span data-ttu-id="53165-133">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v 1.16.3 je teď obecně dostupný.</span><span class="sxs-lookup"><span data-stu-id="53165-133">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability.</span></span> <span data-ttu-id="53165-134">K dispozici jsou také aktualizované [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) .</span><span class="sxs-lookup"><span data-stu-id="53165-134">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="53165-135">V této verzi jsou zahrnuté tyto změny:</span><span class="sxs-lookup"><span data-stu-id="53165-135">The following changes are included in this version:</span></span>

* <span data-ttu-id="53165-136">SelfServePolicies – přidala se nová funkce.</span><span class="sxs-lookup"><span data-stu-id="53165-136">SelfServePolicies - new functionality added</span></span>
  * [<span data-ttu-id="53165-137">GetSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="53165-137">GetSelfServePolicies</span></span>](get-a-self-serve-policy-by-id.md)
  * [<span data-ttu-id="53165-138">GetListOfSelfServicePolicies</span><span class="sxs-lookup"><span data-stu-id="53165-138">GetListOfSelfServicePolicies</span></span>](get-a-list-of-self-serve-policies.md)
  * [<span data-ttu-id="53165-139">CreateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="53165-139">CreateSelfServePolicies</span></span>](create-a-self-serve-policy.md)
  * [<span data-ttu-id="53165-140">UpdateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="53165-140">UpdateSelfServePolicies</span></span>](update-a-self-serve-policy.md)
  * [<span data-ttu-id="53165-141">DeleteSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="53165-141">DeleteSelfServePolicies</span></span>](delete-a-self-serve-policy.md)

* <span data-ttu-id="53165-142">Profil společnosti pro zákazníky</span><span class="sxs-lookup"><span data-stu-id="53165-142">Customers Company Profile</span></span>
  * <span data-ttu-id="53165-143">Přidání [OrganizationRegistrationNumber](create-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="53165-143">Added [OrganizationRegistrationNumber](create-a-customer.md)</span></span>

* <span data-ttu-id="53165-144">CustomerBillingProfile.DefaultAddress</span><span class="sxs-lookup"><span data-stu-id="53165-144">CustomerBillingProfile.DefaultAddress</span></span>
  * <span data-ttu-id="53165-145">Přidání MiddleName</span><span class="sxs-lookup"><span data-stu-id="53165-145">Added MiddleName</span></span>

## <a name="version-1162"></a><span data-ttu-id="53165-146">1.16.2 verze</span><span class="sxs-lookup"><span data-stu-id="53165-146">Version 1.16.2</span></span>

<span data-ttu-id="53165-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 je teď obecně dostupný.</span><span class="sxs-lookup"><span data-stu-id="53165-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability.</span></span> <span data-ttu-id="53165-148">K dispozici jsou také aktualizované [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) .</span><span class="sxs-lookup"><span data-stu-id="53165-148">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="53165-149">V této verzi jsou zahrnuté tyto změny:</span><span class="sxs-lookup"><span data-stu-id="53165-149">The following changes are included in this version:</span></span>

* <span data-ttu-id="53165-150">Aktualizuje podporované typy operací pro záznam auditu.</span><span class="sxs-lookup"><span data-stu-id="53165-150">Update supported operation types for Audit Record.</span></span> <span data-ttu-id="53165-151">Nově přidaná jsou:</span><span class="sxs-lookup"><span data-stu-id="53165-151">The newly added ones are:</span></span>
  * <span data-ttu-id="53165-152">CreateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="53165-152">CreateSelfServePolicy</span></span>
  * <span data-ttu-id="53165-153">UpdateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="53165-153">UpdateSelfServePolicy</span></span>
  * <span data-ttu-id="53165-154">DeleteSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="53165-154">DeleteSelfServePolicy</span></span>
  * <span data-ttu-id="53165-155">RemovePartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="53165-155">RemovePartnerRelationship</span></span>
  * <span data-ttu-id="53165-156">DeleteTipCustomer</span><span class="sxs-lookup"><span data-stu-id="53165-156">DeleteTipCustomer</span></span>
  * <span data-ttu-id="53165-157">CreateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="53165-157">CreateRelatedReferral</span></span>
  * <span data-ttu-id="53165-158">UpdateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="53165-158">UpdateRelatedReferral</span></span>

* <span data-ttu-id="53165-159">Vytváření žádosti o služby je teď zastaralé.</span><span class="sxs-lookup"><span data-stu-id="53165-159">Service request creation is now deprecated</span></span>
* <span data-ttu-id="53165-160">Témata podpory jsou nyní zastaralá.</span><span class="sxs-lookup"><span data-stu-id="53165-160">Support topics are now deprecated</span></span>


## <a name="version-1161"></a><span data-ttu-id="53165-161">1.16.1 verze</span><span class="sxs-lookup"><span data-stu-id="53165-161">Version 1.16.1</span></span>

<span data-ttu-id="53165-162">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 je teď obecně dostupný.</span><span class="sxs-lookup"><span data-stu-id="53165-162">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability.</span></span> <span data-ttu-id="53165-163">K dispozici jsou také aktualizované [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) .</span><span class="sxs-lookup"><span data-stu-id="53165-163">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="53165-164">V této verzi jsou zahrnuté tyto změny:</span><span class="sxs-lookup"><span data-stu-id="53165-164">The following changes are included in this version:</span></span>

<span data-ttu-id="53165-165">Migrovali jsme stávající sadu SDK partnerského centra Microsoft z .NET Framework na platformu .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="53165-165">We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform.</span></span> <span data-ttu-id="53165-166">Sada SDK bude kompatibilní se stávajícími aplikacemi, a to pomocí .NET Framework 4.6.1 a vyšších.</span><span class="sxs-lookup"><span data-stu-id="53165-166">This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above.</span></span> <span data-ttu-id="53165-167">Sada SDK bude podporovat .NET Core 2,0 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="53165-167">The SDK will support .NET Core 2.0 and above.</span></span> <span data-ttu-id="53165-168">Před převedením na existující aplikace ověřte [podporu implementace rozhraní .NET](/dotnet/standard/net-standard) .</span><span class="sxs-lookup"><span data-stu-id="53165-168">Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.</span></span>   


## <a name="version-1153"></a><span data-ttu-id="53165-169">1.15.3 verze</span><span class="sxs-lookup"><span data-stu-id="53165-169">Version 1.15.3</span></span>
<span data-ttu-id="53165-170">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 je teď obecně dostupný.</span><span class="sxs-lookup"><span data-stu-id="53165-170">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability.</span></span> <span data-ttu-id="53165-171">K dispozici jsou také aktualizované rozhraní REST API a [ukázky GitHubu](https://github.com/Microsoft/Partner-Center-DotNet-Samples) .</span><span class="sxs-lookup"><span data-stu-id="53165-171">Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="53165-172">V této verzi jsou zahrnuté tyto změny:</span><span class="sxs-lookup"><span data-stu-id="53165-172">The following changes are included in this version:</span></span>

* <span data-ttu-id="53165-173">Partnerská smlouva</span><span class="sxs-lookup"><span data-stu-id="53165-173">Partner Agreement</span></span>
  * <span data-ttu-id="53165-174">Přidali jsme možnost nepřímých zprostředkovatelů [ověřit stav smluv o nepřímých prodejích u partnerů Microsoftu](verify-indirect-reseller-mpa-status.md).</span><span class="sxs-lookup"><span data-stu-id="53165-174">Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).</span></span>
* <span data-ttu-id="53165-175">Produkty</span><span class="sxs-lookup"><span data-stu-id="53165-175">Products</span></span>
  * <span data-ttu-id="53165-176">Následující dvě rozhraní byly nesprávně umístěny do oboru názvů Microsoft. Store. PartnerCenter. Products.</span><span class="sxs-lookup"><span data-stu-id="53165-176">The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace.</span></span> <span data-ttu-id="53165-177">Teď se nacházejí v oboru názvů Microsoft. Store. PartnerCenter. Customers. Products.</span><span class="sxs-lookup"><span data-stu-id="53165-177">Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.</span></span>
    * <span data-ttu-id="53165-178">ICustomerProductByReservationScope</span><span class="sxs-lookup"><span data-stu-id="53165-178">ICustomerProductByReservationScope</span></span>
    * <span data-ttu-id="53165-179">ICustomerSkuByReservationScope</span><span class="sxs-lookup"><span data-stu-id="53165-179">ICustomerSkuByReservationScope</span></span>
