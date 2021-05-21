---
title: Schopnosti nepřímých poskytovatelů CSP v izolovaném prostoru
description: Nepřímá poskytovatelé můžou vytvořit nepřímé prodejce v izolovaném prostoru (sandbox) pro účely testování.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: bd0f38103e6b6f93ab5da386042b00801b683ccd
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2021
ms.locfileid: "110244601"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="6750e-103">Funkce izolovaného prostoru nepřímých poskytovatelů CSP pro vytváření nepřímých účtů prodejců</span><span class="sxs-lookup"><span data-stu-id="6750e-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="6750e-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="6750e-104">**Applies to**</span></span>

- <span data-ttu-id="6750e-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="6750e-105">Partner Center</span></span>

<span data-ttu-id="6750e-106">**Příslušné role**</span><span class="sxs-lookup"><span data-stu-id="6750e-106">**Appropriate roles**</span></span>

- <span data-ttu-id="6750e-107">Nepřímý poskytovatel</span><span class="sxs-lookup"><span data-stu-id="6750e-107">Indirect provider</span></span>

<span data-ttu-id="6750e-108">Zprostředkovatelé nepřímých poskytovatelů CSP můžou vytvořit účet nepřímého prodejce CSP prostřednictvím vlastního účtu izolovaného prostoru (sandboxu) na portálu pro partnery v partnerském centru.</span><span class="sxs-lookup"><span data-stu-id="6750e-108">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6750e-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6750e-109">Prerequisites</span></span> 

<span data-ttu-id="6750e-110">Přihlašovací údaje k izolovanému prostoru nepřímých zprostředkovatelů (vrstvy 2) partnerského centra</span><span class="sxs-lookup"><span data-stu-id="6750e-110">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="6750e-111">Scénář izolovaného prostoru (sandbox) podporuje ověřování jak pro samostatnou aplikaci, tak i pro přihlašovací údaje uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="6750e-111">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="6750e-112">Nepřímý poskytovatel izolovaného prostoru – vytvoření nepřímého prodejce izolovaného prostoru pomocí uživatelského rozhraní partnerského centra</span><span class="sxs-lookup"><span data-stu-id="6750e-112">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="6750e-113">Jedná se o funkci pouze izolovaného prostoru, která umožňuje nepřímým poskytovatelům izolovaného prostoru vytvořit účet nepřímých prodejců izolovaného prostoru prostřednictvím portálu pro partnery služby.</span><span class="sxs-lookup"><span data-stu-id="6750e-113">This is a Sandbox- only feature that allows Sandbox Indirect Providers the ability to create Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="6750e-114">Následující scénáře se dají nepřímým poskytovatelům provádět u nepřímých prodejců v izolovaném prostoru (sandbox) prostřednictvím uživatelského rozhraní partnerského centra:</span><span class="sxs-lookup"><span data-stu-id="6750e-114">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="6750e-115">Nepřímá poskytovatelé CSP můžou vytvořit účet nepřímých prodejců CSP prostřednictvím vlastního účtu izolovaného prostoru (sandboxu) v portálu pro partnery v partnerském centru.</span><span class="sxs-lookup"><span data-stu-id="6750e-115">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="6750e-116">Nepřímým prodejcům CSP můžou zákazníka zobrazit nepřímými poskytovateli.</span><span class="sxs-lookup"><span data-stu-id="6750e-116">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="6750e-117">Nepřímí prodejci CSP můžou spravovat účet zákazníka pomocí delegovaných oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="6750e-117">CSP Indirect Resellers  can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="6750e-118">Nepřímá poskytovatelé CSP můžou pozvat nepřímým prodejcům CSP.</span><span class="sxs-lookup"><span data-stu-id="6750e-118">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="6750e-119">Nepřímá poskytovatelé CSP mohou odstranit účet nepřímého prodejce CSP prostřednictvím vlastního účtu izolovaného prostoru (sandbox) v portálu pro partnery.</span><span class="sxs-lookup"><span data-stu-id="6750e-119">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="6750e-120">a.</span><span class="sxs-lookup"><span data-stu-id="6750e-120">a.</span></span>  <span data-ttu-id="6750e-121">Když nepřímý poskytovatel izolovaného prostoru odstraní relaci s nepřímým prodejcem izolovaného prostoru.</span><span class="sxs-lookup"><span data-stu-id="6750e-121">When Sandbox Indirect Provider deletes relationship with Sandbox Indirect Reseller.</span></span>

    <span data-ttu-id="6750e-122">b.</span><span class="sxs-lookup"><span data-stu-id="6750e-122">b.</span></span>  <span data-ttu-id="6750e-123">Zkontroluje, jestli má nepřímý prodejce jiné vztahy s ostatními poskytovateli.</span><span class="sxs-lookup"><span data-stu-id="6750e-123">Check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="6750e-124">Pokud ano, bude odebrán pouze vztah s tímto konkrétním nepřímým zprostředkovatelem.</span><span class="sxs-lookup"><span data-stu-id="6750e-124">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="6750e-125">c.</span><span class="sxs-lookup"><span data-stu-id="6750e-125">c.</span></span> <span data-ttu-id="6750e-126">Pokud se jedná o jediný vztah pro IR, bude IR odstraněn.</span><span class="sxs-lookup"><span data-stu-id="6750e-126">If that is the only relationship for the IR, then the IR will be deleted.</span></span>

