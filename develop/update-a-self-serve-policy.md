---
title: Aktualizace samoobslužné zásady
description: Jak aktualizovat zásady pro samoobslužné zpracování.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4d53ab8e5b8ef5b7be83360a3f43ec7791b2e3b4
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/08/2020
ms.locfileid: "97767158"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="a551f-103">Aktualizovat SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a551f-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="a551f-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="a551f-104">**Applies to:**</span></span>

- <span data-ttu-id="a551f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="a551f-105">Partner Center</span></span>

<span data-ttu-id="a551f-106">Toto téma vysvětluje, jak aktualizovat zásadu samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="a551f-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a551f-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a551f-107">Prerequisites</span></span>

- <span data-ttu-id="a551f-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a551f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a551f-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="a551f-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a551f-110">C\#</span><span class="sxs-lookup"><span data-stu-id="a551f-110">C\#</span></span>

<span data-ttu-id="a551f-111">Postup odstranění samoobslužné zásady:</span><span class="sxs-lookup"><span data-stu-id="a551f-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="a551f-112">Voláním metody [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) s identifikátorem entity načtěte rozhraní pro operace s těmito zásadami.</span><span class="sxs-lookup"><span data-stu-id="a551f-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="a551f-113">Chcete-li aktualizovat zásadu samoobslužného zpracování, zavolejte metodu [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) nebo [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) .</span><span class="sxs-lookup"><span data-stu-id="a551f-113">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="a551f-114">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="a551f-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a551f-115">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="a551f-115">Request syntax</span></span>

| <span data-ttu-id="a551f-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="a551f-116">Method</span></span>   | <span data-ttu-id="a551f-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a551f-117">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="a551f-118">**PUT**</span><span class="sxs-lookup"><span data-stu-id="a551f-118">**PUT**</span></span> | <span data-ttu-id="a551f-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a551f-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a551f-120">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a551f-120">Request headers</span></span>

- <span data-ttu-id="a551f-121">Identifikátor požadavku a identifikátor korelace jsou povinné.</span><span class="sxs-lookup"><span data-stu-id="a551f-121">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="a551f-122">Další informace najdete v tématu [záhlaví REST v partnerském centru](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="a551f-122">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="a551f-123">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a551f-123">Request body</span></span>

<span data-ttu-id="a551f-124">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="a551f-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="a551f-125">Název</span><span class="sxs-lookup"><span data-stu-id="a551f-125">Name</span></span>                              | <span data-ttu-id="a551f-126">Typ</span><span class="sxs-lookup"><span data-stu-id="a551f-126">Type</span></span>   | <span data-ttu-id="a551f-127">Description</span><span class="sxs-lookup"><span data-stu-id="a551f-127">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="a551f-128">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a551f-128">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="a551f-129">object</span><span class="sxs-lookup"><span data-stu-id="a551f-129">object</span></span> | <span data-ttu-id="a551f-130">Informace o zásadách samostatného poskytování.</span><span class="sxs-lookup"><span data-stu-id="a551f-130">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="a551f-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="a551f-131">SelfServePolicy</span></span>

<span data-ttu-id="a551f-132">Tato tabulka popisuje minimální požadovaná pole z prostředku [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) , který je potřeba k vytvoření nových samoobslužných zásad.</span><span class="sxs-lookup"><span data-stu-id="a551f-132">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="a551f-133">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a551f-133">Property</span></span>              | <span data-ttu-id="a551f-134">Typ</span><span class="sxs-lookup"><span data-stu-id="a551f-134">Type</span></span>             | <span data-ttu-id="a551f-135">Description</span><span class="sxs-lookup"><span data-stu-id="a551f-135">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a551f-136">id</span><span class="sxs-lookup"><span data-stu-id="a551f-136">id</span></span>                    | <span data-ttu-id="a551f-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="a551f-137">string</span></span>           | <span data-ttu-id="a551f-138">Identifikátor zásady, který se poskytuje po úspěšném vytvoření zásady samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="a551f-138">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="a551f-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="a551f-139">SelfServeEntity</span></span>       | <span data-ttu-id="a551f-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="a551f-140">SelfServeEntity</span></span>  | <span data-ttu-id="a551f-141">Entita, která má udělen přístup k sobě.</span><span class="sxs-lookup"><span data-stu-id="a551f-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="a551f-142">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="a551f-142">Grantor</span></span>               | <span data-ttu-id="a551f-143">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="a551f-143">Grantor</span></span>          | <span data-ttu-id="a551f-144">Uděluje udělení přístupu.</span><span class="sxs-lookup"><span data-stu-id="a551f-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="a551f-145">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="a551f-145">Permissions</span></span>           | <span data-ttu-id="a551f-146">Pole oprávnění</span><span class="sxs-lookup"><span data-stu-id="a551f-146">Array of Permission</span></span>| <span data-ttu-id="a551f-147">Pole prostředků [oprávnění](self-serve-policy-resources.md#permission)</span><span class="sxs-lookup"><span data-stu-id="a551f-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="a551f-148">Značk</span><span class="sxs-lookup"><span data-stu-id="a551f-148">Etag</span></span>                  | <span data-ttu-id="a551f-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="a551f-149">string</span></span>           | <span data-ttu-id="a551f-150">Značka ETag</span><span class="sxs-lookup"><span data-stu-id="a551f-150">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="a551f-151">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a551f-151">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

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

## <a name="rest-response"></a><span data-ttu-id="a551f-152">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a551f-152">REST response</span></span>

<span data-ttu-id="a551f-153">V případě úspěchu toto rozhraní API vrátí prostředek [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) pro aktualizované zásady samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="a551f-153">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a551f-154">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="a551f-154">Response success and error codes</span></span>

<span data-ttu-id="a551f-155">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a551f-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a551f-156">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="a551f-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a551f-157">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a551f-157">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="a551f-158">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="a551f-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="a551f-159">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="a551f-159">HTTP Status Code</span></span>     | <span data-ttu-id="a551f-160">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="a551f-160">Error code</span></span>   | <span data-ttu-id="a551f-161">Description</span><span class="sxs-lookup"><span data-stu-id="a551f-161">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="a551f-162">404</span><span class="sxs-lookup"><span data-stu-id="a551f-162">404</span></span>                  | <span data-ttu-id="a551f-163">600039</span><span class="sxs-lookup"><span data-stu-id="a551f-163">600039</span></span>       | <span data-ttu-id="a551f-164">Zásady samoobslužné podpory nebyly nalezeny.</span><span class="sxs-lookup"><span data-stu-id="a551f-164">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="a551f-165">404</span><span class="sxs-lookup"><span data-stu-id="a551f-165">404</span></span>                  | <span data-ttu-id="a551f-166">600040</span><span class="sxs-lookup"><span data-stu-id="a551f-166">600040</span></span>       | <span data-ttu-id="a551f-167">Identifikátor zásady samoobslužného ovládání není správný.</span><span class="sxs-lookup"><span data-stu-id="a551f-167">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="a551f-168">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a551f-168">Response example</span></span>

```http
HTTP/1.1 200 Ok
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
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
