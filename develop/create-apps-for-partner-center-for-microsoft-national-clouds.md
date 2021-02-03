---
title: Registrace podrobností o aplikaci pro partnerského centra pro národní Cloud Microsoftu
description: Přečtěte si, jak a proč můžou vývojáři aplikací pro partnerské Centrum pro národní Cloud od Microsoftu zaregistrovat podrobnosti o své aplikaci pomocí služby Azure AD prostřednictvím Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767132"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="2ac0d-103">Zaregistrujte podrobnosti o aplikaci pro partnerského centra pro národní Cloud Microsoftu prostřednictvím Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2ac0d-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="2ac0d-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="2ac0d-104">**Applies to:**</span></span>

- <span data-ttu-id="2ac0d-105">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="2ac0d-105">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2ac0d-106">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2ac0d-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2ac0d-107">Vývojáři musí zaregistrovat podrobnosti o své aplikaci pomocí služby Azure AD prostřednictvím Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-107">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="2ac0d-108">To pomáhá zajistit, že se k partnerům a zákaznickým datům budou moci připojit pouze konkrétní aplikace.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-108">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="2ac0d-109">Pro partnerského centra Microsoft Cloud pro státní správu USA je aktuálně nutné spravovat aplikace prostřednictvím PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-109">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="2ac0d-110">Další informace najdete v [dokumentaci Azure PowerShell reference](/powershell/module/Azuread/#applications).</span><span class="sxs-lookup"><span data-stu-id="2ac0d-110">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="2ac0d-111">Pamatujte na následující další požadavky, když vytvoříte aplikaci pro partnerského centra pro Microsoft Cloud Německo nebo partnerské Centrum pro Microsoft Cloud pro státní správu USA.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-111">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="2ac0d-112">Webové aplikace</span><span class="sxs-lookup"><span data-stu-id="2ac0d-112">Web apps</span></span>

<span data-ttu-id="2ac0d-113">Pro webové aplikace použijte následující postupy k registraci ID aplikace.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-113">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="2ac0d-114">Vytvořit nebo aktualizovat webovou aplikaci</span><span class="sxs-lookup"><span data-stu-id="2ac0d-114">Create or update web app</span></span>

