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
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="94cc4-103">Povolení architektury zabezpečeného aplikačního modelu</span><span class="sxs-lookup"><span data-stu-id="94cc4-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="94cc4-104">Microsoft představuje zabezpečenou a škálovatelnou architekturu pro ověřování partnerů CSP (Cloud Solution Provider) a dodavatelů ovládacích panelů (CPV) prostřednictvím architektury Microsoft Azure Active Directory Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="94cc4-104">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure Active Directory Multi-Factor Authentication (MFA) architecture.</span></span>

<span data-ttu-id="94cc4-105">Nový model můžete použít ke zvýšení zabezpečení pro Partnerské centrum integrace rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="94cc4-105">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="94cc4-106">To pomůže všem stranám (včetně Microsoftu, partnerů CSP a CPV) chránit infrastrukturu a zákaznická data před riziky zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="94cc4-106">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="94cc4-107">Obor</span><span class="sxs-lookup"><span data-stu-id="94cc4-107">Scope</span></span>

<span data-ttu-id="94cc4-108">Tento článek se týká následujících aktérů:</span><span class="sxs-lookup"><span data-stu-id="94cc4-108">This article concerns the following actors:</span></span>

- <span data-ttu-id="94cc4-109">Dodavatelé ovládacích panelů (CPV)</span><span class="sxs-lookup"><span data-stu-id="94cc4-109">CPVs</span></span>
  - <span data-ttu-id="94cc4-110">Dodavatel ovládacích panelů (CPV) je nezávislý výrobce softwaru, který vyvíjí aplikace, které můžou partneři CSP integrovat s rozhraními API Partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="94cc4-110">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="94cc4-111">Dodavatel ovládacích panelů (CPV) není partnerem CSP s přímým přístupem k řídicímu panelu pro Partnerské centrum ani rozhraním API Partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="94cc4-111">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="94cc4-112">Nepřímí poskytovatelé CSP a přímou partneři CSP, kteří používají ID aplikace a ověřování uživatelů a přímo se integrují Partnerské centrum rozhraníMI API.</span><span class="sxs-lookup"><span data-stu-id="94cc4-112">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="94cc4-113">Požadavky na zabezpečení</span><span class="sxs-lookup"><span data-stu-id="94cc4-113">Security requirements</span></span>

<span data-ttu-id="94cc4-114">Podrobnosti o požadavcích na zabezpečení najdete v tématu [Požadavky na zabezpečení partnerů.](/partner-center/partner-security-requirements)</span><span class="sxs-lookup"><span data-stu-id="94cc4-114">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="94cc4-115">Model zapezpečených aplikací</span><span class="sxs-lookup"><span data-stu-id="94cc4-115">Secure Application Model</span></span>

