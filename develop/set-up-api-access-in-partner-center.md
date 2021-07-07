---
title: Nastavení přístupu k rozhraní API v Partnerském centru
description: Nastavte účty pro vývoj proti SDK pro Partnerské centrum a testování v sandboxu integrace.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2c564baa9b626ff6ce21f9bcc517902d7cf99244
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547423"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="632c7-103">Nastavení přístupu k rozhraní API v Partnerském centru</span><span class="sxs-lookup"><span data-stu-id="632c7-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="632c7-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government | Partnerské centrum pro Microsoft Cloud (Německo)</span><span class="sxs-lookup"><span data-stu-id="632c7-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="632c7-105">Tento článek popisuje účty, které potřebujete k vývoji pro SDK pro Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="632c7-105">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="632c7-106">Tento článek také vysvětluje, jak vytvořit účet [sandboxu pro integraci](#integration-sandbox-account) a otestovat ho v sandboxu pro integraci.</span><span class="sxs-lookup"><span data-stu-id="632c7-106">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="632c7-107">Abyste získali přístup k rozhraním API, váš tenant musí být tenant CSP a musíte být nepřímý poskytovatel nebo partner s přímým vyúčtováním.</span><span class="sxs-lookup"><span data-stu-id="632c7-107">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="632c7-108">Definice účtů</span><span class="sxs-lookup"><span data-stu-id="632c7-108">Account definitions</span></span>

<span data-ttu-id="632c7-109">Pro lepší integraci a testování integrace rozhraní API Partnerské centrum podporuje dva druhy účtů:</span><span class="sxs-lookup"><span data-stu-id="632c7-109">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="632c7-110">Primární partnerský účet</span><span class="sxs-lookup"><span data-stu-id="632c7-110">Primary Partner account</span></span>

<span data-ttu-id="632c7-111">V tomto účtu vytváříte skutečné objednávky pro skutečné zákazníky.</span><span class="sxs-lookup"><span data-stu-id="632c7-111">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="632c7-112">Pokud při přihlášení k primárnímu účtu nebo pomocí uživatelského rozhraní řídicího panelu partnera nebo řídicího panelu SDK pro Partnerské centrum jakékoli změny nebo transakce, budou se považovat za oficiální objednávky skutečných zákazníků.</span><span class="sxs-lookup"><span data-stu-id="632c7-112">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="632c7-113">Projeví se na vaší faktuře a vaše společnost za ně zodpovídá.</span><span class="sxs-lookup"><span data-stu-id="632c7-113">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="632c7-114">Účet sandboxu pro integraci</span><span class="sxs-lookup"><span data-stu-id="632c7-114">Integration sandbox account</span></span>

<span data-ttu-id="632c7-115">Tento účet je pro testování kódu a jeho integraci s rozhraními API Partnerské centrum před jeho širším nasazením.</span><span class="sxs-lookup"><span data-stu-id="632c7-115">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="632c7-116">Změny a transakce, které jste provést při přihlášení k účtu sandboxu pro integraci, se zobrazí na faktuře, ale částku faktury platit nemusíte.</span><span class="sxs-lookup"><span data-stu-id="632c7-116">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="632c7-117">Soubor PDF faktury bude mít právní omezení s textem NEZAPLATIT.</span><span class="sxs-lookup"><span data-stu-id="632c7-117">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="632c7-118">JEDNÁ SE O FAKTURU ZA SANDBOX A NEVYŽADUJE SE ŽÁDNÁ AKCE.</span><span class="sxs-lookup"><span data-stu-id="632c7-118">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="632c7-119">Účet sandboxu pro integraci a primární účet se chová nezávisle a nesdílejí účty správců, uživatelské účty, zákazníky, objednávky, předplatná ani jiná data.</span><span class="sxs-lookup"><span data-stu-id="632c7-119">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="632c7-120">Integrační sandbox podporuje transakce s omezeným počtem zákazníků, objednávek, předplatných, licencí atd.</span><span class="sxs-lookup"><span data-stu-id="632c7-120">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="632c7-121">Podle zásad jsou účty sandboxu integrace jenom pro účely testování integrace.</span><span class="sxs-lookup"><span data-stu-id="632c7-121">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="632c7-122">Ve výchozím nastavení žádný účet sandboxu pro integraci neexistuje.</span><span class="sxs-lookup"><span data-stu-id="632c7-122">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="632c7-123">Pokud plánujete používat tuto aplikaci, musíte si ji vytvořit SDK pro Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="632c7-123">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="632c7-124">Nastavení účtů</span><span class="sxs-lookup"><span data-stu-id="632c7-124">Set up your accounts</span></span>

<span data-ttu-id="632c7-125">Tato část popisuje, jak nastavit primární partnerský účet a účet sandboxu pro integraci pro SDK pro Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="632c7-125">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="632c7-126">Vytvoření sandboxu pro integraci</span><span class="sxs-lookup"><span data-stu-id="632c7-126">Create an integration sandbox</span></span>

1. <span data-ttu-id="632c7-127">Přihlaste se k řídicímu panelu pro partnery pomocí účtu globálního správce (primárního partnerského účtu).</span><span class="sxs-lookup"><span data-stu-id="632c7-127">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="632c7-128">V nabídce **Nastavení** (ikona ozubeného kola) zvolte **Nastavení partnera**.</span><span class="sxs-lookup"><span data-stu-id="632c7-128">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="632c7-129">Zvolte **kartu Sandbox integrace.**</span><span class="sxs-lookup"><span data-stu-id="632c7-129">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="632c7-130">Pokud možnost Sandbox integrace nevidíte, možná nemáte účet globálního správce.</span><span class="sxs-lookup"><span data-stu-id="632c7-130">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="632c7-131">Můžete také používat účet sandboxu pro integraci a integrační sandbox už je nastavený.</span><span class="sxs-lookup"><span data-stu-id="632c7-131">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="632c7-132">Zadejte kontaktní informace pro účet správce sandboxu pro integraci.</span><span class="sxs-lookup"><span data-stu-id="632c7-132">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="632c7-133">Pak zvolte **Vytvořit účet.**</span><span class="sxs-lookup"><span data-stu-id="632c7-133">Then, choose **Create account**.</span></span> <span data-ttu-id="632c7-134">Počkejte několik minut, než se zobrazí potvrzovací zpráva o vytvoření účtu.</span><span class="sxs-lookup"><span data-stu-id="632c7-134">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="632c7-135">Po zobrazení potvrzovací zprávy se odhlásit z řídicího panelu partnera.</span><span class="sxs-lookup"><span data-stu-id="632c7-135">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="632c7-136">Znovu se přihlaste pomocí nového účtu správce sandboxu pro integraci.</span><span class="sxs-lookup"><span data-stu-id="632c7-136">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="632c7-137">Nezapomeňte použít formát svých **username@domain** přihlašovacích údajů spolu s heslem, které jste zadali.</span><span class="sxs-lookup"><span data-stu-id="632c7-137">Be sure to use the format **username@domain** for your credentials along with the password that you specified.</span></span>

7. <span data-ttu-id="632c7-138">Zvolte **Nastavit účet nad aktuálními** úkoly **a** dokončete nastavení účtu sandboxu.</span><span class="sxs-lookup"><span data-stu-id="632c7-138">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="632c7-139">Povolení přístupu k rozhraní API</span><span class="sxs-lookup"><span data-stu-id="632c7-139">Enable API access</span></span>

<span data-ttu-id="632c7-140">Po nastavení účtu musíte povolit přístup k rozhraní API, a teprve pak budete moct používat sadu SDK Partnerského centra se sandboxem pro integraci.</span><span class="sxs-lookup"><span data-stu-id="632c7-140">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="632c7-141">Přístup k rozhraní API musíte povolit zvlášť pro svůj primární partnerský účet a účet sandboxu pro integraci.</span><span class="sxs-lookup"><span data-stu-id="632c7-141">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="632c7-142">Přihlaste se k řídicímu panelu pro partnery pomocí účtu globálního správce.</span><span class="sxs-lookup"><span data-stu-id="632c7-142">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="632c7-143">V nabídce **Nastavení** (ikona ozubeného kola) vyberte **Nastavení partnera**.</span><span class="sxs-lookup"><span data-stu-id="632c7-143">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="632c7-144">Na stránce **Nastavení účtu** zvolte **Správa aplikací.**</span><span class="sxs-lookup"><span data-stu-id="632c7-144">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="632c7-145">Pokud ještě nemáte existující aplikaci, přidejte novou webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="632c7-145">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="632c7-146">Pokud máte existující webovou aplikaci, zvolte **tlačítko Přidat** klíč.</span><span class="sxs-lookup"><span data-stu-id="632c7-146">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="632c7-147">Zkopírujte informace o registraci  aplikace, zejména klíč, pokud vytváříte webovou aplikaci, a uložte je na bezpečném místě.</span><span class="sxs-lookup"><span data-stu-id="632c7-147">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="632c7-148">Odhlásit se z řídicího panelu pro partnery.</span><span class="sxs-lookup"><span data-stu-id="632c7-148">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="632c7-149">Znovu se přihlaste pomocí účtu sandboxu pro integraci.</span><span class="sxs-lookup"><span data-stu-id="632c7-149">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="632c7-150">Opakováním kroků 2 až 5 povolte přístup k rozhraní API v sandboxu integrace.</span><span class="sxs-lookup"><span data-stu-id="632c7-150">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="632c7-151">Psaní a testování kódu</span><span class="sxs-lookup"><span data-stu-id="632c7-151">Write and test code</span></span>

<span data-ttu-id="632c7-152">V sandboxu pro integraci můžete psát kód a testovat kód.</span><span class="sxs-lookup"><span data-stu-id="632c7-152">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="632c7-153">K nastavení ověřování pomocí Azure AD [Partnerské centrum následující](partner-center-authentication.md) informace.</span><span class="sxs-lookup"><span data-stu-id="632c7-153">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="632c7-154">Název položky</span><span class="sxs-lookup"><span data-stu-id="632c7-154">Item name</span></span> | <span data-ttu-id="632c7-155">Umístění položky</span><span class="sxs-lookup"><span data-stu-id="632c7-155">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="632c7-156">ID aplikace / ID klienta</span><span class="sxs-lookup"><span data-stu-id="632c7-156">App ID / Client ID</span></span> | <span data-ttu-id="632c7-157">V nabídce **Nastavení** (ikona ozubeného kola) vyberte **Nastavení partnera**.</span><span class="sxs-lookup"><span data-stu-id="632c7-157">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="632c7-158">Na stránce **Nastavení účtu** vyberte **Správa aplikací.**</span><span class="sxs-lookup"><span data-stu-id="632c7-158">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="632c7-159">ID aplikace nebo ID klienta je uvedené jako **ID registrované aplikace.**</span><span class="sxs-lookup"><span data-stu-id="632c7-159">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="632c7-160">Klíč</span><span class="sxs-lookup"><span data-stu-id="632c7-160">Key</span></span> | <span data-ttu-id="632c7-161">Pokud jste vytvořili webovou aplikaci v části [Povolení přístupu k rozhraní API,](#enable-api-access)jedná se o klíč, který jste si uložili v kroku 5.</span><span class="sxs-lookup"><span data-stu-id="632c7-161">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="632c7-162">Doména</span><span class="sxs-lookup"><span data-stu-id="632c7-162">Domain</span></span> | <span data-ttu-id="632c7-163">Doména pro sandbox integrace.</span><span class="sxs-lookup"><span data-stu-id="632c7-163">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="632c7-164">Spuštění testovaného kódu</span><span class="sxs-lookup"><span data-stu-id="632c7-164">Run tested code</span></span>

<span data-ttu-id="632c7-165">Pokud chcete řešení používat s reálnými zákaznickými daty, musíte změnit přihlašovací údaje sandboxu integrace na přihlašovací údaje primárního partnerského účtu.</span><span class="sxs-lookup"><span data-stu-id="632c7-165">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="632c7-166">Až budete připraveni použít testovaný kód v primárním partnerském účtu, musíte získat token zabezpečení Azure AD.</span><span class="sxs-lookup"><span data-stu-id="632c7-166">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="632c7-167">Tento token zabezpečení je založený na vaší Partnerské centrum, klíči a doméně (místo vaší aplikace, klíče a domény sandboxu integrace).</span><span class="sxs-lookup"><span data-stu-id="632c7-167">This security token is based on your Partner Center app, key, and domain (instead of your integration sandbox app, key, and domain).</span></span>

1. <span data-ttu-id="632c7-168">Postupujte podle kroků v [Partnerské centrum ověřování](partner-center-authentication.md) a získejte token zabezpečení Azure AD pomocí primárních přihlašovacích Partnerské centrum účtu.</span><span class="sxs-lookup"><span data-stu-id="632c7-168">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="632c7-169">(Dříve jste pomocí těchto kroků získali token zabezpečení Azure AD pro sandbox integrace.)</span><span class="sxs-lookup"><span data-stu-id="632c7-169">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="632c7-170">Nahraďte token zabezpečení integrace v kódu novým tokenem zabezpečení pro primární partnerský účet.</span><span class="sxs-lookup"><span data-stu-id="632c7-170">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
