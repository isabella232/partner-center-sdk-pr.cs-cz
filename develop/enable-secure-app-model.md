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
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="506be-103">Povolení architektury zabezpečeného aplikačního modelu</span><span class="sxs-lookup"><span data-stu-id="506be-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="506be-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="506be-104">**Applies to:**</span></span>

- <span data-ttu-id="506be-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="506be-105">Partner Center</span></span>

<span data-ttu-id="506be-106">Microsoft zavádí zabezpečenou, škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) prostřednictvím architektury Microsoft Azure Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="506be-106">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>

<span data-ttu-id="506be-107">Pomocí nového modelu můžete zvýšit zabezpečení pro volání Integration Center API pro partnery.</span><span class="sxs-lookup"><span data-stu-id="506be-107">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="506be-108">Pomůže všem stranám (včetně Microsoftu, partnerům CSP a CPVs) chránit svá data infrastruktury a zákaznická data před bezpečnostními riziky.</span><span class="sxs-lookup"><span data-stu-id="506be-108">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="506be-109">Obor</span><span class="sxs-lookup"><span data-stu-id="506be-109">Scope</span></span>

<span data-ttu-id="506be-110">Tento článek se týká následujících aktérů:</span><span class="sxs-lookup"><span data-stu-id="506be-110">This article concerns the following actors:</span></span>

- <span data-ttu-id="506be-111">Dodavatelé ovládacích panelů (CPV)</span><span class="sxs-lookup"><span data-stu-id="506be-111">CPVs</span></span>
  - <span data-ttu-id="506be-112">Dodavatel ovládacích panelů (CPV) je nezávislý výrobce softwaru, který vyvíjí aplikace, které můžou partneři CSP integrovat s rozhraními API Partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="506be-112">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="506be-113">Dodavatel ovládacích panelů (CPV) není partnerem CSP s přímým přístupem k řídicímu panelu pro Partnerské centrum ani rozhraním API Partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="506be-113">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="506be-114">Nepřímá poskytovatelé CSP a partneři CSP Direct, kteří používají ID aplikace + ověřování uživatelů a přímo integrují s rozhraními API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="506be-114">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="506be-115">Požadavky na zabezpečení</span><span class="sxs-lookup"><span data-stu-id="506be-115">Security requirements</span></span>

<span data-ttu-id="506be-116">Podrobnosti o požadavcích na zabezpečení najdete v tématu [požadavky na zabezpečení partnerů](/partner-center/partner-security-requirements).</span><span class="sxs-lookup"><span data-stu-id="506be-116">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="506be-117">Model zabezpečené aplikace</span><span class="sxs-lookup"><span data-stu-id="506be-117">Secure Application Model</span></span>

<span data-ttu-id="506be-118">Aplikace z Marketplace potřebují zosobnit oprávnění partnera CSP pro volání rozhraní API Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="506be-118">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="506be-119">Bezpečnostní útoky na těchto citlivých aplikacích můžou vést k ohrožení zákaznických dat.</span><span class="sxs-lookup"><span data-stu-id="506be-119">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="506be-120">Přehled a podrobnosti nové architektury ověřování si můžete stáhnout v dokumentu Framework pro [model zabezpečených aplikací](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) .</span><span class="sxs-lookup"><span data-stu-id="506be-120">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="506be-121">Tento dokument popisuje principy a osvědčené postupy pro zajištění trvalého a robustního zabezpečení aplikací pro Marketplace před ohroženími zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="506be-121">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="506be-122">ukázky</span><span class="sxs-lookup"><span data-stu-id="506be-122">Samples</span></span>

<span data-ttu-id="506be-123">Následující dokumenty přehledu a ukázkový kód popisují, jak můžou partneři implementovat rozhraní zabezpečeného modelu aplikace:</span><span class="sxs-lookup"><span data-stu-id="506be-123">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="506be-124">Dokument s přehledem CPV</span><span class="sxs-lookup"><span data-stu-id="506be-124">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="506be-125">Dokument s přehledem CSP</span><span class="sxs-lookup"><span data-stu-id="506be-125">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="506be-126">Ukázky .NET</span><span class="sxs-lookup"><span data-stu-id="506be-126">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="506be-127">Ukázky Java</span><span class="sxs-lookup"><span data-stu-id="506be-127">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="506be-128">Pokyny a ukázky pro REST</span><span class="sxs-lookup"><span data-stu-id="506be-128">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="506be-129">Pokyny a ukázky prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="506be-129">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="506be-130">REST</span><span class="sxs-lookup"><span data-stu-id="506be-130">REST</span></span>

