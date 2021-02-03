---
title: Získání informací o nasazení licencí pro partnery
description: Jak získat agregované informace o nasazení partnerských licencí, aby zahrnovaly všechny zákazníky.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 229f63d4df4f59cd0fde2bd0fc5e3f10cf6b25c0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767030"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="d6fd4-103">Získání informací o nasazení licencí pro partnery</span><span class="sxs-lookup"><span data-stu-id="d6fd4-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="d6fd4-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="d6fd4-104">**Applies To**</span></span>

- <span data-ttu-id="d6fd4-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d6fd4-105">Partner Center</span></span>

<span data-ttu-id="d6fd4-106">Jak získat agregované informace o nasazení partnerských licencí, aby zahrnovaly všechny zákazníky.</span><span class="sxs-lookup"><span data-stu-id="d6fd4-106">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="d6fd4-107">Tento scénář se nahrazuje [informacemi o nasazení získat licence](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="d6fd4-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6fd4-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d6fd4-108">Prerequisites</span></span>

<span data-ttu-id="d6fd4-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d6fd4-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d6fd4-110">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d6fd4-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d6fd4-111">C\#</span><span class="sxs-lookup"><span data-stu-id="d6fd4-111">C\#</span></span>

<span data-ttu-id="d6fd4-112">Chcete-li načíst agregovaná data při nasazení licencí, nejprve z vlastnosti [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) Získejte rozhraní k operacím shromažďování na úrovni partnera úrovně Analytics.</span><span class="sxs-lookup"><span data-stu-id="d6fd4-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="d6fd4-113">Pak z vlastnosti [**licence**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) načtěte rozhraní pro kolekci Analytics License licenses Analytics.</span><span class="sxs-lookup"><span data-stu-id="d6fd4-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="d6fd4-114">Nakonec zavolejte metodu [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , která načte agregovaná data při nasazení licencí.</span><span class="sxs-lookup"><span data-stu-id="d6fd4-114">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="d6fd4-115">Pokud je metoda úspěšná, získáte kolekci objektů [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) .</span><span class="sxs-lookup"><span data-stu-id="d6fd4-115">If the method succeeds you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="d6fd4-116">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d6fd4-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d6fd4-117">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d6fd4-117">Request syntax</span></span>

| <span data-ttu-id="d6fd4-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="d6fd4-118">Method</span></span>  | <span data-ttu-id="d6fd4-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d6fd4-119">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="d6fd4-120">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="d6fd4-120">**GET**</span></span> | <span data-ttu-id="d6fd4-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/licenses/Deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d6fd4-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d6fd4-122">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d6fd4-122">Request headers</span></span>

<span data-ttu-id="d6fd4-123">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d6fd4-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d6fd4-124">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d6fd4-124">Request body</span></span>

<span data-ttu-id="d6fd4-125">Žádné</span><span class="sxs-lookup"><span data-stu-id="d6fd4-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d6fd4-126">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d6fd4-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d6fd4-127">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d6fd4-127">REST response</span></span>

<span data-ttu-id="d6fd4-128">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) , které poskytují informace o nasazených licencích.</span><span class="sxs-lookup"><span data-stu-id="d6fd4-128">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d6fd4-129">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d6fd4-129">Response success and error codes</span></span>

<span data-ttu-id="d6fd4-130">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d6fd4-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d6fd4-131">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d6fd4-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d6fd4-132">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d6fd4-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d6fd4-133">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d6fd4-133">Response example</span></span>

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
