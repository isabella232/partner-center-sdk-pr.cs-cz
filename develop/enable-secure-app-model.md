---
title: Povolení zabezpečeného aplikačního modelu
description: Zabezpečte své Partnerské centrum a aplikace ovládacích panelů.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 3e153e1e7d4e38580d8cb39a3996e56365ff5fbe
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766852"
---
# <a name="enabling-the-secure-application-model-framework"></a>Povolení architektury zabezpečeného aplikačního modelu

**Platí pro:**

- Partnerské centrum

Microsoft zavádí zabezpečenou, škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) prostřednictvím architektury Microsoft Azure Multi-Factor Authentication (MFA).

Pomocí nového modelu můžete zvýšit zabezpečení pro volání Integration Center API pro partnery. Pomůže všem stranám (včetně Microsoftu, partnerům CSP a CPVs) chránit svá data infrastruktury a zákaznická data před bezpečnostními riziky.

## <a name="scope"></a>Obor

Tento článek se týká následujících aktérů:

- Dodavatelé ovládacích panelů (CPV)
  - Dodavatel ovládacích panelů (CPV) je nezávislý výrobce softwaru, který vyvíjí aplikace, které můžou partneři CSP integrovat s rozhraními API Partnerského centra.
  - Dodavatel ovládacích panelů (CPV) není partnerem CSP s přímým přístupem k řídicímu panelu pro Partnerské centrum ani rozhraním API Partnerského centra.

- Nepřímá poskytovatelé CSP a partneři CSP Direct, kteří používají ID aplikace + ověřování uživatelů a přímo integrují s rozhraními API partnerského centra.

## <a name="security-requirements"></a>Požadavky na zabezpečení

Podrobnosti o požadavcích na zabezpečení najdete v tématu [požadavky na zabezpečení partnerů](/partner-center/partner-security-requirements).

## <a name="secure-application-model"></a>Model zabezpečené aplikace

Aplikace z Marketplace potřebují zosobnit oprávnění partnera CSP pro volání rozhraní API Microsoftu. Bezpečnostní útoky na těchto citlivých aplikacích můžou vést k ohrožení zákaznických dat.

Přehled a podrobnosti nové architektury ověřování si můžete stáhnout v dokumentu Framework pro [model zabezpečených aplikací](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) . Tento dokument popisuje principy a osvědčené postupy pro zajištění trvalého a robustního zabezpečení aplikací pro Marketplace před ohroženími zabezpečení.

## <a name="samples"></a>ukázky

Následující dokumenty přehledu a ukázkový kód popisují, jak můžou partneři implementovat rozhraní zabezpečeného modelu aplikace:

- [Dokument s přehledem CPV](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [Dokument s přehledem CSP](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [Ukázky .NET](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Ukázky Java](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [Pokyny a ukázky pro REST](#rest)
- [Pokyny a ukázky prostředí PowerShell](#powershell)

## <a name="rest"></a>REST

Chcete-li provést volání REST pomocí rozhraní zabezpečeného modelu aplikace s ukázkovým kódem, postupujte následovně:

1. [Vytvoření webové aplikace](#create-a-web-app)

2. [Získání autorizačního kódu](#get-authorization-code)

3. [Získat obnovovací token](#get-refresh-token)

4. [Získání přístupového tokenu](#get-access-token)

5. [Zavolání rozhraní API Partnerského centra](#make-partner-center-api-calls)

> [!TIP]
> K získání autorizačního kódu a obnovovacího tokenu můžete použít modul PowerShell pro partnerských Center. Tuto možnost můžete vybrat místo kroků 2 a 3. Další informace najdete v [části a příklady prostředí PowerShell](#powershell).

### <a name="create-a-web-app"></a>Vytvoření webové aplikace

Před tím, než zahájíte volání REST, je nutné vytvořit a zaregistrovat webovou aplikaci v partnerském centru.

1. Přihlaste se na [Azure Portal](https://portal.azure.com).

2. Vytvořte aplikaci Azure Active Directory (Azure AD).

3. Udělte delegovaným aplikacím oprávnění k následujícím prostředkům *v závislosti na požadavcích vaší aplikace*. V případě potřeby můžete přidat další delegovaná oprávnění pro prostředky aplikace.

   1. **Partnerské centrum Microsoftu** (někteří klienti to ukazují jako **SampleBECApp**)

   2. **Rozhraní API pro správu Azure** (Pokud plánujete volat rozhraní API Azure)

   3. **Windows Azure Active Directory**

4. Ujistěte se, že adresa URL domů vaší aplikace je nastavená na koncový bod, ve kterém běží živá webová aplikace. Tato aplikace bude muset přijmout [autorizační kód](#get-authorization-code) z přihlašovacího volání služby Azure AD. Například v příkladu kódu v [následující části](#get-authorization-code)je webová aplikace spuštěna v `https://localhost:44395/` .

5. Všimněte si následujících informací z nastavení vaší webové aplikace ve službě Azure AD:

   - ID aplikace
   - Tajný kód aplikace

> [!NOTE]
> Doporučuje se [použít certifikát jako tajný kód aplikace](/azure/active-directory/develop/active-directory-certificate-credentials). Můžete ale také vytvořit klíč aplikace v Azure Portal. Vzorový kód v [následující části](#get-authorization-code) používá klíč aplikace.

### <a name="get-authorization-code"></a>Získání autorizačního kódu

Abyste mohli přijmout přihlašovací údaje služby Azure AD, musíte získat autorizační kód pro vaši webovou aplikaci:

1. Přihlaste se k Azure AD na následující adrese URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Přihlaste se pomocí uživatelského účtu, ze kterého budete provádět volání rozhraní API partnerského centra (například Agent správce nebo účet agenta pro prodej).

2. Nahraďte **Application-ID** ID aplikace Azure AD (GUID).

3. Po zobrazení výzvy se přihlaste pomocí uživatelského účtu s nakonfigurovaným MFA.

4. Po zobrazení výzvy zadejte další informace MFA (telefonní číslo nebo e-mailovou adresu), abyste ověřili své přihlašovací údaje.

5. Po přihlášení bude prohlížeč přesměrovat volání do koncového bodu webové aplikace pomocí vašeho autorizačního kódu. Například následující vzorový kód přesměruje na `https://localhost:44395/` .

#### <a name="authorization-code-call-trace"></a>Trasování volání autorizačního kódu

```http
POST https://localhost:44395/ HTTP/1.1
Origin: https://login.microsoftonline.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referrer: https://login.microsoftonline.com/kmsi
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: OpenIdConnect.nonce.hOMjjrivcxzuI4YqAw4uYC%2F%2BILFk4%2FCx3kHTHP3lBvA%3D=dHVyRXdlbk9WVUZFdlFONVdiY01nNEpUc0JRR0RiYWFLTHhQYlRGNl9VeXJqNjdLTGV3cFpIWFg1YmpnWVdQUURtN0dvMkdHS2kzTm02NGdQS09veVNEbTZJMDk1TVVNYkczYmstQmlKUzFQaTBFMEdhNVJGVHlES2d3WGlCSlVlN1c2UE9sd2kzckNrVGN2RFNULWdHY2JET3RDQUxSaXRfLXZQdG00RnlUM0E1TUo1YWNKOWxvQXRwSkhRYklQbmZUV3d3eHVfNEpMUUthMFlQUFgzS01RS2NvMXYtbnV4UVJOYkl4TTN0cw%3D%3D

code=AuthorizationCodeValue&id_token=IdTokenValue&<rest of properties for state>
```

### <a name="get-refresh-token"></a>Získat obnovovací token

K získání obnovovacího tokenu musíte použít svůj autorizační kód:

1. Proveďte následné volání koncového bodu přihlášení služby Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` pomocí autorizačního kódu. Příklad naleznete v následujícím [ukázkovém volání](#sample-refresh-call).

2. Poznamenejte si obnovovací token, který se vrátí.

3. Uložte obnovovací token do Azure Key Vault. Další informace najdete v dokumentaci k [rozhraní API Key Vault](/rest/api/keyvault/).

> [!IMPORTANT]
> Token obnovení musí být [uložený jako tajný klíč](/rest/api/keyvault/setsecret/setsecret) ve službě Key Vault.

#### <a name="sample-refresh-call"></a>Ukázka aktualizačního hovoru

Požadavek na zástupný symbol:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

Text požadavku:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

Zástupná odpověď:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Tělo odpovědi:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Získat přístupový token

Aby bylo možné volat rozhraní API partnerského centra, musíte získat přístupový token. K získání přístupového tokenu je nutné použít obnovovací token, protože přístupový token obvykle má velmi omezené trvání (například méně než hodinu).

Požadavek na zástupný symbol:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

Text požadavku:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

Zástupná odpověď:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Tělo odpovědi:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Zajištění volání rozhraní API partnerského centra

K volání rozhraní API partnerského centra musíte použít váš přístupový token. Podívejte se na následující příklad volání.

#### <a name="example-partner-center-api-call"></a>Příklad volání rozhraní API partnerského centra

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

K omezení požadované infrastruktury pro výměnu autorizačního kódu pro přístupový token můžete použít [modul PowerShellu pro partnerských Center](https://www.powershellgallery.com/packages/PartnerCenter) . Tato metoda je volitelná pro zajištění [volání REST v partnerském centru](#rest).

Další informace o tomto procesu najdete v dokumentaci k nástroji PowerShell pro [model zabezpečení aplikace](/powershell/partnercenter/secure-app-model) .

1. Nainstalujte moduly PowerShellu pro Azure AD a partnerská centra.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Pomocí příkazu **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** proveďte proces souhlasu a zachyťte požadovaný obnovovací token.

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > Parametr **ServicePrincipal** se používá v příkazu **New-PartnerAccessToken** , protože se používá aplikace Azure AD s typem **webu nebo rozhraní API** . Tento typ aplikace vyžaduje, aby byl v žádosti o přístupový token zahrnutý identifikátor klienta a tajný klíč. Po vyvolání příkazu **Get-Credential** se zobrazí výzva k zadání uživatelského jména a hesla. Jako uživatelské jméno zadejte identifikátor aplikace. Jako heslo zadejte tajný klíč aplikace. Po vyvolání příkazu **New-PartnerAccessToken** se zobrazí výzva k zadání přihlašovacích údajů znovu. Zadejte pověření pro účet služby, který používáte. Tento účet služby by měl být partnerským účtem s příslušnými oprávněními.

3. Zkopírujte hodnotu obnovovacího tokenu.

    ```powershell
    $token.RefreshToken | clip
    ```

Hodnotu obnovovacího tokenu byste měli uložit do zabezpečeného úložiště, například Azure Key Vault. Další informace o tom, jak použít modul zabezpečení aplikace pomocí prostředí PowerShell, najdete v článku [Multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) .
