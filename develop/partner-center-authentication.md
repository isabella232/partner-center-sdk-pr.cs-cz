---
title: Ověřování v Partnerském centru
description: Partnerské centrum používá pro ověřování Azure AD a používá rozhraní API partnerského centra. musíte nakonfigurovat nastavení ověřování správně.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: 46ef9c6bc151c368281e943b7d24ebc07e34b66d
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/19/2020
ms.locfileid: "97767668"
---
# <a name="partner-center-authentication"></a><span data-ttu-id="b3361-103">Ověřování v Partnerském centru</span><span class="sxs-lookup"><span data-stu-id="b3361-103">Partner Center authentication</span></span>

<span data-ttu-id="b3361-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="b3361-104">**Applies to:**</span></span>

- <span data-ttu-id="b3361-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b3361-105">Partner Center</span></span>
- <span data-ttu-id="b3361-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b3361-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b3361-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="b3361-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b3361-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b3361-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b3361-109">Partnerské centrum k ověřování využívá Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b3361-109">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="b3361-110">Při práci s rozhraním API, sadou SDK nebo modulem PowerShellu Partnerského centra musíte správně nakonfigurovat aplikaci Azure AD a pak požádat o přístupový token.</span><span class="sxs-lookup"><span data-stu-id="b3361-110">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="b3361-111">Přístupové tokeny získané jenom pro aplikace nebo ověřování pomocí aplikace a uživatele se dají použít s partnerským centrem.</span><span class="sxs-lookup"><span data-stu-id="b3361-111">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="b3361-112">Existují však dvě důležité položky, které je třeba vzít v úvahu.</span><span class="sxs-lookup"><span data-stu-id="b3361-112">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="b3361-113">Použijte vícefaktorové ověřování při přístupu k rozhraní API partnerského centra pomocí ověřování aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b3361-113">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="b3361-114">Další informace o této změně najdete v tématu [Povolení zabezpečení aplikačního modelu](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="b3361-114">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="b3361-115">Ne všechny operace: rozhraní API partnerského centra podporuje pouze ověřování aplikace.</span><span class="sxs-lookup"><span data-stu-id="b3361-115">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="b3361-116">Existují některé scénáře, kdy budete muset použít aplikaci a ověřování uživatelů.</span><span class="sxs-lookup"><span data-stu-id="b3361-116">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="b3361-117">V nadpisu *požadavky* každého [článku](scenarios.md)najdete dokumentaci s informací, jestli jsou podporované jenom ověřování, aplikace + ověřování uživatelů nebo obojí.</span><span class="sxs-lookup"><span data-stu-id="b3361-117">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="b3361-118">Počáteční nastavení</span><span class="sxs-lookup"><span data-stu-id="b3361-118">Initial setup</span></span>

