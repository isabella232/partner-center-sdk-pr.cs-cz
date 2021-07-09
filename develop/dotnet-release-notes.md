---
title: Partnerské centrum poznámky k verzi sady .NET SDK
description: Poznámky k nejnovější verzi sady .NET SDK Partnerské centrum.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1532d48c00550f5eb437ed0164d6a1f7bb340dd
ms.sourcegitcommit: 53c94db33b09c30e762b842c4275b2b531dba932
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2021
ms.locfileid: "113522630"
---
# <a name="net-sdk-release-notes"></a><span data-ttu-id="f451e-103">Poznámky k verzi sady .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f451e-103">.NET SDK release notes</span></span>

<span data-ttu-id="f451e-104">Následující poznámky k verzi jsou k dispozici pro nové verze [sady Microsoft Partnerské centrum .NET SDK.](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)</span><span class="sxs-lookup"><span data-stu-id="f451e-104">The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span></span> <span data-ttu-id="f451e-105">Ukázky [.NET SDK najdete na](https://github.com/Microsoft/Partner-Center-DotNet-Samples) GitHub.</span><span class="sxs-lookup"><span data-stu-id="f451e-105">You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub.</span></span> <span data-ttu-id="f451e-106">Referenční informace k [Partnerské centrum .NET API](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) najdete v prohlížeči rozhraní .NET API.</span><span class="sxs-lookup"><span data-stu-id="f451e-106">You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.</span></span>

## <a name="version-201"></a><span data-ttu-id="f451e-107">Verze 2.0.1</span><span class="sxs-lookup"><span data-stu-id="f451e-107">Version 2.0.1</span></span>

<span data-ttu-id="f451e-108">[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 je teď obecně dostupné.</span><span class="sxs-lookup"><span data-stu-id="f451e-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 is now general availability.</span></span> <span data-ttu-id="f451e-109">K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky.</span><span class="sxs-lookup"><span data-stu-id="f451e-109">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="f451e-110">V této verzi jsou zahrnuté následující změny:</span><span class="sxs-lookup"><span data-stu-id="f451e-110">The following changes are included in this version:</span></span>

> [!NOTE]
> <span data-ttu-id="f451e-111">Některé změny zavedené v rámci nových obchodních prostředí (NCE), které jsou aktuálně k dispozici pouze na základě pozvánek partnerům, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview.</span><span class="sxs-lookup"><span data-stu-id="f451e-111">Some of changes introduced as part of New Commerce Experiences (“NCE”) which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span> <span data-ttu-id="f451e-112">Partneři, kteří nejsou součástí privátní verze New Commerce Preview, by si neměli všimnout dopadu a měli by být zpětně kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="f451e-112">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>

### <a name="common"></a><span data-ttu-id="f451e-113">Společné</span><span class="sxs-lookup"><span data-stu-id="f451e-113">Common</span></span>
* <span data-ttu-id="f451e-114">Změna odkazu na knihovnu ověřování – Odkaz se změnil z knihovny Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)na knihovnu Microsoft Authentication Library[(MSAL).](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)</span><span class="sxs-lookup"><span data-stu-id="f451e-114">Change on the reference to authentication library – The reference is changed from Azure Active Directory Authentication Library ([ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)) to Microsoft Authentication Library ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet))</span></span>

  <span data-ttu-id="f451e-115">Je třeba provést následující změny, aby se zajistilo správné spuštění MSAL ve vaší aplikaci nebo ukázce .NET:</span><span class="sxs-lookup"><span data-stu-id="f451e-115">Following changes should be made to ensure MSAL runs correctly on your application or .NET sample:</span></span>

  * <span data-ttu-id="f451e-116">Přidání `https://login.microsoftonline.com/common/oauth2/nativeclient` jako RedirectUrl pro mobilní a desktopové aplikace</span><span class="sxs-lookup"><span data-stu-id="f451e-116">Add `https://login.microsoftonline.com/common/oauth2/nativeclient` as RedirectUrl for Mobile and desktop applications</span></span>
  * <span data-ttu-id="f451e-117">Do **části** UserAuthentication v konfiguračním souboru aplikace přidejte Domain.</span><span class="sxs-lookup"><span data-stu-id="f451e-117">Add **Domain** into UserAuthentication section in your application configuration file.</span></span> 

    <span data-ttu-id="f451e-118">Doména je id Azure Active Directory domény nebo tenanta, ve které se vytvořila aplikace Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f451e-118">Domain is the Azure Active Directory domain or tenant ID where the Azure AD application was created</span></span>

