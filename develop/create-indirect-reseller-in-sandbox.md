---
title: Vytvoření nepřímého prodejce v izolovaném prostoru
description: Poskytuje informace o nepřímých poskytovatelích izolovaného prostoru na povolení koncových testování pomocí rozhraní API.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93e26792b66e447a0047bd550f4302c7fca4e87b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973430"
---
# <a name="create-indirect-reseller-in-sandbox"></a><span data-ttu-id="e714f-103">Vytvoření nepřímého prodejce v izolovaném prostoru</span><span class="sxs-lookup"><span data-stu-id="e714f-103">Create Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="e714f-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="e714f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e714f-105">Tento dokument ukazuje, jak vytvořit nepřímé zprostředkovatele izolovaného prostoru (sandbox) a jak povolit komplexní testování pomocí rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="e714f-105">This document shows how to create Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e714f-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e714f-106">Prerequisites</span></span>

- <span data-ttu-id="e714f-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e714f-107">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e714f-108">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="e714f-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="csp-indirect-provider"></a><span data-ttu-id="e714f-109">CSP Indirect Provider</span><span class="sxs-lookup"><span data-stu-id="e714f-109">CSP Indirect Provider</span></span>

| <span data-ttu-id="e714f-110">Provozní možnosti</span><span class="sxs-lookup"><span data-stu-id="e714f-110">Production capabilities</span></span>             | <span data-ttu-id="e714f-111">Možnosti izolovaného prostoru</span><span class="sxs-lookup"><span data-stu-id="e714f-111">Sandbox capabilities</span></span>                            |
|-------------------------------------|-------------------------------------------------|
| <span data-ttu-id="e714f-112">Prodává se prostřednictvím nepřímého prodejce k koncovému zákazníkovi</span><span class="sxs-lookup"><span data-stu-id="e714f-112">Sells through the indirect reseller to the end customer</span></span> | <span data-ttu-id="e714f-113">Podporováno</span><span class="sxs-lookup"><span data-stu-id="e714f-113">Supported</span></span> |
| <span data-ttu-id="e714f-114">Vlastní prodej, fakturace, zřizování a Správa/podpora</span><span class="sxs-lookup"><span data-stu-id="e714f-114">Owns all sales, billing, provisioning, and management/support</span></span> | <span data-ttu-id="e714f-115">Podporováno</span><span class="sxs-lookup"><span data-stu-id="e714f-115">Supported</span></span> |
| <span data-ttu-id="e714f-116">Požádat o partnerství se prodejci</span><span class="sxs-lookup"><span data-stu-id="e714f-116">Request a partnership with the resellers</span></span> | <span data-ttu-id="e714f-117">Podporováno</span><span class="sxs-lookup"><span data-stu-id="e714f-117">Supported</span></span> |
| <span data-ttu-id="e714f-118">Zobrazit zákazníky podle prodejce</span><span class="sxs-lookup"><span data-stu-id="e714f-118">View customers by Reseller</span></span> | <span data-ttu-id="e714f-119">Podporováno</span><span class="sxs-lookup"><span data-stu-id="e714f-119">Supported</span></span> |
| <span data-ttu-id="e714f-120">Přidat nové zákazníky podle prodejců</span><span class="sxs-lookup"><span data-stu-id="e714f-120">Add new customers by resellers</span></span> | <span data-ttu-id="e714f-121">Podporováno</span><span class="sxs-lookup"><span data-stu-id="e714f-121">Supported</span></span> |
| <span data-ttu-id="e714f-122">Pozvat zákazníky</span><span class="sxs-lookup"><span data-stu-id="e714f-122">Invite customers</span></span> | <span data-ttu-id="e714f-123">Požadavek vztahu zákazníka není v izolovaném prostoru (sandbox) podporován.</span><span class="sxs-lookup"><span data-stu-id="e714f-123">Customer relationship request not supported in Sandbox</span></span> |
| <span data-ttu-id="e714f-124">Nepřímý poskytovatel izolovaného prostoru může jako POR při umísťování transakce vybrat Sandbox IR (MPN ID).</span><span class="sxs-lookup"><span data-stu-id="e714f-124">Sandbox Indirect Provider can select Sandbox IR (MPN ID) as the POR while placing the transaction</span></span> | <span data-ttu-id="e714f-125">Podporováno</span><span class="sxs-lookup"><span data-stu-id="e714f-125">Supported</span></span> |
| <span data-ttu-id="e714f-126">Nepodporováno v produkčním prostředí</span><span class="sxs-lookup"><span data-stu-id="e714f-126">Not supported in production</span></span> | <span data-ttu-id="e714f-127">Nepřímý poskytovatel izolovaného prostoru může vytvořit nepřímý prodejce izolovaného prostoru (sandbox)</span><span class="sxs-lookup"><span data-stu-id="e714f-127">Sandbox Indirect Provider can create Sandbox Indirect Reseller</span></span> |
| <span data-ttu-id="e714f-128">ID MPN izolovaného prostoru (sandbox) by mělo být zadané, ID MPN produktu nebude fungovat.</span><span class="sxs-lookup"><span data-stu-id="e714f-128">Sandbox MPN ID should be entered, the product MPN ID will not work</span></span> | <span data-ttu-id="e714f-129">Nepodporováno v produkčním prostředí</span><span class="sxs-lookup"><span data-stu-id="e714f-129">Not supported in production</span></span> |
| <span data-ttu-id="e714f-130">Nepodporováno v produkčním prostředí</span><span class="sxs-lookup"><span data-stu-id="e714f-130">Not supported in production</span></span> | <span data-ttu-id="e714f-131">Přímý poskytovatel izolovaného prostoru může odstranit nepřímý prodejce izolovaného prostoru (sandbox).</span><span class="sxs-lookup"><span data-stu-id="e714f-131">Sandbox Indirect Provider can delete Sandbox Indirect Reseller</span></span> |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a><span data-ttu-id="e714f-132">Nepřímý poskytovatel izolovaného prostoru – vytvoření nepřímý prodejce izolovaného prostoru</span><span class="sxs-lookup"><span data-stu-id="e714f-132">Sandbox Indirect Provider – Create Sandbox Indirect Reseller</span></span>

