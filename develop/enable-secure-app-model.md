---
title: Povolení zabezpečeného aplikačního modelu
description: Zabezpečte své Partnerské centrum a aplikace ovládacích panelů.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5d35c0512ba8edcf3742ee69d38c699a9a8c16d2
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906410"
---
# <a name="enabling-the-secure-application-model-framework"></a>Povolení architektury zabezpečeného aplikačního modelu

Microsoft představuje zabezpečenou a škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) prostřednictvím architektury Microsoft Azure Active Directory Multi-Factor Authentication (MFA).

Nový model můžete použít ke zvýšení zabezpečení pro Partnerské centrum integrace rozhraní API. To pomůže všem stranám (včetně Microsoftu, partnerů CSP a CPV) chránit infrastrukturu a zákaznická data před riziky zabezpečení.

## <a name="scope"></a>Obor

Tento článek se týká následujících aktérů:

- Dodavatelé ovládacích panelů (CPV)
  - Dodavatel ovládacích panelů (CPV) je nezávislý výrobce softwaru, který vyvíjí aplikace, které můžou partneři CSP integrovat s rozhraními API Partnerského centra.
  - Dodavatel ovládacích panelů (CPV) není partnerem CSP s přímým přístupem k řídicímu panelu pro Partnerské centrum ani rozhraním API Partnerského centra.

- Nepřímí poskytovatelé CSP a přímou partneři CSP, kteří používají ID aplikace a ověřování uživatelů a přímo se integrují Partnerské centrum rozhraníMI API.

## <a name="security-requirements"></a>Požadavky na zabezpečení

Podrobnosti o požadavcích na zabezpečení najdete v tématu [Požadavky na zabezpečení partnerů.](/partner-center/partner-security-requirements)

## <a name="secure-application-model"></a>Model zapezpečených aplikací

Aplikace z Marketplace musí k volání rozhraní API Microsoftu zosobnit oprávnění partnera CSP. Útoky na zabezpečení těchto citlivých aplikací mohou vést k ohrožení zákaznických dat.

Přehled a podrobnosti o nové ověřovací rozhraní najdete v dokumentu Model zapezpečených aplikací [framework.](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) Tento dokument se věnuje principům a osvědčeným postupům, aby aplikace z marketplace byly udržitelné a odolné před ohrožením zabezpečení.

## <a name="samples"></a>ukázky

Následující přehledové dokumenty a vzorový kód popisují, jak mohou partneři implementovat Model zapezpečených aplikací rozhraní:

