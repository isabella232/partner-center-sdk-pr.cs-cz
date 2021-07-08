---
title: Ověřování v Partnerském centru
description: Partnerské centrum ověřování používá Azure AD a k použití Partnerské centrum API musíte správně nakonfigurovat nastavení ověřování.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: e54feba7ea727bb7f7eff8de76dcdf28c8a453ee
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548069"
---
# <a name="partner-center-authentication"></a><span data-ttu-id="3486a-103">Ověřování v Partnerském centru</span><span class="sxs-lookup"><span data-stu-id="3486a-103">Partner Center authentication</span></span>

<span data-ttu-id="3486a-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3486a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3486a-105">Partnerské centrum k ověřování využívá Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3486a-105">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="3486a-106">Při práci s rozhraním API, sadou SDK nebo modulem PowerShellu Partnerského centra musíte správně nakonfigurovat aplikaci Azure AD a pak požádat o přístupový token.</span><span class="sxs-lookup"><span data-stu-id="3486a-106">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="3486a-107">Přístupové tokeny získané pouze pomocí aplikace nebo ověřování aplikací a uživatelů je možné použít s Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="3486a-107">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="3486a-108">Je však potřeba zvážit dvě důležité položky.</span><span class="sxs-lookup"><span data-stu-id="3486a-108">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="3486a-109">Vícefaktorové ověřování použijte při přístupu k rozhraní PARTNERSKÉ CENTRUM API pomocí ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="3486a-109">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="3486a-110">Další informace o této změně najdete v tématu [Povolení zabezpečeného aplikačního modelu](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="3486a-110">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="3486a-111">Ne všechny operace, které rozhraní API Partnerské centrum podporuje pouze ověřování aplikací.</span><span class="sxs-lookup"><span data-stu-id="3486a-111">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="3486a-112">Existují určité scénáře, ve kterých budete muset použít ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="3486a-112">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="3486a-113">Pod *nadpisem Požadavky* v každém článku [najdete](scenarios.md)dokumentaci, která uvádí, jestli se podporuje jenom ověřování aplikací, ověřování aplikací a uživatelů nebo obojí.</span><span class="sxs-lookup"><span data-stu-id="3486a-113">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="3486a-114">Počáteční nastavení</span><span class="sxs-lookup"><span data-stu-id="3486a-114">Initial setup</span></span>

1. <span data-ttu-id="3486a-115">Nejprve se musíte ujistit, že máte primární účet Partnerské centrum i účet sandboxu pro integraci Partnerské centrum účet.</span><span class="sxs-lookup"><span data-stu-id="3486a-115">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="3486a-116">Další informace najdete v tématu [Nastavení účtů Partnerské centrum přístup přes rozhraní API.](set-up-api-access-in-partner-center.md)</span><span class="sxs-lookup"><span data-stu-id="3486a-116">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="3486a-117">Poznamenejte si ID registrace aplikace Azure AAD a tajný klíč (tajný kód klienta se vyžaduje jenom pro identifikaci aplikace) pro primární účet i účet sandboxu pro integraci.</span><span class="sxs-lookup"><span data-stu-id="3486a-117">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="3486a-118">Přihlaste se k Azure AD z Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3486a-118">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="3486a-119">V **části** Oprávnění k jiným aplikacím nastavte oprávnění pro **Windows Azure Active Directory** na Delegovaná oprávnění a vyberte Přístup k adresáři jako přihlášený **uživatel** a Přihlásit se a Číst **profil uživatele.** </span><span class="sxs-lookup"><span data-stu-id="3486a-119">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="3486a-120">V Azure Portal přidat **aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="3486a-120">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="3486a-121">Vyhledejte "Microsoft Partnerské centrum", což je aplikace Microsoft Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="3486a-121">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="3486a-122">**Delegovaná oprávnění nastavte** **na Access Partnerské centrum API.**</span><span class="sxs-lookup"><span data-stu-id="3486a-122">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="3486a-123">Pokud používáte nástroj pro Partnerské centrum Microsoft Cloud Germany nebo Partnerské centrum pro Microsoft Cloud for US Government, je tento krok povinný.</span><span class="sxs-lookup"><span data-stu-id="3486a-123">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="3486a-124">Pokud používáte globální instanci Partnerské centrum, je tento krok volitelný.</span><span class="sxs-lookup"><span data-stu-id="3486a-124">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="3486a-125">Partneři CSP mohou pomocí funkce Správa aplikací na Partnerské centrum Portal obejít tento krok pro Partnerské centrum instanci.</span><span class="sxs-lookup"><span data-stu-id="3486a-125">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="3486a-126">Ověřování pouze na základě aplikace</span><span class="sxs-lookup"><span data-stu-id="3486a-126">App-only authentication</span></span>

