---
title: Nastavení přístupu k rozhraní API v Partnerském centru
description: Nastavte účty pro vývoj na základě sady SDK partnerského centra a testování v izolovaném prostoru integrace.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/28/2020
ms.locfileid: "97766890"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="016f7-103">Nastavení přístupu k rozhraní API v Partnerském centru</span><span class="sxs-lookup"><span data-stu-id="016f7-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="016f7-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="016f7-104">**Applies to:**</span></span>

- <span data-ttu-id="016f7-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="016f7-105">Partner Center</span></span>
- <span data-ttu-id="016f7-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="016f7-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="016f7-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="016f7-107">Partner Center for Microsoft Cloud for US Government</span></span>
- <span data-ttu-id="016f7-108">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="016f7-108">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="016f7-109">Tento článek popisuje účty, které potřebujete pro vývoj v rámci sady SDK pro partnerský server.</span><span class="sxs-lookup"><span data-stu-id="016f7-109">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="016f7-110">Tento článek také vysvětluje, jak vytvořit [účet izolovaného prostoru (sandbox) integrace](#integration-sandbox-account) a testovat v izolovaném prostoru (sandbox) Integration.</span><span class="sxs-lookup"><span data-stu-id="016f7-110">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="016f7-111">K získání přístupu k rozhraním API musí být váš tenant tenant CSP a Vy musíte být buď nepřímým poskytovatelem, nebo přímým partnerem pro fakturaci.</span><span class="sxs-lookup"><span data-stu-id="016f7-111">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="016f7-112">Definice účtu</span><span class="sxs-lookup"><span data-stu-id="016f7-112">Account definitions</span></span>

<span data-ttu-id="016f7-113">Pro usnadnění integrace a testování integrace rozhraní API podporuje partnerské Centrum dva druhy účtů:</span><span class="sxs-lookup"><span data-stu-id="016f7-113">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="016f7-114">Primární Partnerský účet</span><span class="sxs-lookup"><span data-stu-id="016f7-114">Primary Partner account</span></span>

<span data-ttu-id="016f7-115">Tento účet vám umožní vytvářet reálné objednávky pro skutečné zákazníky.</span><span class="sxs-lookup"><span data-stu-id="016f7-115">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="016f7-116">Pokud provedete nějaké změny nebo transakce, když jste přihlášeni k primárnímu účtu, pomocí sady SDK partnerského centra nebo uživatelského rozhraní partnerského řídicího panelu se budou považovat za oficiální objednávky pro skutečné zákazníky.</span><span class="sxs-lookup"><span data-stu-id="016f7-116">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="016f7-117">Ve vaší faktuře se projeví i vaše společnost za jejich placení.</span><span class="sxs-lookup"><span data-stu-id="016f7-117">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="016f7-118">Účet sandboxu pro integraci</span><span class="sxs-lookup"><span data-stu-id="016f7-118">Integration sandbox account</span></span>

<span data-ttu-id="016f7-119">Tento účet je určen pro testování vašeho kódu a jeho integraci s rozhraními API partnerského centra předtím, než bude široce nasazen.</span><span class="sxs-lookup"><span data-stu-id="016f7-119">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="016f7-120">Změny a transakce, které uděláte po přihlášení k účtu izolovaného prostoru (sandbox), se zobrazí ve vaší faktuře, ale nebudete muset platit částku faktury.</span><span class="sxs-lookup"><span data-stu-id="016f7-120">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="016f7-121">PDF faktury bude mít zřeknutí se jako Neplaťte.</span><span class="sxs-lookup"><span data-stu-id="016f7-121">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="016f7-122">JEDNÁ SE O FAKTURU IZOLOVANÉHO PROSTORU (SANDBOX) A NEVYŽADUJE SE ŽÁDNÁ AKCE. "</span><span class="sxs-lookup"><span data-stu-id="016f7-122">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="016f7-123">Účet izolovaného prostoru (sandbox) a primární účet se chovají nezávisle a nesdílí účty správců, uživatelské účty, zákazníky, objednávky, odběry nebo jiná data.</span><span class="sxs-lookup"><span data-stu-id="016f7-123">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="016f7-124">Izolovaný prostor integrace podporuje transakce s omezeným počtem zákazníků, objednávek, předplatných, licencí atd.</span><span class="sxs-lookup"><span data-stu-id="016f7-124">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="016f7-125">Pomocí zásad jsou účty izolovaného prostoru pro integraci jenom pro účely testování Integration.</span><span class="sxs-lookup"><span data-stu-id="016f7-125">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="016f7-126">Ve výchozím nastavení žádný účet sandboxu pro integraci neexistuje.</span><span class="sxs-lookup"><span data-stu-id="016f7-126">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="016f7-127">Pokud plánujete použít sadu SDK partnerského centra, musíte si ji sami vytvořit sami.</span><span class="sxs-lookup"><span data-stu-id="016f7-127">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="016f7-128">Nastavení účtů</span><span class="sxs-lookup"><span data-stu-id="016f7-128">Set up your accounts</span></span>

<span data-ttu-id="016f7-129">Tato část popisuje, jak nastavit primární Partnerský účet a účet izolovaného prostoru pro integraci pro sadu SDK pro partnerský server.</span><span class="sxs-lookup"><span data-stu-id="016f7-129">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="016f7-130">Vytvoření izolovaného prostoru integrace</span><span class="sxs-lookup"><span data-stu-id="016f7-130">Create an integration sandbox</span></span>

1. <span data-ttu-id="016f7-131">Přihlaste se k řídicímu panelu partnera pomocí účtu globálního správce (váš primární Partnerský účet).</span><span class="sxs-lookup"><span data-stu-id="016f7-131">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="016f7-132">V nabídce **Nastavení** (ikona ozubeného kolečka) vyberte **nastavení partnera**.</span><span class="sxs-lookup"><span data-stu-id="016f7-132">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="016f7-133">Vyberte kartu **izolovaný prostor integrace** .</span><span class="sxs-lookup"><span data-stu-id="016f7-133">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="016f7-134">Pokud nevidíte možnost izolovaného prostoru pro integraci, možná nemáte účet globálního správce.</span><span class="sxs-lookup"><span data-stu-id="016f7-134">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="016f7-135">Můžete použít také účet izolovaného prostoru pro integraci a izolovaný prostor integrace již byl nastaven.</span><span class="sxs-lookup"><span data-stu-id="016f7-135">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="016f7-136">Zadejte kontaktní informace pro účet správce izolovaného prostoru pro integraci.</span><span class="sxs-lookup"><span data-stu-id="016f7-136">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="016f7-137">Pak zvolte **vytvořit účet**.</span><span class="sxs-lookup"><span data-stu-id="016f7-137">Then, choose **Create account**.</span></span> <span data-ttu-id="016f7-138">Počkejte několik minut, než se zobrazí zpráva s potvrzením, že byl účet vytvořen.</span><span class="sxs-lookup"><span data-stu-id="016f7-138">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="016f7-139">Až se zobrazí zpráva s potvrzením, odhlaste se z řídicího panelu partnerského serveru.</span><span class="sxs-lookup"><span data-stu-id="016f7-139">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="016f7-140">Znovu se přihlaste pomocí nového účtu správce izolovaného prostoru pro integraci.</span><span class="sxs-lookup"><span data-stu-id="016f7-140">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="016f7-141">Nezapomeňte použít formát **username@domain** vašich přihlašovacích údajů společně s heslem, které jste zadali.</span><span class="sxs-lookup"><span data-stu-id="016f7-141">Be sure to use the format **username@domain** for your credentials along with the password that you just specified.</span></span>

7. <span data-ttu-id="016f7-142">Chcete-li dokončit nastavení účtu izolovaného prostoru (sandbox), vyberte možnost **nastavit účet** nad **aktuálními úkoly** .</span><span class="sxs-lookup"><span data-stu-id="016f7-142">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="016f7-143">Povolit přístup přes rozhraní API</span><span class="sxs-lookup"><span data-stu-id="016f7-143">Enable API access</span></span>

<span data-ttu-id="016f7-144">Po nastavení účtu musíte povolit přístup k rozhraní API, a teprve pak budete moct používat sadu SDK Partnerského centra se sandboxem pro integraci.</span><span class="sxs-lookup"><span data-stu-id="016f7-144">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="016f7-145">Přístup k rozhraní API musíte povolit zvlášť pro svůj primární partnerský účet a účet sandboxu pro integraci.</span><span class="sxs-lookup"><span data-stu-id="016f7-145">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="016f7-146">Přihlaste se k řídicímu panelu partnerského serveru pomocí účtu globálního správce.</span><span class="sxs-lookup"><span data-stu-id="016f7-146">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="016f7-147">V nabídce **Nastavení** (ikona ozubeného kolečka) vyberte **nastavení partnera**.</span><span class="sxs-lookup"><span data-stu-id="016f7-147">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="016f7-148">Na stránce **Nastavení účtu** klikněte na možnost **Správa aplikací**.</span><span class="sxs-lookup"><span data-stu-id="016f7-148">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="016f7-149">Pokud ještě nemáte existující aplikaci, přidejte novou webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="016f7-149">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="016f7-150">Pokud máte existující webovou aplikaci, klikněte na tlačítko **Přidat klíč** .</span><span class="sxs-lookup"><span data-stu-id="016f7-150">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="016f7-151">Zkopírujte informace o registraci aplikace, zejména **klíč** , pokud vytváříte webovou aplikaci, a uložte ji na bezpečném místě.</span><span class="sxs-lookup"><span data-stu-id="016f7-151">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="016f7-152">Odhlaste se z řídicího panelu partnerů.</span><span class="sxs-lookup"><span data-stu-id="016f7-152">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="016f7-153">Přihlaste se zpátky pomocí účtu izolovaného prostoru (sandbox) Integration.</span><span class="sxs-lookup"><span data-stu-id="016f7-153">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="016f7-154">Zopakováním kroků 2-5 povolte přístup k rozhraní API v izolovaném prostoru integrace.</span><span class="sxs-lookup"><span data-stu-id="016f7-154">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="016f7-155">Zápis a testování kódu</span><span class="sxs-lookup"><span data-stu-id="016f7-155">Write and test code</span></span>

<span data-ttu-id="016f7-156">Můžete napsat kód a testovat kód v izolovaném prostoru integrace.</span><span class="sxs-lookup"><span data-stu-id="016f7-156">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="016f7-157">K [nastavení ověřování partnerského centra](partner-center-authentication.md) pomocí služby Azure AD budete potřebovat následující informace.</span><span class="sxs-lookup"><span data-stu-id="016f7-157">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="016f7-158">Název položky</span><span class="sxs-lookup"><span data-stu-id="016f7-158">Item name</span></span> | <span data-ttu-id="016f7-159">Umístění položky</span><span class="sxs-lookup"><span data-stu-id="016f7-159">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="016f7-160">ID aplikace/ID klienta</span><span class="sxs-lookup"><span data-stu-id="016f7-160">App ID / Client ID</span></span> | <span data-ttu-id="016f7-161">V nabídce **Nastavení** (ikona ozubeného kolečka) vyberte **nastavení partnera**.</span><span class="sxs-lookup"><span data-stu-id="016f7-161">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="016f7-162">Na stránce **Nastavení účtu** vyberte **Správa aplikací**.</span><span class="sxs-lookup"><span data-stu-id="016f7-162">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="016f7-163">ID aplikace/ID klienta je uvedené jako ID aplikace **registrované aplikace**.</span><span class="sxs-lookup"><span data-stu-id="016f7-163">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="016f7-164">Klíč</span><span class="sxs-lookup"><span data-stu-id="016f7-164">Key</span></span> | <span data-ttu-id="016f7-165">Pokud jste vytvořili webovou aplikaci v části [Povolení přístupu k rozhraní API](#enable-api-access), je to klíč, který jste uložili v kroku 5.</span><span class="sxs-lookup"><span data-stu-id="016f7-165">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="016f7-166">Doména</span><span class="sxs-lookup"><span data-stu-id="016f7-166">Domain</span></span> | <span data-ttu-id="016f7-167">Doména pro izolovaný prostor integrace</span><span class="sxs-lookup"><span data-stu-id="016f7-167">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="016f7-168">Spustit testovaný kód</span><span class="sxs-lookup"><span data-stu-id="016f7-168">Run tested code</span></span>

<span data-ttu-id="016f7-169">Pokud chcete používat vaše řešení se skutečnými Zákaznickými daty, musíte změnit přihlašovací údaje izolovaného prostoru (sandbox) na svůj primární účet partnerského účtu.</span><span class="sxs-lookup"><span data-stu-id="016f7-169">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="016f7-170">Až budete připraveni použít testovaný kód v primárním partnerském účtu, musíte získat token zabezpečení Azure AD.</span><span class="sxs-lookup"><span data-stu-id="016f7-170">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="016f7-171">Tento token zabezpečení je založený na vaší aplikaci, klíči a doméně partnerského centra (namísto vaší aplikace, klíče a domény Integration sandbox).</span><span class="sxs-lookup"><span data-stu-id="016f7-171">This security token is based on your Partner Center app, key and domain (instead of your integration sandbox app, key and domain).</span></span>

1. <span data-ttu-id="016f7-172">Postupujte podle kroků v části [ověřování partnerského centra](partner-center-authentication.md) a získejte token zabezpečení služby Azure AD pomocí vašich primárních přihlašovacích údajů partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="016f7-172">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="016f7-173">(Dřív jste použili tento postup k získání tokenu zabezpečení Azure AD pro izolovaný prostor integrace.)</span><span class="sxs-lookup"><span data-stu-id="016f7-173">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="016f7-174">Nahraďte token zabezpečení Integration v kódu novým tokenem zabezpečení pro váš primární Partnerský účet.</span><span class="sxs-lookup"><span data-stu-id="016f7-174">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
