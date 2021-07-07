---
title: Aktualizace samoobslužné zásady
description: Jak aktualizovat zásady pro samoobslužné zpracování.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d94382e73fd2a79751fe5f8f8414df2befde584f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445251"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="ed734-103">Aktualizovat SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ed734-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="ed734-104">Tento článek vysvětluje, jak aktualizovat zásadu samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="ed734-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed734-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ed734-105">Prerequisites</span></span>

- <span data-ttu-id="ed734-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ed734-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ed734-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ed734-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="ed734-108">C\#</span><span class="sxs-lookup"><span data-stu-id="ed734-108">C\#</span></span>

<span data-ttu-id="ed734-109">Postup odstranění samoobslužné zásady:</span><span class="sxs-lookup"><span data-stu-id="ed734-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="ed734-110">Voláním metody [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) s identifikátorem entity načtěte rozhraní pro operace s těmito zásadami.</span><span class="sxs-lookup"><span data-stu-id="ed734-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="ed734-111">Chcete-li aktualizovat zásadu samoobslužného zpracování, zavolejte metodu [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) nebo [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) .</span><span class="sxs-lookup"><span data-stu-id="ed734-111">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="ed734-112">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ed734-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ed734-113">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ed734-113">Request syntax</span></span>

| <span data-ttu-id="ed734-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="ed734-114">Method</span></span>   | <span data-ttu-id="ed734-115">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ed734-115">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="ed734-116">**PUT**</span><span class="sxs-lookup"><span data-stu-id="ed734-116">**PUT**</span></span> | <span data-ttu-id="ed734-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ed734-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ed734-118">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ed734-118">Request headers</span></span>

- <span data-ttu-id="ed734-119">Identifikátor požadavku a identifikátor korelace jsou povinné.</span><span class="sxs-lookup"><span data-stu-id="ed734-119">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="ed734-120">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ed734-120">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ed734-121">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ed734-121">Request body</span></span>

<span data-ttu-id="ed734-122">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="ed734-122">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="ed734-123">Název</span><span class="sxs-lookup"><span data-stu-id="ed734-123">Name</span></span>                              | <span data-ttu-id="ed734-124">Typ</span><span class="sxs-lookup"><span data-stu-id="ed734-124">Type</span></span>   | <span data-ttu-id="ed734-125">Description</span><span class="sxs-lookup"><span data-stu-id="ed734-125">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="ed734-126">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ed734-126">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="ed734-127">object</span><span class="sxs-lookup"><span data-stu-id="ed734-127">object</span></span> | <span data-ttu-id="ed734-128">Informace o zásadách samostatného poskytování.</span><span class="sxs-lookup"><span data-stu-id="ed734-128">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="ed734-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ed734-129">SelfServePolicy</span></span>

<span data-ttu-id="ed734-130">Tato tabulka popisuje minimální požadovaná pole z prostředku [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) , který je potřeba k vytvoření nových samoobslužných zásad.</span><span class="sxs-lookup"><span data-stu-id="ed734-130">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="ed734-131">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ed734-131">Property</span></span>              | <span data-ttu-id="ed734-132">Typ</span><span class="sxs-lookup"><span data-stu-id="ed734-132">Type</span></span>             | <span data-ttu-id="ed734-133">Description</span><span class="sxs-lookup"><span data-stu-id="ed734-133">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ed734-134">id</span><span class="sxs-lookup"><span data-stu-id="ed734-134">id</span></span>                    | <span data-ttu-id="ed734-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="ed734-135">string</span></span>           | <span data-ttu-id="ed734-136">Identifikátor zásady, který se poskytuje po úspěšném vytvoření zásady samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="ed734-136">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="ed734-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="ed734-137">SelfServeEntity</span></span>       | <span data-ttu-id="ed734-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="ed734-138">SelfServeEntity</span></span>  | <span data-ttu-id="ed734-139">Entita, která má udělen přístup k sobě.</span><span class="sxs-lookup"><span data-stu-id="ed734-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="ed734-140">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="ed734-140">Grantor</span></span>               | <span data-ttu-id="ed734-141">Udělovatel</span><span class="sxs-lookup"><span data-stu-id="ed734-141">Grantor</span></span>          | <span data-ttu-id="ed734-142">Uděluje udělení přístupu.</span><span class="sxs-lookup"><span data-stu-id="ed734-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="ed734-143">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="ed734-143">Permissions</span></span>           | <span data-ttu-id="ed734-144">Pole oprávnění</span><span class="sxs-lookup"><span data-stu-id="ed734-144">Array of Permission</span></span>| <span data-ttu-id="ed734-145">Pole prostředků [oprávnění](self-serve-policy-resources.md#permission)</span><span class="sxs-lookup"><span data-stu-id="ed734-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="ed734-146">Značk</span><span class="sxs-lookup"><span data-stu-id="ed734-146">Etag</span></span>                  | <span data-ttu-id="ed734-147">řetězec</span><span class="sxs-lookup"><span data-stu-id="ed734-147">string</span></span>           | <span data-ttu-id="ed734-148">Značka ETag</span><span class="sxs-lookup"><span data-stu-id="ed734-148">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="ed734-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ed734-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ed734-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ed734-150">REST response</span></span>

<span data-ttu-id="ed734-151">V případě úspěchu toto rozhraní API vrátí prostředek [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) pro aktualizované zásady samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="ed734-151">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ed734-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ed734-152">Response success and error codes</span></span>

<span data-ttu-id="ed734-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ed734-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ed734-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ed734-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ed734-155">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ed734-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="ed734-156">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="ed734-156">This method returns the following error codes:</span></span>

| <span data-ttu-id="ed734-157">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="ed734-157">HTTP Status Code</span></span>     | <span data-ttu-id="ed734-158">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="ed734-158">Error code</span></span>   | <span data-ttu-id="ed734-159">Description</span><span class="sxs-lookup"><span data-stu-id="ed734-159">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="ed734-160">404</span><span class="sxs-lookup"><span data-stu-id="ed734-160">404</span></span>                  | <span data-ttu-id="ed734-161">600039</span><span class="sxs-lookup"><span data-stu-id="ed734-161">600039</span></span>       | <span data-ttu-id="ed734-162">Zásady samoobslužné podpory nebyly nalezeny.</span><span class="sxs-lookup"><span data-stu-id="ed734-162">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="ed734-163">404</span><span class="sxs-lookup"><span data-stu-id="ed734-163">404</span></span>                  | <span data-ttu-id="ed734-164">600040</span><span class="sxs-lookup"><span data-stu-id="ed734-164">600040</span></span>       | <span data-ttu-id="ed734-165">Identifikátor zásady samoobslužného ovládání není správný.</span><span class="sxs-lookup"><span data-stu-id="ed734-165">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="ed734-166">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ed734-166">Response example</span></span>

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
