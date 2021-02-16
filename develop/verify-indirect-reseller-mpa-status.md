---
title: Ověření stavu podepisování smlouvy Microsoft Partner pro nepřímý prodejce
description: Pomocí rozhraní AgreementStatus API můžete ověřit, jestli se nepřímý prodejce zaregistroval v rámci smlouvy o partnerovi Microsoftu.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9501f245a6c98fa90e77de7bc0caed8ca51fa4f2
ms.sourcegitcommit: 40baf4d825ce0ca6a254b5f368c308f025be7034
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/16/2021
ms.locfileid: "100537572"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="b4f45-103">Ověření stavu podepisování smlouvy Microsoft Partner pro nepřímý prodejce</span><span class="sxs-lookup"><span data-stu-id="b4f45-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="b4f45-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="b4f45-104">**Applies to:**</span></span>

- <span data-ttu-id="b4f45-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b4f45-105">Partner Center</span></span>
- <span data-ttu-id="b4f45-106">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b4f45-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b4f45-107">Můžete ověřit, jestli nepřímý prodejce podepsal smlouvu s partnerem Microsoftu pomocí svého Microsoft Partner Network (MPN) ID (PGA/PLA) nebo ID tenanta Cloud Solution Provider (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="b4f45-107">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="b4f45-108">Jeden z těchto identifikátorů můžete použít ke kontrole stavu podepisování smlouvy Microsoft Partner pomocí rozhraní **AgreementStatus** API.</span><span class="sxs-lookup"><span data-stu-id="b4f45-108">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4f45-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b4f45-109">Prerequisites</span></span>

- <span data-ttu-id="b4f45-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b4f45-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b4f45-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b4f45-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b4f45-112">ID MPN (PGA/PLA) nebo ID tenanta CSP (Microsoft ID) nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="b4f45-112">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="b4f45-113">*Je nutné použít jeden z těchto dvou identifikátorů.*</span><span class="sxs-lookup"><span data-stu-id="b4f45-113">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="b4f45-114">C\#</span><span class="sxs-lookup"><span data-stu-id="b4f45-114">C\#</span></span>