* <span data-ttu-id="f451e-119">[Kódy chyb](error-codes.md) – Přidání nového kódu chyby</span><span class="sxs-lookup"><span data-stu-id="f451e-119">[Error codes](error-codes.md) – New error code added</span></span> 
  * <span data-ttu-id="f451e-120">408: Časový limit požadavku</span><span class="sxs-lookup"><span data-stu-id="f451e-120">408: Request timeout</span></span>
  * <span data-ttu-id="f451e-121">504: Časový limit brány</span><span class="sxs-lookup"><span data-stu-id="f451e-121">504: Gateway timeout</span></span> 

### <a name="manage-billing"></a><span data-ttu-id="f451e-122">Správa vyúčtování</span><span class="sxs-lookup"><span data-stu-id="f451e-122">Manage billing</span></span>

* <span data-ttu-id="f451e-123">[Řádkové položky faktury](get-invoiceline-items.md) – nové atributy přidané do následujících rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="f451e-123">[Invoice line-items](get-invoiceline-items.md) - new attributes added to following APIs:</span></span>
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  <span data-ttu-id="f451e-124">Nové atributy:</span><span class="sxs-lookup"><span data-stu-id="f451e-124">New attributes:</span></span> 
  * <span data-ttu-id="f451e-125">ProductQualifiers</span><span class="sxs-lookup"><span data-stu-id="f451e-125">productQualifiers</span></span>
  * <span data-ttu-id="f451e-126">subscriptionStartDate</span><span class="sxs-lookup"><span data-stu-id="f451e-126">subscriptionStartDate</span></span>
  * <span data-ttu-id="f451e-127">subscriptionEndDate</span><span class="sxs-lookup"><span data-stu-id="f451e-127">subscriptionEndDate</span></span>
  * <span data-ttu-id="f451e-128">ID odkazu</span><span class="sxs-lookup"><span data-stu-id="f451e-128">referenceId</span></span>
  * <span data-ttu-id="f451e-129">creditReasonCode (vztahuje se pouze na NCE)</span><span class="sxs-lookup"><span data-stu-id="f451e-129">creditReasonCode  (Only applicable to NCE)</span></span>
  * <span data-ttu-id="f451e-130">ID povýšení</span><span class="sxs-lookup"><span data-stu-id="f451e-130">promotionId</span></span> 


* <span data-ttu-id="f451e-131">[Daily rated usage Line-items](get-invoice-billed-consumption-lineitems.md) – nové atributy přidané do následujícího rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="f451e-131">[Daily rated usage Line-items](get-invoice-billed-consumption-lineitems.md) – new attributes added to following API:</span></span> 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  <span data-ttu-id="f451e-132">Nové atributy:</span><span class="sxs-lookup"><span data-stu-id="f451e-132">New attributes:</span></span> 
  * <span data-ttu-id="f451e-133">hasPartnerEarnedCredit (platí pouze pro NCE)</span><span class="sxs-lookup"><span data-stu-id="f451e-133">hasPartnerEarnedCredit (Only applicable to NCE)</span></span>
  * <span data-ttu-id="f451e-134">creditType (vztahuje se pouze na NCE)</span><span class="sxs-lookup"><span data-stu-id="f451e-134">creditType (Only applicable to NCE)</span></span>
  * <span data-ttu-id="f451e-135">rateOfCredit (vztahuje se pouze na NCE)</span><span class="sxs-lookup"><span data-stu-id="f451e-135">rateOfCredit (Only applicable to NCE)</span></span>