1. <span data-ttu-id="b3361-119">Abyste mohli začít, musíte se ujistit, že máte primární účet partnerského centra a účet partnerského centra pro integraci izolovaného prostoru (sandbox).</span><span class="sxs-lookup"><span data-stu-id="b3361-119">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="b3361-120">Další informace najdete v tématu [Nastavení účtů partnerského centra pro přístup přes rozhraní API](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="b3361-120">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="b3361-121">Poznamenejte si ID registrace a tajný kód aplikace Azure AAD (pro identifikaci aplikace se vyžaduje tajný klíč klienta) pro váš primární účet i váš účet izolovaného prostoru (sandbox).</span><span class="sxs-lookup"><span data-stu-id="b3361-121">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="b3361-122">Přihlaste se k Azure AD z Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b3361-122">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="b3361-123">V **oprávněních k ostatním aplikacím** nastavte oprávnění pro **Windows Azure Active Directory** na **delegovaná oprávnění** a **jako přihlášeného uživatele vyberte přístup k adresáři** , **Přihlaste se a přečtěte si profil uživatele**.</span><span class="sxs-lookup"><span data-stu-id="b3361-123">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="b3361-124">V Azure Portal **přidejte aplikaci**.</span><span class="sxs-lookup"><span data-stu-id="b3361-124">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="b3361-125">Vyhledejte "partnerské Centrum Microsoftu", což je aplikace partnerského centra Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="b3361-125">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="b3361-126">Nastavte **delegovaná oprávnění** pro **přístup k rozhraní API partnerského centra**.</span><span class="sxs-lookup"><span data-stu-id="b3361-126">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="b3361-127">Pokud používáte partnerské Centrum pro Microsoft Cloud Německo nebo partnerské Centrum pro Microsoft Cloud pro státní správu USA, je tento krok povinný.</span><span class="sxs-lookup"><span data-stu-id="b3361-127">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="b3361-128">Pokud používáte globální instanci partnerského centra, je tento krok nepovinný.</span><span class="sxs-lookup"><span data-stu-id="b3361-128">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="b3361-129">Partneři CSP můžou pomocí funkce správy aplikací na portálu partnerského centra obejít tento krok pro globální instanci partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b3361-129">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="b3361-130">Ověřování pouze pro aplikace</span><span class="sxs-lookup"><span data-stu-id="b3361-130">App-only authentication</span></span>

<span data-ttu-id="b3361-131">Pokud chcete používat ověřování jenom pro aplikace pro přístup k REST API partnerských Center, rozhraní API .NET, Java API nebo modul PowerShellu, můžete to udělat pomocí následujících pokynů.</span><span class="sxs-lookup"><span data-stu-id="b3361-131">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by leveraging the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="b3361-132">.NET (ověřování pouze pro aplikace)</span><span class="sxs-lookup"><span data-stu-id="b3361-132">.NET (app-only authentication)</span></span>

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

## <a name="java-app-only-authentication"></a><span data-ttu-id="b3361-133">Java (ověřování pouze aplikací)</span><span class="sxs-lookup"><span data-stu-id="b3361-133">Java (app-only authentication)</span></span>

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

## <a name="rest-app-only-authentication"></a><span data-ttu-id="b3361-134">REST (ověřování pouze pro aplikace)</span><span class="sxs-lookup"><span data-stu-id="b3361-134">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="b3361-135">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b3361-135">REST request</span></span>

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

### <a name="rest-response"></a><span data-ttu-id="b3361-136">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b3361-136">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="b3361-137">Ověřování aplikací a uživatelů</span><span class="sxs-lookup"><span data-stu-id="b3361-137">App + User authentication</span></span>

<span data-ttu-id="b3361-138">Historické [přihlašovací údaje pro heslo vlastníka prostředku](https://tools.ietf.org/html/rfc6749#section-4.3) se použily k vyžádání přístupového tokenu pro použití s REST API partnerských Center, rozhraní API .NET, Java API nebo modul PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="b3361-138">Historically the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="b3361-139">Tato metoda se použila k vyžádání přístupového tokenu z Azure Active Directory pomocí identifikátoru klienta a přihlašovacích údajů uživatele.</span><span class="sxs-lookup"><span data-stu-id="b3361-139">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="b3361-140">Tento přístup ale už nebude fungovat, protože partnerské Centrum vyžaduje vícefaktorové ověřování, když se používá ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="b3361-140">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="b3361-141">Pro splnění tohoto požadavku společnost Microsoft zavedla zabezpečenou, škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) pomocí služby Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="b3361-141">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="b3361-142">Tato architektura se označuje jako model zabezpečené aplikace a skládá se z procesu souhlasu a žádosti o přístupový token pomocí obnovovacího tokenu.</span><span class="sxs-lookup"><span data-stu-id="b3361-142">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="b3361-143">Souhlas partnera</span><span class="sxs-lookup"><span data-stu-id="b3361-143">Partner consent</span></span>

<span data-ttu-id="b3361-144">Proces souhlasu s partnerem je interaktivní proces, ve kterém se partner ověřuje pomocí služby Multi-Factor Authentication, souhlasí s aplikací a je uložený v zabezpečeném úložišti, jako je Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b3361-144">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="b3361-145">Pro účely tohoto procesu doporučujeme použít vyhrazený účet pro účely integrace.</span><span class="sxs-lookup"><span data-stu-id="b3361-145">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3361-146">Pro účet služby, který se používá v procesu souhlasu s partnerem, by mělo být povoleno příslušné řešení Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="b3361-146">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="b3361-147">Pokud není, výsledný obnovovací token nebude kompatibilní s požadavky na zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="b3361-147">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="b3361-148">Ukázky pro ověřování aplikací a uživatelů</span><span class="sxs-lookup"><span data-stu-id="b3361-148">Samples for App + User authentication</span></span>

<span data-ttu-id="b3361-149">Proces souhlasu s partnerem je možné provést několika způsoby.</span><span class="sxs-lookup"><span data-stu-id="b3361-149">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="b3361-150">Abychom pomohli partnerům pochopit, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky.</span><span class="sxs-lookup"><span data-stu-id="b3361-150">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="b3361-151">Při implementaci vhodného řešení ve vašem prostředí je důležité vyvíjet řešení, které je stížností se standardy kódování a zásadami zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="b3361-151">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="b3361-152">.NET (ověřování aplikací a uživatelů)</span><span class="sxs-lookup"><span data-stu-id="b3361-152">.NET (app+user authentication)</span></span>

<span data-ttu-id="b3361-153">Ukázkový projekt [souhlasu s partnerem](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) ukazuje, jak používat web vyvinutý pomocí ASP.NET k zachycení souhlasu, vyžádání obnovovacího tokenu a bezpečnému uložení v Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b3361-153">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="b3361-154">Chcete-li vytvořit požadované požadavky pro tuto ukázku, proveďte následující kroky.</span><span class="sxs-lookup"><span data-stu-id="b3361-154">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="b3361-155">Vytvořte instanci Azure Key Vault pomocí Azure Portal nebo následujících příkazů PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="b3361-155">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="b3361-156">Před provedením příkazu nezapomeňte odpovídajícím způsobem upravit hodnoty parametrů.</span><span class="sxs-lookup"><span data-stu-id="b3361-156">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="b3361-157">Název trezoru musí být jedinečný.</span><span class="sxs-lookup"><span data-stu-id="b3361-157">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="b3361-158">Další informace o vytváření Azure Key Vault najdete v tématu [rychlý Start: nastavení a načtení tajného klíče z Azure Key Vault pomocí Azure Portal](/azure/key-vault/quick-create-portal) nebo [rychlý Start: nastavení a načtení tajného klíče ze Azure Key Vault pomocí prostředí PowerShell](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="b3361-158">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="b3361-159">Pak nastavte a načtěte tajný klíč.</span><span class="sxs-lookup"><span data-stu-id="b3361-159">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="b3361-160">Vytvořte aplikaci Azure AD a klíč pomocí Azure Portal nebo následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="b3361-160">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="b3361-161">Nezapomeňte si poznamenat identifikátor aplikace a tajné hodnoty, protože se použijí v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="b3361-161">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="b3361-162">Udělte nově vytvořeným aplikacím Azure AD oprávnění číst tajné klíče pomocí Azure Portal nebo následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="b3361-162">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="b3361-163">Vytvořte aplikaci Azure AD, která je nakonfigurovaná pro partnerské Centrum.</span><span class="sxs-lookup"><span data-stu-id="b3361-163">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="b3361-164">Provedením následujících akcí dokončete tento krok.</span><span class="sxs-lookup"><span data-stu-id="b3361-164">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="b3361-165">Přejděte do funkce [Správa aplikací](https://partner.microsoft.com/pcv/apiintegration/appmanagement) na řídicím panelu partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b3361-165">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="b3361-166">Klikněte na *Přidat novou webovou aplikaci* a vytvořte novou aplikaci Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3361-166">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="b3361-167">Nezapomeňte zdokumentovat *ID aplikace*\* ID účtu \* \* a hodnoty *klíče* , protože se použijí v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="b3361-167">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="b3361-168">Pomocí sady Visual Studio naklonujte úložiště [partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) nebo použijte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="b3361-168">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="b3361-169">Otevřete projekt *PartnerConsent* , který se nachází v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři.</span><span class="sxs-lookup"><span data-stu-id="b3361-169">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="b3361-170">Naplňte nastavení aplikace nalezené v [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span><span class="sxs-lookup"><span data-stu-id="b3361-170">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

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
    > <span data-ttu-id="b3361-171">Citlivé informace, jako jsou tajné klíče aplikace, by neměly být uloženy v konfiguračních souborech.</span><span class="sxs-lookup"><span data-stu-id="b3361-171">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="b3361-172">To bylo provedeno, protože se jedná o ukázkovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b3361-172">It was done here because this is a sample application.</span></span> <span data-ttu-id="b3361-173">V produkční aplikaci důrazně doporučujeme používat ověřování pomocí certifikátů.</span><span class="sxs-lookup"><span data-stu-id="b3361-173">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="b3361-174">Další informace najdete v tématu [přihlašovací údaje certifikátu pro ověřování aplikací]( /azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="b3361-174">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="b3361-175">Když spustíte tento ukázkový projekt, zobrazí se výzva k ověření.</span><span class="sxs-lookup"><span data-stu-id="b3361-175">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="b3361-176">Po úspěšném ověření se z Azure AD vyžádá přístupový token.</span><span class="sxs-lookup"><span data-stu-id="b3361-176">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="b3361-177">Informace vrácené z Azure AD obsahují obnovovací token, který je uložený v nakonfigurované instanci Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b3361-177">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="b3361-178">Java (ověřování aplikací a uživatelů)</span><span class="sxs-lookup"><span data-stu-id="b3361-178">Java (app+user authentication)</span></span>

<span data-ttu-id="b3361-179">Ukázkový projekt [souhlasu s partnerem](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) ukazuje, jak používat web vyvinutý pomocí JSP k zachycení souhlasu, vyžádání obnovovacího tokenu a zabezpečeného úložiště v Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b3361-179">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="b3361-180">Pro vytvoření požadovaných požadavků pro tuto ukázku proveďte následující kroky.</span><span class="sxs-lookup"><span data-stu-id="b3361-180">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="b3361-181">Vytvořte instanci Azure Key Vault pomocí Azure Portal nebo následujících příkazů PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="b3361-181">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="b3361-182">Před provedením příkazu nezapomeňte odpovídajícím způsobem upravit hodnoty parametrů.</span><span class="sxs-lookup"><span data-stu-id="b3361-182">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="b3361-183">Název trezoru musí být jedinečný.</span><span class="sxs-lookup"><span data-stu-id="b3361-183">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="b3361-184">Další informace o vytváření Azure Key Vault najdete v tématu [rychlý Start: nastavení a načtení tajného klíče z Azure Key Vault pomocí Azure Portal](/azure/key-vault/quick-create-portal) nebo [rychlý Start: nastavení a načtení tajného klíče ze Azure Key Vault pomocí prostředí PowerShell](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="b3361-184">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="b3361-185">Vytvořte aplikaci Azure AD a klíč pomocí Azure Portal nebo následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="b3361-185">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="b3361-186">Nezapomeňte zdokumentovat identifikátor aplikace a tajné hodnoty, protože budou použity v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="b3361-186">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="b3361-187">Udělte nově vytvořeným aplikacím Azure AD oprávnění číst tajné klíče pomocí Azure Portal nebo následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="b3361-187">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="b3361-188">Vytvořte aplikaci Azure AD, která je nakonfigurovaná pro partnerské Centrum.</span><span class="sxs-lookup"><span data-stu-id="b3361-188">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="b3361-189">K dokončení tohoto kroku proveďte následující kroky.</span><span class="sxs-lookup"><span data-stu-id="b3361-189">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="b3361-190">Přejděte do funkce [Správa aplikací](https://partner.microsoft.com/pcv/apiintegration/appmanagement) na řídicím panelu partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b3361-190">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="b3361-191">Klikněte na *Přidat novou webovou aplikaci* a vytvořte novou aplikaci Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3361-191">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="b3361-192">Nezapomeňte zdokumentovat *ID aplikace*\* ID účtu \* \* a hodnoty *klíče* , protože se použijí v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="b3361-192">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="b3361-193">Naklonujte úložiště [partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="b3361-193">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="b3361-194">Otevřete projekt *PartnerConsent* , který se nachází v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři.</span><span class="sxs-lookup"><span data-stu-id="b3361-194">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="b3361-195">Naplnit nastavení aplikace nalezené v souboru [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)</span><span class="sxs-lookup"><span data-stu-id="b3361-195">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

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
    > <span data-ttu-id="b3361-196">Citlivé informace, jako jsou tajné klíče aplikace, by neměly být uloženy v konfiguračních souborech.</span><span class="sxs-lookup"><span data-stu-id="b3361-196">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="b3361-197">To bylo provedeno, protože se jedná o ukázkovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b3361-197">It was done here because this is a sample application.</span></span> <span data-ttu-id="b3361-198">V produkční aplikaci důrazně doporučujeme použít ověřování založené na certifikátech.</span><span class="sxs-lookup"><span data-stu-id="b3361-198">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="b3361-199">Další informace najdete v tématu [Key Vault ověřování certifikátů](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span><span class="sxs-lookup"><span data-stu-id="b3361-199">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="b3361-200">Když spustíte tento ukázkový projekt, zobrazí se výzva k ověření.</span><span class="sxs-lookup"><span data-stu-id="b3361-200">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="b3361-201">Po úspěšném ověření se z Azure AD vyžádá přístupový token.</span><span class="sxs-lookup"><span data-stu-id="b3361-201">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="b3361-202">Informace vrácené z Azure AD obsahují obnovovací token, který je uložený v nakonfigurované instanci Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b3361-202">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="b3361-203">Ověřování poskytovatele Cloud Solution Provider</span><span class="sxs-lookup"><span data-stu-id="b3361-203">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="b3361-204">Partneři poskytovatele Cloud Solution Provider můžou použít obnovovací token získaný prostřednictvím procesu [souhlasu s partnerem](#partner-consent) .</span><span class="sxs-lookup"><span data-stu-id="b3361-204">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="b3361-205">Ukázky pro ověřování poskytovatele Cloud Solution Provider</span><span class="sxs-lookup"><span data-stu-id="b3361-205">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="b3361-206">Abychom pomohli partnerům pochopit, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky.</span><span class="sxs-lookup"><span data-stu-id="b3361-206">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="b3361-207">Při implementaci vhodného řešení ve vašem prostředí je důležité vyvíjet řešení, které je stížností se standardy kódování a zásadami zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="b3361-207">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="b3361-208">.NET (ověřování CSP)</span><span class="sxs-lookup"><span data-stu-id="b3361-208">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="b3361-209">Pokud jste to ještě neudělali, proveďte [proces souhlasu s partnerem](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="b3361-209">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="b3361-210">Naklonujte úložiště s možností [partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) pomocí sady Visual Studio nebo následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="b3361-210">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="b3361-211">Otevřete projekt, který se `CSPApplication` nachází v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři.</span><span class="sxs-lookup"><span data-stu-id="b3361-211">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="b3361-212">Aktualizujte nastavení aplikace nalezené v souboru [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) .</span><span class="sxs-lookup"><span data-stu-id="b3361-212">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="b3361-213">Nastavte příslušné hodnoty pro proměnné **PartnerId** a **KódZákazníka** , které se nacházejí v souboru [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="b3361-213">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="b3361-214">Když spustíte tento ukázkový projekt, získá obnovovací token získaný během procesu souhlasu s partnerem.</span><span class="sxs-lookup"><span data-stu-id="b3361-214">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="b3361-215">Pak se požádá o přístupový token, který bude komunikovat s SDK partnerského centra za jménem partnera.</span><span class="sxs-lookup"><span data-stu-id="b3361-215">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="b3361-216">Nakonec vyžaduje přístupový token, který bude komunikovat s Microsoft Graph jménem zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b3361-216">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="b3361-217">Java (ověřování CSP)</span><span class="sxs-lookup"><span data-stu-id="b3361-217">Java (CSP authentication)</span></span>

1. <span data-ttu-id="b3361-218">Pokud jste to ještě neudělali, proveďte [proces souhlasu s partnerem](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="b3361-218">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="b3361-219">Naklonujte úložiště [partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí sady Visual Studio nebo následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="b3361-219">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="b3361-220">Otevřete projekt, který se `cspsample` nachází v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři.</span><span class="sxs-lookup"><span data-stu-id="b3361-220">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="b3361-221">Aktualizujte nastavení aplikace nalezené v souboru [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) .</span><span class="sxs-lookup"><span data-stu-id="b3361-221">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="b3361-222">Když spustíte tento ukázkový projekt, získá obnovovací token získaný během procesu souhlasu s partnerem.</span><span class="sxs-lookup"><span data-stu-id="b3361-222">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="b3361-223">Pak se požádá o přístupový token, který bude komunikovat s SDK partnerského centra za jménem partnera.</span><span class="sxs-lookup"><span data-stu-id="b3361-223">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="b3361-224">Volitelné – Odkomentujte volání funkcí *RunAzureTask* a *RunGraphTask* , pokud chcete zjistit, jak pracovat s Azure Resource Manager a Microsoft Graph jménem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b3361-224">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="b3361-225">Ověřování poskytovatele ovládacích panelů</span><span class="sxs-lookup"><span data-stu-id="b3361-225">Control Panel Provider authentication</span></span>

<span data-ttu-id="b3361-226">Dodavatelé ovládacích panelů potřebují, aby každý partner, který podporuje, prováděli proces [souhlasu s partnerem](#partner-consent) .</span><span class="sxs-lookup"><span data-stu-id="b3361-226">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="b3361-227">Po dokončení tohoto procesu se k přístupu k REST API partnerského centra a rozhraní .NET API použije aktualizační token získaný prostřednictvím tohoto procesu.</span><span class="sxs-lookup"><span data-stu-id="b3361-227">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="b3361-228">Ukázky pro ověřování poskytovatele na panelu cloudu</span><span class="sxs-lookup"><span data-stu-id="b3361-228">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="b3361-229">Aby mohli prodejci v Ovládacích panelech porozumět tomu, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky.</span><span class="sxs-lookup"><span data-stu-id="b3361-229">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="b3361-230">Při implementaci vhodného řešení ve vašem prostředí je důležité vyvíjet řešení, které je stížností se standardy kódování a zásadami zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="b3361-230">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="b3361-231">.NET (ověřování CPV)</span><span class="sxs-lookup"><span data-stu-id="b3361-231">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="b3361-232">Vytvořte a nasaďte proces pro partnery poskytovatele Cloud Solution Provider a poskytněte odpovídající souhlas.</span><span class="sxs-lookup"><span data-stu-id="b3361-232">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="b3361-233">Další informace najdete v tématu o [souhlasu partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="b3361-233">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b3361-234">Přihlašovací údaje uživatele z partnera poskytovatele Cloud Solution Provider by se neměly ukládat.</span><span class="sxs-lookup"><span data-stu-id="b3361-234">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="b3361-235">Obnovovací token získaný prostřednictvím procesu souhlasu s partnerem by měl být uložen a použit k vyžádání přístupových tokenů pro interakci s jakýmkoli rozhraním API společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b3361-235">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="b3361-236">Naklonujte úložiště s možností [partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) pomocí sady Visual Studio nebo následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="b3361-236">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="b3361-237">Otevřete projekt, který se `CPVApplication` nachází v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři.</span><span class="sxs-lookup"><span data-stu-id="b3361-237">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="b3361-238">Aktualizujte nastavení aplikace nalezené v souboru [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) .</span><span class="sxs-lookup"><span data-stu-id="b3361-238">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="b3361-239">Nastavte příslušné hodnoty pro proměnné **PartnerId** a **KódZákazníka** , které se nacházejí v souboru [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="b3361-239">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="b3361-240">Když spustíte tento ukázkový projekt, získá obnovovací token pro zadaného partnera.</span><span class="sxs-lookup"><span data-stu-id="b3361-240">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="b3361-241">Pak požádá o přístupový token pro přístup k partnerskému centru a k Azure AD Graph jménem partnera.</span><span class="sxs-lookup"><span data-stu-id="b3361-241">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="b3361-242">Další úloha, kterou provede, je odstranění a vytvoření oprávnění udělených pro tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b3361-242">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="b3361-243">Vzhledem k tomu, že mezi dodavatelem ovládacího panelu a zákazníkem neexistuje žádný vztah, musí být tato oprávnění přidána pomocí rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b3361-243">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="b3361-244">Následující příklad ukazuje, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="b3361-244">The following example shows how to accomplish that.</span></span>

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

<span data-ttu-id="b3361-245">Po navázání těchto oprávnění ukázka provede operace pomocí Azure AD Graph jménem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b3361-245">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="b3361-246">Java (ověřování CPV)</span><span class="sxs-lookup"><span data-stu-id="b3361-246">Java (CPV authentication)</span></span>

1. <span data-ttu-id="b3361-247">Vytvořte a nasaďte proces pro partnery poskytovatele Cloud Solution Provider a poskytněte odpovídající souhlas.</span><span class="sxs-lookup"><span data-stu-id="b3361-247">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="b3361-248">Další informace a příklad najdete v tématu o [souhlasu partnera](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="b3361-248">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b3361-249">Přihlašovací údaje uživatele z partnera poskytovatele Cloud Solution Provider by se neměly ukládat.</span><span class="sxs-lookup"><span data-stu-id="b3361-249">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="b3361-250">Obnovovací token získaný prostřednictvím procesu souhlasu s partnerem by měl být uložen a použit k vyžádání přístupových tokenů pro interakci s jakýmkoli rozhraním API společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b3361-250">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="b3361-251">Naklonujte úložiště [partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="b3361-251">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="b3361-252">Otevřete projekt, který se `cpvsample` nachází v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři.</span><span class="sxs-lookup"><span data-stu-id="b3361-252">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="b3361-253">Aktualizujte nastavení aplikace nalezené v souboru [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) .</span><span class="sxs-lookup"><span data-stu-id="b3361-253">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

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

    <span data-ttu-id="b3361-254">Hodnota `partnercenter.displayName` by měla být zobrazovaným názvem vaší aplikace Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b3361-254">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="b3361-255">Nastavte příslušné hodnoty pro proměnné **partnerId** a **KódZákazníka** , které se nacházejí v souboru [program. Java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) .</span><span class="sxs-lookup"><span data-stu-id="b3361-255">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="b3361-256">Když spustíte tento ukázkový projekt, získá obnovovací token pro zadaného partnera.</span><span class="sxs-lookup"><span data-stu-id="b3361-256">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="b3361-257">Potom vyžaduje přístupový token pro přístup k partnerskému centru jménem partnera.</span><span class="sxs-lookup"><span data-stu-id="b3361-257">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="b3361-258">Další úloha, kterou provede, je odstranění a vytvoření oprávnění udělených pro tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b3361-258">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="b3361-259">Vzhledem k tomu, že mezi dodavatelem ovládacího panelu a zákazníkem neexistuje žádný vztah, musí být tato oprávnění přidána pomocí rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b3361-259">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="b3361-260">Následující příklad ukazuje, jak udělit oprávnění.</span><span class="sxs-lookup"><span data-stu-id="b3361-260">The following example shows how to grant the permissions.</span></span>

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

<span data-ttu-id="b3361-261">Pokud chcete vidět, jak pracovat s Azure Resource Manager a Microsoft Graph jménem zákazníka, odkomentujte volání funkcí *RunAzureTask* a *RunGraphTask* .</span><span class="sxs-lookup"><span data-stu-id="b3361-261">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
