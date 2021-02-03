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
# <a name="partner-center-authentication"></a>Ověřování v Partnerském centru

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Partnerské centrum k ověřování využívá Azure Active Directory. Při práci s rozhraním API, sadou SDK nebo modulem PowerShellu Partnerského centra musíte správně nakonfigurovat aplikaci Azure AD a pak požádat o přístupový token. Přístupové tokeny získané jenom pro aplikace nebo ověřování pomocí aplikace a uživatele se dají použít s partnerským centrem. Existují však dvě důležité položky, které je třeba vzít v úvahu.

- Použijte vícefaktorové ověřování při přístupu k rozhraní API partnerského centra pomocí ověřování aplikace a uživatele. Další informace o této změně najdete v tématu [Povolení zabezpečení aplikačního modelu](enable-secure-app-model.md).

- Ne všechny operace: rozhraní API partnerského centra podporuje pouze ověřování aplikace. Existují některé scénáře, kdy budete muset použít aplikaci a ověřování uživatelů. V nadpisu *požadavky* každého [článku](scenarios.md)najdete dokumentaci s informací, jestli jsou podporované jenom ověřování, aplikace + ověřování uživatelů nebo obojí.

## <a name="initial-setup"></a>Počáteční nastavení

1. Abyste mohli začít, musíte se ujistit, že máte primární účet partnerského centra a účet partnerského centra pro integraci izolovaného prostoru (sandbox). Další informace najdete v tématu [Nastavení účtů partnerského centra pro přístup přes rozhraní API](set-up-api-access-in-partner-center.md). Poznamenejte si ID registrace a tajný kód aplikace Azure AAD (pro identifikaci aplikace se vyžaduje tajný klíč klienta) pro váš primární účet i váš účet izolovaného prostoru (sandbox).

2. Přihlaste se k Azure AD z Azure Portal. V **oprávněních k ostatním aplikacím** nastavte oprávnění pro **Windows Azure Active Directory** na **delegovaná oprávnění** a **jako přihlášeného uživatele vyberte přístup k adresáři** , **Přihlaste se a přečtěte si profil uživatele**.

3. V Azure Portal **přidejte aplikaci**. Vyhledejte "partnerské Centrum Microsoftu", což je aplikace partnerského centra Microsoftu. Nastavte **delegovaná oprávnění** pro **přístup k rozhraní API partnerského centra**. Pokud používáte partnerské Centrum pro Microsoft Cloud Německo nebo partnerské Centrum pro Microsoft Cloud pro státní správu USA, je tento krok povinný. Pokud používáte globální instanci partnerského centra, je tento krok nepovinný. Partneři CSP můžou pomocí funkce správy aplikací na portálu partnerského centra obejít tento krok pro globální instanci partnerského centra.

## <a name="app-only-authentication"></a>Ověřování pouze pro aplikace

Pokud chcete používat ověřování jenom pro aplikace pro přístup k REST API partnerských Center, rozhraní API .NET, Java API nebo modul PowerShellu, můžete to udělat pomocí následujících pokynů.

## <a name="net-app-only-authentication"></a>.NET (ověřování pouze pro aplikace)

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

## <a name="java-app-only-authentication"></a>Java (ověřování pouze aplikací)

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

## <a name="rest-app-only-authentication"></a>REST (ověřování pouze pro aplikace)

### <a name="rest-request"></a>Žádost REST

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