### <a name="manage-orders"></a><span data-ttu-id="f451e-136">Správa objednávek</span><span class="sxs-lookup"><span data-stu-id="f451e-136">Manage orders</span></span>

* <span data-ttu-id="f451e-137">[Prostředky předplatného](subscription-resources.md) – Přidaná nová vlastnost.</span><span class="sxs-lookup"><span data-stu-id="f451e-137">[Subscription Resources](subscription-resources.md) – New property added.</span></span> 
  * <span data-ttu-id="f451e-138">CancellationAllowedUntilDate – (vztahuje se pouze na NCE)</span><span class="sxs-lookup"><span data-stu-id="f451e-138">CancellationAllowedUntilDate  - (Only applicable to NCE)</span></span>

* <span data-ttu-id="f451e-139">Transition Resources (platí jenom pro NCE) – Přidaná nová vlastnost</span><span class="sxs-lookup"><span data-stu-id="f451e-139">Transition Resources (Only applicable to NCE) – New property added</span></span> 
  * <span data-ttu-id="f451e-140">FromSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="f451e-140">FromSubscriptionId</span></span>

### <a name="manage-customer-accounts"></a><span data-ttu-id="f451e-141">Správa zákaznických účtů</span><span class="sxs-lookup"><span data-stu-id="f451e-141">Manage customer accounts</span></span>

* <span data-ttu-id="f451e-142">[Ověření adresy –](validate-an-address.md) Odpověď se změnila z logické hodnoty na nový model pro rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="f451e-142">[Validate an address](validate-an-address.md) – Response is changed from a Boolean to a new model for API:</span></span>
  * `POST /validations/address`
  
  <span data-ttu-id="f451e-143">Nový model odpovědí:</span><span class="sxs-lookup"><span data-stu-id="f451e-143">New response model:</span></span> 
  * <span data-ttu-id="f451e-144">AddressValidationResponse</span><span class="sxs-lookup"><span data-stu-id="f451e-144">AddressValidationResponse</span></span>

* <span data-ttu-id="f451e-145">Synchronní rozhraní API kvalifikace zákazníka je zastaralé.</span><span class="sxs-lookup"><span data-stu-id="f451e-145">Customer’s qualification synchronous API is deprecated.</span></span>  


## <a name="version-1170"></a><span data-ttu-id="f451e-146">Verze 1.17.0</span><span class="sxs-lookup"><span data-stu-id="f451e-146">Version 1.17.0</span></span>

<span data-ttu-id="f451e-147">[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) verze 1.17.0 je teď obecně dostupné.</span><span class="sxs-lookup"><span data-stu-id="f451e-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability.</span></span> <span data-ttu-id="f451e-148">K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky.</span><span class="sxs-lookup"><span data-stu-id="f451e-148">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="f451e-149">V této verzi jsou zahrnuté následující změny:</span><span class="sxs-lookup"><span data-stu-id="f451e-149">The following changes are included in this version:</span></span>

* <span data-ttu-id="f451e-150">Audit byl aktualizován – Přidání nových typů operací pro znalost, kdy zákazník schválil a ukončil DAP</span><span class="sxs-lookup"><span data-stu-id="f451e-150">Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP</span></span>
  * [<span data-ttu-id="f451e-151">DapAdminRelationshipApproved</span><span class="sxs-lookup"><span data-stu-id="f451e-151">DapAdminRelationshipApproved</span></span>](auditing-resources.md)
  * [<span data-ttu-id="f451e-152">DapAdminRelationshipTerminated</span><span class="sxs-lookup"><span data-stu-id="f451e-152">DapAdminRelationshipTerminated</span></span>](auditing-resources.md)

