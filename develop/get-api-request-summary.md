---
title: Získání stavu přechodu na více ověřování
description: Získejte seznam stavu přijetí vícefaktorového ověřování pro jednotlivé partnery pomocí partnerského REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9b8848c2a4531dd6609f86aae6876cec436eeea9
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760517"
---
# <a name="get-mfa-adoption-status"></a><span data-ttu-id="0dbd3-103">Získání stavu přijetí MFA</span><span class="sxs-lookup"><span data-stu-id="0dbd3-103">Get MFA adoption status</span></span>

<span data-ttu-id="0dbd3-104">**Platí pro:** Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="0dbd3-104">**Applies to**: Partner Center API</span></span>

<span data-ttu-id="0dbd3-105">Tento článek vysvětluje, jak získat stav přijetí vícefaktorového ověřování (MFA) pro každého partnera v rámci tenanta.</span><span class="sxs-lookup"><span data-stu-id="0dbd3-105">This article explains how to get the multi-factor authentication (MFA) adoption status for each partner within a tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dbd3-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0dbd3-106">Prerequisites</span></span>

- <span data-ttu-id="0dbd3-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0dbd3-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0dbd3-108">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="0dbd3-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="0dbd3-109">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="0dbd3-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0dbd3-110">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="0dbd3-110">Request syntax</span></span>

| <span data-ttu-id="0dbd3-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="0dbd3-111">Method</span></span>  | <span data-ttu-id="0dbd3-112">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0dbd3-112">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="0dbd3-113">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="0dbd3-113">**GET**</span></span> | <span data-ttu-id="0dbd3-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span><span class="sxs-lookup"><span data-stu-id="0dbd3-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span></span> |

### <a name="request-headers"></a><span data-ttu-id="0dbd3-115">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0dbd3-115">Request headers</span></span>

- <span data-ttu-id="0dbd3-116">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0dbd3-116">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0dbd3-117">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0dbd3-117">Request body</span></span>

<span data-ttu-id="0dbd3-118">Žádné</span><span class="sxs-lookup"><span data-stu-id="0dbd3-118">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0dbd3-119">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0dbd3-119">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="0dbd3-120">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0dbd3-120">REST response</span></span>

<span data-ttu-id="0dbd3-121">V případě úspěchu vrátí tato metoda v textu odpovědi kolekci požadavku [rozhraní API](mfa-resources.md#api-request-summarized-by-application) shrnutou prostředky aplikace.</span><span class="sxs-lookup"><span data-stu-id="0dbd3-121">If successful, this method returns a collection of [API request summarized by Application](mfa-resources.md#api-request-summarized-by-application) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0dbd3-122">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="0dbd3-122">Response success and error codes</span></span>

<span data-ttu-id="0dbd3-123">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0dbd3-123">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0dbd3-124">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="0dbd3-124">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0dbd3-125">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0dbd3-125">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0dbd3-126">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0dbd3-126">Response example</span></span>

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
