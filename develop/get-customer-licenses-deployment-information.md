---
title: Získání informací o nasazení licencí pro zákazníky
description: Jak získat přehledy o nasazení licencí pro konkrétního zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3a39c6c908048305ff2dabf85a29d7ddc3628500
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767036"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="f4477-103">Získání informací o nasazení licencí pro zákazníky</span><span class="sxs-lookup"><span data-stu-id="f4477-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="f4477-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="f4477-104">**Applies To**</span></span>

- <span data-ttu-id="f4477-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="f4477-105">Partner Center</span></span>

<span data-ttu-id="f4477-106">Jak získat přehledy o nasazení licencí pro konkrétního zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f4477-106">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="f4477-107">Tento scénář se nahrazuje [informacemi o nasazení získat licence](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="f4477-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4477-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f4477-108">Prerequisites</span></span>

<span data-ttu-id="f4477-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f4477-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f4477-110">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="f4477-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="f4477-111">C\#</span><span class="sxs-lookup"><span data-stu-id="f4477-111">C\#</span></span>

<span data-ttu-id="f4477-112">Chcete-li načíst agregovaná data v nasazení pro určitého zákazníka, nejprve zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f4477-112">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="f4477-113">Pak z [**analytické**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) vlastnosti Získejte rozhraní operace shromažďování na úrovni zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f4477-113">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="f4477-114">Pak z vlastnosti [**licence**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) načtěte rozhraní pro kolekci Customer License License Analytics.</span><span class="sxs-lookup"><span data-stu-id="f4477-114">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="f4477-115">Nakonec zavolejte metodu [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , která načte agregovaná data při nasazení licencí.</span><span class="sxs-lookup"><span data-stu-id="f4477-115">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="f4477-116">Pokud je metoda úspěšná, získáte kolekci objektů [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) .</span><span class="sxs-lookup"><span data-stu-id="f4477-116">If the method succeeds you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="f4477-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f4477-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f4477-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f4477-118">Request syntax</span></span>

| <span data-ttu-id="f4477-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="f4477-119">Method</span></span>  | <span data-ttu-id="f4477-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f4477-120">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f4477-121">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="f4477-121">**GET**</span></span> | <span data-ttu-id="f4477-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Analytics/licenses/Deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f4477-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f4477-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f4477-123">URI parameter</span></span>

<span data-ttu-id="f4477-124">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="f4477-124">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="f4477-125">Název</span><span class="sxs-lookup"><span data-stu-id="f4477-125">Name</span></span>        | <span data-ttu-id="f4477-126">Typ</span><span class="sxs-lookup"><span data-stu-id="f4477-126">Type</span></span> | <span data-ttu-id="f4477-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f4477-127">Required</span></span> | <span data-ttu-id="f4477-128">Popis</span><span class="sxs-lookup"><span data-stu-id="f4477-128">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="f4477-129">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="f4477-129">customer-id</span></span> | <span data-ttu-id="f4477-130">guid</span><span class="sxs-lookup"><span data-stu-id="f4477-130">guid</span></span> | <span data-ttu-id="f4477-131">Yes</span><span class="sxs-lookup"><span data-stu-id="f4477-131">Yes</span></span>      | <span data-ttu-id="f4477-132">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f4477-132">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f4477-133">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f4477-133">Request headers</span></span>

<span data-ttu-id="f4477-134">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f4477-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f4477-135">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f4477-135">Request body</span></span>

<span data-ttu-id="f4477-136">Žádné</span><span class="sxs-lookup"><span data-stu-id="f4477-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f4477-137">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f4477-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f4477-138">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f4477-138">REST response</span></span>

<span data-ttu-id="f4477-139">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) , které poskytují informace o nasazených licencích.</span><span class="sxs-lookup"><span data-stu-id="f4477-139">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f4477-140">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f4477-140">Response success and error codes</span></span>

<span data-ttu-id="f4477-141">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f4477-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f4477-142">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f4477-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f4477-143">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f4477-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f4477-144">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f4477-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1012
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CV: deEp2Wy6DUitMCYA.0
MS-ServerId: 102030524
Date: Wed, 15 Mar 2017 01:19:18 GMT

{
    "totalCount": 3,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 1,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 5,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 2,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
