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
# <a name="partner-center-authentication"></a>Ověřování v Partnerském centru

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Partnerské centrum k ověřování využívá Azure Active Directory. Při práci s rozhraním API, sadou SDK nebo modulem PowerShellu Partnerského centra musíte správně nakonfigurovat aplikaci Azure AD a pak požádat o přístupový token. Přístupové tokeny získané pouze pomocí aplikace nebo ověřování aplikací a uživatelů je možné použít s Partnerské centrum. Je však potřeba zvážit dvě důležité položky.

- Vícefaktorové ověřování použijte při přístupu k rozhraní PARTNERSKÉ CENTRUM API pomocí ověřování aplikací a uživatelů. Další informace o této změně najdete v tématu [Povolení zabezpečeného aplikačního modelu](enable-secure-app-model.md).

- Ne všechny operace, které rozhraní API Partnerské centrum podporuje pouze ověřování aplikací. Existují určité scénáře, ve kterých budete muset použít ověřování aplikací a uživatelů. Pod *nadpisem Požadavky* v každém článku [najdete](scenarios.md)dokumentaci, která uvádí, jestli se podporuje jenom ověřování aplikací, ověřování aplikací a uživatelů nebo obojí.

## <a name="initial-setup"></a>Počáteční nastavení

1. Nejprve se musíte ujistit, že máte primární účet Partnerské centrum i účet sandboxu pro integraci Partnerské centrum účet. Další informace najdete v tématu [Nastavení účtů Partnerské centrum přístup přes rozhraní API.](set-up-api-access-in-partner-center.md) Poznamenejte si ID registrace aplikace Azure AAD a tajný klíč (tajný kód klienta se vyžaduje jenom pro identifikaci aplikace) pro primární účet i účet sandboxu pro integraci.

2. Přihlaste se k Azure AD z Azure Portal. V **části** Oprávnění k jiným aplikacím nastavte oprávnění pro **Windows Azure Active Directory** na Delegovaná oprávnění a vyberte Přístup k adresáři jako přihlášený **uživatel** a Přihlásit se a Číst **profil uživatele.** 

3. V Azure Portal přidat **aplikaci**. Vyhledejte "Microsoft Partnerské centrum", což je aplikace Microsoft Partnerské centrum. **Delegovaná oprávnění nastavte** **na Access Partnerské centrum API.** Pokud používáte nástroj pro Partnerské centrum Microsoft Cloud Germany nebo Partnerské centrum pro Microsoft Cloud for US Government, je tento krok povinný. Pokud používáte globální instanci Partnerské centrum, je tento krok volitelný. Partneři CSP mohou pomocí funkce Správa aplikací na Partnerské centrum Portal obejít tento krok pro Partnerské centrum instanci.

## <a name="app-only-authentication"></a>Ověřování pouze na základě aplikace

Pokud chcete pro přístup k modulu Partnerské centrum REST API, .NET API, Java API nebo PowerShellu použít ověřování jenom pro aplikace, můžete to udělat podle následujících pokynů.

## <a name="net-app-only-authentication"></a>.NET (ověřování pouze na základě aplikace)

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

## <a name="java-app-only-authentication"></a>Java (ověřování pouze na základě aplikace)

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

## <a name="rest-app-only-authentication"></a>REST (ověřování pouze na základě aplikace)

### <a name="rest-request"></a>Požadavek REST

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

### <a name="rest-response"></a>Odpověď REST

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>Ověřování aplikací a uživatelů

