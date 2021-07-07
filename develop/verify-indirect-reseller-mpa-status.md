---
title: Ověření stavu podepisování Smlouva s partnerem Microsoftu prodejce
description: Pomocí rozhraní AGREEMENTStatus API můžete ověřit, jestli nepřímý prodejce smlouvu Smlouva s partnerem Microsoftu.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f83acc61624a72354c390905b1250bc021dd39aa
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529830"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="6e4f3-103">Ověření stavu podepisování Smlouva s partnerem Microsoftu prodejce</span><span class="sxs-lookup"><span data-stu-id="6e4f3-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="6e4f3-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6e4f3-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6e4f3-105">Pomocí ID tenanta (Microsoft ID) Microsoft Partner Network (PGA/PLA) nebo CLOUD SOLUTION PROVIDER (CSP) můžete ověřit, jestli nepřímý prodejce smlouvu Smlouva s partnerem Microsoftu podepsal.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-105">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="6e4f3-106">Pomocí jednoho z těchto identifikátorů můžete zkontrolovat stav podepisování Smlouva s partnerem Microsoftu pomocí rozhraní **AgreementStatus** API.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-106">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e4f3-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6e4f3-107">Prerequisites</span></span>

- <span data-ttu-id="6e4f3-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6e4f3-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6e4f3-109">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6e4f3-110">ID MPN (PGA/PLA) nebo ID tenanta CSP (Microsoft ID) nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-110">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="6e4f3-111">*Musíte použít jeden z těchto dvou identifikátorů.*</span><span class="sxs-lookup"><span data-stu-id="6e4f3-111">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="6e4f3-112">C\#</span><span class="sxs-lookup"><span data-stu-id="6e4f3-112">C\#</span></span>

