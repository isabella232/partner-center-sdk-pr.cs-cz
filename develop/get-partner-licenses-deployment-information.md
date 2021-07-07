---
title: Získání informací o nasazení licencí pro partnery
description: Jak získat informace o nasazení licencí partnerů agregované tak, aby zahrnovaly všechny zákazníky.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2464242fc6dc4e7464511eac5d4197630e22fac0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445968"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="1e29a-103">Získání informací o nasazení licencí pro partnery</span><span class="sxs-lookup"><span data-stu-id="1e29a-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="1e29a-104">Jak získat informace o nasazení licencí partnerů agregované tak, aby zahrnovaly všechny zákazníky.</span><span class="sxs-lookup"><span data-stu-id="1e29a-104">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="1e29a-105">Tento scénář je nástavěn pomocí [možnosti Získat informace o nasazení licencí.](get-licenses-deployment-information.md)</span><span class="sxs-lookup"><span data-stu-id="1e29a-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e29a-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1e29a-106">Prerequisites</span></span>

<span data-ttu-id="1e29a-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1e29a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1e29a-108">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="1e29a-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="1e29a-109">C\#</span><span class="sxs-lookup"><span data-stu-id="1e29a-109">C\#</span></span>

<span data-ttu-id="1e29a-110">Pokud chcete načíst agregovaná data při nasazení licencí, nejprve z vlastnosti [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) získejte rozhraní pro operace shromažďování analýz na úrovni partnera.</span><span class="sxs-lookup"><span data-stu-id="1e29a-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="1e29a-111">Pak z vlastnosti Licence načtěte rozhraní do analytické kolekce licencí na [**úrovni**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) partnera.</span><span class="sxs-lookup"><span data-stu-id="1e29a-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="1e29a-112">Nakonec zavolejte [**metodu Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) a získejte agregovaná data o nasazení licencí.</span><span class="sxs-lookup"><span data-stu-id="1e29a-112">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="1e29a-113">Pokud je metoda úspěšná, získáte kolekci objektů [**PartnerLicensesDeploymentInsights.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights)</span><span class="sxs-lookup"><span data-stu-id="1e29a-113">If the method succeeds, you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="1e29a-114">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="1e29a-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1e29a-115">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="1e29a-115">Request syntax</span></span>

| <span data-ttu-id="1e29a-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="1e29a-116">Method</span></span>  | <span data-ttu-id="1e29a-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1e29a-117">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="1e29a-118">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="1e29a-118">**GET**</span></span> | <span data-ttu-id="1e29a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1e29a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1e29a-120">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1e29a-120">Request headers</span></span>

<span data-ttu-id="1e29a-121">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1e29a-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1e29a-122">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1e29a-122">Request body</span></span>

<span data-ttu-id="1e29a-123">Žádné</span><span class="sxs-lookup"><span data-stu-id="1e29a-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1e29a-124">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1e29a-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1e29a-125">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1e29a-125">REST response</span></span>

<span data-ttu-id="1e29a-126">V případě úspěchu text odpovědi obsahuje kolekci [prostředků PartnerLicensesDeploymentInsights,](analytics-resources.md#partnerlicensesdeploymentinsights) které poskytují informace o nasazených licencích.</span><span class="sxs-lookup"><span data-stu-id="1e29a-126">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1e29a-127">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="1e29a-127">Response success and error codes</span></span>

<span data-ttu-id="1e29a-128">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1e29a-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1e29a-129">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="1e29a-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1e29a-130">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1e29a-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1e29a-131">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1e29a-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
    "totalCount": 2,
    "items": [{
            "proratedDeploymentPercent": 0.0,
            "licensesSold": 343,
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }, {
            "proratedDeploymentPercent": 1.0,
            "licensesSold": 4464,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