* <span data-ttu-id="f451e-153">Audit byl aktualizován – Přidání nových typů prostředků a operací pro podporu scénáře role adresáře zákazníka</span><span class="sxs-lookup"><span data-stu-id="f451e-153">Audit Updated – Added new resource and operation types for supporting the customer directory role scenario</span></span>
  * <span data-ttu-id="f451e-154">Typ prostředku[CustomerDirectoryRole](auditing-resources.md)</span><span class="sxs-lookup"><span data-stu-id="f451e-154">Resource type "[CustomerDirectoryRole](auditing-resources.md)"</span></span>
  * <span data-ttu-id="f451e-155">Typy operací[AddUserMember](auditing-resources.md)a[RemoveUserMember](auditing-resources.md)</span><span class="sxs-lookup"><span data-stu-id="f451e-155">Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"</span></span>

* <span data-ttu-id="f451e-156">Aktualizace sady SDK pro účet zákazníků – Podpora následujících rozhraní API</span><span class="sxs-lookup"><span data-stu-id="f451e-156">SDK Updates to Customers Account - Support for following API's</span></span>
  * <span data-ttu-id="f451e-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="f451e-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span></span>
  * <span data-ttu-id="f451e-158">GET /customers/{id-tenanta zákazníka}/kvalifikace</span><span class="sxs-lookup"><span data-stu-id="f451e-158">GET /customers/{customer-tenant-id}/qualifications</span></span> 
  * <span data-ttu-id="f451e-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span><span class="sxs-lookup"><span data-stu-id="f451e-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span></span>

* <span data-ttu-id="f451e-160">**Následující změny zavedené v rámci nového obchodování jsou v současné době k dispozici pouze na základě pozvánek pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview.**</span><span class="sxs-lookup"><span data-stu-id="f451e-160">**Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.**</span></span> <span data-ttu-id="f451e-161">Partneři, kteří nejsou součástí privátní verze New Commerce Preview, by si neměli všimnout dopadu a měli by být zpětně kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="f451e-161">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>
  * <span data-ttu-id="f451e-162">Catalog Changes (Změny katalogu):</span><span class="sxs-lookup"><span data-stu-id="f451e-162">Catalog Changes:</span></span>
    * <span data-ttu-id="f451e-163">GET /products/{id-produktu}/skus/{sku-id}</span><span class="sxs-lookup"><span data-stu-id="f451e-163">GET /products/{product-id}/skus/{sku-id}</span></span>
  * <span data-ttu-id="f451e-164">Nákup a správa:</span><span class="sxs-lookup"><span data-stu-id="f451e-164">Purchase and Manage:</span></span>
    * <span data-ttu-id="f451e-165">GET /customers/{customerId}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="f451e-165">GET /customers/{customerId}/subscriptions</span></span>
    * <span data-ttu-id="f451e-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="f451e-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="f451e-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="f451e-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="f451e-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitionelibilities</span><span class="sxs-lookup"><span data-stu-id="f451e-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span></span>
    * <span data-ttu-id="f451e-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="f451e-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>
    * <span data-ttu-id="f451e-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="f451e-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>


## <a name="version-1163"></a><span data-ttu-id="f451e-171">Verze 1.16.3</span><span class="sxs-lookup"><span data-stu-id="f451e-171">Version 1.16.3</span></span>

<span data-ttu-id="f451e-172">[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) verze 1.16.3 je teď obecně dostupné.</span><span class="sxs-lookup"><span data-stu-id="f451e-172">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability.</span></span> <span data-ttu-id="f451e-173">K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky.</span><span class="sxs-lookup"><span data-stu-id="f451e-173">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="f451e-174">V této verzi jsou zahrnuté následující změny:</span><span class="sxs-lookup"><span data-stu-id="f451e-174">The following changes are included in this version:</span></span>