<span data-ttu-id="3486a-127">Pokud chcete pro přístup k modulu Partnerské centrum REST API, .NET API, Java API nebo PowerShellu použít ověřování jenom pro aplikace, můžete to udělat podle následujících pokynů.</span><span class="sxs-lookup"><span data-stu-id="3486a-127">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by using the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="3486a-128">.NET (ověřování pouze na základě aplikace)</span><span class="sxs-lookup"><span data-stu-id="3486a-128">.NET (app-only authentication)</span></span>

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials =
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId,
            PartnerApplicationConfiguration.ApplicationSecret,
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

## <a name="java-app-only-authentication"></a><span data-ttu-id="3486a-129">Java (ověřování pouze na základě aplikace)</span><span class="sxs-lookup"><span data-stu-id="3486a-129">Java (app-only authentication)</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(),
        PartnerApplicationConfiguration.getApplicationSecret(),
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

## <a name="rest-app-only-authentication"></a><span data-ttu-id="3486a-130">REST (ověřování pouze na základě aplikace)</span><span class="sxs-lookup"><span data-stu-id="3486a-130">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="3486a-131">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="3486a-131">REST request</span></span>

```http
POST https://login.microsoftonline.com/{tenantId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

### <a name="rest-response"></a><span data-ttu-id="3486a-132">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3486a-132">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="3486a-133">Ověřování aplikací a uživatelů</span><span class="sxs-lookup"><span data-stu-id="3486a-133">App + User authentication</span></span>

<span data-ttu-id="3486a-134">V minulosti [](https://tools.ietf.org/html/rfc6749#section-4.3) se k vyžádání přístupového tokenu pro použití s modulem Partnerské centrum REST API, .NET API, Java API nebo PowerShell použilo udělení přihlašovacích údajů vlastníka prostředku.</span><span class="sxs-lookup"><span data-stu-id="3486a-134">Historically, the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="3486a-135">Tato metoda se použila k vyžádání přístupového tokenu od Azure Active Directory pomocí identifikátoru klienta a přihlašovacích údajů uživatele.</span><span class="sxs-lookup"><span data-stu-id="3486a-135">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="3486a-136">Tento přístup ale už nebude fungovat, protože Partnerské centrum vyžaduje vícefaktorové ověřování při použití ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="3486a-136">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="3486a-137">Pro splnění tohoto požadavku společnost Microsoft zavedla zabezpečenou a škálovatelnou rozhraní pro ověřování partnerů Cloud Solution Provider (CSP) a dodavatelů ovládacích panelů (CPV) pomocí vícefaktorového ověřování.</span><span class="sxs-lookup"><span data-stu-id="3486a-137">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="3486a-138">Tato rozhraní se označuje jako Model zapezpečených aplikací a skládá se z procesu souhlasu a žádosti o přístupový token pomocí obnovovacího tokenu.</span><span class="sxs-lookup"><span data-stu-id="3486a-138">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="3486a-139">Souhlas partnera</span><span class="sxs-lookup"><span data-stu-id="3486a-139">Partner consent</span></span>

<span data-ttu-id="3486a-140">Proces souhlasu partnera je interaktivní proces, ve kterém se partner ověřuje pomocí vícefaktorového ověřování, souhlasí s aplikací a obnovovací token je uložený v zabezpečeném úložišti, jako je Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3486a-140">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="3486a-141">Pro tento proces doporučujeme použít vyhrazený účet pro účely integrace.</span><span class="sxs-lookup"><span data-stu-id="3486a-141">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3486a-142">Pro účet služby použitý v procesu souhlasu partnera by mělo být povolené vhodné řešení vícefaktorového ověřování.</span><span class="sxs-lookup"><span data-stu-id="3486a-142">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="3486a-143">Pokud tomu tak není, výsledný obnovovací token nebude splňovat požadavky na zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="3486a-143">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="3486a-144">Ukázky ověřování aplikací a uživatelů</span><span class="sxs-lookup"><span data-stu-id="3486a-144">Samples for App + User authentication</span></span>

<span data-ttu-id="3486a-145">Proces souhlasu partnera je možné provést několika způsoby.</span><span class="sxs-lookup"><span data-stu-id="3486a-145">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="3486a-146">Aby partneři pochopili, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky.</span><span class="sxs-lookup"><span data-stu-id="3486a-146">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="3486a-147">Při implementaci vhodného řešení ve vašem prostředí je důležité vyvinout řešení, které je v souladu s vašimi standardy kódování a zásadami zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="3486a-147">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="3486a-148">.NET (ověřování aplikací a uživatelů)</span><span class="sxs-lookup"><span data-stu-id="3486a-148">.NET (app+user authentication)</span></span>

<span data-ttu-id="3486a-149">Ukázkový [projekt souhlasu](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) partnera ukazuje, jak využít web vyvinutý pomocí ASP.NET k zachycení souhlasu, vyžádání obnovovacího tokenu a jeho bezpečnému uložení v Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3486a-149">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="3486a-150">Provedením následujících kroků vytvořte požadované součásti pro tuto ukázku.</span><span class="sxs-lookup"><span data-stu-id="3486a-150">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="3486a-151">Vytvořte instanci služby Azure Key Vault pomocí Azure Portal nebo následujících příkazů PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="3486a-151">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="3486a-152">Před spuštěním příkazu nezapomeňte odpovídajícím způsobem upravit hodnoty parametrů.</span><span class="sxs-lookup"><span data-stu-id="3486a-152">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="3486a-153">Název trezoru musí být jedinečný.</span><span class="sxs-lookup"><span data-stu-id="3486a-153">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="3486a-154">Další informace o vytvoření Azure Key Vault najdete v tématu Rychlý [start:](/azure/key-vault/quick-create-portal) Nastavení a načtení tajného klíče ze služby Azure Key Vault pomocí Azure Portal nebo Rychlý start: Nastavení a načtení tajného klíče z [Azure Key Vault pomocí PowerShellu.](/azure/key-vault/quick-create-powershell)</span><span class="sxs-lookup"><span data-stu-id="3486a-154">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="3486a-155">Potom nastavte a načtěte tajný kód.</span><span class="sxs-lookup"><span data-stu-id="3486a-155">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="3486a-156">Vytvořte aplikaci Azure AD a klíč pomocí Azure Portal nebo následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="3486a-156">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="3486a-157">Nezapomeňte si poznamenat hodnoty identifikátoru a tajného kódu aplikace, protože je použijete v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="3486a-157">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="3486a-158">Udělte nově vytvořené aplikaci Azure AD oprávnění ke čtení tajných kódů pomocí Azure Portal nebo následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="3486a-158">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="3486a-159">Vytvořte aplikaci Azure AD, která je nakonfigurovaná pro Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="3486a-159">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="3486a-160">K dokončení tohoto kroku proveďte následující akce.</span><span class="sxs-lookup"><span data-stu-id="3486a-160">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="3486a-161">Přejděte na [funkci Správa aplikací řídicího](https://partner.microsoft.com/pcv/apiintegration/appmanagement) panelu Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="3486a-161">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="3486a-162">Vyberte *Přidat novou webovou aplikaci* a vytvořte novou aplikaci Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3486a-162">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="3486a-163">Nezapomeňte zdokumentovat *hodnoty ID aplikace,\*\*ID účtu*\* a *Klíč,* protože je použijete v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="3486a-163">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="3486a-164">[Naklonovat úložiště Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) Visual Studio nebo následujícím příkazem.</span><span class="sxs-lookup"><span data-stu-id="3486a-164">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="3486a-165">Otevřete projekt *PartnerConsent* v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři .</span><span class="sxs-lookup"><span data-stu-id="3486a-165">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="3486a-166">Vyplňte nastavení aplikace nalezená v [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span><span class="sxs-lookup"><span data-stu-id="3486a-166">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!--
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="3486a-167">Citlivé informace, jako jsou tajné kódy aplikací, by neměly být uložené v konfiguračních souborech.</span><span class="sxs-lookup"><span data-stu-id="3486a-167">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="3486a-168">Bylo to tady, protože se jedná o ukázkovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="3486a-168">It was done here because this is a sample application.</span></span> <span data-ttu-id="3486a-169">U produkční aplikace důrazně doporučujeme používat ověřování pomocí certifikátů.</span><span class="sxs-lookup"><span data-stu-id="3486a-169">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="3486a-170">Další informace najdete v tématu Přihlašovací [údaje certifikátu pro ověřování aplikací.]( /azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="3486a-170">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="3486a-171">Při spuštění tohoto ukázkového projektu se zobrazí výzva k ověření.</span><span class="sxs-lookup"><span data-stu-id="3486a-171">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="3486a-172">Po úspěšném ověření se z Azure AD vyžádá přístupový token.</span><span class="sxs-lookup"><span data-stu-id="3486a-172">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="3486a-173">Informace vrácené z Azure AD zahrnují obnovovací token, který je uložený v nakonfigurované instanci Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3486a-173">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="3486a-174">Java (ověřování aplikací a uživatelů)</span><span class="sxs-lookup"><span data-stu-id="3486a-174">Java (app+user authentication)</span></span>

<span data-ttu-id="3486a-175">Ukázkový [projekt souhlasu](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) partnera ukazuje, jak využít web vyvinutý pomocí JSP k zachycení souhlasu, vyžádání obnovovacího tokenu a zabezpečeného úložiště v Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3486a-175">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="3486a-176">Následujícím způsobem vytvořte požadované součásti pro tuto ukázku.</span><span class="sxs-lookup"><span data-stu-id="3486a-176">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="3486a-177">Vytvořte instanci služby Azure Key Vault pomocí Azure Portal nebo následujících příkazů PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="3486a-177">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="3486a-178">Před spuštěním příkazu nezapomeňte odpovídajícím způsobem upravit hodnoty parametrů.</span><span class="sxs-lookup"><span data-stu-id="3486a-178">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="3486a-179">Název trezoru musí být jedinečný.</span><span class="sxs-lookup"><span data-stu-id="3486a-179">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="3486a-180">Další informace o vytvoření Azure Key Vault najdete v tématu Rychlý [start:](/azure/key-vault/quick-create-portal) Nastavení a načtení tajného klíče ze služby Azure Key Vault pomocí Azure Portal nebo Rychlý start: Nastavení a načtení tajného klíče z [Azure Key Vault pomocí PowerShellu.](/azure/key-vault/quick-create-powershell)</span><span class="sxs-lookup"><span data-stu-id="3486a-180">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="3486a-181">Vytvořte aplikaci Azure AD a klíč pomocí Azure Portal nebo následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="3486a-181">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="3486a-182">Nezapomeňte zdokumentovat hodnoty identifikátoru a tajného kódu aplikace, protože je použijete v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="3486a-182">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="3486a-183">Udělte nově vytvořené aplikaci Azure AD oprávnění ke čtení tajných kódů pomocí Azure Portal nebo následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="3486a-183">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="3486a-184">Vytvořte aplikaci Azure AD, která je nakonfigurovaná pro Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="3486a-184">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="3486a-185">K dokončení tohoto kroku proveďte následující kroky.</span><span class="sxs-lookup"><span data-stu-id="3486a-185">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="3486a-186">Přejděte na [funkci Správa aplikací řídicího](https://partner.microsoft.com/pcv/apiintegration/appmanagement) panelu Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="3486a-186">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="3486a-187">Vyberte *Přidat novou webovou aplikaci* a vytvořte novou aplikaci Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3486a-187">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="3486a-188">Nezapomeňte zdokumentovat *hodnoty ID aplikace,\*\*ID účtu*\* a *Klíč,* protože je použijete v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="3486a-188">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="3486a-189">[Naklonování úložiště Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí následujícího příkazu</span><span class="sxs-lookup"><span data-stu-id="3486a-189">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="3486a-190">Otevřete projekt *PartnerConsent* v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři .</span><span class="sxs-lookup"><span data-stu-id="3486a-190">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="3486a-191">Naplnění nastavení aplikace nalezených v [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) souboru</span><span class="sxs-lookup"><span data-stu-id="3486a-191">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="3486a-192">Citlivé informace, jako jsou tajné kódy aplikací, by neměly být uložené v konfiguračních souborech.</span><span class="sxs-lookup"><span data-stu-id="3486a-192">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="3486a-193">Bylo to tady, protože se jedná o ukázkovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="3486a-193">It was done here because this is a sample application.</span></span> <span data-ttu-id="3486a-194">U produkční aplikace důrazně doporučujeme používat ověřování na základě certifikátů.</span><span class="sxs-lookup"><span data-stu-id="3486a-194">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="3486a-195">Další informace najdete v tématu [Key Vault certifikátu](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span><span class="sxs-lookup"><span data-stu-id="3486a-195">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="3486a-196">Při spuštění tohoto ukázkového projektu se zobrazí výzva k ověření.</span><span class="sxs-lookup"><span data-stu-id="3486a-196">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="3486a-197">Po úspěšném ověření se z Azure AD vyžádá přístupový token.</span><span class="sxs-lookup"><span data-stu-id="3486a-197">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="3486a-198">Informace vrácené z Azure AD zahrnují obnovovací token, který je uložený v nakonfigurované instanci Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3486a-198">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="3486a-199">Cloud Solution Provider ověřování</span><span class="sxs-lookup"><span data-stu-id="3486a-199">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="3486a-200">Cloud Solution Provider partneři mohou použít obnovovací token získaný prostřednictvím procesu [souhlasu partnera.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="3486a-200">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="3486a-201">Ukázky pro Cloud Solution Provider ověřování</span><span class="sxs-lookup"><span data-stu-id="3486a-201">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="3486a-202">Aby partneři pochopili, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky.</span><span class="sxs-lookup"><span data-stu-id="3486a-202">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="3486a-203">Při implementaci vhodného řešení ve vašem prostředí je důležité vyvinout řešení, které je v souladu s vašimi standardy kódování a zásadami zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="3486a-203">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="3486a-204">.NET (ověřování CSP)</span><span class="sxs-lookup"><span data-stu-id="3486a-204">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="3486a-205">Pokud jste to ještě neudělali, proveďte proces [souhlasu partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="3486a-205">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="3486a-206">[Naklonování úložiště Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) pomocí Visual Studio nebo následujícího příkazu</span><span class="sxs-lookup"><span data-stu-id="3486a-206">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="3486a-207">Otevřete projekt `CSPApplication` nalezený v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři .</span><span class="sxs-lookup"><span data-stu-id="3486a-207">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="3486a-208">Aktualizujte nastavení aplikace, které najdete v [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) souboru.</span><span class="sxs-lookup"><span data-stu-id="3486a-208">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. <span data-ttu-id="3486a-209">Nastavte odpovídající hodnoty pro proměnné **PartnerId** a **CustomerId** v souboru [Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="3486a-209">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="3486a-210">Když tento ukázkový projekt spustíte, získá obnovovací token získaný během procesu souhlasu partnera.</span><span class="sxs-lookup"><span data-stu-id="3486a-210">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="3486a-211">Pak požádá o přístupový token k interakci s SDK pro Partnerské centrum jménem partnera.</span><span class="sxs-lookup"><span data-stu-id="3486a-211">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="3486a-212">Nakonec požádá o přístupový token pro interakci s Microsoftem Graph jménem zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3486a-212">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="3486a-213">Java (ověřování CSP)</span><span class="sxs-lookup"><span data-stu-id="3486a-213">Java (CSP authentication)</span></span>

1. <span data-ttu-id="3486a-214">Pokud jste to ještě neudělali, proveďte proces [souhlasu partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="3486a-214">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="3486a-215">[Naklonování úložiště Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí Visual Studio nebo následujícího příkazu</span><span class="sxs-lookup"><span data-stu-id="3486a-215">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="3486a-216">Otevřete projekt `cspsample` nalezený v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři .</span><span class="sxs-lookup"><span data-stu-id="3486a-216">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="3486a-217">Aktualizujte nastavení aplikace v souboru [application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties)</span><span class="sxs-lookup"><span data-stu-id="3486a-217">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="3486a-218">Když tento ukázkový projekt spustíte, získá obnovovací token získaný během procesu souhlasu partnera.</span><span class="sxs-lookup"><span data-stu-id="3486a-218">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="3486a-219">Pak požádá o přístupový token k interakci s SDK pro Partnerské centrum jménem partnera.</span><span class="sxs-lookup"><span data-stu-id="3486a-219">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="3486a-220">Volitelné – odkomentování volání funkcí *RunAzureTask* a *RunGraphTask,* pokud chcete vidět, jak pracovat s Azure Resource Manager a Microsoft Graph jménem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3486a-220">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="3486a-221">Ovládací panely zprostředkovatele ověřování</span><span class="sxs-lookup"><span data-stu-id="3486a-221">Control Panel Provider authentication</span></span>

<span data-ttu-id="3486a-222">Dodavatelé ovládacích panelů musí mít každého partnera, který podporují, aby mohli provést [proces souhlasu partnera.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="3486a-222">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="3486a-223">Po dokončení se obnovovací token získaný prostřednictvím tohoto procesu použije pro přístup k Partnerské centrum REST API a rozhraní .NET API.</span><span class="sxs-lookup"><span data-stu-id="3486a-223">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="3486a-224">Ukázky pro ověřování poskytovatele cloudových panelů</span><span class="sxs-lookup"><span data-stu-id="3486a-224">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="3486a-225">Aby dodavatelé ovládacích panelů pochopili, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky.</span><span class="sxs-lookup"><span data-stu-id="3486a-225">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="3486a-226">Při implementaci vhodného řešení ve vašem prostředí je důležité vyvinout řešení, které je v souladu s vašimi standardy kódování a zásadami zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="3486a-226">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="3486a-227">.NET (ověřování CPV)</span><span class="sxs-lookup"><span data-stu-id="3486a-227">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="3486a-228">Vytvořte a nasaďte proces, který Cloud Solution Provider partnerům s odpovídajícím souhlasem.</span><span class="sxs-lookup"><span data-stu-id="3486a-228">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="3486a-229">Další informace najdete v příkladu se [souhlasem partnera.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="3486a-229">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3486a-230">Přihlašovací údaje uživatele od Cloud Solution Provider by se neměly ukládat.</span><span class="sxs-lookup"><span data-stu-id="3486a-230">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="3486a-231">Obnovovací token získaný prostřednictvím procesu souhlasu partnera by se měl uložit a použít k vyžádání přístupových tokenů pro interakci s libovolným rozhraním API Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="3486a-231">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="3486a-232">[Naklonování úložiště Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) pomocí Visual Studio nebo následujícího příkazu</span><span class="sxs-lookup"><span data-stu-id="3486a-232">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="3486a-233">Otevřete projekt `CPVApplication` nalezený v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři .</span><span class="sxs-lookup"><span data-stu-id="3486a-233">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="3486a-234">Aktualizujte nastavení aplikace, které najdete v [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) souboru.</span><span class="sxs-lookup"><span data-stu-id="3486a-234">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

    ```xml
    <!-- AppID that represents Control panel vendor application -->
    <add key="ida:CPVApplicationId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CPVApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. <span data-ttu-id="3486a-235">Nastavte odpovídající hodnoty pro proměnné **PartnerId** a **CustomerId** v souboru [Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="3486a-235">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="3486a-236">Když tento ukázkový projekt spustíte, získá obnovovací token pro zadaného partnera.</span><span class="sxs-lookup"><span data-stu-id="3486a-236">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="3486a-237">Potom požádá o přístupový token pro přístup Partnerské centrum a Azure AD Graph jménem partnera.</span><span class="sxs-lookup"><span data-stu-id="3486a-237">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="3486a-238">Dalším úkolem, který provede, je odstranění a vytvoření udělených oprávnění do tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3486a-238">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="3486a-239">Vzhledem k tomu, že mezi dodavatelem ovládacích panelů a zákazníkem neexistuje žádný vztah, je potřeba tato oprávnění přidat pomocí Partnerské centrum API.</span><span class="sxs-lookup"><span data-stu-id="3486a-239">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="3486a-240">Následující příklad ukazuje, jak toho dosáhnout.</span><span class="sxs-lookup"><span data-stu-id="3486a-240">The following example shows how to accomplish that.</span></span>

    ```csharp
    JObject contents = new JObject
    {
        // Provide your application display name
        ["displayName"] = "CPV Marketplace",

        // Provide your application id
        ["applicationId"] = CPVApplicationId,

        // Provide your application grants
        ["applicationGrants"] = new JArray(
            JObject.Parse("{\"enterpriseApplicationId\": \"00000002-0000-0000-c000-000000000000\", \"scope\":\"Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All\"}"), // for Azure AD Graph access,  Directory.Read.All
            JObject.Parse("{\"enterpriseApplicationId\": \"797f4846-ba00-4fd7-ba43-dac1f8f63013\", \"scope\":\"user_impersonation\"}")) // for Azure Resource Manager access
    };

    /**
     * The following steps have to be performed once per customer tenant if your application is
     * a control panel vendor application and requires customer tenant Azure AD Graph access.
     **/

    // delete the previous grant into customer tenant
    JObject consentDeletion = await ApiCalls.DeleteAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents/{1}", CustomerId, CPVApplicationId));

    // create new grants for the application given the setting in application grants payload.
    JObject consentCreation = await ApiCalls.PostAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents", CustomerId),
        contents.ToString());
    ```