- [Dokument s přehledem CPV](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [Dokument s přehledem CSP](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [Ukázky .NET](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Ukázky v Javě](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [Pokyny a ukázky REST](#rest)
- [Pokyny a ukázky PowerShellu](#powershell)

## <a name="rest"></a>REST

Pokud chcete provádět volání REST s Model zapezpečených aplikací architekturou s ukázkovým kódem, postupujte takto:

1. [Vytvoření webové aplikace](#create-a-web-app)

2. [Získání autorizačního kódu](#get-authorization-code)

3. [Získání obnovovacího tokenu](#get-refresh-token)

4. [Získání přístupového tokenu](#get-access-token)

5. [Zavolání rozhraní API Partnerského centra](#make-partner-center-api-calls)

> [!TIP]
> Pomocí modulu Partnerské centrum PowerShell můžete získat autorizační kód a obnovovací token. Tuto možnost můžete zvolit místo kroků 2 a 3. Další informace najdete v části [PowerShellu a v příkladech](#powershell).

### <a name="create-a-web-app"></a>Vytvoření webové aplikace

Před voláním REST musíte vytvořit a zaregistrovat webovou Partnerské centrum ve službě .

1. Přihlaste se na [Azure Portal](https://portal.azure.com).

2. Vytvořte aplikaci Azure Active Directory (Azure AD).

3. V závislosti na požadavcích vaší aplikace udejte delegovaná oprávnění aplikací následujícím *prostředkům.* V případě potřeby můžete přidat další delegovaná oprávnění pro prostředky aplikace.

   1. **Microsoft Partnerské centrum** (někteří tenanti to ukazují jako **SampleBECApp)**

   2. **Rozhraní API pro správu Azure** (pokud plánujete volat rozhraní API Azure)

   3. **Windows Azure Active Directory**

4. Ujistěte se, že je domovská adresa URL vaší aplikace nastavená na koncový bod, ve kterém běží živá webová aplikace. Tato aplikace bude muset přijmout [autorizační kód z](#get-authorization-code) volání přihlášení azure AD. Například v příkladu kódu v [následující části](#get-authorization-code)běží webová aplikace v `https://localhost:44395/` .

5. Všimněte si následujících informací z nastavení vaší webové aplikace v Azure AD:

   - ID aplikace
   - Tajný kód aplikace

> [!NOTE]
> Jako tajný klíč [aplikace se doporučuje použít certifikát.](/azure/active-directory/develop/active-directory-certificate-credentials) Klíč aplikace ale můžete vytvořit také v Azure Portal. Vzorový kód [v následující části](#get-authorization-code) používá klíč aplikace.

### <a name="get-authorization-code"></a>Získání autorizačního kódu

K přijetí z přihlašovacího volání Azure AD musíte získat autorizační kód pro vaši webovou aplikaci:

1. Přihlaste se k Azure AD na následující adrese URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Nezapomeňte se přihlásit pomocí uživatelského účtu, ze kterého budete volat Partnerské centrum API (například pomocí agenta pro správu nebo účtu agenta prodeje).

2. Nahraďte **Application-Id id** vaší aplikace Azure AD (GUID).

3. Po zobrazení výzvy se přihlaste pomocí svého uživatelského účtu s nakonfigurovanou MFA.

4. Po zobrazení výzvy zadejte další informace o MFA (telefonní číslo nebo e-mailovou adresu) a ověřte své přihlášení.

5. Po přihlášení prohlížeč přesměruje volání do koncového bodu webové aplikace s vaším autorizačním kódem. Například následující ukázkový kód přesměruje na `https://localhost:44395/` .

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

### <a name="get-refresh-token"></a>Získání obnovovacího tokenu

Pak musíte pomocí autorizačního kódu získat obnovovací token:

1. Proveďte volání POST do koncového bodu přihlášení Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` s autorizačním kódem. Příklad najdete v následujícím [ukázkovém volání](#sample-refresh-call).

2. Všimněte si obnovovacího tokenu, který se vrátí.

3. Uložte obnovovací token do Azure Key Vault. Další informace najdete v dokumentaci [Key Vault API.](/rest/api/keyvault/)

> [!IMPORTANT]
> Token obnovení musí být [uložený jako tajný klíč](/rest/api/keyvault/setsecret/setsecret) ve službě Key Vault.

#### <a name="sample-refresh-call"></a>Ukázkové volání aktualizace

Zástupný text požadavku:

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

Odpověď zástupného symbolu:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Text odpovědi:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Získání přístupového tokenu

Přístupový token je nutné získat před voláním rozhraní API Partnerské centrum rozhraní API. K získání přístupového tokenu musíte použít obnovovací token, protože přístupové tokeny mají obecně velmi omezenou životnost (například méně než hodinu).

Zástupný text požadavku:

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

Odpověď zástupného symbolu:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Text odpovědi:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Volání Partnerské centrum API

Přístupový token musíte použít k volání rozhraní API Partnerské centrum api. Podívejte se na následující příklad volání.

#### <a name="example-partner-center-api-call"></a>Příklad Partnerské centrum rozhraní API

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pomocí modulu [Partnerské centrum PowerShell můžete](https://www.powershellgallery.com/packages/PartnerCenter) snížit požadovanou infrastrukturu pro výměnu autorizačního kódu pro přístupový token. Tato metoda je volitelná pro [Partnerské centrum volání REST.](#rest)

Další informace o tomto procesu najdete v dokumentaci [k Secure Model aplikací](/powershell/partnercenter/secure-app-model) PowerShellu.

1. Nainstalujte azure AD a Partnerské centrum moduly PowerShellu.

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
    > Parametr **ServicePrincipal** se používá s příkazem **New-PartnerAccessToken,** protože se používá aplikace Azure AD s typem webu nebo rozhraní **API.** Tento typ aplikace vyžaduje, aby byl do žádosti o přístupový token zahrnutý identifikátor klienta a tajný kód. Po **vyvolání příkazu Get-Credential** se zobrazí výzva k zadání uživatelského jména a hesla. Jako uživatelské jméno zadejte identifikátor aplikace. Jako heslo zadejte tajný klíč aplikace. Po vyvolání příkazu **New-PartnerAccessToken** se zobrazí výzva k zadání přihlašovacích údajů znovu. Zadejte pověření pro účet služby, který používáte. Tento účet služby by měl být partnerským účtem s příslušnými oprávněními.

3. Zkopírujte hodnotu obnovovacího tokenu.

    ```powershell
    $token.RefreshToken | clip
    ```

Hodnotu obnovovacího tokenu byste měli uložit do zabezpečeného úložiště, například Azure Key Vault. Další informace o tom, jak použít modul zabezpečení aplikace pomocí prostředí PowerShell, najdete v článku [Multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) .
