---
title: Získat stav přijetí MFA
description: Získejte seznam stavu přijetí služby Multi-Factor Authentication pro každého partnera pomocí REST API partnera.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: f82d163b704323c81e2948b78eb9b9d1a14ddc52
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766758"
---
# <a name="get-mfa-adoption-status"></a><span data-ttu-id="51225-103">Získat stav přijetí MFA</span><span class="sxs-lookup"><span data-stu-id="51225-103">Get MFA adoption status</span></span>

<span data-ttu-id="51225-104">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="51225-104">Applies to:</span></span>

- <span data-ttu-id="51225-105">Rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="51225-105">Partner Center API</span></span>

<span data-ttu-id="51225-106">Tento článek vysvětluje, jak získat stav přijetí služby Multi-Factor Authentication (MFA) pro každého partnera v rámci tenanta.</span><span class="sxs-lookup"><span data-stu-id="51225-106">This article explains how to get the multi-factor authentication (MFA) adoption status for each partner within a tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51225-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="51225-107">Prerequisites</span></span>

- <span data-ttu-id="51225-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="51225-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="51225-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="51225-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="51225-110">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="51225-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="51225-111">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="51225-111">Request syntax</span></span>

| <span data-ttu-id="51225-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="51225-112">Method</span></span>  | <span data-ttu-id="51225-113">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="51225-113">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="51225-114">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="51225-114">**GET**</span></span> | <span data-ttu-id="51225-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span><span class="sxs-lookup"><span data-stu-id="51225-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span></span> |

### <a name="request-headers"></a><span data-ttu-id="51225-116">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="51225-116">Request headers</span></span>

- <span data-ttu-id="51225-117">Další informace najdete v tématu [záhlaví REST v partnerském centru](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="51225-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="51225-118">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="51225-118">Request body</span></span>

<span data-ttu-id="51225-119">Žádné</span><span class="sxs-lookup"><span data-stu-id="51225-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="51225-120">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="51225-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="51225-121">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="51225-121">REST response</span></span>

<span data-ttu-id="51225-122">V případě úspěchu tato metoda vrátí kolekci [požadavků rozhraní API shrnutých prostředky aplikace](mfa-resources.md#api-request-summarized-by-application) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="51225-122">If successful, this method returns a collection of [API request summarized by Application](mfa-resources.md#api-request-summarized-by-application) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="51225-123">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="51225-123">Response success and error codes</span></span>

<span data-ttu-id="51225-124">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="51225-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="51225-125">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="51225-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="51225-126">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="51225-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="51225-127">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="51225-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 313
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
[
    {
        "loginDate": "2020-05-20",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 7,
        "applicationId": "14f38d7d-c4fc-448a-b2df-0fc60e75465a",
        "applicationName": ""
    },
    {
        "loginDate": "2020-05-19",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 14,
        "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
        "applicationName": ""
    }
]
```