* <span data-ttu-id="f451e-175">SelfServePolicies – přidání nových funkcí</span><span class="sxs-lookup"><span data-stu-id="f451e-175">SelfServePolicies - new functionality added</span></span>
  * [<span data-ttu-id="f451e-176">GetSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="f451e-176">GetSelfServePolicies</span></span>](get-a-self-serve-policy-by-id.md)
  * [<span data-ttu-id="f451e-177">GetListOfSelfServicePolicies</span><span class="sxs-lookup"><span data-stu-id="f451e-177">GetListOfSelfServicePolicies</span></span>](get-a-list-of-self-serve-policies.md)
  * [<span data-ttu-id="f451e-178">CreateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="f451e-178">CreateSelfServePolicies</span></span>](create-a-self-serve-policy.md)
  * [<span data-ttu-id="f451e-179">UpdateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="f451e-179">UpdateSelfServePolicies</span></span>](update-a-self-serve-policy.md)
  * [<span data-ttu-id="f451e-180">DeleteSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="f451e-180">DeleteSelfServePolicies</span></span>](delete-a-self-serve-policy.md)

* <span data-ttu-id="f451e-181">Profil společnosti zákazníků</span><span class="sxs-lookup"><span data-stu-id="f451e-181">Customers Company Profile</span></span>
  * <span data-ttu-id="f451e-182">Přidání [OrganizationRegistrationNumber](create-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="f451e-182">Added [OrganizationRegistrationNumber](create-a-customer.md)</span></span>

* <span data-ttu-id="f451e-183">CustomerBillingProfile.DefaultAddress</span><span class="sxs-lookup"><span data-stu-id="f451e-183">CustomerBillingProfile.DefaultAddress</span></span>
  * <span data-ttu-id="f451e-184">Přidání middleName</span><span class="sxs-lookup"><span data-stu-id="f451e-184">Added MiddleName</span></span>

## <a name="version-1162"></a><span data-ttu-id="f451e-185">Verze 1.16.2</span><span class="sxs-lookup"><span data-stu-id="f451e-185">Version 1.16.2</span></span>

<span data-ttu-id="f451e-186">[Sada Microsoft Partnerské centrum .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) verze 1.16.2 je teď obecně dostupné.</span><span class="sxs-lookup"><span data-stu-id="f451e-186">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability.</span></span> <span data-ttu-id="f451e-187">K [dispozici GitHub aktualizované](https://github.com/Microsoft/Partner-Center-DotNet-Samples) ukázky.</span><span class="sxs-lookup"><span data-stu-id="f451e-187">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="f451e-188">V této verzi jsou zahrnuté následující změny:</span><span class="sxs-lookup"><span data-stu-id="f451e-188">The following changes are included in this version:</span></span>

* <span data-ttu-id="f451e-189">Aktualizujte podporované typy operací pro záznam auditu.</span><span class="sxs-lookup"><span data-stu-id="f451e-189">Update supported operation types for Audit Record.</span></span> <span data-ttu-id="f451e-190">Nově přidané jsou tyto:</span><span class="sxs-lookup"><span data-stu-id="f451e-190">The newly added ones are:</span></span>
  * <span data-ttu-id="f451e-191">CreateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="f451e-191">CreateSelfServePolicy</span></span>
  * <span data-ttu-id="f451e-192">UpdateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="f451e-192">UpdateSelfServePolicy</span></span>
  * <span data-ttu-id="f451e-193">DeleteSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="f451e-193">DeleteSelfServePolicy</span></span>
  * <span data-ttu-id="f451e-194">RemovePartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="f451e-194">RemovePartnerRelationship</span></span>
  * <span data-ttu-id="f451e-195">DeleteTipCustomer</span><span class="sxs-lookup"><span data-stu-id="f451e-195">DeleteTipCustomer</span></span>
  * <span data-ttu-id="f451e-196">CreateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="f451e-196">CreateRelatedReferral</span></span>
  * <span data-ttu-id="f451e-197">UpdateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="f451e-197">UpdateRelatedReferral</span></span>

* <span data-ttu-id="f451e-198">Vytváření žádostí o služby je teď zastaralé</span><span class="sxs-lookup"><span data-stu-id="f451e-198">Service request creation is now deprecated</span></span>
* <span data-ttu-id="f451e-199">Témata podpory jsou teď zastaralá.</span><span class="sxs-lookup"><span data-stu-id="f451e-199">Support topics are now deprecated</span></span>


## <a name="version-1161"></a><span data-ttu-id="f451e-200">Verze 1.16.1</span><span class="sxs-lookup"><span data-stu-id="f451e-200">Version 1.16.1</span></span>

<span data-ttu-id="f451e-201">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 je teď obecně dostupný.</span><span class="sxs-lookup"><span data-stu-id="f451e-201">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability.</span></span> <span data-ttu-id="f451e-202">k dispozici jsou také aktualizované [ukázky GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) .</span><span class="sxs-lookup"><span data-stu-id="f451e-202">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="f451e-203">V této verzi jsou zahrnuté tyto změny:</span><span class="sxs-lookup"><span data-stu-id="f451e-203">The following changes are included in this version:</span></span>

<span data-ttu-id="f451e-204">migrovali jsme stávající sadu SDK partnerského centra Microsoft z .NET Framework na platformu .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="f451e-204">We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform.</span></span> <span data-ttu-id="f451e-205">sada SDK bude kompatibilní se stávajícími aplikacemi, a to pomocí .NET Framework 4.6.1 a vyšších.</span><span class="sxs-lookup"><span data-stu-id="f451e-205">This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above.</span></span> <span data-ttu-id="f451e-206">Sada SDK bude podporovat .NET Core 2,0 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="f451e-206">The SDK will support .NET Core 2.0 and above.</span></span> <span data-ttu-id="f451e-207">Před převedením na existující aplikace ověřte [podporu implementace rozhraní .NET](/dotnet/standard/net-standard) .</span><span class="sxs-lookup"><span data-stu-id="f451e-207">Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.</span></span>   


## <a name="version-1153"></a><span data-ttu-id="f451e-208">1.15.3 verze</span><span class="sxs-lookup"><span data-stu-id="f451e-208">Version 1.15.3</span></span>
<span data-ttu-id="f451e-209">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 je teď obecně dostupný.</span><span class="sxs-lookup"><span data-stu-id="f451e-209">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability.</span></span> <span data-ttu-id="f451e-210">k dispozici jsou také aktualizovaná rozhraní REST api a [ukázky GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) .</span><span class="sxs-lookup"><span data-stu-id="f451e-210">Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="f451e-211">V této verzi jsou zahrnuté tyto změny:</span><span class="sxs-lookup"><span data-stu-id="f451e-211">The following changes are included in this version:</span></span>

* <span data-ttu-id="f451e-212">Partnerská smlouva</span><span class="sxs-lookup"><span data-stu-id="f451e-212">Partner Agreement</span></span>
  * <span data-ttu-id="f451e-213">Přidali jsme možnost nepřímých zprostředkovatelů [ověřit stav smluv o nepřímých prodejích u partnerů Microsoftu](verify-indirect-reseller-mpa-status.md).</span><span class="sxs-lookup"><span data-stu-id="f451e-213">Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).</span></span>
* <span data-ttu-id="f451e-214">Produkty</span><span class="sxs-lookup"><span data-stu-id="f451e-214">Products</span></span>
  * <span data-ttu-id="f451e-215">Následující dvě rozhraní byly nesprávně umístěny do oboru názvů Microsoft. Store. PartnerCenter. Products.</span><span class="sxs-lookup"><span data-stu-id="f451e-215">The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace.</span></span> <span data-ttu-id="f451e-216">Teď se nacházejí v oboru názvů Microsoft. Store. PartnerCenter. Customers. Products.</span><span class="sxs-lookup"><span data-stu-id="f451e-216">Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.</span></span>
    * <span data-ttu-id="f451e-217">ICustomerProductByReservationScope</span><span class="sxs-lookup"><span data-stu-id="f451e-217">ICustomerProductByReservationScope</span></span>
    * <span data-ttu-id="f451e-218">ICustomerSkuByReservationScope</span><span class="sxs-lookup"><span data-stu-id="f451e-218">ICustomerSkuByReservationScope</span></span>
