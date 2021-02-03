---
title: Vytvoření samoobslužné zásady
description: Vytvoření nových samoobslužných zásad.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd1579b2775ead57a440db0d6afb3bf22164c319
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/08/2020
ms.locfileid: "97767150"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="0ed8b-103">Vytvoření SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="0ed8b-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="0ed8b-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="0ed8b-104">**Applies to:**</span></span>

- <span data-ttu-id="0ed8b-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0ed8b-105">Partner Center</span></span>

<span data-ttu-id="0ed8b-106">V tomto tématu se dozvíte, jak vytvořit nové zásady pro samoobslužné zpracování.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-106">This topic explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ed8b-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0ed8b-107">Prerequisites</span></span>

- <span data-ttu-id="0ed8b-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0ed8b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0ed8b-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="0ed8b-110">C\#</span><span class="sxs-lookup"><span data-stu-id="0ed8b-110">C\#</span></span>

<span data-ttu-id="0ed8b-111">Vytvoření samoobslužné zásady:</span><span class="sxs-lookup"><span data-stu-id="0ed8b-111">Create a self-serve policy:</span></span>

1. <span data-ttu-id="0ed8b-112">Zavolejte metodu [**IAggregatePartner. SelfServePolicies. Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) nebo [**IAggregatePartner. SelfServePolicies. CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) s informacemi o zásadách, které samy o sobě slouží.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-112">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string customerIdAsEntity;

var selfServePolicy = new SelfServePolicy
{
    SelfServeEntity = new SelfServeEntity
    {
        SelfServeEntityType = "customer",
        TenantID = customerIdAsEntity,
    },
    Grantor = new Grantor
    {
        GrantorType = "billToPartner",
        TenantID = partnerIdAsGrantor,
    },
    Permissions = new Permission[]
    {
        new Permission
        {
        Action = "Purchase",
        Resource = "AzureReservedInstances",
        },
    },
};

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// creates the self-serve policy
SelfServePolicy createdSelfServePolicy = scopedPartnerOperations.selfServePolicies.Create(selfServePolicy);
```

<span data-ttu-id="0ed8b-113">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="0ed8b-113">For an example, see the following:</span></span>

- <span data-ttu-id="0ed8b-114">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="0ed8b-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="0ed8b-115">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="0ed8b-115">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="0ed8b-116">Třída: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="0ed8b-116">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="0ed8b-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0ed8b-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0ed8b-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0ed8b-118">Request syntax</span></span>

| <span data-ttu-id="0ed8b-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="0ed8b-119">Method</span></span>   | <span data-ttu-id="0ed8b-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0ed8b-120">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="0ed8b-121">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="0ed8b-121">**POST**</span></span> | <span data-ttu-id="0ed8b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0ed8b-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0ed8b-123">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0ed8b-123">Request headers</span></span>

- <span data-ttu-id="0ed8b-124">Vyžaduje se ID žádosti a ID korelace.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-124">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="0ed8b-125">Další informace najdete v tématu [záhlaví REST v partnerském centru](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="0ed8b-125">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="0ed8b-126">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0ed8b-126">Request body</span></span>

<span data-ttu-id="0ed8b-127">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-127">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="0ed8b-128">Název</span><span class="sxs-lookup"><span data-stu-id="0ed8b-128">Name</span></span>                              | <span data-ttu-id="0ed8b-129">Typ</span><span class="sxs-lookup"><span data-stu-id="0ed8b-129">Type</span></span>   | <span data-ttu-id="0ed8b-130">Description</span><span class="sxs-lookup"><span data-stu-id="0ed8b-130">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="0ed8b-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="0ed8b-131">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="0ed8b-132">object</span><span class="sxs-lookup"><span data-stu-id="0ed8b-132">object</span></span> | <span data-ttu-id="0ed8b-133">Informace o zásadách samostatného poskytování.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-133">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="0ed8b-134">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="0ed8b-134">SelfServePolicy</span></span>

<span data-ttu-id="0ed8b-135">Tato tabulka popisuje minimální požadovaná pole z prostředku [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) , který je potřeba k vytvoření nových samoobslužných zásad.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-135">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="0ed8b-136">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="0ed8b-136">Property</span></span>              | <span data-ttu-id="0ed8b-137">Typ</span><span class="sxs-lookup"><span data-stu-id="0ed8b-137">Type</span></span>             | <span data-ttu-id="0ed8b-138">Description</span><span class="sxs-lookup"><span data-stu-id="0ed8b-138">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0ed8b-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="0ed8b-139">SelfServeEntity</span></span>       | <span data-ttu-id="0ed8b-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="0ed8b-140">SelfServeEntity</span></span>  | <span data-ttu-id="0ed8b-141">Entita, která má udělen přístup k sobě.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="0ed8b-142">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="0ed8b-142">Grantor</span></span>               | <span data-ttu-id="0ed8b-143">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="0ed8b-143">Grantor</span></span>          | <span data-ttu-id="0ed8b-144">Uděluje udělení přístupu.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="0ed8b-145">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="0ed8b-145">Permissions</span></span>           | <span data-ttu-id="0ed8b-146">Pole oprávnění</span><span class="sxs-lookup"><span data-stu-id="0ed8b-146">Array of Permission</span></span>| <span data-ttu-id="0ed8b-147">Pole prostředků [oprávnění](self-serve-policy-resources.md#permission)</span><span class="sxs-lookup"><span data-stu-id="0ed8b-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="0ed8b-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0ed8b-148">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="0ed8b-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0ed8b-149">REST response</span></span>

<span data-ttu-id="0ed8b-150">Pokud je toto rozhraní API úspěšné, vrátí [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) prostředek pro nové zásady samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-150">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0ed8b-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0ed8b-151">Response success and error codes</span></span>

<span data-ttu-id="0ed8b-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0ed8b-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0ed8b-154">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0ed8b-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="0ed8b-155">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="0ed8b-155">This method returns the following error codes:</span></span>

| <span data-ttu-id="0ed8b-156">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="0ed8b-156">HTTP Status Code</span></span>     | <span data-ttu-id="0ed8b-157">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="0ed8b-157">Error code</span></span>   | <span data-ttu-id="0ed8b-158">Description</span><span class="sxs-lookup"><span data-stu-id="0ed8b-158">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="0ed8b-159">409</span><span class="sxs-lookup"><span data-stu-id="0ed8b-159">409</span></span>                  | <span data-ttu-id="0ed8b-160">600041</span><span class="sxs-lookup"><span data-stu-id="0ed8b-160">600041</span></span>       | <span data-ttu-id="0ed8b-161">Samoobslužná zásada již existuje.</span><span class="sxs-lookup"><span data-stu-id="0ed8b-161">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="0ed8b-162">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0ed8b-162">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```
