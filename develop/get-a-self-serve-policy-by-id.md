---
title: Získat samoobslužnou zásadu podle ID
description: Získá zadanou zásadu samoobslužného zpracování pomocí jejího ID.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 074d7ba65c7aab91687a67f50e871cee913fc2bb
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873832"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="aab3c-103">Získat samoobslužnou zásadu podle ID</span><span class="sxs-lookup"><span data-stu-id="aab3c-103">Get a self-serve policy by ID</span></span>

<span data-ttu-id="aab3c-104">Získá zadanou zásadu samoobslužného zpracování pomocí jejího ID.</span><span class="sxs-lookup"><span data-stu-id="aab3c-104">Gets the specified self-serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aab3c-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="aab3c-105">Prerequisites</span></span>

- <span data-ttu-id="aab3c-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="aab3c-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="aab3c-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="aab3c-107">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="aab3c-108">ID zásady, která slouží samy na sebe.</span><span class="sxs-lookup"><span data-stu-id="aab3c-108">A self-serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="aab3c-109">Příklady</span><span class="sxs-lookup"><span data-stu-id="aab3c-109">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="aab3c-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>Žádost REST</span><span class="sxs-lookup"><span data-stu-id="aab3c-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="aab3c-111">**Syntaxe žádosti**</span><span class="sxs-lookup"><span data-stu-id="aab3c-111">**Request syntax**</span></span>

| <span data-ttu-id="aab3c-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="aab3c-112">Method</span></span>  | <span data-ttu-id="aab3c-113">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="aab3c-113">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="aab3c-114">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="aab3c-114">**GET**</span></span> | <span data-ttu-id="aab3c-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="aab3c-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="aab3c-116">**Parametr URI**</span><span class="sxs-lookup"><span data-stu-id="aab3c-116">**URI parameter**</span></span>

<span data-ttu-id="aab3c-117">K získání zadaného produktu použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="aab3c-117">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="aab3c-118">Název</span><span class="sxs-lookup"><span data-stu-id="aab3c-118">Name</span></span>                       | <span data-ttu-id="aab3c-119">Typ</span><span class="sxs-lookup"><span data-stu-id="aab3c-119">Type</span></span>         | <span data-ttu-id="aab3c-120">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="aab3c-120">Required</span></span> | <span data-ttu-id="aab3c-121">Popis</span><span class="sxs-lookup"><span data-stu-id="aab3c-121">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="aab3c-122">**SelfServePolicy-ID**</span><span class="sxs-lookup"><span data-stu-id="aab3c-122">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="aab3c-123">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="aab3c-123">**string**</span></span>   | <span data-ttu-id="aab3c-124">Yes</span><span class="sxs-lookup"><span data-stu-id="aab3c-124">Yes</span></span>      | <span data-ttu-id="aab3c-125">Řetězec, který identifikuje zásadu samoobslužného zpracování.</span><span class="sxs-lookup"><span data-stu-id="aab3c-125">A string that identifies the self-serve policy.</span></span>                 |

<span data-ttu-id="aab3c-126">**Hlavičky požadavku**</span><span class="sxs-lookup"><span data-stu-id="aab3c-126">**Request headers**</span></span>

- <span data-ttu-id="aab3c-127">Další informace naleznete v části [Headers](headers.md).</span><span class="sxs-lookup"><span data-stu-id="aab3c-127">For more information, see [Headers](headers.md).</span></span>

<span data-ttu-id="aab3c-128">**Text žádosti**</span><span class="sxs-lookup"><span data-stu-id="aab3c-128">**Request body**</span></span>

<span data-ttu-id="aab3c-129">Žádné</span><span class="sxs-lookup"><span data-stu-id="aab3c-129">None.</span></span>

<span data-ttu-id="aab3c-130">**Příklad požadavku**</span><span class="sxs-lookup"><span data-stu-id="aab3c-130">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="aab3c-131">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="aab3c-131">REST response</span></span>

<span data-ttu-id="aab3c-132">V případě úspěchu obsahuje tělo odpovědi prostředek [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) .</span><span class="sxs-lookup"><span data-stu-id="aab3c-132">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="aab3c-133">**Úspěšné odpovědi a chybové kódy**</span><span class="sxs-lookup"><span data-stu-id="aab3c-133">**Response success and error codes**</span></span>

<span data-ttu-id="aab3c-134">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="aab3c-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="aab3c-135">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="aab3c-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="aab3c-136">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="aab3c-136">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="aab3c-137">Tato metoda vrací následující kódy chyb:</span><span class="sxs-lookup"><span data-stu-id="aab3c-137">This method returns the following error codes:</span></span>

| <span data-ttu-id="aab3c-138">Stavový kód HTTP</span><span class="sxs-lookup"><span data-stu-id="aab3c-138">HTTP Status Code</span></span>     | <span data-ttu-id="aab3c-139">Kód chyby</span><span class="sxs-lookup"><span data-stu-id="aab3c-139">Error code</span></span>   | <span data-ttu-id="aab3c-140">Description</span><span class="sxs-lookup"><span data-stu-id="aab3c-140">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="aab3c-141">404</span><span class="sxs-lookup"><span data-stu-id="aab3c-141">404</span></span>                  | <span data-ttu-id="aab3c-142">600039</span><span class="sxs-lookup"><span data-stu-id="aab3c-142">600039</span></span>       | <span data-ttu-id="aab3c-143">Zásady samoobslužného ovládání nebyly nalezeny.</span><span class="sxs-lookup"><span data-stu-id="aab3c-143">Self-serve policy not found.</span></span>                                                     |

<span data-ttu-id="aab3c-144">**Příklad odpovědi**</span><span class="sxs-lookup"><span data-stu-id="aab3c-144">**Response example**</span></span>

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