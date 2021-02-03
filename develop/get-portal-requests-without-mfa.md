---
title: Získání požadavků na portál bez MFA
description: Získejte seznam uživatelských požadavků bez vícefaktorového ověřování (MFA) pomocí REST API partnera.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: fd350aa3301f00926942ae6c6af359b0d0edc423
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766776"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="1f847-103">Získání požadavků na portál bez MFA</span><span class="sxs-lookup"><span data-stu-id="1f847-103">Get portal requests without MFA</span></span>

<span data-ttu-id="1f847-104">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="1f847-104">Applies to:</span></span>

- <span data-ttu-id="1f847-105">Rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="1f847-105">Partner Center API</span></span>

<span data-ttu-id="1f847-106">Tento článek vysvětluje, jak získat seznam nejaktuálnějších požadavků od uživatelů, kteří přistupují k portálu partnerského centra bez dokončení vícefaktorového ověřování (MFA).</span><span class="sxs-lookup"><span data-stu-id="1f847-106">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f847-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1f847-107">Prerequisites</span></span>

- <span data-ttu-id="1f847-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1f847-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1f847-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="1f847-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="1f847-110">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1f847-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1f847-111">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="1f847-111">Request syntax</span></span>

| <span data-ttu-id="1f847-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="1f847-112">Method</span></span>  | <span data-ttu-id="1f847-113">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1f847-113">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="1f847-114">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="1f847-114">**GET**</span></span> | <span data-ttu-id="1f847-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="1f847-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1f847-116">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1f847-116">Request headers</span></span>

- <span data-ttu-id="1f847-117">Další informace najdete v tématu [záhlaví REST v partnerském centru](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="1f847-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="1f847-118">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1f847-118">Request body</span></span>

<span data-ttu-id="1f847-119">Žádné</span><span class="sxs-lookup"><span data-stu-id="1f847-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1f847-120">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1f847-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="1f847-121">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1f847-121">REST response</span></span>

<span data-ttu-id="1f847-122">V případě úspěchu tato metoda vrátí kolekci prostředků [žádosti portálu](mfa-resources.md#portal-request-without-mfa) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="1f847-122">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1f847-123">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="1f847-123">Response success and error codes</span></span>

<span data-ttu-id="1f847-124">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1f847-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1f847-125">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="1f847-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1f847-126">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1f847-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1f847-127">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1f847-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 296
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 23 Apr 2020 22:10:30 GMT
{
    "totalCount": 1,
    "items": [
        {
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "lastNonMfaCompliantRequestDateTime": "2020-04-21T22:09:53.051"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
