---
title: Registrace podrobností o aplikaci Partnerské centrum pro národní cloud Microsoftu
description: Zjistěte, jak a proč musí vývojáři aplikací pro Partnerské centrum pro národní cloud Microsoftu registrovat podrobnosti o své aplikaci ve službě Azure AD prostřednictvím Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d46a17bc26e9586e5e773bdf934653a571367f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973447"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="20e44-103">Registrace podrobností o aplikaci Partnerské centrum pro národní cloud Microsoftu prostřednictvím Azure Portal</span><span class="sxs-lookup"><span data-stu-id="20e44-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="20e44-104">**Platí pro:** Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="20e44-104">**Applies to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="20e44-105">Vývojáři musí podrobnosti o své aplikaci zaregistrovat v Azure AD prostřednictvím Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="20e44-105">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="20e44-106">To pomáhá zajistit, že se k datům partnerů a zákazníků budou moct připojit jenom zadané aplikace.</span><span class="sxs-lookup"><span data-stu-id="20e44-106">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="20e44-107">Pro Partnerské centrum pro Microsoft Cloud for US Government v současné době musíte spravovat aplikace prostřednictvím PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="20e44-107">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="20e44-108">Další informace najdete v referenční [Azure PowerShell dokumentaci.](/powershell/module/Azuread/#applications)</span><span class="sxs-lookup"><span data-stu-id="20e44-108">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="20e44-109">Při vytváření aplikace pro službu Microsoft Cloud Germany Partnerské centrum Microsoft Cloud Germany nebo pro Partnerské centrum pro Microsoft Cloud for US Government je třeba mít na paměti následující Microsoft Cloud for US Government.</span><span class="sxs-lookup"><span data-stu-id="20e44-109">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="20e44-110">Webové aplikace</span><span class="sxs-lookup"><span data-stu-id="20e44-110">Web apps</span></span>

<span data-ttu-id="20e44-111">Pro webové aplikace použijte následující postupy k registraci ID vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="20e44-111">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="20e44-112">Vytvoření nebo aktualizace webové aplikace</span><span class="sxs-lookup"><span data-stu-id="20e44-112">Create or update web app</span></span>

1. <span data-ttu-id="20e44-113">Přejděte na [stránku Azure Portal – Registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) a zaregistrujte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="20e44-113">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="20e44-114">Přihlaste se k webu Azure Portal pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.</span><span class="sxs-lookup"><span data-stu-id="20e44-114">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="20e44-115">Vyberte **New registration (Nová registrace).**</span><span class="sxs-lookup"><span data-stu-id="20e44-115">Select **New registration**.</span></span> <span data-ttu-id="20e44-116">Další informace najdete v tématu [Rychlý start: Registrace aplikace v Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="20e44-116">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="20e44-117">Konfigurace přístupových oprávnění rozhraní API pro webovou aplikaci</span><span class="sxs-lookup"><span data-stu-id="20e44-117">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="20e44-118">Zvolte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="20e44-118">Choose your app.</span></span> <span data-ttu-id="20e44-119">Přejděte **Nastavení** webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="20e44-119">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="20e44-120">V **části Přístup rozhraní API** zvolte **Požadovaná oprávnění.**</span><span class="sxs-lookup"><span data-stu-id="20e44-120">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="20e44-121">Další Windows Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="20e44-121">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="20e44-122">Zvolte **Windows Azure Active Directory oprávnění.**</span><span class="sxs-lookup"><span data-stu-id="20e44-122">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="20e44-123">V **části Oprávnění aplikací** vyberte Číst data adresáře.</span><span class="sxs-lookup"><span data-stu-id="20e44-123">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="20e44-124">Uložte oprávnění.</span><span class="sxs-lookup"><span data-stu-id="20e44-124">Save the permissions.</span></span>

4. <span data-ttu-id="20e44-125">Poznamenejte si ID aplikace v **části Vlastnosti** vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="20e44-125">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="20e44-126">Přidání tajného klíče do aplikace</span><span class="sxs-lookup"><span data-stu-id="20e44-126">Add a secret key to your app</span></span>

1. <span data-ttu-id="20e44-127">Přejděte do **části Klíče** vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="20e44-127">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="20e44-128">Zadejte popis klíče a vyberte dobu trvání 1 nebo 2 roky podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="20e44-128">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="20e44-129">Uložte a zkopírujte hodnotu tajného klíče.</span><span class="sxs-lookup"><span data-stu-id="20e44-129">Save and copy the secret key value.</span></span> <span data-ttu-id="20e44-130">**Po opouštění této stránky se tato hodnota znovu nezobrazí.**</span><span class="sxs-lookup"><span data-stu-id="20e44-130">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="20e44-131">Z konfigurace webové aplikace byste měli mít následující podrobnosti:</span><span class="sxs-lookup"><span data-stu-id="20e44-131">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="20e44-132">ID aplikace</span><span class="sxs-lookup"><span data-stu-id="20e44-132">Application ID</span></span>
- <span data-ttu-id="20e44-133">Tajný kód aplikace</span><span class="sxs-lookup"><span data-stu-id="20e44-133">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="20e44-134">Registrace webové aplikace v Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="20e44-134">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="20e44-135">Přihlaste se k webu [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="20e44-135">Sign in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="20e44-136">Zvolte **Řídicí** panel, zvolte **Účet Nastavení** a pak zvolte Správa **aplikací.**</span><span class="sxs-lookup"><span data-stu-id="20e44-136">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="20e44-137">V části **Webová aplikace** zvolte **Zaregistrovat existující aplikaci.**</span><span class="sxs-lookup"><span data-stu-id="20e44-137">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="20e44-138">Vyberte webovou aplikaci, kterou jste vytvořili v Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="20e44-138">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="20e44-139">Zvolte **zaregistrovat aplikaci.**</span><span class="sxs-lookup"><span data-stu-id="20e44-139">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="20e44-140">Nativní aplikace</span><span class="sxs-lookup"><span data-stu-id="20e44-140">Native apps</span></span>

<span data-ttu-id="20e44-141">Nativní aplikace nemusí být zaregistrované k Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="20e44-141">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="20e44-142">Tyto aplikace je ale potřeba nakonfigurovat tak, aby poskytovaly přístup Partnerské centrum rozhraním API.</span><span class="sxs-lookup"><span data-stu-id="20e44-142">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="20e44-143">Před vytvořením nativní aplikace v Azure Portal se přihlaste k Partnerské centrum pomocí přihlašovacích údajů správce z partnerského tenanta.</span><span class="sxs-lookup"><span data-stu-id="20e44-143">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="20e44-144">Tím se v tenantovi vytvoří nastavení pro povolení oprávnění aplikace.</span><span class="sxs-lookup"><span data-stu-id="20e44-144">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="20e44-145">Vytvoření nativní aplikace</span><span class="sxs-lookup"><span data-stu-id="20e44-145">Create native app</span></span>

1. <span data-ttu-id="20e44-146">Přejděte na [stránku Azure Portal – Registrace aplikací](https://go.microsoft.com/fwlink/?linkid=2083908) a zaregistrujte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="20e44-146">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="20e44-147">Přihlaste se k webu Azure Portal pomocí pracovního nebo školního účtu nebo osobního účtu Microsoft.</span><span class="sxs-lookup"><span data-stu-id="20e44-147">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="20e44-148">Vyberte **New registration (Nová registrace).**</span><span class="sxs-lookup"><span data-stu-id="20e44-148">Select **New registration**.</span></span> <span data-ttu-id="20e44-149">Další informace najdete v tématu [Rychlý start: Registrace aplikace v Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="20e44-149">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="20e44-150">Konfigurace přístupových oprávnění rozhraní API pro nativní aplikaci</span><span class="sxs-lookup"><span data-stu-id="20e44-150">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="20e44-151">Zvolte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="20e44-151">Choose your app.</span></span> <span data-ttu-id="20e44-152">Přejděte na **Nastavení**.</span><span class="sxs-lookup"><span data-stu-id="20e44-152">Go to **Settings**.</span></span>

2. <span data-ttu-id="20e44-153">V části Přístup pomocí rozhraní API zvolte **Požadovaná oprávnění.**</span><span class="sxs-lookup"><span data-stu-id="20e44-153">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="20e44-154">Zvolte **Windows Azure Active Directory oprávnění.**</span><span class="sxs-lookup"><span data-stu-id="20e44-154">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="20e44-155">V **části Delegovaná** oprávnění vyberte tato oprávnění:</span><span class="sxs-lookup"><span data-stu-id="20e44-155">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="20e44-156">**Přihlášení a čtení profilu uživatele**</span><span class="sxs-lookup"><span data-stu-id="20e44-156">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="20e44-157">**Čtení dat z adresáře**</span><span class="sxs-lookup"><span data-stu-id="20e44-157">**Read directory data**</span></span>
    - <span data-ttu-id="20e44-158">**Přístup k adresáři jako přihlášený uživatel**</span><span class="sxs-lookup"><span data-stu-id="20e44-158">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="20e44-159">**Čtení všech skupin**</span><span class="sxs-lookup"><span data-stu-id="20e44-159">**Read all groups**</span></span>

4. <span data-ttu-id="20e44-160">Uložte oprávnění.</span><span class="sxs-lookup"><span data-stu-id="20e44-160">Save the permissions.</span></span>

5. <span data-ttu-id="20e44-161">V **části Požadovaná** **oprávnění zvolte Přidat.**</span><span class="sxs-lookup"><span data-stu-id="20e44-161">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="20e44-162">Zvolte **Vyberte rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="20e44-162">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="20e44-163">Do vyhledávacího pole zadejte **Microsoft Partnerské centrum** a vyberte ho ze seznamu výsledků.</span><span class="sxs-lookup"><span data-stu-id="20e44-163">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="20e44-164">Zvolte **Vybrat**.</span><span class="sxs-lookup"><span data-stu-id="20e44-164">Choose **Select**.</span></span>

7. <span data-ttu-id="20e44-165">Zvolte **Vybrat oprávnění.**</span><span class="sxs-lookup"><span data-stu-id="20e44-165">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="20e44-166">Vyberte **Přístupový Partnerské centrum PPE.**</span><span class="sxs-lookup"><span data-stu-id="20e44-166">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="20e44-167">Zvolte **Vybrat**.</span><span class="sxs-lookup"><span data-stu-id="20e44-167">Choose **Select**.</span></span>

8. <span data-ttu-id="20e44-168">Vyberte **Hotovo**.</span><span class="sxs-lookup"><span data-stu-id="20e44-168">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="20e44-169">Poznamenejte si ID aplikace ve vlastnostech vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="20e44-169">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="20e44-170">Není nutné registrovat nativní aplikace v Partnerské centrum, ale nativní aplikace musí být odsoulaná správcem.</span><span class="sxs-lookup"><span data-stu-id="20e44-170">You do not need to register native apps in Partner Center, however the native app must be admin consented.</span></span> <span data-ttu-id="20e44-171">Poznamenejte si ID vaší nativní aplikace.</span><span class="sxs-lookup"><span data-stu-id="20e44-171">Note the application ID of your native app.</span></span>