1. <span data-ttu-id="6750e-127">CSP Indirect Provider můžete odstranit CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="6750e-127">CSP Indirect Provider can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="6750e-128">a.</span><span class="sxs-lookup"><span data-stu-id="6750e-128">a.</span></span> <span data-ttu-id="6750e-129">Jedná se o funkci sandboxu, která umožňuje nepřímým poskytovatelům sandboxu odstranit nepřímé prodejce Sandboxu.</span><span class="sxs-lookup"><span data-stu-id="6750e-129">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="6750e-130">Předpoklady pro odstranění nepřímého prodejce sandboxu:</span><span class="sxs-lookup"><span data-stu-id="6750e-130">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="6750e-131">Pozastavíte předplatná pro každého zákazníka nepřímého prodejce sandboxu.</span><span class="sxs-lookup"><span data-stu-id="6750e-131">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="6750e-132">Odstraňte všechny zákazníky nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="6750e-132">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="6750e-133">Povolený limit 5 nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu.</span><span class="sxs-lookup"><span data-stu-id="6750e-133">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="6750e-134">Po odstranění nepřímého prodejce sandboxu se kvóta resetuje.</span><span class="sxs-lookup"><span data-stu-id="6750e-134">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="6750e-135">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6750e-135">Pre-requisites</span></span>

- <span data-ttu-id="6750e-136">Povolený limit 5 nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu.</span><span class="sxs-lookup"><span data-stu-id="6750e-136">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="6750e-137">Stejné ID MPN můžete použít k vytvoření několika účtů sandboxu nepřímého prodejce, pokud je země MPN ID země a země sandboxu nepřímého prodejce stejné.</span><span class="sxs-lookup"><span data-stu-id="6750e-137">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="6750e-138">Pokud máte k dispozici testovací ID MPN, můžete ho použít nebo můžete získat seznam ID MPN prostřednictvím našeho [kanálu Yammeru]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span><span class="sxs-lookup"><span data-stu-id="6750e-138">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="6750e-139">Pokud nemáte přístup k Yammeru, Yammer vás požádá o přístup.</span><span class="sxs-lookup"><span data-stu-id="6750e-139">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="6750e-140">Na nepřímého poskytovatele sandboxu je povolených jenom 75 zákazníků.</span><span class="sxs-lookup"><span data-stu-id="6750e-140">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="6750e-141">Vytvoření CSP Indirect Reseller sandboxu</span><span class="sxs-lookup"><span data-stu-id="6750e-141">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="6750e-142">Přihlaste se Partnerské centrum účtu sandboxu úrovně 2.</span><span class="sxs-lookup"><span data-stu-id="6750e-142">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="6750e-143">V levé nabídce přejděte na Indirect Resellers (Nepřímí prodejci).</span><span class="sxs-lookup"><span data-stu-id="6750e-143">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="6750e-144">Klikněte na tlačítko Add Reseller Sandbox (Přidat sandbox prodejce).</span><span class="sxs-lookup"><span data-stu-id="6750e-144">Click on “Add Reseller Sandbox” button.</span></span> 

