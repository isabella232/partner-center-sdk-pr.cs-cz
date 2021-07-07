---
title: Získat seznam zásad pro samoobslužné zpracování
description: Jak získat kolekci prostředků představujících samoobslužné zásady zákazníka.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b18fde8a11d3ed3dd31e50fdba746dd6b0bf3f97
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025725"
---
# <a name="get-a-list-of-self-serve-policies"></a><span data-ttu-id="1be22-103">Získat seznam zásad pro samoobslužné zpracování</span><span class="sxs-lookup"><span data-stu-id="1be22-103">Get a list of self-serve policies</span></span>

<span data-ttu-id="1be22-104">Získá kolekci prostředků, které představují samoobslužné zásady pro entitu.</span><span class="sxs-lookup"><span data-stu-id="1be22-104">Gets a collection of resources that represents self-serve policies for an entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1be22-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1be22-105">Prerequisites</span></span>

- <span data-ttu-id="1be22-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1be22-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1be22-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="1be22-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="1be22-108">C\#</span><span class="sxs-lookup"><span data-stu-id="1be22-108">C\#</span></span>

<span data-ttu-id="1be22-109">Získání seznamu všech samoobslužných zásad:</span><span class="sxs-lookup"><span data-stu-id="1be22-109">To get a list of all self-serve policies:</span></span>

1. <span data-ttu-id="1be22-110">Voláním metody [**IAggregatePartner. SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) s identifikátorem entity načtěte rozhraní pro operace s těmito zásadami.</span><span class="sxs-lookup"><span data-stu-id="1be22-110">Call the [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

<span data-ttu-id="1be22-111">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="1be22-111">For an example, see the following:</span></span>

- <span data-ttu-id="1be22-112">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1be22-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1be22-113">Project: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="1be22-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="1be22-114">Třída: **GetSelfServePolicies. cs**</span><span class="sxs-lookup"><span data-stu-id="1be22-114">Class: **GetSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1be22-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1be22-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1be22-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="1be22-116">Request syntax</span></span>

| <span data-ttu-id="1be22-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="1be22-117">Method</span></span>  | <span data-ttu-id="1be22-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1be22-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="1be22-119">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="1be22-119">**GET**</span></span> | <span data-ttu-id="1be22-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy? entity_id = {ENTITY_ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1be22-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="1be22-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1be22-121">URI parameter</span></span>

<span data-ttu-id="1be22-122">Chcete-li získat seznam zákazníků, použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="1be22-122">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="1be22-123">Název</span><span class="sxs-lookup"><span data-stu-id="1be22-123">Name</span></span>          | <span data-ttu-id="1be22-124">Typ</span><span class="sxs-lookup"><span data-stu-id="1be22-124">Type</span></span>       | <span data-ttu-id="1be22-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1be22-125">Required</span></span> | <span data-ttu-id="1be22-126">Popis</span><span class="sxs-lookup"><span data-stu-id="1be22-126">Description</span></span>                                        |
|---------------|------------|----------|----------------------------------------------------|
| <span data-ttu-id="1be22-127">**entity_id**</span><span class="sxs-lookup"><span data-stu-id="1be22-127">**entity_id**</span></span> | <span data-ttu-id="1be22-128">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="1be22-128">**string**</span></span> | <span data-ttu-id="1be22-129">Y</span><span class="sxs-lookup"><span data-stu-id="1be22-129">Y</span></span>        | <span data-ttu-id="1be22-130">Identifikátor entity požadující přístup pro.</span><span class="sxs-lookup"><span data-stu-id="1be22-130">The entity identifier requesting access for.</span></span> <span data-ttu-id="1be22-131">Toto bude ID tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1be22-131">This will be the customer's tenant ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1be22-132">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1be22-132">Request headers</span></span>

<span data-ttu-id="1be22-133">Další informace naleznete v části [Headers](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1be22-133">For more information, see [Headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1be22-134">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1be22-134">Request body</span></span>

<span data-ttu-id="1be22-135">Žádné</span><span class="sxs-lookup"><span data-stu-id="1be22-135">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1be22-136">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1be22-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="1be22-137">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1be22-137">REST response</span></span>

<span data-ttu-id="1be22-138">V případě úspěchu tato metoda vrátí kolekci prostředků [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="1be22-138">If successful, this method returns a collection of [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1be22-139">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="1be22-139">Response success and error codes</span></span>

<span data-ttu-id="1be22-140">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1be22-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1be22-141">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="1be22-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1be22-142">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1be22-142">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1be22-143">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1be22-143">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 1,
    "items": [{
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
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
