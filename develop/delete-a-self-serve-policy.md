---
title: Odstranění zásady samostatného poskytování
description: Jak odstranit zásadu samoobslužného ovládání.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3450145d6daf2ffca5e2886245e592406cb0886d
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/08/2020
ms.locfileid: "97767152"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="ea0ed-103">Odstranit SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ea0ed-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="ea0ed-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="ea0ed-104">**Applies to:**</span></span>

- <span data-ttu-id="ea0ed-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="ea0ed-105">Partner Center</span></span>

<span data-ttu-id="ea0ed-106">Toto téma vysvětluje, jak aktualizovat zásadu samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea0ed-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ea0ed-107">Prerequisites</span></span>

- <span data-ttu-id="ea0ed-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ea0ed-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ea0ed-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="ea0ed-110">C\#</span><span class="sxs-lookup"><span data-stu-id="ea0ed-110">C\#</span></span>

<span data-ttu-id="ea0ed-111">Postup odstranění samoobslužné zásady:</span><span class="sxs-lookup"><span data-stu-id="ea0ed-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="ea0ed-112">Voláním metody [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) s identifikátorem entity načtěte rozhraní pro operace s těmito zásadami.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="ea0ed-113">Voláním metody [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) nebo [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) odstraníte zásadu samoobslužné obsluhy.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-113">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="ea0ed-114">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="ea0ed-114">For an example, see the following:</span></span>

- <span data-ttu-id="ea0ed-115">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ea0ed-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ea0ed-116">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="ea0ed-116">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="ea0ed-117">Třída: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="ea0ed-117">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="ea0ed-118">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ea0ed-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ea0ed-119">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ea0ed-119">Request syntax</span></span>

| <span data-ttu-id="ea0ed-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="ea0ed-120">Method</span></span>  | <span data-ttu-id="ea0ed-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ea0ed-121">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="ea0ed-122">**DSTRANIT**</span><span class="sxs-lookup"><span data-stu-id="ea0ed-122">**DELETE**</span></span> | <span data-ttu-id="ea0ed-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ea0ed-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="ea0ed-124">**Parametr URI**</span><span class="sxs-lookup"><span data-stu-id="ea0ed-124">**URI parameter**</span></span>

<span data-ttu-id="ea0ed-125">K získání zadaného produktu použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="ea0ed-126">Název</span><span class="sxs-lookup"><span data-stu-id="ea0ed-126">Name</span></span>                       | <span data-ttu-id="ea0ed-127">Typ</span><span class="sxs-lookup"><span data-stu-id="ea0ed-127">Type</span></span>         | <span data-ttu-id="ea0ed-128">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ea0ed-128">Required</span></span> | <span data-ttu-id="ea0ed-129">Popis</span><span class="sxs-lookup"><span data-stu-id="ea0ed-129">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="ea0ed-130">**SelfServePolicy-ID**</span><span class="sxs-lookup"><span data-stu-id="ea0ed-130">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="ea0ed-131">**řetezce**</span><span class="sxs-lookup"><span data-stu-id="ea0ed-131">**string**</span></span>   | <span data-ttu-id="ea0ed-132">Yes</span><span class="sxs-lookup"><span data-stu-id="ea0ed-132">Yes</span></span>      | <span data-ttu-id="ea0ed-133">Řetězec, který identifikuje zásadu samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-133">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="ea0ed-134">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ea0ed-134">Request headers</span></span>

- <span data-ttu-id="ea0ed-135">Vyžaduje se ID žádosti a ID korelace.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-135">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="ea0ed-136">Další informace najdete v tématu [záhlaví REST v partnerském centru](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="ea0ed-136">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="ea0ed-137">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ea0ed-137">Request body</span></span>

<span data-ttu-id="ea0ed-138">Žádné</span><span class="sxs-lookup"><span data-stu-id="ea0ed-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ea0ed-139">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ea0ed-139">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ea0ed-140">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ea0ed-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ea0ed-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ea0ed-141">Response success and error codes</span></span>

<span data-ttu-id="ea0ed-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ea0ed-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ea0ed-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ea0ed-144">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ea0ed-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ea0ed-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ea0ed-145">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
