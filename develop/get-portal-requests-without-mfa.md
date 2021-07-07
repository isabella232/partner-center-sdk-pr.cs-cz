---
title: Získání požadavků na portál bez MFA
description: Seznam uživatelských požadavků bez vícefaktorového ověřování (MFA) získáte pomocí partnerského REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 41627751d3402d7712d96c15c4281a25ed9a44a7
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445574"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="75cdb-103">Získání požadavků na portál bez MFA</span><span class="sxs-lookup"><span data-stu-id="75cdb-103">Get portal requests without MFA</span></span>

<span data-ttu-id="75cdb-104">Tento článek vysvětluje, jak získat seznam nejnovějších požadavků od uživatelů, kteří přistupují k portálu Partnerské centrum, aniž by se dokončilo vícefaktorové ověřování (MFA).</span><span class="sxs-lookup"><span data-stu-id="75cdb-104">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75cdb-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="75cdb-105">Prerequisites</span></span>

- <span data-ttu-id="75cdb-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="75cdb-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="75cdb-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="75cdb-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="75cdb-108">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="75cdb-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="75cdb-109">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="75cdb-109">Request syntax</span></span>

| <span data-ttu-id="75cdb-110">Metoda</span><span class="sxs-lookup"><span data-stu-id="75cdb-110">Method</span></span>  | <span data-ttu-id="75cdb-111">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="75cdb-111">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="75cdb-112">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="75cdb-112">**GET**</span></span> | <span data-ttu-id="75cdb-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="75cdb-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="75cdb-114">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="75cdb-114">Request headers</span></span>

- <span data-ttu-id="75cdb-115">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="75cdb-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="75cdb-116">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="75cdb-116">Request body</span></span>

<span data-ttu-id="75cdb-117">Žádné</span><span class="sxs-lookup"><span data-stu-id="75cdb-117">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="75cdb-118">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="75cdb-118">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="75cdb-119">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="75cdb-119">REST response</span></span>

<span data-ttu-id="75cdb-120">V případě úspěchu tato metoda vrátí kolekci prostředků [požadavku portálu](mfa-resources.md#portal-request-without-mfa) v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="75cdb-120">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="75cdb-121">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="75cdb-121">Response success and error codes</span></span>

<span data-ttu-id="75cdb-122">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="75cdb-122">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="75cdb-123">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="75cdb-123">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="75cdb-124">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="75cdb-124">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="75cdb-125">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="75cdb-125">Response example</span></span>

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
