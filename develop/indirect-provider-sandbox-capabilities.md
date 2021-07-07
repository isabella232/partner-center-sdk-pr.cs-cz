---
title: Možnosti nepřímého poskytovatele CSP v sandboxu
description: Nepřímí poskytovatelé mohou pro účely testování vytvářet nepřímé prodejce v Sandboxu.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: da35dadd4e13247e923259a1cf3a67852f4b9e00
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445897"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="966c1-103">Možnosti sandboxu nepřímého poskytovatele CSP pro vytváření účtů nepřímých prodejců</span><span class="sxs-lookup"><span data-stu-id="966c1-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="966c1-104">**Odpovídající role:** Nepřímý poskytovatel</span><span class="sxs-lookup"><span data-stu-id="966c1-104">**Appropriate roles**: Indirect provider</span></span>

<span data-ttu-id="966c1-105">Nepřímí poskytovatelé CSP si CSP Indirect Reseller sandboxu prostřednictvím svého vlastního účtu sandboxu vrstvy 2 na Partnerské centrum Portal.</span><span class="sxs-lookup"><span data-stu-id="966c1-105">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="966c1-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="966c1-106">Prerequisites</span></span> 

<span data-ttu-id="966c1-107">Partnerské centrum sandboxu nepřímého poskytovatele (vrstva 2).</span><span class="sxs-lookup"><span data-stu-id="966c1-107">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="966c1-108">Scénář sandboxu podporuje ověřování pomocí samostatné aplikace i přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="966c1-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="966c1-109">Nepřímý poskytovatel sandboxu – Vytvoření nepřímého prodejce sandboxu pomocí Partnerské centrum rozhraní</span><span class="sxs-lookup"><span data-stu-id="966c1-109">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="966c1-110">Jedná se o funkci pouze pro sandbox, která nepřímým poskytovatelům sandboxu umožňuje vytvořit účet nepřímého prodejce sandboxu prostřednictvím Partnerské centrum Portal.</span><span class="sxs-lookup"><span data-stu-id="966c1-110">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to create a Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="966c1-111">Nepřímí poskytovatelé mohou pro nepřímé prodejce v Sandboxu dělat následující scénáře prostřednictvím Partnerské centrum rozhraní:</span><span class="sxs-lookup"><span data-stu-id="966c1-111">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="966c1-112">Nepřímí poskytovatelé CSP si CSP Indirect Reseller sandboxu prostřednictvím vlastního účtu sandboxu vrstvy 2 na Partnerské centrum Portal.</span><span class="sxs-lookup"><span data-stu-id="966c1-112">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="966c1-113">Nepřímí prodejci CSP mohou zobrazit zákazníka podle nepřímých poskytovatelů.</span><span class="sxs-lookup"><span data-stu-id="966c1-113">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="966c1-114">Nepřímí prodejci CSP mohou spravovat zákaznický účet pomocí delegovaných oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="966c1-114">CSP Indirect Resellers can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="966c1-115">Nepřímí poskytovatelé CSP mohou pozvat nepřímé prodejce CSP.</span><span class="sxs-lookup"><span data-stu-id="966c1-115">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="966c1-116">Nepřímí poskytovatelé CSP mohou odstranit účet CSP Indirect Reseller sandboxu prostřednictvím vlastního účtu sandboxu vrstvy 2 na Partnerské centrum Portal.</span><span class="sxs-lookup"><span data-stu-id="966c1-116">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="966c1-117">a.</span><span class="sxs-lookup"><span data-stu-id="966c1-117">a.</span></span>  <span data-ttu-id="966c1-118">Když nepřímý poskytovatel sandboxu odstraní relaci s nepřímým prodejcem sandboxu, zkontrolujte, jestli má nepřímý prodejce nějaký jiný vztah s jinými poskytovateli.</span><span class="sxs-lookup"><span data-stu-id="966c1-118">When Sandbox Indirect Provider deletes the relationship with Sandbox Indirect Reseller, check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="966c1-119">Pokud ano, odebere se pouze vztah s tímto konkrétním nepřímým poskytovatelem.</span><span class="sxs-lookup"><span data-stu-id="966c1-119">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="966c1-120">c.</span><span class="sxs-lookup"><span data-stu-id="966c1-120">c.</span></span> <span data-ttu-id="966c1-121">Pokud je to jediný vztah pro nepřímého prodejce, nepřímý prodejce se odstraní.</span><span class="sxs-lookup"><span data-stu-id="966c1-121">If that is the only relationship for the Indirect Reseller, then the Indirect Reseller will be deleted.</span></span>