<span data-ttu-id="6e4f3-113">Získání stavu Smlouva s partnerem Microsoftu podpisu nepřímého prodejce:</span><span class="sxs-lookup"><span data-stu-id="6e4f3-113">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="6e4f3-114">Pomocí kolekce **IAggregatePartner.Compliance** zavolejte vlastnost **AgreementSignatureStatus.**</span><span class="sxs-lookup"><span data-stu-id="6e4f3-114">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="6e4f3-115">Volejte [**metodu Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)</span><span class="sxs-lookup"><span data-stu-id="6e4f3-115">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="6e4f3-116">Ukázka: **[Konzolová testovací aplikace](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="6e4f3-116">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="6e4f3-117">Project: **PartnerCenterSDK.FeaturesSamples**</span><span class="sxs-lookup"><span data-stu-id="6e4f3-117">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="6e4f3-118">Třída: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="6e4f3-118">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6e4f3-119">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="6e4f3-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6e4f3-120">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="6e4f3-120">Request syntax</span></span>

| <span data-ttu-id="6e4f3-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="6e4f3-121">Method</span></span> | <span data-ttu-id="6e4f3-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="6e4f3-122">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="6e4f3-123">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="6e4f3-123">**GET**</span></span> | <span data-ttu-id="6e4f3-124">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{Název Programu}/agreementstatus?mpnId={MpnId}&tenantId={ID tenanta}</span><span class="sxs-lookup"><span data-stu-id="6e4f3-124">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="6e4f3-125">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="6e4f3-125">URI parameters</span></span>

<span data-ttu-id="6e4f3-126">K identifikaci partnera musíte zadat jeden z následujících dvou parametrů dotazu.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-126">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="6e4f3-127">Pokud jeden z těchto dvou parametrů dotazu nezadáte, zobrazí se **chyba 400 (Chybný** požadavek).</span><span class="sxs-lookup"><span data-stu-id="6e4f3-127">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="6e4f3-128">Název</span><span class="sxs-lookup"><span data-stu-id="6e4f3-128">Name</span></span> | <span data-ttu-id="6e4f3-129">Typ</span><span class="sxs-lookup"><span data-stu-id="6e4f3-129">Type</span></span> | <span data-ttu-id="6e4f3-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="6e4f3-130">Required</span></span> | <span data-ttu-id="6e4f3-131">Popis</span><span class="sxs-lookup"><span data-stu-id="6e4f3-131">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="6e4f3-132">**ID mpn**</span><span class="sxs-lookup"><span data-stu-id="6e4f3-132">**MpnId**</span></span> | <span data-ttu-id="6e4f3-133">int</span><span class="sxs-lookup"><span data-stu-id="6e4f3-133">int</span></span> | <span data-ttu-id="6e4f3-134">No</span><span class="sxs-lookup"><span data-stu-id="6e4f3-134">No</span></span> | <span data-ttu-id="6e4f3-135">ID Microsoft Partner Network (PGA/PLA), které identifikuje nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-135">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="6e4f3-136">**ID tenanta**</span><span class="sxs-lookup"><span data-stu-id="6e4f3-136">**TenantId**</span></span> | <span data-ttu-id="6e4f3-137">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="6e4f3-137">GUID</span></span> | <span data-ttu-id="6e4f3-138">No</span><span class="sxs-lookup"><span data-stu-id="6e4f3-138">No</span></span> | <span data-ttu-id="6e4f3-139">Id Microsoftu, které identifikuje účet CSP nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-139">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6e4f3-140">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="6e4f3-140">Request headers</span></span>

<span data-ttu-id="6e4f3-141">Další informace najdete v tématu [Partnerské centrum REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6e4f3-141">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="6e4f3-142">Příklady požadavků</span><span class="sxs-lookup"><span data-stu-id="6e4f3-142">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="6e4f3-143">Žádost s využitím ID MPN (PGA/PLA)</span><span class="sxs-lookup"><span data-stu-id="6e4f3-143">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="6e4f3-144">Následující příklad požadavku získá stav podepisování Smlouva s partnerem Microsoftu nepřímého prodejce s použitím ID Microsoft Partner Network prodejce.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-144">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="6e4f3-145">Žádost s využitím ID tenanta CSP</span><span class="sxs-lookup"><span data-stu-id="6e4f3-145">Request using CSP tenant ID</span></span>

<span data-ttu-id="6e4f3-146">Následující příklad požadavku získá stav podepisování Smlouva s partnerem Microsoftu nepřímého prodejce pomocí ID tenanta CSP nepřímého prodejce (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="6e4f3-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6e4f3-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="6e4f3-147">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6e4f3-148">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="6e4f3-148">Response success and error codes</span></span>

<span data-ttu-id="6e4f3-149">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6e4f3-150">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6e4f3-151">Úplný seznam najdete v Partnerské centrum [REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6e4f3-151">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="6e4f3-152">Příklad odpovědi (úspěch)</span><span class="sxs-lookup"><span data-stu-id="6e4f3-152">Response example (success)</span></span>

<span data-ttu-id="6e4f3-153">Následující příklad odpovědi úspěšně vrátí, jestli nepřímý prodejce smlouvu Smlouva s partnerem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-153">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a><span data-ttu-id="6e4f3-154">Příklady odpovědí (selhání)</span><span class="sxs-lookup"><span data-stu-id="6e4f3-154">Response examples (failure)</span></span>

<span data-ttu-id="6e4f3-155">Odpovědi podobné následujícím příkladům můžete dostávat v případě, že stav podepisování nepřímého prodejce Smlouva s partnerem Microsoftu nelze vrátit.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-155">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="6e4f3-156">ID tenanta CSP, který není formátovaný guid</span><span class="sxs-lookup"><span data-stu-id="6e4f3-156">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="6e4f3-157">Následující příklad odpovědi se vrátí, když ID tenanta CSP, které jste předáli rozhraní API, není identifikátor GUID.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-157">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="6e4f3-158">Necílové ID MPN</span><span class="sxs-lookup"><span data-stu-id="6e4f3-158">Non-numeric MPN ID</span></span>

<span data-ttu-id="6e4f3-159">Následující příklad odpovědi se vrátí, když ID MPN (PGA/PLA), které jste předali rozhraní API, není číselné.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-159">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="6e4f3-160">Žádné ID MPN nebo ID tenanta CSP</span><span class="sxs-lookup"><span data-stu-id="6e4f3-160">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="6e4f3-161">Následující příklad odpovědi se vrátí, když do rozhraní API předáte ID MPN (PGA/PLA) nebo ID tenanta CSP.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-161">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="6e4f3-162">Rozhraní API musíte předat jeden ze dvou typů ID.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-162">You must pass one of the two ID types to the API.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="6e4f3-163">Předané ID tenanta MPN i ID tenanta CSP</span><span class="sxs-lookup"><span data-stu-id="6e4f3-163">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="6e4f3-164">Následující příklad odpovědi se vrátí, když do rozhraní API předáte ID MPN (PGA/PLA) i ID tenanta CSP.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-164">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="6e4f3-165">Rozhraní API *musíte předat* pouze jeden ze dvou typů identifikátorů.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-165">You must pass *only one* of the two identifier types to the API.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="6e4f3-166">CSP Indirect Reseller ID MPN (PGA/PLA) je neplatné nebo se nemigruje z Partner Membership Center na Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="6e4f3-166">CSP Indirect Reseller MPN ID (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="6e4f3-167">Následující příklad odpovědi se vrátí, když je předané ID MPN nepřímého prodejce (PGA nebo PLA) neplatné nebo se nemigruje z Partner Membership Center na Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-167">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="6e4f3-168">Další informace</span><span class="sxs-lookup"><span data-stu-id="6e4f3-168">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="6e4f3-169">CSP Indirect Provider oblasti CSP Indirect Reseller oblasti se neshodují.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-169">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="6e4f3-170">Následující příklad odpovědi se vrátí, když se oblast ID MPN nepřímého prodejce (PGA/PLA) neshoduje s oblastí nepřímého poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-170">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="6e4f3-171">[Přečtěte si další](/partner-center/mpa-indirect-provider-faq) informace o oblastech CSP.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-171">[Learn more](/partner-center/mpa-indirect-provider-faq) about CSP Regions.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="6e4f3-172">CSP Indirect Reseller účet existuje v Partnerské centrum, ale ještě nepodepsal MPA.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-172">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="6e4f3-173">Následující příklad odpovědi se vrátí, CSP Indirect Reseller účet v Partnerské centrum ještě podepsání MPA.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-173">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="6e4f3-174">Další informace</span><span class="sxs-lookup"><span data-stu-id="6e4f3-174">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="6e4f3-175">K CSP Indirect Reseller ID MPN není přidružený žádný účet.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-175">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="6e4f3-176">Následující příklad odpovědi se vrátí, když Partnerské centrum rozpozná ID MPN (PGA/PLA) předané v požadavku, ale k danému ID MPN (PGA/PLA) není přidružená žádná registrace CSP.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-176">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="6e4f3-177">Další informace</span><span class="sxs-lookup"><span data-stu-id="6e4f3-177">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a><span data-ttu-id="6e4f3-178">Neplatné ID tenanta</span><span class="sxs-lookup"><span data-stu-id="6e4f3-178">Invalid Tenant ID</span></span>

<span data-ttu-id="6e4f3-179">Následující příklad odpovědi se vrátí, Partnerské centrum nenajde žádný účet přidružený k ID tenanta předané v požadavku.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-179">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="6e4f3-180">S daným ID tenanta se nenašlo žádné MPA</span><span class="sxs-lookup"><span data-stu-id="6e4f3-180">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="6e4f3-181">Následující příklad odpovědi se vrátí, Partnerské centrum nemůže najít žádný podpis MPA s daným ID tenanta.</span><span class="sxs-lookup"><span data-stu-id="6e4f3-181">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span> [<span data-ttu-id="6e4f3-182">Další informace</span><span class="sxs-lookup"><span data-stu-id="6e4f3-182">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```