<span data-ttu-id="e714f-133">Tato funkce je k dispozici pouze v izolovaném prostoru (sandbox) a poskytuje nepřímým poskytovatelům izolovaného prostoru možnost vytvářet nepřímé prodejce izolovaného prostoru.</span><span class="sxs-lookup"><span data-stu-id="e714f-133">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="e714f-134">Limit pěti nepřímých prodejců v izolovaném prostoru (sandbox) povolených pro jednotlivé nepřímých dodavatele</span><span class="sxs-lookup"><span data-stu-id="e714f-134">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider</span></span>
2. <span data-ttu-id="e714f-135">Nepřímé zprostředkovatele izolovaného prostoru můžou vytvářet zákazníky s `associatedPartnerId` nepřímým prodejcem izolovaného prostoru (sandbox)</span><span class="sxs-lookup"><span data-stu-id="e714f-135">Sandbox Indirect Providers can create customers with `associatedPartnerId` of Sandbox Indirect Reseller</span></span>
3. <span data-ttu-id="e714f-136">Zadejte ID [MPN](/partner-center/mpn-create-a-partner-center-account) konkrétní oblasti při vytváření nepřímého prodejce izolovaného prostoru (sandbox).</span><span class="sxs-lookup"><span data-stu-id="e714f-136">Enter the [MPN](/partner-center/mpn-create-a-partner-center-account) ID of a specific region while creating a Sandbox Indirect Reseller.</span></span> <span data-ttu-id="e714f-137">Víc nepřímých prodejců izolovaného prostoru (sandbox) je možné vytvořit se stejným ID MPN izolovaného prostoru.</span><span class="sxs-lookup"><span data-stu-id="e714f-137">Multiple Sandbox Indirect Resellers can be created with the same Sandbox MPN ID.</span></span>
4. <span data-ttu-id="e714f-138">Pro nepřímý poskytovatel izolovaného prostoru (sandboxu) jsou povoleni jenom 75</span><span class="sxs-lookup"><span data-stu-id="e714f-138">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="sandbox-indirect-resellers--view-customers"></a><span data-ttu-id="e714f-139">Nepřímý prodej v izolovaném prostoru – zobrazit zákazníky</span><span class="sxs-lookup"><span data-stu-id="e714f-139">Sandbox Indirect Resellers – View customers</span></span>