1. <span data-ttu-id="966c1-122">Nepřímí poskytovatelé CSP mohou odstranit CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="966c1-122">CSP Indirect Providers can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="966c1-123">a.</span><span class="sxs-lookup"><span data-stu-id="966c1-123">a.</span></span> <span data-ttu-id="966c1-124">Jedná se o funkci pouze sandboxu, která umožňuje nepřímým poskytovatelům sandboxu odstranit nepřímé prodejce sandboxu.</span><span class="sxs-lookup"><span data-stu-id="966c1-124">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="966c1-125">Předpoklady pro odstranění nepřímého prodejce sandboxu:</span><span class="sxs-lookup"><span data-stu-id="966c1-125">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="966c1-126">Pozastavíte předplatná pro každého zákazníka nepřímého prodejce sandboxu.</span><span class="sxs-lookup"><span data-stu-id="966c1-126">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="966c1-127">Odstraňte všechny zákazníky nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="966c1-127">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="966c1-128">Povolený limit pěti nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu.</span><span class="sxs-lookup"><span data-stu-id="966c1-128">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="966c1-129">Po odstranění nepřímého prodejce sandboxu se kvóta resetuje.</span><span class="sxs-lookup"><span data-stu-id="966c1-129">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="966c1-130">Požadavky</span><span class="sxs-lookup"><span data-stu-id="966c1-130">Pre-requisites</span></span>

- <span data-ttu-id="966c1-131">Povolený limit pěti nepřímých prodejců sandboxu na nepřímého poskytovatele sandboxu.</span><span class="sxs-lookup"><span data-stu-id="966c1-131">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="966c1-132">Stejné ID MPN můžete použít k vytvoření několika účtů sandboxu nepřímého prodejce, pokud je země MPN ID země a země sandboxu nepřímého prodejce stejné.</span><span class="sxs-lookup"><span data-stu-id="966c1-132">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="966c1-133">Pokud máte k dispozici testovací ID MPN, můžete ho použít nebo můžete získat seznam ID MPN prostřednictvím našeho [Yammer kanálu]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span><span class="sxs-lookup"><span data-stu-id="966c1-133">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="966c1-134">Pokud nemáte přístup k Yammer, Yammer požádat o přístup.</span><span class="sxs-lookup"><span data-stu-id="966c1-134">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="966c1-135">Na nepřímého poskytovatele sandboxu je povolených jenom 75 zákazníků.</span><span class="sxs-lookup"><span data-stu-id="966c1-135">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="966c1-136">Vytvoření CSP Indirect Reseller sandboxu</span><span class="sxs-lookup"><span data-stu-id="966c1-136">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="966c1-137">Přihlaste se Partnerské centrum účtu sandboxu úrovně 2.</span><span class="sxs-lookup"><span data-stu-id="966c1-137">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="966c1-138">V levé nabídce přejděte na Indirect Resellers (Nepřímí prodejci).</span><span class="sxs-lookup"><span data-stu-id="966c1-138">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="966c1-139">Vyberte tlačítko **Add Reseller Sandbox (Přidat sandbox prodejce).**</span><span class="sxs-lookup"><span data-stu-id="966c1-139">Select the **Add Reseller Sandbox** button.</span></span> 