4. <span data-ttu-id="6750e-145">Vyplňte formulář pro registraci účtu.</span><span class="sxs-lookup"><span data-stu-id="6750e-145">Fill the account enrollment form.</span></span> <span data-ttu-id="6750e-146">Je to samozřejmé, ale nezapomeňte, že vytváříte účet sandboxu pro nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="6750e-146">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="6750e-147">Tento účet se nebude prověřovat a aktivuje se ihned po dokončení registrace účtu.</span><span class="sxs-lookup"><span data-stu-id="6750e-147">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="6750e-148">Po vytvoření účtu získáte na portálu přihlašovací údaje globálního správce pro účet sandboxu nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="6750e-148">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="6750e-149">Nezapomeňte ho uložit hned, jinak se nebudete moct přihlásit jako nepřímý prodejce prodejců.</span><span class="sxs-lookup"><span data-stu-id="6750e-149">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="6750e-150">Odhlaste se a znovu se přihlaste do partnerského centra pomocí nových přihlašovacích údajů pro nepřímý izolovaný prostor prodejce.</span><span class="sxs-lookup"><span data-stu-id="6750e-150">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="6750e-151">Prozkoumejte možnosti, které můžete udělat jako nepřímý prodejce.</span><span class="sxs-lookup"><span data-stu-id="6750e-151">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="6750e-152">Některé věci:</span><span class="sxs-lookup"><span data-stu-id="6750e-152">Some things are :</span></span>  

    - <span data-ttu-id="6750e-153">Správa profilů</span><span class="sxs-lookup"><span data-stu-id="6750e-153">Manage profiles</span></span>  

    - <span data-ttu-id="6750e-154">Správa uživatelů a skupin</span><span class="sxs-lookup"><span data-stu-id="6750e-154">Manage users and roles</span></span> 

    - <span data-ttu-id="6750e-155">Správa nepřímých zprostředkovatelů</span><span class="sxs-lookup"><span data-stu-id="6750e-155">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="6750e-156">Správa zákazníků v izolovaném prostoru (CSP)</span><span class="sxs-lookup"><span data-stu-id="6750e-156">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="6750e-157">Správa relací</span><span class="sxs-lookup"><span data-stu-id="6750e-157">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="6750e-158">Nepřímý poskytovatel izolovaného prostoru – odstranění nepřímého prodejce izolovaného prostoru pomocí uživatelského rozhraní partnerského centra</span><span class="sxs-lookup"><span data-stu-id="6750e-158">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="6750e-159">Jedná se o funkci pouze izolovaného prostoru, která umožňuje nepřímým poskytovatelům izolovaného prostoru odstranit stávající účet nepřímých prodejců izolovaného prostoru prostřednictvím portálu pro partnery.</span><span class="sxs-lookup"><span data-stu-id="6750e-159">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="6750e-160">Požadavky na odstranění nepřímého prodejce izolovaného prostoru:</span><span class="sxs-lookup"><span data-stu-id="6750e-160">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="6750e-161">Existující účet izolovaného prostoru nepřímých prodejců CSP přidružený k vlastnímu účtu izolovaného poskytovatele CSP – 2.</span><span class="sxs-lookup"><span data-stu-id="6750e-161">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="6750e-162">Odstranit účet izolovaného prostoru nepřímých prodejců CSP</span><span class="sxs-lookup"><span data-stu-id="6750e-162">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="6750e-163">Přihlaste se k partnerskému centru pomocí účtu sandboxu vrstvy 2.</span><span class="sxs-lookup"><span data-stu-id="6750e-163">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="6750e-164">V nabídce vlevo přejděte na nepřímé prodejce.</span><span class="sxs-lookup"><span data-stu-id="6750e-164">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="6750e-165">Klikněte na odkaz **Odstranit prodejce izolovaného prostoru** vedle nepřímým účtem izolovaného prostoru (sandbox) prodejce, který chcete odstranit.</span><span class="sxs-lookup"><span data-stu-id="6750e-165">Click on **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="6750e-166">Účet izolovaného prostoru pro prodejce se trvale odstraní a nebude možné ho obnovit.</span><span class="sxs-lookup"><span data-stu-id="6750e-166">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="6750e-167">Referenční informace k rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6750e-167">API references</span></span>

- <span data-ttu-id="6750e-168">Vytvořit nepřímý prodejce</span><span class="sxs-lookup"><span data-stu-id="6750e-168">Create Indirect Reseller</span></span> 
- <span data-ttu-id="6750e-169">Odstranit nepřímý prodejce</span><span class="sxs-lookup"><span data-stu-id="6750e-169">Delete Indirect Reseller</span></span> 

 

 