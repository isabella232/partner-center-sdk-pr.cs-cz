---
title: Získání samoobslužné zásady podle ID
description: Načte zadané samoobslužné zásady pomocí jejího ID.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ec01d0d9b7c3858cdacf1dbaad3b2b0bb7b6a1a4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766780"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="d70b0-103">Získání samoobslužné zásady podle ID</span><span class="sxs-lookup"><span data-stu-id="d70b0-103">Get a self serve policy by ID</span></span>

<span data-ttu-id="d70b0-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="d70b0-104">**Applies To**</span></span>

- <span data-ttu-id="d70b0-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d70b0-105">Partner Center</span></span>

<span data-ttu-id="d70b0-106">Načte zadané samoobslužné zásady pomocí jejího ID.</span><span class="sxs-lookup"><span data-stu-id="d70b0-106">Gets the specified self serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d70b0-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d70b0-107">Prerequisites</span></span>

- <span data-ttu-id="d70b0-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d70b0-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d70b0-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d70b0-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="d70b0-110">ID zásad samostatného poskytování.</span><span class="sxs-lookup"><span data-stu-id="d70b0-110">A self serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="d70b0-111">Příklady</span><span class="sxs-lookup"><span data-stu-id="d70b0-111">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="d70b0-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d70b0-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="d70b0-113">**Syntaxe žádosti**</span><span class="sxs-lookup"><span data-stu-id="d70b0-113">**Request syntax**</span></span>

| <span data-ttu-id="d70b0-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="d70b0-114">Method</span></span>  | <span data-ttu-id="d70b0-115">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d70b0-115">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="d70b0-116">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="d70b0-116">**GET**</span></span> | <span data-ttu-id="d70b0-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d70b0-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="d70b0-118">**Parametr URI**</span><span class="sxs-lookup"><span data-stu-id="d70b0-118">**URI parameter**</span></span>

<span data-ttu-id="d70b0-119">K získání zadaného produktu použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="d70b0-119">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="d70b0-120">Název</span><span class="sxs-lookup"><span data-stu-id="d70b0-120">Name</span></span>                       | <span data-ttu-id="d70b0-121">Typ</span><span class="sxs-lookup"><span data-stu-id="d70b0-121">Type</span></span>         | <span data-ttu-id="d70b0-122">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d70b0-122">Required</span></span> | <span data-ttu-id="d70b0-123">Popis</span><span class="sxs-lookup"><span data-stu-id="d70b0-123">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="d70b0-124">**SelfServePolicy-ID**</span><span class="sxs-lookup"><span data-stu-id="d70b0-124">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="d70b0-125">**řetezce**</span><span class="sxs-lookup"><span data-stu-id="d70b0-125">**string**</span></span>   | <span data-ttu-id="d70b0-126">Yes</span><span class="sxs-lookup"><span data-stu-id="d70b0-126">Yes</span></span>      | <span data-ttu-id="d70b0-127">Řetězec, který identifikuje zásadu samoobslužného ovládání.</span><span class="sxs-lookup"><span data-stu-id="d70b0-127">A string that identifies the self serve policy.</span></span>                 |

<span data-ttu-id="d70b0-128">**Hlavičky požadavku**</span><span class="sxs-lookup"><span data-stu-id="d70b0-128">**Request headers**</span></span>

- <span data-ttu-id="d70b0-129">Další informace najdete v [záhlavích](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="d70b0-129">See [Headers](headers.md) for more information.</span></span>

<span data-ttu-id="d70b0-130">**Text žádosti**</span><span class="sxs-lookup"><span data-stu-id="d70b0-130">**Request body**</span></span>

<span data-ttu-id="d70b0-131">Žádné</span><span class="sxs-lookup"><span data-stu-id="d70b0-131">None.</span></span>

<span data-ttu-id="d70b0-132">**Příklad požadavku**</span><span class="sxs-lookup"><span data-stu-id="d70b0-132">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="d70b0-133">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d70b0-133">REST response</span></span>

<span data-ttu-id="d70b0-134">V případě úspěchu obsahuje tělo odpovědi prostředek [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) .</span><span class="sxs-lookup"><span data-stu-id="d70b0-134">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="d70b0-135">**Úspěšné odpovědi a chybové kódy**</span><span class="sxs-lookup"><span data-stu-id="d70b0-135">**Response success and error codes**</span></span>

<span data-ttu-id="d70b0-136">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d70b0-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d70b0-137">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d70b0-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d70b0-138">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d70b0-138">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="d70b0-139">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="d70b0-139">This method returns the following error codes:</span></span>

| <span data-ttu-id="d70b0-140">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="d70b0-140">HTTP Status Code</span></span>     | <span data-ttu-id="d70b0-141">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="d70b0-141">Error code</span></span>   | <span data-ttu-id="d70b0-142">Description</span><span class="sxs-lookup"><span data-stu-id="d70b0-142">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="d70b0-143">404</span><span class="sxs-lookup"><span data-stu-id="d70b0-143">404</span></span>                  | <span data-ttu-id="d70b0-144">600039</span><span class="sxs-lookup"><span data-stu-id="d70b0-144">600039</span></span>       | <span data-ttu-id="d70b0-145">Zásady samoobslužné obsluhy nebyly nalezeny.</span><span class="sxs-lookup"><span data-stu-id="d70b0-145">Self serve policy not found.</span></span>                                                     |

<span data-ttu-id="d70b0-146">**Příklad odpovědi**</span><span class="sxs-lookup"><span data-stu-id="d70b0-146">**Response example**</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

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