Historické [přihlašovací údaje pro heslo vlastníka prostředku](https://tools.ietf.org/html/rfc6749#section-4.3) se použily k vyžádání přístupového tokenu pro použití s REST API partnerských Center, rozhraní API .NET, Java API nebo modul PowerShellu. Tato metoda se použila k vyžádání přístupového tokenu z Azure Active Directory pomocí identifikátoru klienta a přihlašovacích údajů uživatele. Tento přístup ale už nebude fungovat, protože partnerské Centrum vyžaduje vícefaktorové ověřování, když se používá ověřování aplikací a uživatelů. Pro splnění tohoto požadavku společnost Microsoft zavedla zabezpečenou, škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) pomocí služby Multi-Factor Authentication. Tato architektura se označuje jako model zabezpečené aplikace a skládá se z procesu souhlasu a žádosti o přístupový token pomocí obnovovacího tokenu.

### <a name="partner-consent"></a>Souhlas partnera

Proces souhlasu s partnerem je interaktivní proces, ve kterém se partner ověřuje pomocí služby Multi-Factor Authentication, souhlasí s aplikací a je uložený v zabezpečeném úložišti, jako je Azure Key Vault. Pro účely tohoto procesu doporučujeme použít vyhrazený účet pro účely integrace.

> [!IMPORTANT]
> Pro účet služby, který se používá v procesu souhlasu s partnerem, by mělo být povoleno příslušné řešení Multi-Factor Authentication. Pokud není, výsledný obnovovací token nebude kompatibilní s požadavky na zabezpečení.

### <a name="samples-for-app--user-authentication"></a>Ukázky pro ověřování aplikací a uživatelů

Proces souhlasu s partnerem je možné provést několika způsoby. Abychom pomohli partnerům pochopit, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky. Při implementaci vhodného řešení ve vašem prostředí je důležité vyvíjet řešení, které je stížností se standardy kódování a zásadami zabezpečení.

## <a name="net-appuser-authentication"></a>.NET (ověřování aplikací a uživatelů)

Ukázkový projekt [souhlasu s partnerem](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) ukazuje, jak používat web vyvinutý pomocí ASP.NET k zachycení souhlasu, vyžádání obnovovacího tokenu a bezpečnému uložení v Azure Key Vault. Chcete-li vytvořit požadované požadavky pro tuto ukázku, proveďte následující kroky.

1. Vytvořte instanci Azure Key Vault pomocí Azure Portal nebo následujících příkazů PowerShellu. Před provedením příkazu nezapomeňte odpovídajícím způsobem upravit hodnoty parametrů. Název trezoru musí být jedinečný.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Další informace o vytváření Azure Key Vault najdete v tématu [rychlý Start: nastavení a načtení tajného klíče z Azure Key Vault pomocí Azure Portal](/azure/key-vault/quick-create-portal) nebo [rychlý Start: nastavení a načtení tajného klíče ze Azure Key Vault pomocí prostředí PowerShell](/azure/key-vault/quick-create-powershell). Pak nastavte a načtěte tajný klíč.

2. Vytvořte aplikaci Azure AD a klíč pomocí Azure Portal nebo následujících příkazů.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Nezapomeňte si poznamenat identifikátor aplikace a tajné hodnoty, protože se použijí v následujících krocích.

3. Udělte nově vytvořeným aplikacím Azure AD oprávnění číst tajné klíče pomocí Azure Portal nebo následujících příkazů.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Vytvořte aplikaci Azure AD, která je nakonfigurovaná pro partnerské Centrum. Provedením následujících akcí dokončete tento krok.

    - Přejděte do funkce [Správa aplikací](https://partner.microsoft.com/pcv/apiintegration/appmanagement) na řídicím panelu partnerského centra.
    - Klikněte na *Přidat novou webovou aplikaci* a vytvořte novou aplikaci Azure AD.

    Nezapomeňte zdokumentovat *ID aplikace** ID účtu * * a hodnoty *klíče* , protože se použijí v následujících krocích.

5. Pomocí sady Visual Studio naklonujte úložiště [partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) nebo použijte následující příkaz.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Otevřete projekt *PartnerConsent* , který se nachází v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři.

7. Naplňte nastavení aplikace nalezené v [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

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
    > Citlivé informace, jako jsou tajné klíče aplikace, by neměly být uloženy v konfiguračních souborech. To bylo provedeno, protože se jedná o ukázkovou aplikaci. V produkční aplikaci důrazně doporučujeme používat ověřování pomocí certifikátů. Další informace najdete v tématu [přihlašovací údaje certifikátu pro ověřování aplikací]( /azure/active-directory/develop/active-directory-certificate-credentials).

8. Když spustíte tento ukázkový projekt, zobrazí se výzva k ověření. Po úspěšném ověření se z Azure AD vyžádá přístupový token. Informace vrácené z Azure AD obsahují obnovovací token, který je uložený v nakonfigurované instanci Azure Key Vault.

## <a name="java-appuser-authentication"></a>Java (ověřování aplikací a uživatelů)

Ukázkový projekt [souhlasu s partnerem](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) ukazuje, jak používat web vyvinutý pomocí JSP k zachycení souhlasu, vyžádání obnovovacího tokenu a zabezpečeného úložiště v Azure Key Vault. Pro vytvoření požadovaných požadavků pro tuto ukázku proveďte následující kroky.

1. Vytvořte instanci Azure Key Vault pomocí Azure Portal nebo následujících příkazů PowerShellu. Před provedením příkazu nezapomeňte odpovídajícím způsobem upravit hodnoty parametrů. Název trezoru musí být jedinečný.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Další informace o vytváření Azure Key Vault najdete v tématu [rychlý Start: nastavení a načtení tajného klíče z Azure Key Vault pomocí Azure Portal](/azure/key-vault/quick-create-portal) nebo [rychlý Start: nastavení a načtení tajného klíče ze Azure Key Vault pomocí prostředí PowerShell](/azure/key-vault/quick-create-powershell).

2. Vytvořte aplikaci Azure AD a klíč pomocí Azure Portal nebo následujících příkazů.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Nezapomeňte zdokumentovat identifikátor aplikace a tajné hodnoty, protože budou použity v následujících krocích.

3. Udělte nově vytvořeným aplikacím Azure AD oprávnění číst tajné klíče pomocí Azure Portal nebo následujících příkazů.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Vytvořte aplikaci Azure AD, která je nakonfigurovaná pro partnerské Centrum. K dokončení tohoto kroku proveďte následující kroky.

    - Přejděte do funkce [Správa aplikací](https://partner.microsoft.com/pcv/apiintegration/appmanagement) na řídicím panelu partnerského centra.
    - Klikněte na *Přidat novou webovou aplikaci* a vytvořte novou aplikaci Azure AD.

    Nezapomeňte zdokumentovat *ID aplikace** ID účtu * * a hodnoty *klíče* , protože se použijí v následujících krocích.

5. Naklonujte úložiště [partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí následujícího příkazu.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Otevřete projekt *PartnerConsent* , který se nachází v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři.

7. Naplnit nastavení aplikace nalezené v souboru [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)

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
    > Citlivé informace, jako jsou tajné klíče aplikace, by neměly být uloženy v konfiguračních souborech. To bylo provedeno, protože se jedná o ukázkovou aplikaci. V produkční aplikaci důrazně doporučujeme použít ověřování založené na certifikátech. Další informace najdete v tématu [Key Vault ověřování certifikátů](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).

8. Když spustíte tento ukázkový projekt, zobrazí se výzva k ověření. Po úspěšném ověření se z Azure AD vyžádá přístupový token. Informace vrácené z Azure AD obsahují obnovovací token, který je uložený v nakonfigurované instanci Azure Key Vault.

## <a name="cloud-solution-provider-authentication"></a>Ověřování poskytovatele Cloud Solution Provider

Partneři poskytovatele Cloud Solution Provider můžou použít obnovovací token získaný prostřednictvím procesu [souhlasu s partnerem](#partner-consent) .

### <a name="samples-for-cloud-solution-provider-authentication"></a>Ukázky pro ověřování poskytovatele Cloud Solution Provider

Abychom pomohli partnerům pochopit, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky. Při implementaci vhodného řešení ve vašem prostředí je důležité vyvíjet řešení, které je stížností se standardy kódování a zásadami zabezpečení.

## <a name="net-csp-authentication"></a>.NET (ověřování CSP)

1. Pokud jste to ještě neudělali, proveďte [proces souhlasu s partnerem](#partner-consent).

2. Naklonujte úložiště s možností [partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) pomocí sady Visual Studio nebo následujícího příkazu.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Otevřete projekt, který se `CSPApplication` nachází v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři.

4. Aktualizujte nastavení aplikace nalezené v souboru [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) .

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

5. Nastavte příslušné hodnoty pro proměnné **PartnerId** a **KódZákazníka** , které se nacházejí v souboru [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) .

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Když spustíte tento ukázkový projekt, získá obnovovací token získaný během procesu souhlasu s partnerem. Pak se požádá o přístupový token, který bude komunikovat s SDK partnerského centra za jménem partnera. Nakonec vyžaduje přístupový token, který bude komunikovat s Microsoft Graph jménem zadaného zákazníka.

## <a name="java-csp-authentication"></a>Java (ověřování CSP)

1. Pokud jste to ještě neudělali, proveďte [proces souhlasu s partnerem](#partner-consent).

2. Naklonujte úložiště [partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí sady Visual Studio nebo následujícího příkazu.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Otevřete projekt, který se `cspsample` nachází v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři.

4. Aktualizujte nastavení aplikace nalezené v souboru [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) .

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. Když spustíte tento ukázkový projekt, získá obnovovací token získaný během procesu souhlasu s partnerem. Pak se požádá o přístupový token, který bude komunikovat s SDK partnerského centra za jménem partnera.

6. Volitelné – Odkomentujte volání funkcí *RunAzureTask* a *RunGraphTask* , pokud chcete zjistit, jak pracovat s Azure Resource Manager a Microsoft Graph jménem zákazníka.

## <a name="control-panel-provider-authentication"></a>Ověřování poskytovatele ovládacích panelů

Dodavatelé ovládacích panelů potřebují, aby každý partner, který podporuje, prováděli proces [souhlasu s partnerem](#partner-consent) . Po dokončení tohoto procesu se k přístupu k REST API partnerského centra a rozhraní .NET API použije aktualizační token získaný prostřednictvím tohoto procesu.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Ukázky pro ověřování poskytovatele na panelu cloudu

Aby mohli prodejci v Ovládacích panelech porozumět tomu, jak provést jednotlivé požadované operace, vyvinuli jsme následující ukázky. Při implementaci vhodného řešení ve vašem prostředí je důležité vyvíjet řešení, které je stížností se standardy kódování a zásadami zabezpečení.

## <a name="net-cpv-authentication"></a>.NET (ověřování CPV)

1. Vytvořte a nasaďte proces pro partnery poskytovatele Cloud Solution Provider a poskytněte odpovídající souhlas. Další informace najdete v tématu o [souhlasu partnera](#partner-consent).

    > [!IMPORTANT]
    > Přihlašovací údaje uživatele z partnera poskytovatele Cloud Solution Provider by se neměly ukládat. Obnovovací token získaný prostřednictvím procesu souhlasu s partnerem by měl být uložen a použit k vyžádání přístupových tokenů pro interakci s jakýmkoli rozhraním API společnosti Microsoft.

2. Naklonujte úložiště s možností [partner-Center-dotnet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) pomocí sady Visual Studio nebo následujícího příkazu.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. Otevřete projekt, který se `CPVApplication` nachází v `Partner-Center-DotNet-Samples\secure-app-model\keyvault` adresáři.

4. Aktualizujte nastavení aplikace nalezené v souboru [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) .

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

5. Nastavte příslušné hodnoty pro proměnné **PartnerId** a **KódZákazníka** , které se nacházejí v souboru [program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) .

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Když spustíte tento ukázkový projekt, získá obnovovací token pro zadaného partnera. Pak požádá o přístupový token pro přístup k partnerskému centru a k Azure AD Graph jménem partnera. Další úloha, kterou provede, je odstranění a vytvoření oprávnění udělených pro tenanta zákazníka. Vzhledem k tomu, že mezi dodavatelem ovládacího panelu a zákazníkem neexistuje žádný vztah, musí být tato oprávnění přidána pomocí rozhraní API partnerského centra. Následující příklad ukazuje, jak to provést.

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

Po navázání těchto oprávnění ukázka provede operace pomocí Azure AD Graph jménem zákazníka.

## <a name="java-cpv-authentication"></a>Java (ověřování CPV)

1. Vytvořte a nasaďte proces pro partnery poskytovatele Cloud Solution Provider a poskytněte odpovídající souhlas. Další informace a příklad najdete v tématu o [souhlasu partnera](#partner-consent).

    > [!IMPORTANT]
    > Přihlašovací údaje uživatele z partnera poskytovatele Cloud Solution Provider by se neměly ukládat. Obnovovací token získaný prostřednictvím procesu souhlasu s partnerem by měl být uložen a použit k vyžádání přístupových tokenů pro interakci s jakýmkoli rozhraním API společnosti Microsoft.

2. Naklonujte úložiště [partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) pomocí následujícího příkazu.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. Otevřete projekt, který se `cpvsample` nachází v `Partner-Center-Java-Samples\secure-app-model\keyvault` adresáři.

4. Aktualizujte nastavení aplikace nalezené v souboru [Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) .

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

    Hodnota `partnercenter.displayName` by měla být zobrazovaným názvem vaší aplikace Marketplace.

5. Nastavte příslušné hodnoty pro proměnné **partnerId** a **KódZákazníka** , které se nacházejí v souboru [program. Java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) .

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. Když spustíte tento ukázkový projekt, získá obnovovací token pro zadaného partnera. Potom vyžaduje přístupový token pro přístup k partnerskému centru jménem partnera. Další úloha, kterou provede, je odstranění a vytvoření oprávnění udělených pro tenanta zákazníka. Vzhledem k tomu, že mezi dodavatelem ovládacího panelu a zákazníkem neexistuje žádný vztah, musí být tato oprávnění přidána pomocí rozhraní API partnerského centra. Následující příklad ukazuje, jak udělit oprávnění.

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

Pokud chcete vidět, jak pracovat s Azure Resource Manager a Microsoft Graph jménem zákazníka, odkomentujte volání funkcí *RunAzureTask* a *RunGraphTask* .