<span data-ttu-id="506be-131">Chcete-li provést volání REST pomocí rozhraní zabezpečeného modelu aplikace s ukázkovým kódem, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="506be-131">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="506be-132">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="506be-132">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="506be-133">Získání autorizačního kódu</span><span class="sxs-lookup"><span data-stu-id="506be-133">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="506be-134">Získat obnovovací token</span><span class="sxs-lookup"><span data-stu-id="506be-134">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="506be-135">Získání přístupového tokenu</span><span class="sxs-lookup"><span data-stu-id="506be-135">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="506be-136">Zavolání rozhraní API Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="506be-136">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="506be-137">K získání autorizačního kódu a obnovovacího tokenu můžete použít modul PowerShell pro partnerských Center.</span><span class="sxs-lookup"><span data-stu-id="506be-137">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="506be-138">Tuto možnost můžete vybrat místo kroků 2 a 3.</span><span class="sxs-lookup"><span data-stu-id="506be-138">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="506be-139">Další informace najdete v [části a příklady prostředí PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="506be-139">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="506be-140">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="506be-140">Create a web app</span></span>

<span data-ttu-id="506be-141">Před tím, než zahájíte volání REST, je nutné vytvořit a zaregistrovat webovou aplikaci v partnerském centru.</span><span class="sxs-lookup"><span data-stu-id="506be-141">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="506be-142">Přihlaste se na [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="506be-142">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="506be-143">Vytvořte aplikaci Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="506be-143">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="506be-144">Udělte delegovaným aplikacím oprávnění k následujícím prostředkům *v závislosti na požadavcích vaší aplikace*.</span><span class="sxs-lookup"><span data-stu-id="506be-144">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="506be-145">V případě potřeby můžete přidat další delegovaná oprávnění pro prostředky aplikace.</span><span class="sxs-lookup"><span data-stu-id="506be-145">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="506be-146">**Partnerské centrum Microsoftu** (někteří klienti to ukazují jako **SampleBECApp**)</span><span class="sxs-lookup"><span data-stu-id="506be-146">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="506be-147">**Rozhraní API pro správu Azure** (Pokud plánujete volat rozhraní API Azure)</span><span class="sxs-lookup"><span data-stu-id="506be-147">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="506be-148">**Windows Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="506be-148">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="506be-149">Ujistěte se, že adresa URL domů vaší aplikace je nastavená na koncový bod, ve kterém běží živá webová aplikace.</span><span class="sxs-lookup"><span data-stu-id="506be-149">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="506be-150">Tato aplikace bude muset přijmout [autorizační kód](#get-authorization-code) z přihlašovacího volání služby Azure AD.</span><span class="sxs-lookup"><span data-stu-id="506be-150">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="506be-151">Například v příkladu kódu v [následující části](#get-authorization-code)je webová aplikace spuštěna v `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="506be-151">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="506be-152">Všimněte si následujících informací z nastavení vaší webové aplikace ve službě Azure AD:</span><span class="sxs-lookup"><span data-stu-id="506be-152">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="506be-153">ID aplikace</span><span class="sxs-lookup"><span data-stu-id="506be-153">Application ID</span></span>
   - <span data-ttu-id="506be-154">Tajný kód aplikace</span><span class="sxs-lookup"><span data-stu-id="506be-154">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="506be-155">Doporučuje se [použít certifikát jako tajný kód aplikace](/azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="506be-155">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="506be-156">Můžete ale také vytvořit klíč aplikace v Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="506be-156">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="506be-157">Vzorový kód v [následující části](#get-authorization-code) používá klíč aplikace.</span><span class="sxs-lookup"><span data-stu-id="506be-157">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="506be-158">Získání autorizačního kódu</span><span class="sxs-lookup"><span data-stu-id="506be-158">Get authorization code</span></span>

<span data-ttu-id="506be-159">Abyste mohli přijmout přihlašovací údaje služby Azure AD, musíte získat autorizační kód pro vaši webovou aplikaci:</span><span class="sxs-lookup"><span data-stu-id="506be-159">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="506be-160">Přihlaste se k Azure AD na následující adrese URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="506be-160">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="506be-161">Přihlaste se pomocí uživatelského účtu, ze kterého budete provádět volání rozhraní API partnerského centra (například Agent správce nebo účet agenta pro prodej).</span><span class="sxs-lookup"><span data-stu-id="506be-161">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="506be-162">Nahraďte **Application-ID** ID aplikace Azure AD (GUID).</span><span class="sxs-lookup"><span data-stu-id="506be-162">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="506be-163">Po zobrazení výzvy se přihlaste pomocí uživatelského účtu s nakonfigurovaným MFA.</span><span class="sxs-lookup"><span data-stu-id="506be-163">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="506be-164">Po zobrazení výzvy zadejte další informace MFA (telefonní číslo nebo e-mailovou adresu), abyste ověřili své přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="506be-164">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="506be-165">Po přihlášení bude prohlížeč přesměrovat volání do koncového bodu webové aplikace pomocí vašeho autorizačního kódu.</span><span class="sxs-lookup"><span data-stu-id="506be-165">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="506be-166">Například následující vzorový kód přesměruje na `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="506be-166">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="506be-167">Trasování volání autorizačního kódu</span><span class="sxs-lookup"><span data-stu-id="506be-167">Authorization code call trace</span></span>

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

### <a name="get-refresh-token"></a><span data-ttu-id="506be-168">Získat obnovovací token</span><span class="sxs-lookup"><span data-stu-id="506be-168">Get refresh token</span></span>

<span data-ttu-id="506be-169">K získání obnovovacího tokenu musíte použít svůj autorizační kód:</span><span class="sxs-lookup"><span data-stu-id="506be-169">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="506be-170">Proveďte následné volání koncového bodu přihlášení služby Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` pomocí autorizačního kódu.</span><span class="sxs-lookup"><span data-stu-id="506be-170">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="506be-171">Příklad naleznete v následujícím [ukázkovém volání](#sample-refresh-call).</span><span class="sxs-lookup"><span data-stu-id="506be-171">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="506be-172">Poznamenejte si obnovovací token, který se vrátí.</span><span class="sxs-lookup"><span data-stu-id="506be-172">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="506be-173">Uložte obnovovací token do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="506be-173">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="506be-174">Další informace najdete v dokumentaci k [rozhraní API Key Vault](/rest/api/keyvault/).</span><span class="sxs-lookup"><span data-stu-id="506be-174">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="506be-175">Token obnovení musí být [uložený jako tajný klíč](/rest/api/keyvault/setsecret/setsecret) ve službě Key Vault.</span><span class="sxs-lookup"><span data-stu-id="506be-175">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="506be-176">Ukázka aktualizačního hovoru</span><span class="sxs-lookup"><span data-stu-id="506be-176">Sample refresh call</span></span>

<span data-ttu-id="506be-177">Požadavek na zástupný symbol:</span><span class="sxs-lookup"><span data-stu-id="506be-177">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="506be-178">Text požadavku:</span><span class="sxs-lookup"><span data-stu-id="506be-178">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="506be-179">Zástupná odpověď:</span><span class="sxs-lookup"><span data-stu-id="506be-179">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="506be-180">Tělo odpovědi:</span><span class="sxs-lookup"><span data-stu-id="506be-180">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="506be-181">Získat přístupový token</span><span class="sxs-lookup"><span data-stu-id="506be-181">Get access token</span></span>

<span data-ttu-id="506be-182">Aby bylo možné volat rozhraní API partnerského centra, musíte získat přístupový token.</span><span class="sxs-lookup"><span data-stu-id="506be-182">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="506be-183">K získání přístupového tokenu je nutné použít obnovovací token, protože přístupový token obvykle má velmi omezené trvání (například méně než hodinu).</span><span class="sxs-lookup"><span data-stu-id="506be-183">You must use a refresh token to obtain an access token because access token generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="506be-184">Požadavek na zástupný symbol:</span><span class="sxs-lookup"><span data-stu-id="506be-184">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="506be-185">Text požadavku:</span><span class="sxs-lookup"><span data-stu-id="506be-185">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="506be-186">Zástupná odpověď:</span><span class="sxs-lookup"><span data-stu-id="506be-186">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="506be-187">Tělo odpovědi:</span><span class="sxs-lookup"><span data-stu-id="506be-187">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="506be-188">Zajištění volání rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="506be-188">Make Partner Center API calls</span></span>

<span data-ttu-id="506be-189">K volání rozhraní API partnerského centra musíte použít váš přístupový token.</span><span class="sxs-lookup"><span data-stu-id="506be-189">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="506be-190">Podívejte se na následující příklad volání.</span><span class="sxs-lookup"><span data-stu-id="506be-190">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="506be-191">Příklad volání rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="506be-191">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="506be-192">PowerShell</span><span class="sxs-lookup"><span data-stu-id="506be-192">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="506be-193">K omezení požadované infrastruktury pro výměnu autorizačního kódu pro přístupový token můžete použít [modul PowerShellu pro partnerských Center](https://www.powershellgallery.com/packages/PartnerCenter) .</span><span class="sxs-lookup"><span data-stu-id="506be-193">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="506be-194">Tato metoda je volitelná pro zajištění [volání REST v partnerském centru](#rest).</span><span class="sxs-lookup"><span data-stu-id="506be-194">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="506be-195">Další informace o tomto procesu najdete v dokumentaci k nástroji PowerShell pro [model zabezpečení aplikace](/powershell/partnercenter/secure-app-model) .</span><span class="sxs-lookup"><span data-stu-id="506be-195">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="506be-196">Nainstalujte moduly PowerShellu pro Azure AD a partnerská centra.</span><span class="sxs-lookup"><span data-stu-id="506be-196">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="506be-197">Pomocí příkazu **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** proveďte proces souhlasu a zachyťte požadovaný obnovovací token.</span><span class="sxs-lookup"><span data-stu-id="506be-197">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="506be-198">Parametr **ServicePrincipal** se používá v příkazu **New-PartnerAccessToken** , protože se používá aplikace Azure AD s typem **webu nebo rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="506be-198">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="506be-199">Tento typ aplikace vyžaduje, aby byl v žádosti o přístupový token zahrnutý identifikátor klienta a tajný klíč.</span><span class="sxs-lookup"><span data-stu-id="506be-199">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="506be-200">Po vyvolání příkazu **Get-Credential** se zobrazí výzva k zadání uživatelského jména a hesla.</span><span class="sxs-lookup"><span data-stu-id="506be-200">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="506be-201">Jako uživatelské jméno zadejte identifikátor aplikace.</span><span class="sxs-lookup"><span data-stu-id="506be-201">Enter the application identifier as the username.</span></span> <span data-ttu-id="506be-202">Jako heslo zadejte tajný klíč aplikace.</span><span class="sxs-lookup"><span data-stu-id="506be-202">Enter the application secret as the password.</span></span> <span data-ttu-id="506be-203">Po vyvolání příkazu **New-PartnerAccessToken** se zobrazí výzva k zadání přihlašovacích údajů znovu.</span><span class="sxs-lookup"><span data-stu-id="506be-203">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="506be-204">Zadejte pověření pro účet služby, který používáte.</span><span class="sxs-lookup"><span data-stu-id="506be-204">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="506be-205">Tento účet služby by měl být partnerským účtem s příslušnými oprávněními.</span><span class="sxs-lookup"><span data-stu-id="506be-205">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="506be-206">Zkopírujte hodnotu obnovovacího tokenu.</span><span class="sxs-lookup"><span data-stu-id="506be-206">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="506be-207">Hodnotu obnovovacího tokenu byste měli uložit do zabezpečeného úložiště, například Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="506be-207">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="506be-208">Další informace o tom, jak použít modul zabezpečení aplikace pomocí prostředí PowerShell, najdete v článku [Multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) .</span><span class="sxs-lookup"><span data-stu-id="506be-208">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