V minulosti [](https://tools.ietf.org/html/rfc6749#section-4.3) se k vyžádání přístupového tokenu pro použití s modulem Partnerské centrum REST API, .NET API, Java API nebo PowerShell použilo udělení přihlašovacích údajů vlastníka prostředku. Tato metoda se použila k vyžádání přístupového tokenu od Azure Active Directory pomocí identifikátoru klienta a přihlašovacích údajů uživatele. Tento přístup ale už nebude fungovat, protože Partnerské centrum vyžaduje vícefaktorové ověřování při použití ověřování aplikací a uživatelů. Pro splnění tohoto požadavku společnost Microsoft zavedla zabezpečenou a škálovatelnou rozhraní pro ověřování partnerů Cloud Solution Provider (CSP) a dodavatelů ovládacích panelů (CPV) pomocí vícefaktorového ověřování. Tato rozhraní se označuje jako Model zapezpečených aplikací a skládá se z procesu souhlasu a žádosti o přístupový token pomocí obnovovacího tokenu.

### <a name="partner-consent"></a>Souhlas partnera

Proces souhlasu partnera je interaktivní proces, ve kterém se partner ověřuje pomocí vícefaktorového ověřování, souhlasí s aplikací a obnovovací token je uložený v zabezpečeném úložišti, jako je Azure Key Vault. Pro tento proces doporučujeme použít vyhrazený účet pro účely integrace.

> [!IMPORTANT]
> Pro účet služby použitý v procesu souhlasu partnera by mělo být povolené vhodné řešení vícefaktorového ověřování. Pokud tomu tak není, výsledný obnovovací token nebude splňovat požadavky na zabezpečení.

### <a name="samples-for-app--user-authentication"></a>Ukázky ověřování aplikací a uživatelů

Proces souhlasu partnera je možné provést několika způsoby. Aby partneři pochopili, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky. Při implementaci vhodného řešení ve vašem prostředí je důležité vyvinout řešení, které je v souladu s vašimi standardy kódování a zásadami zabezpečení.

## <a name="net-appuser-authentication"></a>.NET (ověřování aplikací a uživatelů)

Ukázkový [projekt souhlasu](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) partnera ukazuje, jak využít web vyvinutý pomocí ASP.NET k zachycení souhlasu, vyžádání obnovovacího tokenu a jeho bezpečnému uložení v Azure Key Vault. Provedením následujících kroků vytvořte požadované součásti pro tuto ukázku.

1. Vytvořte instanci služby Azure Key Vault pomocí Azure Portal nebo následujících příkazů PowerShellu. Před spuštěním příkazu nezapomeňte odpovídajícím způsobem upravit hodnoty parametrů. Název trezoru musí být jedinečný.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Další informace o vytvoření Azure Key Vault najdete v tématu Rychlý [start:](/azure/key-vault/quick-create-portal) Nastavení a načtení tajného klíče ze služby Azure Key Vault pomocí Azure Portal nebo Rychlý start: Nastavení a načtení tajného klíče z [Azure Key Vault pomocí PowerShellu.](/azure/key-vault/quick-create-powershell) Potom nastavte a načtěte tajný kód.

2. Vytvořte aplikaci Azure AD a klíč pomocí Azure Portal nebo následujících příkazů.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Nezapomeňte si poznamenat hodnoty identifikátoru a tajného kódu aplikace, protože je použijete v následujících krocích.

3. Udělte nově vytvořené aplikaci Azure AD oprávnění ke čtení tajných kódů pomocí Azure Portal nebo následujících příkazů.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Vytvořte aplikaci Azure AD, která je nakonfigurovaná pro Partnerské centrum. K dokončení tohoto kroku proveďte následující akce.

    - Přejděte na [funkci Správa aplikací řídicího](https://partner.microsoft.com/pcv/apiintegration/appmanagement) panelu Partnerské centrum.
    - Vyberte *Přidat novou webovou aplikaci* a vytvořte novou aplikaci Azure AD.

    Nezapomeňte zdokumentovat *hodnoty ID aplikace,**ID účtu** a *Klíč,* protože je použijete v následujících krocích.

5. [Naklonovat úložiště Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) Visual Studio nebo následujícím příkazem.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Otevřete projekt *PartnerConsent* v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři .

7. Vyplňte nastavení aplikace nalezená v [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

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
    > Citlivé informace, jako jsou tajné kódy aplikací, by neměly být uložené v konfiguračních souborech. Bylo to tady, protože se jedná o ukázkovou aplikaci. U produkční aplikace důrazně doporučujeme používat ověřování pomocí certifikátů. Další informace najdete v tématu Přihlašovací [údaje certifikátu pro ověřování aplikací.]( /azure/active-directory/develop/active-directory-certificate-credentials)

8. Při spuštění tohoto ukázkového projektu se zobrazí výzva k ověření. Po úspěšném ověření se z Azure AD vyžádá přístupový token. Informace vrácené z Azure AD zahrnují obnovovací token, který je uložený v nakonfigurované instanci Azure Key Vault.

## <a name="java-appuser-authentication"></a>Java (ověřování aplikací a uživatelů)

Ukázkový [projekt souhlasu](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) partnera ukazuje, jak využít web vyvinutý pomocí JSP k zachycení souhlasu, vyžádání obnovovacího tokenu a zabezpečeného úložiště v Azure Key Vault. Následujícím způsobem vytvořte požadované součásti pro tuto ukázku.

1. Vytvořte instanci služby Azure Key Vault pomocí Azure Portal nebo následujících příkazů PowerShellu. Před spuštěním příkazu nezapomeňte odpovídajícím způsobem upravit hodnoty parametrů. Název trezoru musí být jedinečný.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Další informace o vytvoření Azure Key Vault najdete v tématu Rychlý [start:](/azure/key-vault/quick-create-portal) Nastavení a načtení tajného klíče ze služby Azure Key Vault pomocí Azure Portal nebo Rychlý start: Nastavení a načtení tajného klíče z [Azure Key Vault pomocí PowerShellu.](/azure/key-vault/quick-create-powershell)

2. Vytvořte aplikaci Azure AD a klíč pomocí Azure Portal nebo následujících příkazů.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Nezapomeňte zdokumentovat hodnoty identifikátoru a tajného kódu aplikace, protože je použijete v následujících krocích.

3. Udělte nově vytvořené aplikaci Azure AD oprávnění ke čtení tajných kódů pomocí Azure Portal nebo následujících příkazů.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Vytvořte aplikaci Azure AD, která je nakonfigurovaná pro Partnerské centrum. K dokončení tohoto kroku proveďte následující kroky.

    - Přejděte na [funkci Správa aplikací řídicího](https://partner.microsoft.com/pcv/apiintegration/appmanagement) panelu Partnerské centrum.
    - Vyberte *Přidat novou webovou aplikaci* a vytvořte novou aplikaci Azure AD.

    Nezapomeňte zdokumentovat *hodnoty ID aplikace,**ID účtu** a *Klíč,* protože je použijete v následujících krocích.

5. [Naklonování úložiště Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí následujícího příkazu

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Otevřete projekt *PartnerConsent* v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři .

7. Naplnění nastavení aplikace nalezených v [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) souboru

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
    > Citlivé informace, jako jsou tajné kódy aplikací, by neměly být uložené v konfiguračních souborech. Bylo to tady, protože se jedná o ukázkovou aplikaci. U produkční aplikace důrazně doporučujeme používat ověřování na základě certifikátů. Další informace najdete v tématu [Key Vault certifikátu](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).

8. Při spuštění tohoto ukázkového projektu se zobrazí výzva k ověření. Po úspěšném ověření se z Azure AD vyžádá přístupový token. Informace vrácené z Azure AD zahrnují obnovovací token, který je uložený v nakonfigurované instanci Azure Key Vault.

## <a name="cloud-solution-provider-authentication"></a>Cloud Solution Provider ověřování

Cloud Solution Provider partneři mohou použít obnovovací token získaný prostřednictvím procesu [souhlasu partnera.](#partner-consent)

### <a name="samples-for-cloud-solution-provider-authentication"></a>Ukázky pro Cloud Solution Provider ověřování

Aby partneři pochopili, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky. Při implementaci vhodného řešení ve vašem prostředí je důležité vyvinout řešení, které je v souladu s vašimi standardy kódování a zásadami zabezpečení.

## <a name="net-csp-authentication"></a>.NET (ověřování CSP)

1. Pokud jste to ještě neudělali, proveďte proces [souhlasu partnera](#partner-consent).

2. [Naklonování úložiště Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) pomocí Visual Studio nebo následujícího příkazu

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Otevřete projekt `CSPApplication` nalezený v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři .

4. Aktualizujte nastavení aplikace, které najdete v [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) souboru.

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

5. Nastavte odpovídající hodnoty pro proměnné **PartnerId** a **CustomerId** v souboru [Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Když tento ukázkový projekt spustíte, získá obnovovací token získaný během procesu souhlasu partnera. Pak požádá o přístupový token k interakci s SDK pro Partnerské centrum jménem partnera. Nakonec požádá o přístupový token pro interakci s Microsoftem Graph jménem zadaného zákazníka.

## <a name="java-csp-authentication"></a>Java (ověřování CSP)

1. Pokud jste to ještě neudělali, proveďte proces [souhlasu partnera](#partner-consent).

2. [Naklonování úložiště Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí Visual Studio nebo následujícího příkazu

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Otevřete projekt `cspsample` nalezený v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři .

4. Aktualizujte nastavení aplikace v souboru [application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties)

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. Když tento ukázkový projekt spustíte, získá obnovovací token získaný během procesu souhlasu partnera. Pak požádá o přístupový token k interakci s SDK pro Partnerské centrum jménem partnera.

6. Volitelné – odkomentování volání funkcí *RunAzureTask* a *RunGraphTask,* pokud chcete vidět, jak pracovat s Azure Resource Manager a Microsoft Graph jménem zákazníka.

## <a name="control-panel-provider-authentication"></a>Ovládací panely zprostředkovatele ověřování

Dodavatelé ovládacích panelů musí mít každého partnera, který podporují, aby mohli provést [proces souhlasu partnera.](#partner-consent) Po dokončení se obnovovací token získaný prostřednictvím tohoto procesu použije pro přístup k Partnerské centrum REST API a rozhraní .NET API.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Ukázky pro ověřování poskytovatele cloudových panelů

Aby dodavatelé ovládacích panelů pochopili, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky. Při implementaci vhodného řešení ve vašem prostředí je důležité vyvinout řešení, které je v souladu s vašimi standardy kódování a zásadami zabezpečení.

## <a name="net-cpv-authentication"></a>.NET (ověřování CPV)

1. Vytvořte a nasaďte proces, který Cloud Solution Provider partnerům s odpovídajícím souhlasem. Další informace najdete v příkladu se [souhlasem partnera.](#partner-consent)

    > [!IMPORTANT]
    > Přihlašovací údaje uživatele od Cloud Solution Provider by se neměly ukládat. Obnovovací token získaný prostřednictvím procesu souhlasu partnera by se měl uložit a použít k vyžádání přístupových tokenů pro interakci s libovolným rozhraním API Microsoftu.

2. [Naklonování úložiště Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) pomocí Visual Studio nebo následujícího příkazu

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Otevřete projekt `CPVApplication` nalezený v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři .

4. Aktualizujte nastavení aplikace, které najdete v [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) souboru.

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

5. Nastavte odpovídající hodnoty pro proměnné **PartnerId** a **CustomerId** v souboru [Program.cs.](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Když tento ukázkový projekt spustíte, získá obnovovací token pro zadaného partnera. Potom požádá o přístupový token pro přístup Partnerské centrum a Azure AD Graph jménem partnera. Dalším úkolem, který provede, je odstranění a vytvoření udělených oprávnění do tenanta zákazníka. Vzhledem k tomu, že mezi dodavatelem ovládacích panelů a zákazníkem neexistuje žádný vztah, je potřeba tato oprávnění přidat pomocí Partnerské centrum API. Následující příklad ukazuje, jak toho dosáhnout.

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

Po navázání těchto oprávnění ukázka provede operace pomocí služby Azure AD Graph jménem zákazníka.

## <a name="java-cpv-authentication"></a>Java (ověřování CPV)

1. Vytvořte a nasaďte proces, který Cloud Solution Provider partnerům s odpovídajícím souhlasem. Další informace a příklad najdete v tématu o [souhlasu partnera.](#partner-consent)

    > [!IMPORTANT]
    > Přihlašovací údaje uživatele od Cloud Solution Provider by se neměly ukládat. Obnovovací token získaný prostřednictvím procesu souhlasu partnera by se měl uložit a použít k vyžádání přístupových tokenů pro interakci s libovolným rozhraním API Microsoftu.

2. [Naklonování úložiště Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí následujícího příkazu

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Otevřete projekt `cpvsample` nalezený v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři .

4. Aktualizujte nastavení aplikace v souboru [application.properties.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties)

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

    Hodnota by `partnercenter.displayName` měla být zobrazovaný název vaší aplikace marketplace.

5. Nastavte odpovídající hodnoty pro **proměnné partnerId** a **customerId** v souboru [Program.java.](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java)

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. Když tento ukázkový projekt spustíte, získá obnovovací token pro zadaného partnera. Potom požádá o přístupový token pro přístup Partnerské centrum jménem partnera. Dalším úkolem, který provede, je odstranění a vytvoření udělených oprávnění do tenanta zákazníka. Vzhledem k tomu, že mezi dodavatelem ovládacích panelů a zákazníkem neexistuje žádný vztah, je potřeba tato oprávnění přidat pomocí Partnerské centrum API. Následující příklad ukazuje, jak udělit oprávnění.

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

Odkomentování volání funkcí *RunAzureTask* a *RunGraphTask,* pokud chcete vidět, jak pracovat s Azure Resource Manager a Microsoft Graph jménem zákazníka.