1. <span data-ttu-id="2ac0d-115">Pro registraci aplikace přejděte na stránku [Azure Portal-registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) .</span><span class="sxs-lookup"><span data-stu-id="2ac0d-115">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="2ac0d-116">Přihlaste se k webu Azure Portal pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-116">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="2ac0d-117">Vyberte **Nová registrace**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-117">Select **New registration**.</span></span> <span data-ttu-id="2ac0d-118">Další informace najdete v tématu [rychlý Start: registrace aplikace s platformou Microsoft Identity](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="2ac0d-118">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="2ac0d-119">Konfigurace přístupových oprávnění k rozhraní API pro webovou aplikaci</span><span class="sxs-lookup"><span data-stu-id="2ac0d-119">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="2ac0d-120">Zvolte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-120">Choose your app.</span></span> <span data-ttu-id="2ac0d-121">Přejít na **Nastavení** webové aplikace</span><span class="sxs-lookup"><span data-stu-id="2ac0d-121">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="2ac0d-122">V části **přístup k rozhraní API** vyberte **požadovaná oprávnění** .</span><span class="sxs-lookup"><span data-stu-id="2ac0d-122">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="2ac0d-123">Oprávnění pro Windows Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="2ac0d-123">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="2ac0d-124">Vyberte možnost **Windows Azure Active Directory oprávnění**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-124">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="2ac0d-125">V **oprávnění aplikace** vyberte číst data adresáře.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-125">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="2ac0d-126">Uložte oprávnění.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-126">Save the permissions.</span></span>

4. <span data-ttu-id="2ac0d-127">Poznamenejte si ID aplikace v části **vlastnosti** vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-127">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="2ac0d-128">Přidání tajného klíče do aplikace</span><span class="sxs-lookup"><span data-stu-id="2ac0d-128">Add a secret key to your app</span></span>

1. <span data-ttu-id="2ac0d-129">Přejít do části **klíče** ve vaší webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-129">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="2ac0d-130">Zadejte popis klíče a vyberte dobu trvání 1 nebo 2 roky, jak potřebujete.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-130">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="2ac0d-131">Uložte a zkopírujte hodnotu tajného klíče.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-131">Save and copy the secret key value.</span></span> <span data-ttu-id="2ac0d-132">**Tato hodnota se po opuštění této stránky znovu nezobrazí.**</span><span class="sxs-lookup"><span data-stu-id="2ac0d-132">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="2ac0d-133">Z konfigurace webové aplikace byste měli mít následující podrobnosti:</span><span class="sxs-lookup"><span data-stu-id="2ac0d-133">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="2ac0d-134">ID aplikace</span><span class="sxs-lookup"><span data-stu-id="2ac0d-134">Application ID</span></span>
- <span data-ttu-id="2ac0d-135">Tajný kód aplikace</span><span class="sxs-lookup"><span data-stu-id="2ac0d-135">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="2ac0d-136">Registrace webové aplikace v partnerském centru</span><span class="sxs-lookup"><span data-stu-id="2ac0d-136">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="2ac0d-137">Přihlaste se k [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="2ac0d-137">Log in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="2ac0d-138">Zvolte **řídicí panel**, vyberte **Nastavení účtu** a pak zvolte **Správa aplikací**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-138">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="2ac0d-139">V části **Webová aplikace** vyberte **zaregistrovat existující aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-139">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="2ac0d-140">Vyberte webovou aplikaci, kterou jste vytvořili v Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-140">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="2ac0d-141">Vyberte možnost **zaregistrovat aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-141">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="2ac0d-142">Nativní aplikace</span><span class="sxs-lookup"><span data-stu-id="2ac0d-142">Native apps</span></span>

<span data-ttu-id="2ac0d-143">Nativní aplikace nemusí být zaregistrované v partnerském centru.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-143">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="2ac0d-144">Tyto aplikace je ale potřeba nakonfigurovat tak, aby poskytovaly přístup k rozhraním API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-144">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="2ac0d-145">Před vytvořením nativní aplikace v Azure Portal se přihlaste do partnerského centra pomocí pověření uživatele správce z partnerského tenanta.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-145">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="2ac0d-146">Tím se vytvoří nastavení v tenantovi, aby se povolila oprávnění aplikace.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-146">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="2ac0d-147">Vytvořit nativní aplikaci</span><span class="sxs-lookup"><span data-stu-id="2ac0d-147">Create native app</span></span>

1. <span data-ttu-id="2ac0d-148">Pro registraci aplikace přejděte na stránku [Azure Portal-registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) .</span><span class="sxs-lookup"><span data-stu-id="2ac0d-148">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="2ac0d-149">Přihlaste se k webu Azure Portal pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-149">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="2ac0d-150">Vyberte **Nová registrace**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-150">Select **New registration**.</span></span> <span data-ttu-id="2ac0d-151">Další informace najdete v tématu [rychlý Start: registrace aplikace s platformou Microsoft Identity](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="2ac0d-151">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="2ac0d-152">Konfigurace přístupových oprávnění k rozhraní API pro nativní aplikaci</span><span class="sxs-lookup"><span data-stu-id="2ac0d-152">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="2ac0d-153">Zvolte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-153">Choose your app.</span></span> <span data-ttu-id="2ac0d-154">Přejít na **Nastavení**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-154">Go to **Settings**.</span></span>

2. <span data-ttu-id="2ac0d-155">V možnosti přístup přes rozhraní API vyberte **požadovaná oprávnění**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-155">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="2ac0d-156">Vyberte možnost **Windows Azure Active Directory oprávnění**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-156">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="2ac0d-157">V **delegovaných oprávněních** vyberte Tato oprávnění:</span><span class="sxs-lookup"><span data-stu-id="2ac0d-157">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="2ac0d-158">**Přihlášení a čtení profilu uživatele**</span><span class="sxs-lookup"><span data-stu-id="2ac0d-158">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="2ac0d-159">**Čtení dat z adresáře**</span><span class="sxs-lookup"><span data-stu-id="2ac0d-159">**Read directory data**</span></span>
    - <span data-ttu-id="2ac0d-160">**Přístup k adresáři jako přihlášený uživatel**</span><span class="sxs-lookup"><span data-stu-id="2ac0d-160">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="2ac0d-161">**Číst všechny skupiny**</span><span class="sxs-lookup"><span data-stu-id="2ac0d-161">**Read all groups**</span></span>

4. <span data-ttu-id="2ac0d-162">Uložte oprávnění.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-162">Save the permissions.</span></span>

5. <span data-ttu-id="2ac0d-163">V **požadovaném oprávnění** vyberte **Přidat** .</span><span class="sxs-lookup"><span data-stu-id="2ac0d-163">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="2ac0d-164">Zvolte **Vyberte rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-164">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="2ac0d-165">Do vyhledávacího pole zadejte **Microsoft Partner Center** a vyberte ho ze seznamu výsledků.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-165">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="2ac0d-166">Zvolte **Vybrat**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-166">Choose **Select**.</span></span>

7. <span data-ttu-id="2ac0d-167">Zvolte **možnost vybrat oprávnění**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-167">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="2ac0d-168">Vyberte **OOP Access partner Center**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-168">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="2ac0d-169">Zvolte **Vybrat**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-169">Choose **Select**.</span></span>

8. <span data-ttu-id="2ac0d-170">Vyberte **Hotovo**.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-170">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="2ac0d-171">Poznamenejte si ID aplikace ve vlastnostech vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-171">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="2ac0d-172">V partnerském centru nemusíte registrovat nativní aplikace, ale je potřeba, aby byla v nativní aplikaci souhlas správce.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-172">You do not need to register native apps in Partner Center, however the native app must be admin consented .</span></span> <span data-ttu-id="2ac0d-173">Poznamenejte si ID aplikace vaší nativní aplikace.</span><span class="sxs-lookup"><span data-stu-id="2ac0d-173">Note the application ID of your native app.</span></span>
