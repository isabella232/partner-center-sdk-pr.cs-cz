---
title: Vytvoření samoobslužné zásady
description: Jak vytvořit nové samoobslužné zásady
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14f46e22fbd294c765b745204cf62474250cbfbd
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973684"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="a89a8-103">Vytvoření zásady SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a89a8-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="a89a8-104">Tento článek vysvětluje, jak vytvořit nové samoobslužné zásady.</span><span class="sxs-lookup"><span data-stu-id="a89a8-104">This article explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a89a8-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a89a8-105">Prerequisites</span></span>

- <span data-ttu-id="a89a8-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a89a8-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a89a8-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="a89a8-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a89a8-108">C\#</span><span class="sxs-lookup"><span data-stu-id="a89a8-108">C\#</span></span>

<span data-ttu-id="a89a8-109">Vytvoření samoobslužné zásady:</span><span class="sxs-lookup"><span data-stu-id="a89a8-109">Create a self-serve policy:</span></span>

1. <span data-ttu-id="a89a8-110">Zavolejte [**metodu IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) nebo [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) s informacemi o samoobslužných zásadách.</span><span class="sxs-lookup"><span data-stu-id="a89a8-110">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

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

<span data-ttu-id="a89a8-111">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="a89a8-111">For an example, see the following:</span></span>

- <span data-ttu-id="a89a8-112">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a89a8-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a89a8-113">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="a89a8-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="a89a8-114">Třída: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="a89a8-114">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="a89a8-115">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="a89a8-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a89a8-116">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="a89a8-116">Request syntax</span></span>

| <span data-ttu-id="a89a8-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="a89a8-117">Method</span></span>   | <span data-ttu-id="a89a8-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a89a8-118">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="a89a8-119">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="a89a8-119">**POST**</span></span> | <span data-ttu-id="a89a8-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a89a8-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a89a8-121">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a89a8-121">Request headers</span></span>

- <span data-ttu-id="a89a8-122">Vyžaduje se ID požadavku a ID korelace.</span><span class="sxs-lookup"><span data-stu-id="a89a8-122">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="a89a8-123">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a89a8-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a89a8-124">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a89a8-124">Request body</span></span>

<span data-ttu-id="a89a8-125">Tato tabulka popisuje požadované vlastnosti v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="a89a8-125">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="a89a8-126">Název</span><span class="sxs-lookup"><span data-stu-id="a89a8-126">Name</span></span>                              | <span data-ttu-id="a89a8-127">Typ</span><span class="sxs-lookup"><span data-stu-id="a89a8-127">Type</span></span>   | <span data-ttu-id="a89a8-128">Description</span><span class="sxs-lookup"><span data-stu-id="a89a8-128">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="a89a8-129">Samoobslužné zásady</span><span class="sxs-lookup"><span data-stu-id="a89a8-129">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="a89a8-130">object</span><span class="sxs-lookup"><span data-stu-id="a89a8-130">object</span></span> | <span data-ttu-id="a89a8-131">Informace o samoobslužné zásadách.</span><span class="sxs-lookup"><span data-stu-id="a89a8-131">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="a89a8-132">Samoobslužné zásady</span><span class="sxs-lookup"><span data-stu-id="a89a8-132">SelfServePolicy</span></span>

<span data-ttu-id="a89a8-133">Tato tabulka popisuje minimální povinná pole z prostředku [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) potřebná k vytvoření nové samoobslužné zásady.</span><span class="sxs-lookup"><span data-stu-id="a89a8-133">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="a89a8-134">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a89a8-134">Property</span></span>              | <span data-ttu-id="a89a8-135">Typ</span><span class="sxs-lookup"><span data-stu-id="a89a8-135">Type</span></span>             | <span data-ttu-id="a89a8-136">Description</span><span class="sxs-lookup"><span data-stu-id="a89a8-136">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a89a8-137">Samoobslužná rezervace</span><span class="sxs-lookup"><span data-stu-id="a89a8-137">SelfServeEntity</span></span>       | <span data-ttu-id="a89a8-138">Samoobslužná rezervace</span><span class="sxs-lookup"><span data-stu-id="a89a8-138">SelfServeEntity</span></span>  | <span data-ttu-id="a89a8-139">Samoobslužná entita, které je udělen přístup.</span><span class="sxs-lookup"><span data-stu-id="a89a8-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="a89a8-140">Grantor</span><span class="sxs-lookup"><span data-stu-id="a89a8-140">Grantor</span></span>               | <span data-ttu-id="a89a8-141">Grantor</span><span class="sxs-lookup"><span data-stu-id="a89a8-141">Grantor</span></span>          | <span data-ttu-id="a89a8-142">Grantor, který uděluje přístup.</span><span class="sxs-lookup"><span data-stu-id="a89a8-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="a89a8-143">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="a89a8-143">Permissions</span></span>           | <span data-ttu-id="a89a8-144">Pole oprávnění</span><span class="sxs-lookup"><span data-stu-id="a89a8-144">Array of Permission</span></span>| <span data-ttu-id="a89a8-145">Pole [prostředků](self-serve-policy-resources.md#permission) oprávnění.</span><span class="sxs-lookup"><span data-stu-id="a89a8-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="a89a8-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a89a8-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a89a8-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a89a8-147">REST response</span></span>

<span data-ttu-id="a89a8-148">V případě úspěchu toto rozhraní API vrátí [prostředek SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) pro nové samoobslužné zásady.</span><span class="sxs-lookup"><span data-stu-id="a89a8-148">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a89a8-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="a89a8-149">Response success and error codes</span></span>

<span data-ttu-id="a89a8-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a89a8-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a89a8-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="a89a8-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a89a8-152">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a89a8-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="a89a8-153">Tato metoda vrátí následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="a89a8-153">This method returns the following error codes:</span></span>

| <span data-ttu-id="a89a8-154">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="a89a8-154">HTTP Status Code</span></span>     | <span data-ttu-id="a89a8-155">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="a89a8-155">Error code</span></span>   | <span data-ttu-id="a89a8-156">Description</span><span class="sxs-lookup"><span data-stu-id="a89a8-156">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="a89a8-157">409</span><span class="sxs-lookup"><span data-stu-id="a89a8-157">409</span></span>                  | <span data-ttu-id="a89a8-158">600041</span><span class="sxs-lookup"><span data-stu-id="a89a8-158">600041</span></span>       | <span data-ttu-id="a89a8-159">Samoobslužné zásady už existují.</span><span class="sxs-lookup"><span data-stu-id="a89a8-159">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="a89a8-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a89a8-160">Response example</span></span>

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