1. <span data-ttu-id="e714f-140">Nepřímý prodejci izolovaného prostoru můžou zobrazit seznam zákazníků v izolovaném prostoru (sandbox) podle nepřímých poskytovatelů izolovaného prostoru</span><span class="sxs-lookup"><span data-stu-id="e714f-140">Sandbox Indirect Resellers can view the list of sandbox customers by Sandbox Indirect providers.</span></span>
2. <span data-ttu-id="e714f-141">Nepřímý prodejci v izolovaném prostoru můžou spravovat účet zákazníka pomocí oprávnění delegovaného správce.</span><span class="sxs-lookup"><span data-stu-id="e714f-141">Sandbox Indirect Resellers can manage the customer account by using delegated administrator permissions.</span></span>

## <a name="create-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="e714f-142">Vytvoření nepřímého prodejce izolovaného prostoru prostřednictvím rozhraní API</span><span class="sxs-lookup"><span data-stu-id="e714f-142">Create Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="e714f-143">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e714f-143">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="e714f-144">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e714f-144">Request syntax</span></span>

| <span data-ttu-id="e714f-145">**Metoda**</span><span class="sxs-lookup"><span data-stu-id="e714f-145">**Method**</span></span> | <span data-ttu-id="e714f-146">**Identifikátor URI žádosti**</span><span class="sxs-lookup"><span data-stu-id="e714f-146">**Request URI**</span></span>                                                        |
|------------|------------------------------------------------------------------------|
| <span data-ttu-id="e714f-147">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="e714f-147">**POST**</span></span>   | <span data-ttu-id="e714f-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span><span class="sxs-lookup"><span data-stu-id="e714f-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="e714f-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e714f-149">Request headers</span></span>

- <span data-ttu-id="e714f-150">Toto rozhraní API se idempotentní (nepřinese se mu jiný výsledek, pokud ho zavoláte víckrát).</span><span class="sxs-lookup"><span data-stu-id="e714f-150">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>
- <span data-ttu-id="e714f-151">Vyžaduje se ID žádosti a ID korelace.</span><span class="sxs-lookup"><span data-stu-id="e714f-151">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="e714f-152">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e714f-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="e714f-153">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e714f-153">Request body</span></span>

<span data-ttu-id="e714f-154">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="e714f-154">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="e714f-155">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="e714f-155">Property</span></span>             | <span data-ttu-id="e714f-156">Typ</span><span class="sxs-lookup"><span data-stu-id="e714f-156">Type</span></span>           | <span data-ttu-id="e714f-157">Description</span><span class="sxs-lookup"><span data-stu-id="e714f-157">Description</span></span>                                      |
|----------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="e714f-158">mpnId</span><span class="sxs-lookup"><span data-stu-id="e714f-158">mpnId</span></span>                | <span data-ttu-id="e714f-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-159">string</span></span>         | <span data-ttu-id="e714f-160">ID MPN pro IR v konkrétní oblasti</span><span class="sxs-lookup"><span data-stu-id="e714f-160">The MPN ID for the IR in specific region</span></span>         |
| <span data-ttu-id="e714f-161">tenant</span><span class="sxs-lookup"><span data-stu-id="e714f-161">tenant</span></span>               | <span data-ttu-id="e714f-162">&lt;Řetězec slovníku, řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="e714f-162">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="e714f-163">Kolekce základních informací definující účet, který se má vytvořit</span><span class="sxs-lookup"><span data-stu-id="e714f-163">Collection of basic information that defines an account to be created</span></span> |
| <span data-ttu-id="e714f-164">legalBusinessProfile</span><span class="sxs-lookup"><span data-stu-id="e714f-164">legalBusinessProfile</span></span> | <span data-ttu-id="e714f-165">&lt;Řetězec slovníku, řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="e714f-165">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="e714f-166">Kolekce informací, které představují právní obchodní entitu, jako je kontakt, adresa a jméno</span><span class="sxs-lookup"><span data-stu-id="e714f-166">Collection of information that represents the legal business entity such as contact, address, and name</span></span> |
| <span data-ttu-id="e714f-167">organizationProfileLanguage</span><span class="sxs-lookup"><span data-stu-id="e714f-167">organizationProfileLanguage</span></span> | <span data-ttu-id="e714f-168">&lt;Řetězec slovníku, řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="e714f-168">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="e714f-169">Identifikátor jazyka organizace</span><span class="sxs-lookup"><span data-stu-id="e714f-169">The organization language identifier</span></span> |

