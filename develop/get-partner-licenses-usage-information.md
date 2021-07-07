---
title: Získání informací o využití licencí pro partnery
description: Jak získat agregované informace o využití partnerských licencí, aby zahrnovaly všechny zákazníky.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f3d05d61ac4f2c90b0d8a4bfd93fe24e94bd5c1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445591"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="b8f65-103">Získání informací o využití licencí pro partnery</span><span class="sxs-lookup"><span data-stu-id="b8f65-103">Get partner licenses usage information</span></span>

<span data-ttu-id="b8f65-104">Jak získat agregované informace o využití partnerských licencí, aby zahrnovaly všechny zákazníky.</span><span class="sxs-lookup"><span data-stu-id="b8f65-104">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="b8f65-105">Tento scénář je nahrazen [informacemi o využití licencí získat](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="b8f65-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8f65-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b8f65-106">Prerequisites</span></span>

<span data-ttu-id="b8f65-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b8f65-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b8f65-108">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b8f65-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="b8f65-109">C\#</span><span class="sxs-lookup"><span data-stu-id="b8f65-109">C\#</span></span>

<span data-ttu-id="b8f65-110">Chcete-li načíst agregovaná data při nasazení licencí, nejprve z vlastnosti [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) Získejte rozhraní k operacím shromažďování na úrovni partnera úrovně Analytics.</span><span class="sxs-lookup"><span data-stu-id="b8f65-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="b8f65-111">Pak z vlastnosti [**licence**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) načtěte rozhraní pro kolekci Analytics License licenses Analytics.</span><span class="sxs-lookup"><span data-stu-id="b8f65-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="b8f65-112">Nakonec zavolejte metodu [**Usage. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , která získá agregovaná data o využití licencí.</span><span class="sxs-lookup"><span data-stu-id="b8f65-112">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="b8f65-113">Pokud je metoda úspěšná, získáte kolekci objektů [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) .</span><span class="sxs-lookup"><span data-stu-id="b8f65-113">If the method succeeds, you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="b8f65-114">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b8f65-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b8f65-115">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b8f65-115">Request syntax</span></span>

| <span data-ttu-id="b8f65-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="b8f65-116">Method</span></span>  | <span data-ttu-id="b8f65-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b8f65-117">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="b8f65-118">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b8f65-118">**GET**</span></span> | <span data-ttu-id="b8f65-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/licenses/Usage HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b8f65-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b8f65-120">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b8f65-120">Request headers</span></span>

<span data-ttu-id="b8f65-121">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b8f65-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b8f65-122">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b8f65-122">Request body</span></span>

<span data-ttu-id="b8f65-123">Žádné</span><span class="sxs-lookup"><span data-stu-id="b8f65-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b8f65-124">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b8f65-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="b8f65-125">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b8f65-125">REST response</span></span>

<span data-ttu-id="b8f65-126">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) , které poskytují informace o použitých licencích.</span><span class="sxs-lookup"><span data-stu-id="b8f65-126">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b8f65-127">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b8f65-127">Response success and error codes</span></span>

<span data-ttu-id="b8f65-128">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b8f65-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b8f65-129">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b8f65-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b8f65-130">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b8f65-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b8f65-131">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b8f65-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1156
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CV: wk0/vjugzEe0Z9cv.0
MS-ServerId: 101112012
Date: Wed, 15 Mar 2017 01:18:26 GMT

{
    "totalCount": 5,
    "items": [{
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Microsoft Dynamics CRM",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