<span data-ttu-id="94cc4-116">Aplikace z Marketplace musí k volání rozhraní API Microsoftu zosobnit oprávnění partnera CSP.</span><span class="sxs-lookup"><span data-stu-id="94cc4-116">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="94cc4-117">Útoky na zabezpečení těchto citlivých aplikací mohou vést k ohrožení zákaznických dat.</span><span class="sxs-lookup"><span data-stu-id="94cc4-117">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="94cc4-118">Přehled a podrobnosti o nové ověřovací rozhraní najdete v dokumentu Model zapezpečených aplikací [framework.](https://assetsprod.microsoft.com/secure-application-model-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="94cc4-118">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="94cc4-119">Tento dokument se věnuje principům a osvědčeným postupům, aby aplikace z marketplace byly udržitelné a odolné před ohrožením zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="94cc4-119">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="94cc4-120">ukázky</span><span class="sxs-lookup"><span data-stu-id="94cc4-120">Samples</span></span>

<span data-ttu-id="94cc4-121">Následující přehledové dokumenty a vzorový kód popisují, jak mohou partneři implementovat Model zapezpečených aplikací rozhraní:</span><span class="sxs-lookup"><span data-stu-id="94cc4-121">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="94cc4-122">Dokument s přehledem CPV</span><span class="sxs-lookup"><span data-stu-id="94cc4-122">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="94cc4-123">Dokument s přehledem CSP</span><span class="sxs-lookup"><span data-stu-id="94cc4-123">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="94cc4-124">Ukázky .NET</span><span class="sxs-lookup"><span data-stu-id="94cc4-124">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="94cc4-125">Ukázky v Javě</span><span class="sxs-lookup"><span data-stu-id="94cc4-125">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="94cc4-126">Pokyny a ukázky REST</span><span class="sxs-lookup"><span data-stu-id="94cc4-126">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="94cc4-127">Pokyny a ukázky PowerShellu</span><span class="sxs-lookup"><span data-stu-id="94cc4-127">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="94cc4-128">REST</span><span class="sxs-lookup"><span data-stu-id="94cc4-128">REST</span></span>

<span data-ttu-id="94cc4-129">Pokud chcete provádět volání REST s Model zapezpečených aplikací architekturou s ukázkovým kódem, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="94cc4-129">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="94cc4-130">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="94cc4-130">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="94cc4-131">Získání autorizačního kódu</span><span class="sxs-lookup"><span data-stu-id="94cc4-131">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="94cc4-132">Získání obnovovacího tokenu</span><span class="sxs-lookup"><span data-stu-id="94cc4-132">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="94cc4-133">Získání přístupového tokenu</span><span class="sxs-lookup"><span data-stu-id="94cc4-133">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="94cc4-134">Zavolání rozhraní API Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="94cc4-134">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="94cc4-135">Pomocí modulu Partnerské centrum PowerShell můžete získat autorizační kód a obnovovací token.</span><span class="sxs-lookup"><span data-stu-id="94cc4-135">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="94cc4-136">Tuto možnost můžete zvolit místo kroků 2 a 3.</span><span class="sxs-lookup"><span data-stu-id="94cc4-136">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="94cc4-137">Další informace najdete v části [PowerShellu a v příkladech](#powershell).</span><span class="sxs-lookup"><span data-stu-id="94cc4-137">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="94cc4-138">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="94cc4-138">Create a web app</span></span>

<span data-ttu-id="94cc4-139">Před voláním REST musíte vytvořit a zaregistrovat webovou Partnerské centrum ve službě .</span><span class="sxs-lookup"><span data-stu-id="94cc4-139">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="94cc4-140">Přihlaste se na [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="94cc4-140">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="94cc4-141">Vytvořte aplikaci Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94cc4-141">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="94cc4-142">V závislosti na požadavcích vaší aplikace udejte delegovaná oprávnění aplikací následujícím *prostředkům.*</span><span class="sxs-lookup"><span data-stu-id="94cc4-142">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="94cc4-143">V případě potřeby můžete přidat další delegovaná oprávnění pro prostředky aplikace.</span><span class="sxs-lookup"><span data-stu-id="94cc4-143">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="94cc4-144">**Microsoft Partnerské centrum** (někteří tenanti to ukazují jako **SampleBECApp)**</span><span class="sxs-lookup"><span data-stu-id="94cc4-144">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="94cc4-145">**Rozhraní API pro správu Azure** (pokud plánujete volat rozhraní API Azure)</span><span class="sxs-lookup"><span data-stu-id="94cc4-145">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="94cc4-146">**Windows Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="94cc4-146">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="94cc4-147">Ujistěte se, že je domovská adresa URL vaší aplikace nastavená na koncový bod, ve kterém běží živá webová aplikace.</span><span class="sxs-lookup"><span data-stu-id="94cc4-147">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="94cc4-148">Tato aplikace bude muset přijmout [autorizační kód z](#get-authorization-code) volání přihlášení azure AD.</span><span class="sxs-lookup"><span data-stu-id="94cc4-148">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="94cc4-149">Například v příkladu kódu v [následující části](#get-authorization-code)běží webová aplikace v `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="94cc4-149">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="94cc4-150">Všimněte si následujících informací z nastavení vaší webové aplikace v Azure AD:</span><span class="sxs-lookup"><span data-stu-id="94cc4-150">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="94cc4-151">ID aplikace</span><span class="sxs-lookup"><span data-stu-id="94cc4-151">Application ID</span></span>
   - <span data-ttu-id="94cc4-152">Tajný kód aplikace</span><span class="sxs-lookup"><span data-stu-id="94cc4-152">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="94cc4-153">Jako tajný klíč [aplikace se doporučuje použít certifikát.](/azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="94cc4-153">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="94cc4-154">Klíč aplikace ale můžete vytvořit také v Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="94cc4-154">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="94cc4-155">Vzorový kód [v následující části](#get-authorization-code) používá klíč aplikace.</span><span class="sxs-lookup"><span data-stu-id="94cc4-155">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="94cc4-156">Získání autorizačního kódu</span><span class="sxs-lookup"><span data-stu-id="94cc4-156">Get authorization code</span></span>

<span data-ttu-id="94cc4-157">K přijetí z přihlašovacího volání Azure AD musíte získat autorizační kód pro vaši webovou aplikaci:</span><span class="sxs-lookup"><span data-stu-id="94cc4-157">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="94cc4-158">Přihlaste se k Azure AD na následující adrese URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="94cc4-158">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="94cc4-159">Nezapomeňte se přihlásit pomocí uživatelského účtu, ze kterého budete volat Partnerské centrum API (například pomocí agenta pro správu nebo účtu agenta prodeje).</span><span class="sxs-lookup"><span data-stu-id="94cc4-159">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="94cc4-160">Nahraďte **Application-Id id** vaší aplikace Azure AD (GUID).</span><span class="sxs-lookup"><span data-stu-id="94cc4-160">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="94cc4-161">Po zobrazení výzvy se přihlaste pomocí svého uživatelského účtu s nakonfigurovanou MFA.</span><span class="sxs-lookup"><span data-stu-id="94cc4-161">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="94cc4-162">Po zobrazení výzvy zadejte další informace o MFA (telefonní číslo nebo e-mailovou adresu) a ověřte své přihlášení.</span><span class="sxs-lookup"><span data-stu-id="94cc4-162">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="94cc4-163">Po přihlášení prohlížeč přesměruje volání do koncového bodu webové aplikace s vaším autorizačním kódem.</span><span class="sxs-lookup"><span data-stu-id="94cc4-163">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="94cc4-164">Například následující ukázkový kód přesměruje na `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="94cc4-164">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="94cc4-165">Trasování volání autorizačního kódu</span><span class="sxs-lookup"><span data-stu-id="94cc4-165">Authorization code call trace</span></span>

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

### <a name="get-refresh-token"></a><span data-ttu-id="94cc4-166">Získání obnovovacího tokenu</span><span class="sxs-lookup"><span data-stu-id="94cc4-166">Get refresh token</span></span>

<span data-ttu-id="94cc4-167">Pak musíte pomocí autorizačního kódu získat obnovovací token:</span><span class="sxs-lookup"><span data-stu-id="94cc4-167">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="94cc4-168">Proveďte volání POST do koncového bodu přihlášení Azure AD `https://login.microsoftonline.com/CSPTenantID/oauth2/token` s autorizačním kódem.</span><span class="sxs-lookup"><span data-stu-id="94cc4-168">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="94cc4-169">Příklad najdete v následujícím [ukázkovém volání](#sample-refresh-call).</span><span class="sxs-lookup"><span data-stu-id="94cc4-169">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="94cc4-170">Všimněte si obnovovacího tokenu, který se vrátí.</span><span class="sxs-lookup"><span data-stu-id="94cc4-170">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="94cc4-171">Uložte obnovovací token do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="94cc4-171">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="94cc4-172">Další informace najdete v dokumentaci [Key Vault API.](/rest/api/keyvault/)</span><span class="sxs-lookup"><span data-stu-id="94cc4-172">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94cc4-173">Token obnovení musí být [uložený jako tajný klíč](/rest/api/keyvault/setsecret/setsecret) ve službě Key Vault.</span><span class="sxs-lookup"><span data-stu-id="94cc4-173">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="94cc4-174">Ukázkové volání aktualizace</span><span class="sxs-lookup"><span data-stu-id="94cc4-174">Sample refresh call</span></span>

<span data-ttu-id="94cc4-175">Zástupný text požadavku:</span><span class="sxs-lookup"><span data-stu-id="94cc4-175">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="94cc4-176">Text požadavku:</span><span class="sxs-lookup"><span data-stu-id="94cc4-176">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="94cc4-177">Odpověď zástupného symbolu:</span><span class="sxs-lookup"><span data-stu-id="94cc4-177">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="94cc4-178">Text odpovědi:</span><span class="sxs-lookup"><span data-stu-id="94cc4-178">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="94cc4-179">Získání přístupového tokenu</span><span class="sxs-lookup"><span data-stu-id="94cc4-179">Get access token</span></span>

<span data-ttu-id="94cc4-180">Přístupový token je nutné získat před voláním rozhraní API Partnerské centrum rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="94cc4-180">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="94cc4-181">K získání přístupového tokenu musíte použít obnovovací token, protože přístupové tokeny mají obecně velmi omezenou životnost (například méně než hodinu).</span><span class="sxs-lookup"><span data-stu-id="94cc4-181">You must use a refresh token to obtain an access token because access tokens generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="94cc4-182">Zástupný text požadavku:</span><span class="sxs-lookup"><span data-stu-id="94cc4-182">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="94cc4-183">Text požadavku:</span><span class="sxs-lookup"><span data-stu-id="94cc4-183">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="94cc4-184">Odpověď zástupného symbolu:</span><span class="sxs-lookup"><span data-stu-id="94cc4-184">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="94cc4-185">Text odpovědi:</span><span class="sxs-lookup"><span data-stu-id="94cc4-185">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="94cc4-186">Volání Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="94cc4-186">Make Partner Center API calls</span></span>

<span data-ttu-id="94cc4-187">Přístupový token musíte použít k volání rozhraní API Partnerské centrum api.</span><span class="sxs-lookup"><span data-stu-id="94cc4-187">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="94cc4-188">Podívejte se na následující příklad volání.</span><span class="sxs-lookup"><span data-stu-id="94cc4-188">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="94cc4-189">Příklad Partnerské centrum rozhraní API</span><span class="sxs-lookup"><span data-stu-id="94cc4-189">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="94cc4-190">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94cc4-190">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="94cc4-191">Pomocí modulu [Partnerské centrum PowerShell můžete](https://www.powershellgallery.com/packages/PartnerCenter) snížit požadovanou infrastrukturu pro výměnu autorizačního kódu pro přístupový token.</span><span class="sxs-lookup"><span data-stu-id="94cc4-191">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="94cc4-192">Tato metoda je volitelná pro [Partnerské centrum volání REST.](#rest)</span><span class="sxs-lookup"><span data-stu-id="94cc4-192">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="94cc4-193">Další informace o tomto procesu najdete v dokumentaci [k Secure Model aplikací](/powershell/partnercenter/secure-app-model) PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="94cc4-193">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="94cc4-194">Nainstalujte azure AD a Partnerské centrum moduly PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="94cc4-194">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="94cc4-195">Pomocí příkazu **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** proveďte proces souhlasu a zachyťte požadovaný obnovovací token.</span><span class="sxs-lookup"><span data-stu-id="94cc4-195">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="94cc4-196">Parametr **ServicePrincipal** se používá s příkazem **New-PartnerAccessToken,** protože se používá aplikace Azure AD s typem webu nebo rozhraní **API.**</span><span class="sxs-lookup"><span data-stu-id="94cc4-196">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="94cc4-197">Tento typ aplikace vyžaduje, aby byl do žádosti o přístupový token zahrnutý identifikátor klienta a tajný kód.</span><span class="sxs-lookup"><span data-stu-id="94cc4-197">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="94cc4-198">Po **vyvolání příkazu Get-Credential** se zobrazí výzva k zadání uživatelského jména a hesla.</span><span class="sxs-lookup"><span data-stu-id="94cc4-198">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="94cc4-199">Jako uživatelské jméno zadejte identifikátor aplikace.</span><span class="sxs-lookup"><span data-stu-id="94cc4-199">Enter the application identifier as the username.</span></span> <span data-ttu-id="94cc4-200">Jako heslo zadejte tajný klíč aplikace.</span><span class="sxs-lookup"><span data-stu-id="94cc4-200">Enter the application secret as the password.</span></span> <span data-ttu-id="94cc4-201">Po vyvolání příkazu **New-PartnerAccessToken** se zobrazí výzva k zadání přihlašovacích údajů znovu.</span><span class="sxs-lookup"><span data-stu-id="94cc4-201">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="94cc4-202">Zadejte pověření pro účet služby, který používáte.</span><span class="sxs-lookup"><span data-stu-id="94cc4-202">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="94cc4-203">Tento účet služby by měl být partnerským účtem s příslušnými oprávněními.</span><span class="sxs-lookup"><span data-stu-id="94cc4-203">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="94cc4-204">Zkopírujte hodnotu obnovovacího tokenu.</span><span class="sxs-lookup"><span data-stu-id="94cc4-204">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="94cc4-205">Hodnotu obnovovacího tokenu byste měli uložit do zabezpečeného úložiště, například Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="94cc4-205">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="94cc4-206">Další informace o tom, jak použít modul zabezpečení aplikace pomocí prostředí PowerShell, najdete v článku [Multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) .</span><span class="sxs-lookup"><span data-stu-id="94cc4-206">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