4. <span data-ttu-id="966c1-140">Vyplňte formulář pro registraci účtu.</span><span class="sxs-lookup"><span data-stu-id="966c1-140">Fill the account enrollment form.</span></span> <span data-ttu-id="966c1-141">Je to samozřejmé, ale nezapomeňte, že vytváříte účet sandboxu pro nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="966c1-141">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="966c1-142">Tento účet se nebude prověřovat a aktivuje se ihned po dokončení registrace účtu.</span><span class="sxs-lookup"><span data-stu-id="966c1-142">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="966c1-143">Po vytvoření účtu získáte na portálu přihlašovací údaje globálního správce pro účet sandboxu nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="966c1-143">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="966c1-144">Nezapomeňte ho uložit okamžitě, jinak se nebudete moct přihlásit jako sandbox nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="966c1-144">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="966c1-145">Odhlásit se a znovu se přihlásit Partnerské centrum pomocí nových přihlašovacích údajů pro Sandbox nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="966c1-145">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="966c1-146">Prozkoumejte možnosti, které můžete dělat jako nepřímý prodejce.</span><span class="sxs-lookup"><span data-stu-id="966c1-146">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="966c1-147">Tady jsou některé věci:</span><span class="sxs-lookup"><span data-stu-id="966c1-147">Some things are:</span></span>  

    - <span data-ttu-id="966c1-148">Správa profilů</span><span class="sxs-lookup"><span data-stu-id="966c1-148">Manage profiles</span></span>  

    - <span data-ttu-id="966c1-149">Správa uživatelů a skupin</span><span class="sxs-lookup"><span data-stu-id="966c1-149">Manage users and roles</span></span> 

    - <span data-ttu-id="966c1-150">Správa nepřímých poskytovatelů</span><span class="sxs-lookup"><span data-stu-id="966c1-150">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="966c1-151">Správa zákazníků csp sandboxu</span><span class="sxs-lookup"><span data-stu-id="966c1-151">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="966c1-152">Správa relací</span><span class="sxs-lookup"><span data-stu-id="966c1-152">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="966c1-153">Nepřímý poskytovatel sandboxu – Odstranění nepřímého prodejce sandboxu pomocí Partnerské centrum rozhraní</span><span class="sxs-lookup"><span data-stu-id="966c1-153">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="966c1-154">Jedná se o funkci sandboxu, která umožňuje nepřímým poskytovatelům sandboxu odstranit existující účet nepřímého prodejce sandboxu přes Partnerské centrum Portal.</span><span class="sxs-lookup"><span data-stu-id="966c1-154">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="966c1-155">Předpoklady pro odstranění nepřímého prodejce sandboxu:</span><span class="sxs-lookup"><span data-stu-id="966c1-155">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="966c1-156">Existující účet CSP Indirect Reseller Sandbox přidružený k vašemu vlastnímu účtu CSP Indirect Provider Tier-2 Sandbox.</span><span class="sxs-lookup"><span data-stu-id="966c1-156">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="966c1-157">Odstranění CSP Indirect Reseller sandboxu</span><span class="sxs-lookup"><span data-stu-id="966c1-157">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="966c1-158">Přihlaste se Partnerské centrum účtu sandboxu úrovně 2.</span><span class="sxs-lookup"><span data-stu-id="966c1-158">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="966c1-159">V levé nabídce přejděte na Indirect Resellers (Nepřímí prodejci).</span><span class="sxs-lookup"><span data-stu-id="966c1-159">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="966c1-160">Vyberte odkaz **Delete Reseller Sandbox (Odstranit sandbox prodejce)** vedle účtu sandboxu nepřímého prodejce, který chcete odstranit.</span><span class="sxs-lookup"><span data-stu-id="966c1-160">Select the **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="966c1-161">Účet sandboxu nepřímého prodejce se trvale odstraní a není možné ho obnovit.</span><span class="sxs-lookup"><span data-stu-id="966c1-161">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="966c1-162">Referenční informace k rozhraní API</span><span class="sxs-lookup"><span data-stu-id="966c1-162">API references</span></span>

- <span data-ttu-id="966c1-163">Vytvoření nepřímého prodejce</span><span class="sxs-lookup"><span data-stu-id="966c1-163">Create Indirect Reseller</span></span> 
- <span data-ttu-id="966c1-164">Odstranění nepřímého prodejce</span><span class="sxs-lookup"><span data-stu-id="966c1-164">Delete Indirect Reseller</span></span> 

 

 