<span data-ttu-id="e714f-170">Tato tabulka popisuje požadované vlastnosti v atributu **tenanta** .</span><span class="sxs-lookup"><span data-stu-id="e714f-170">This table describes the required properties in the **tenant** attribute.</span></span>

| <span data-ttu-id="e714f-171">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="e714f-171">Property</span></span>           | <span data-ttu-id="e714f-172">Typ</span><span class="sxs-lookup"><span data-stu-id="e714f-172">Type</span></span>           | <span data-ttu-id="e714f-173">Description</span><span class="sxs-lookup"><span data-stu-id="e714f-173">Description</span></span>                         |
|--------------------|----------------|-------------------------------------|
| <span data-ttu-id="e714f-174">domainPrefix</span><span class="sxs-lookup"><span data-stu-id="e714f-174">domainPrefix</span></span>       | <span data-ttu-id="e714f-175">Řetezce tabulka</span><span class="sxs-lookup"><span data-stu-id="e714f-175">String; unique</span></span> | <span data-ttu-id="e714f-176">Doména pro účet tenanta</span><span class="sxs-lookup"><span data-stu-id="e714f-176">Domain for the tenant account</span></span>       |
| <span data-ttu-id="e714f-177">name</span><span class="sxs-lookup"><span data-stu-id="e714f-177">name</span></span>               | <span data-ttu-id="e714f-178">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-178">string</span></span>         | <span data-ttu-id="e714f-179">Popisný název tenanta</span><span class="sxs-lookup"><span data-stu-id="e714f-179">Friendly name of the tenant</span></span>         |
| <span data-ttu-id="e714f-180">displayName</span><span class="sxs-lookup"><span data-stu-id="e714f-180">displayName</span></span>        | <span data-ttu-id="e714f-181">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-181">string</span></span>         | <span data-ttu-id="e714f-182">Zobrazovaný název účtu</span><span class="sxs-lookup"><span data-stu-id="e714f-182">Display name for the account</span></span>        |
| <span data-ttu-id="e714f-183">adminUserName</span><span class="sxs-lookup"><span data-stu-id="e714f-183">adminUserName</span></span>      | <span data-ttu-id="e714f-184">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-184">string</span></span>         | <span data-ttu-id="e714f-185">Uživatelské jméno pro účet pro přihlášení</span><span class="sxs-lookup"><span data-stu-id="e714f-185">User name for the account for login</span></span> |
| <span data-ttu-id="e714f-186">adminfirstname</span><span class="sxs-lookup"><span data-stu-id="e714f-186">adminfirstname</span></span>     | <span data-ttu-id="e714f-187">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-187">string</span></span>         | <span data-ttu-id="e714f-188">Křestní jméno pro uživatele s oprávněními správce</span><span class="sxs-lookup"><span data-stu-id="e714f-188">First Name for the admin user</span></span>       |
| <span data-ttu-id="e714f-189">adminlastname</span><span class="sxs-lookup"><span data-stu-id="e714f-189">adminlastname</span></span>      | <span data-ttu-id="e714f-190">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-190">string</span></span>         | <span data-ttu-id="e714f-191">Příjmení pro uživatele s oprávněními správce</span><span class="sxs-lookup"><span data-stu-id="e714f-191">Last Name for the admin user</span></span>        |
| <span data-ttu-id="e714f-192">adminAlernateEmail</span><span class="sxs-lookup"><span data-stu-id="e714f-192">adminAlernateEmail</span></span> | <span data-ttu-id="e714f-193">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-193">string</span></span>         | <span data-ttu-id="e714f-194">e-mail pro uživatele s oprávněními správce</span><span class="sxs-lookup"><span data-stu-id="e714f-194">email for the admin user</span></span>            |
| <span data-ttu-id="e714f-195">country</span><span class="sxs-lookup"><span data-stu-id="e714f-195">country</span></span>            | <span data-ttu-id="e714f-196">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-196">string</span></span>         | <span data-ttu-id="e714f-197">Země účtu</span><span class="sxs-lookup"><span data-stu-id="e714f-197">Country of the account</span></span>              |
| <span data-ttu-id="e714f-198">jazyková verze</span><span class="sxs-lookup"><span data-stu-id="e714f-198">culture</span></span>            | <span data-ttu-id="e714f-199">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-199">string</span></span>         | <span data-ttu-id="e714f-200">Jazykové předvolby pro účet</span><span class="sxs-lookup"><span data-stu-id="e714f-200">Language preference for account</span></span>     |