<span data-ttu-id="b4f45-115">Postup získání stavu podpisu partnerské smlouvy Microsoftu pro nepřímý prodejce:</span><span class="sxs-lookup"><span data-stu-id="b4f45-115">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="b4f45-116">Pomocí kolekce **IAggregatePartner. dodržování předpisů** zavolejte vlastnost **AgreementSignatureStatus** .</span><span class="sxs-lookup"><span data-stu-id="b4f45-116">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="b4f45-117">Zavolejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) .</span><span class="sxs-lookup"><span data-stu-id="b4f45-117">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="b4f45-118">Ukázka: **[aplikace testů konzoly](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="b4f45-118">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="b4f45-119">Projekt: **PartnerCenterSDK. FeaturesSamples**</span><span class="sxs-lookup"><span data-stu-id="b4f45-119">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="b4f45-120">Třída: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="b4f45-120">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="b4f45-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b4f45-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b4f45-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b4f45-122">Request syntax</span></span>

| <span data-ttu-id="b4f45-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="b4f45-123">Method</span></span> | <span data-ttu-id="b4f45-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b4f45-124">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="b4f45-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b4f45-125">**GET**</span></span> | <span data-ttu-id="b4f45-126">*[{baseURL}](partner-center-rest-urls.md)*/v1/Compliance/{programname}/agreementstatus? mpnId = {mpnId} &tenantId = {tenantId}</span><span class="sxs-lookup"><span data-stu-id="b4f45-126">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b4f45-127">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="b4f45-127">URI parameters</span></span>

<span data-ttu-id="b4f45-128">Chcete-li identifikovat partnera, je nutné zadat jeden z následujících dvou parametrů dotazu.</span><span class="sxs-lookup"><span data-stu-id="b4f45-128">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="b4f45-129">Pokud neposkytnete jeden z těchto dvou parametrů dotazu, zobrazí se chyba **400 (chybná žádost)** .</span><span class="sxs-lookup"><span data-stu-id="b4f45-129">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="b4f45-130">Název</span><span class="sxs-lookup"><span data-stu-id="b4f45-130">Name</span></span> | <span data-ttu-id="b4f45-131">Typ</span><span class="sxs-lookup"><span data-stu-id="b4f45-131">Type</span></span> | <span data-ttu-id="b4f45-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b4f45-132">Required</span></span> | <span data-ttu-id="b4f45-133">Popis</span><span class="sxs-lookup"><span data-stu-id="b4f45-133">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="b4f45-134">**MpnId**</span><span class="sxs-lookup"><span data-stu-id="b4f45-134">**MpnId**</span></span> | <span data-ttu-id="b4f45-135">int</span><span class="sxs-lookup"><span data-stu-id="b4f45-135">int</span></span> | <span data-ttu-id="b4f45-136">Ne</span><span class="sxs-lookup"><span data-stu-id="b4f45-136">No</span></span> | <span data-ttu-id="b4f45-137">ID Microsoft Partner Network (PGA/PLA), které identifikuje nepřímý prodejce.</span><span class="sxs-lookup"><span data-stu-id="b4f45-137">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="b4f45-138">**TenantId**</span><span class="sxs-lookup"><span data-stu-id="b4f45-138">**TenantId**</span></span> | <span data-ttu-id="b4f45-139">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="b4f45-139">GUID</span></span> | <span data-ttu-id="b4f45-140">Ne</span><span class="sxs-lookup"><span data-stu-id="b4f45-140">No</span></span> | <span data-ttu-id="b4f45-141">ID společnosti Microsoft, které identifikuje účet CSP nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="b4f45-141">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b4f45-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b4f45-142">Request headers</span></span>

<span data-ttu-id="b4f45-143">Další informace najdete v [partnerském centru REST](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b4f45-143">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="b4f45-144">Příklady požadavků</span><span class="sxs-lookup"><span data-stu-id="b4f45-144">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="b4f45-145">Žádost s použitím ID MPN (PGA/PLA)</span><span class="sxs-lookup"><span data-stu-id="b4f45-145">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="b4f45-146">Následující příklad žádosti získá nepřímý prodejce na stav podepisování smlouvy o partnerovi Microsoftu pomocí Microsoft Partner Network ID nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="b4f45-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="b4f45-147">Žádost o použití ID tenanta CSP</span><span class="sxs-lookup"><span data-stu-id="b4f45-147">Request using CSP tenant ID</span></span>

<span data-ttu-id="b4f45-148">Následující příklad žádosti získá nepřímý prodejce na stav podepisování smlouvy o partnerovi Microsoftu pomocí ID tenanta CSP nepřímého prodejce (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="b4f45-148">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="b4f45-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b4f45-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b4f45-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b4f45-150">Response success and error codes</span></span>

<span data-ttu-id="b4f45-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b4f45-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b4f45-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b4f45-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b4f45-153">Úplný seznam najdete v tématu [Chyba REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b4f45-153">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="b4f45-154">Příklad odpovědi (úspěch)</span><span class="sxs-lookup"><span data-stu-id="b4f45-154">Response example (success)</span></span>

<span data-ttu-id="b4f45-155">Následující příklad odpovědi úspěšně vrátí, jestli nepřímý prodejce podepsal smlouvu s partnerem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="b4f45-155">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

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

### <a name="response-examples-failure"></a><span data-ttu-id="b4f45-156">Příklady odezvy (neúspěch)</span><span class="sxs-lookup"><span data-stu-id="b4f45-156">Response examples (failure)</span></span>

<span data-ttu-id="b4f45-157">Pokud stav podepisování smlouvy Microsoft Partner na nepřímý prodejce nemůžete vrátit, můžete dostávat odpovědi podobné následujícím příkladům.</span><span class="sxs-lookup"><span data-stu-id="b4f45-157">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="b4f45-158">ID tenanta CSP naformátovaného jiným IDENTIFIKÁTORem</span><span class="sxs-lookup"><span data-stu-id="b4f45-158">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="b4f45-159">V případě, že ID tenanta CSP, které jste předali do rozhraní API, není identifikátor GUID, vrátí se následující příklad odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b4f45-159">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

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

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="b4f45-160">ID programu MPN, které není číselné</span><span class="sxs-lookup"><span data-stu-id="b4f45-160">Non-numeric MPN ID</span></span>

<span data-ttu-id="b4f45-161">Následující příklad odpovědi se vrátí, když ID MPN (PGA/PLA), které jste předali do rozhraní API, není číselné.</span><span class="sxs-lookup"><span data-stu-id="b4f45-161">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="b4f45-162">Žádné ID MPN nebo ID tenanta CSP</span><span class="sxs-lookup"><span data-stu-id="b4f45-162">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="b4f45-163">Následující příklad odpovědi se vrátí, když jste neprošli předáním ID MPN (PGA/PLA) nebo ID tenanta CSP do rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="b4f45-163">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="b4f45-164">Do rozhraní API musíte předat jeden ze dvou typů ID.</span><span class="sxs-lookup"><span data-stu-id="b4f45-164">You must pass one of the two ID types to the API.</span></span>

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="b4f45-165">Bylo předáno ID MPN i ID tenanta CSP.</span><span class="sxs-lookup"><span data-stu-id="b4f45-165">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="b4f45-166">Následující příklad odpovědi je vrácen při předání ID MPN (PGA/PLA) a ID tenanta CSP do rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="b4f45-166">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="b4f45-167">Rozhraní API musíte předat *jenom jeden* ze dvou typů identifikátorů.</span><span class="sxs-lookup"><span data-stu-id="b4f45-167">You must pass *only one* of the two identifier types to the API.</span></span>

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="b4f45-168">ID programu MPN pro nepřímý prodej CSP (PGA/PLA) není platné nebo se nemigruje z partnerského centra pro členství do partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b4f45-168">CSP Indirect Reseller MPN Id (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="b4f45-169">Následující příklad odpovědi se vrátí, když předaný nepřímý prodejce MPN (PGA/PLA) buď není platný, nebo není migrován z partnerského centra členství v partnerském centru.</span><span class="sxs-lookup"><span data-stu-id="b4f45-169">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="b4f45-170">Další informace</span><span class="sxs-lookup"><span data-stu-id="b4f45-170">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="b4f45-171">Oblast nepřímých poskytovatelů CSP a oblast nepřímých prodejců CSP se neshoduje.</span><span class="sxs-lookup"><span data-stu-id="b4f45-171">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="b4f45-172">Následující příklad odpovědi se vrátí, pokud oblast nepřímých prodejců (PGA/PLA) neodpovídá oblasti nepřímého zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="b4f45-172">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="b4f45-173">[Přečtěte si další informace](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq) o oblastech CSP.</span><span class="sxs-lookup"><span data-stu-id="b4f45-173">[Learn more](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq) about CSP Regions.</span></span>

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

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="b4f45-174">Účet nepřímého prodejce CSP existuje v partnerském centru, ale nepodepsal aktivaci.</span><span class="sxs-lookup"><span data-stu-id="b4f45-174">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="b4f45-175">Následující příklad odpovědi se vrátí, když účet nepřímý prodejce CSP v partnerském centru nepodepsal aktivaci.</span><span class="sxs-lookup"><span data-stu-id="b4f45-175">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="b4f45-176">Další informace</span><span class="sxs-lookup"><span data-stu-id="b4f45-176">Learn More</span></span>](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

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

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="b4f45-177">K danému ID MPN není přidružený žádný účet nepřímý prodejce CSP.</span><span class="sxs-lookup"><span data-stu-id="b4f45-177">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="b4f45-178">Následující příklad odpovědi se vrátí, když partnerské Centrum dokáže rozpoznat ID MPN (PGA/PLA) předané v žádosti, ale k danému ID MPN (PGA/PLA) se nepřidruží žádný zápis CSP.</span><span class="sxs-lookup"><span data-stu-id="b4f45-178">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="b4f45-179">Další informace</span><span class="sxs-lookup"><span data-stu-id="b4f45-179">Learn More</span></span>](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

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

#### <a name="invalid-tenant-id"></a><span data-ttu-id="b4f45-180">Neplatné ID tenanta</span><span class="sxs-lookup"><span data-stu-id="b4f45-180">Invalid Tenant ID</span></span>

<span data-ttu-id="b4f45-181">Následující příklad odpovědi se vrátí, když Partnerská centra nenajde žádný účet přidružený k ID tenanta předanému v žádosti.</span><span class="sxs-lookup"><span data-stu-id="b4f45-181">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="b4f45-182">Nenašly se žádné technologie MPA s daným ID tenanta.</span><span class="sxs-lookup"><span data-stu-id="b4f45-182">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="b4f45-183">Následující příklad odpovědi se vrátí, když Partnerská centra nemůže najít žádný signaturu technologie MPA s daným ID tenanta.</span><span class="sxs-lookup"><span data-stu-id="b4f45-183">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span> [<span data-ttu-id="b4f45-184">Další informace</span><span class="sxs-lookup"><span data-stu-id="b4f45-184">Learn More</span></span>](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

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