<span data-ttu-id="3486a-241">Po navázání těchto oprávnění ukázka provede operace pomocí služby Azure AD Graph jménem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3486a-241">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="3486a-242">Java (ověřování CPV)</span><span class="sxs-lookup"><span data-stu-id="3486a-242">Java (CPV authentication)</span></span>

1. <span data-ttu-id="3486a-243">Vytvořte a nasaďte proces, který Cloud Solution Provider partnerům s odpovídajícím souhlasem.</span><span class="sxs-lookup"><span data-stu-id="3486a-243">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="3486a-244">Další informace a příklad najdete v tématu o [souhlasu partnera.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="3486a-244">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3486a-245">Přihlašovací údaje uživatele od Cloud Solution Provider by se neměly ukládat.</span><span class="sxs-lookup"><span data-stu-id="3486a-245">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="3486a-246">Obnovovací token získaný prostřednictvím procesu souhlasu partnera by se měl uložit a použít k vyžádání přístupových tokenů pro interakci s libovolným rozhraním API Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="3486a-246">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="3486a-247">[Naklonování úložiště Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí následujícího příkazu</span><span class="sxs-lookup"><span data-stu-id="3486a-247">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="3486a-248">Otevřete projekt `cpvsample` nalezený v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři .</span><span class="sxs-lookup"><span data-stu-id="3486a-248">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="3486a-249">Aktualizujte nastavení aplikace v souboru [application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties)</span><span class="sxs-lookup"><span data-stu-id="3486a-249">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

    ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    partnercenter.displayName=
    ```

    <span data-ttu-id="3486a-250">Hodnota by `partnercenter.displayName` měla být zobrazovaný název vaší aplikace marketplace.</span><span class="sxs-lookup"><span data-stu-id="3486a-250">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="3486a-251">Nastavte odpovídající hodnoty pro **proměnné partnerId** a **customerId** v souboru [Program.java.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java)</span><span class="sxs-lookup"><span data-stu-id="3486a-251">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="3486a-252">Když tento ukázkový projekt spustíte, získá obnovovací token pro zadaného partnera.</span><span class="sxs-lookup"><span data-stu-id="3486a-252">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="3486a-253">Potom požádá o přístupový token pro přístup Partnerské centrum jménem partnera.</span><span class="sxs-lookup"><span data-stu-id="3486a-253">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="3486a-254">Dalším úkolem, který provede, je odstranění a vytvoření udělených oprávnění do tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3486a-254">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="3486a-255">Vzhledem k tomu, že mezi dodavatelem ovládacích panelů a zákazníkem neexistuje žádný vztah, je potřeba tato oprávnění přidat pomocí Partnerské centrum API.</span><span class="sxs-lookup"><span data-stu-id="3486a-255">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="3486a-256">Následující příklad ukazuje, jak udělit oprávnění.</span><span class="sxs-lookup"><span data-stu-id="3486a-256">The following example shows how to grant the permissions.</span></span>

    ```java
    ApplicationGrant azureAppGrant = new ApplicationGrant();

    azureAppGrant.setEnterpriseApplication("797f4846-ba00-4fd7-ba43-dac1f8f63013");
    azureAppGrant.setScope("user_impersonation");

    ApplicationGrant graphAppGrant = new ApplicationGrant();

    graphAppGrant.setEnterpriseApplication("00000002-0000-0000-c000-000000000000");
    graphAppGrant.setScope("Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All");

    ApplicationConsent consent = new ApplicationConsent();

    consent.setApplicationGrants(Arrays.asList(azureAppGrant, graphAppGrant));
    consent.setApplicationId(properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID));
    consent.setDisplayName(properties.getProperty(PropertyName.PARTNER_CENTER_DISPLAY_NAME));

    // Deletes the existing grant into the customer it is present.
    partnerOperations.getServiceClient().delete(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents/{1}",
            customerId,
            properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID)));

    // Consent to the defined applications and the respective scopes.
    partnerOperations.getServiceClient().post(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents",
            customerId),
        consent);
    ```

<span data-ttu-id="3486a-257">Odkomentování volání funkcí *RunAzureTask* a *RunGraphTask,* pokud chcete vidět, jak pracovat s Azure Resource Manager a Microsoft Graph jménem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3486a-257">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
