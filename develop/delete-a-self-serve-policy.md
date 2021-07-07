---
title: Odstranění samoobslužných zásad
description: Postup odstranění samoobslužných zásad
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 063cf98d4c78e82622e486427baeb1a5721715e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973090"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="461ce-103">Odstranění zásady SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="461ce-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="461ce-104">Tento článek vysvětluje, jak aktualizovat samoobslužné zásady.</span><span class="sxs-lookup"><span data-stu-id="461ce-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="461ce-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="461ce-105">Prerequisites</span></span>

- <span data-ttu-id="461ce-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="461ce-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="461ce-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="461ce-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="461ce-108">C\#</span><span class="sxs-lookup"><span data-stu-id="461ce-108">C\#</span></span>

<span data-ttu-id="461ce-109">Odstranění samoobslužných zásad:</span><span class="sxs-lookup"><span data-stu-id="461ce-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="461ce-110">Voláním [**metody IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) s identifikátorem entity načtěte rozhraní operací se zásadami.</span><span class="sxs-lookup"><span data-stu-id="461ce-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="461ce-111">Pokud chcete [**odstranit samoobslužné**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) zásady, zavolejte metodu Delete nebo [**DeleteAsync.**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync)</span><span class="sxs-lookup"><span data-stu-id="461ce-111">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="461ce-112">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="461ce-112">For an example, see the following:</span></span>

- <span data-ttu-id="461ce-113">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="461ce-113">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="461ce-114">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="461ce-114">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="461ce-115">Třída: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="461ce-115">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="461ce-116">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="461ce-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="461ce-117">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="461ce-117">Request syntax</span></span>

| <span data-ttu-id="461ce-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="461ce-118">Method</span></span>  | <span data-ttu-id="461ce-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="461ce-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="461ce-120">**Odstranit**</span><span class="sxs-lookup"><span data-stu-id="461ce-120">**DELETE**</span></span> | <span data-ttu-id="461ce-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="461ce-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="461ce-122">**Parametr URI**</span><span class="sxs-lookup"><span data-stu-id="461ce-122">**URI parameter**</span></span>

<span data-ttu-id="461ce-123">K získání zadaného produktu použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="461ce-123">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="461ce-124">Název</span><span class="sxs-lookup"><span data-stu-id="461ce-124">Name</span></span>                       | <span data-ttu-id="461ce-125">Typ</span><span class="sxs-lookup"><span data-stu-id="461ce-125">Type</span></span>         | <span data-ttu-id="461ce-126">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="461ce-126">Required</span></span> | <span data-ttu-id="461ce-127">Popis</span><span class="sxs-lookup"><span data-stu-id="461ce-127">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="461ce-128">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="461ce-128">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="461ce-129">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="461ce-129">**string**</span></span>   | <span data-ttu-id="461ce-130">Yes</span><span class="sxs-lookup"><span data-stu-id="461ce-130">Yes</span></span>      | <span data-ttu-id="461ce-131">Řetězec, který identifikuje samoobslužné zásady.</span><span class="sxs-lookup"><span data-stu-id="461ce-131">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="461ce-132">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="461ce-132">Request headers</span></span>

- <span data-ttu-id="461ce-133">Vyžaduje se ID požadavku a ID korelace.</span><span class="sxs-lookup"><span data-stu-id="461ce-133">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="461ce-134">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="461ce-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="461ce-135">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="461ce-135">Request body</span></span>

<span data-ttu-id="461ce-136">Žádné</span><span class="sxs-lookup"><span data-stu-id="461ce-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="461ce-137">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="461ce-137">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a><span data-ttu-id="461ce-138">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="461ce-138">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="461ce-139">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="461ce-139">Response success and error codes</span></span>

<span data-ttu-id="461ce-140">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="461ce-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="461ce-141">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="461ce-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="461ce-142">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="461ce-142">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="461ce-143">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="461ce-143">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