<span data-ttu-id="e714f-201">Tato tabulka popisuje požadované vlastnosti v atributu **legalBusinessProfile** .</span><span class="sxs-lookup"><span data-stu-id="e714f-201">This table describes the required properties in the **legalBusinessProfile** attribute.</span></span>

| <span data-ttu-id="e714f-202">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="e714f-202">Property</span></span>       | <span data-ttu-id="e714f-203">Typ</span><span class="sxs-lookup"><span data-stu-id="e714f-203">Type</span></span>                             | <span data-ttu-id="e714f-204">Description</span><span class="sxs-lookup"><span data-stu-id="e714f-204">Description</span></span>                          |
|----------------|----------------------------------|--------------------------------------|
| <span data-ttu-id="e714f-205">Společnosti</span><span class="sxs-lookup"><span data-stu-id="e714f-205">companyName</span></span>    | <span data-ttu-id="e714f-206">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-206">string</span></span>                           | <span data-ttu-id="e714f-207">Název společnosti pro právnickou entitu</span><span class="sxs-lookup"><span data-stu-id="e714f-207">Company name for legal entity</span></span>        |
| <span data-ttu-id="e714f-208">adresa</span><span class="sxs-lookup"><span data-stu-id="e714f-208">address</span></span>        | <span data-ttu-id="e714f-209">&lt;Řetězec slovníku, řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="e714f-209">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="e714f-210">Adresa umístění právnické osoby</span><span class="sxs-lookup"><span data-stu-id="e714f-210">Address of the legal entity location</span></span> |
| <span data-ttu-id="e714f-211">primaryContact</span><span class="sxs-lookup"><span data-stu-id="e714f-211">primaryContact</span></span> | <span data-ttu-id="e714f-212">&lt;Řetězec slovníku, řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="e714f-212">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="e714f-213">Kontaktní údaje společnosti</span><span class="sxs-lookup"><span data-stu-id="e714f-213">Contact details of the company</span></span>       |
| <span data-ttu-id="e714f-214">jazyková verze</span><span class="sxs-lookup"><span data-stu-id="e714f-214">culture</span></span>        | <span data-ttu-id="e714f-215">řetězec</span><span class="sxs-lookup"><span data-stu-id="e714f-215">string</span></span>                           | <span data-ttu-id="e714f-216">Jazyk upřednostňovaný společností</span><span class="sxs-lookup"><span data-stu-id="e714f-216">Language preferred by the company</span></span>    |

### <a name="request-example"></a><span data-ttu-id="e714f-217">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e714f-217">Request Example</span></span>

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a><span data-ttu-id="e714f-218">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e714f-218">REST response</span></span>

<span data-ttu-id="e714f-219">V případě úspěchu tato metoda vrátí naplněný zdroj izolovaného prostoru (sandbox) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e714f-219">If successful, this method returns the populated Sandbox IR resource in the response body.</span></span>

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
