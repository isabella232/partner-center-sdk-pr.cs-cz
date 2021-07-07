---
title: Získání informací o využití licencí pro zákazníky
description: Jak získat přehledy využití licencí pro konkrétního zákazníka
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: cfec12d37ce4f5f50baad57bfd45770388f8a2dc
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446424"
---
# <a name="get-customer-licenses-usage-information"></a><span data-ttu-id="0d981-103">Získání informací o využití licencí pro zákazníky</span><span class="sxs-lookup"><span data-stu-id="0d981-103">Get customer licenses usage information</span></span>

<span data-ttu-id="0d981-104">Jak získat přehledy nasazení licencí pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="0d981-104">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="0d981-105">Tento scénář nahrazuje možnost Získat [informace o využití licencí.](get-licenses-usage-information.md)</span><span class="sxs-lookup"><span data-stu-id="0d981-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d981-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0d981-106">Prerequisites</span></span>

<span data-ttu-id="0d981-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0d981-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0d981-108">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="0d981-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="0d981-109">C\#</span><span class="sxs-lookup"><span data-stu-id="0d981-109">C\#</span></span>

<span data-ttu-id="0d981-110">Pokud chcete načíst agregovaná data v nasazení pro konkrétního zákazníka, nejprve zavolejte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0d981-110">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="0d981-111">Pak z vlastnosti Analytics získejte rozhraní pro operace shromažďování [**analytických**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) dat na úrovni zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0d981-111">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="0d981-112">Dále z vlastnosti Licence načtěte rozhraní analytické kolekce licencí na [**úrovni**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0d981-112">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="0d981-113">Nakonec zavolejte [**metodu Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) a získejte agregovaná data o využití licencí.</span><span class="sxs-lookup"><span data-stu-id="0d981-113">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="0d981-114">Pokud je metoda úspěšná, získáte kolekci objektů [**CustomerLicensesUsageInsights.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights)</span><span class="sxs-lookup"><span data-stu-id="0d981-114">If the method succeeds, you'll get a collection of [**CustomerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="0d981-115">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="0d981-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0d981-116">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="0d981-116">Request syntax</span></span>

| <span data-ttu-id="0d981-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="0d981-117">Method</span></span>  | <span data-ttu-id="0d981-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0d981-118">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0d981-119">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="0d981-119">**GET**</span></span> | <span data-ttu-id="0d981-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/analytics/licence/využití HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0d981-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0d981-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0d981-121">URI parameter</span></span>

<span data-ttu-id="0d981-122">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="0d981-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="0d981-123">Název</span><span class="sxs-lookup"><span data-stu-id="0d981-123">Name</span></span>        | <span data-ttu-id="0d981-124">Typ</span><span class="sxs-lookup"><span data-stu-id="0d981-124">Type</span></span> | <span data-ttu-id="0d981-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0d981-125">Required</span></span> | <span data-ttu-id="0d981-126">Popis</span><span class="sxs-lookup"><span data-stu-id="0d981-126">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="0d981-127">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="0d981-127">customer-id</span></span> | <span data-ttu-id="0d981-128">guid</span><span class="sxs-lookup"><span data-stu-id="0d981-128">guid</span></span> | <span data-ttu-id="0d981-129">Yes</span><span class="sxs-lookup"><span data-stu-id="0d981-129">Yes</span></span>      | <span data-ttu-id="0d981-130">Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0d981-130">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0d981-131">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0d981-131">Request headers</span></span>

<span data-ttu-id="0d981-132">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0d981-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0d981-133">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0d981-133">Request body</span></span>

<span data-ttu-id="0d981-134">Žádné</span><span class="sxs-lookup"><span data-stu-id="0d981-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0d981-135">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0d981-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0d981-136">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0d981-136">REST response</span></span>

<span data-ttu-id="0d981-137">V případě úspěchu text odpovědi obsahuje kolekci prostředků [CustomerLicensesUsageInsights,](analytics-resources.md#customerlicensesusageinsights) které poskytují informace o využití licencí.</span><span class="sxs-lookup"><span data-stu-id="0d981-137">If successful, the response body contains a collection of [CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights) resources that provide information about licenses usage.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0d981-138">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="0d981-138">Response success and error codes</span></span>

<span data-ttu-id="0d981-139">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0d981-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0d981-140">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="0d981-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0d981-141">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0d981-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0d981-142">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0d981-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1726
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CV: 0mufM0K1kEOoR7oI.0
MS-ServerId: 030020525
Date: Wed, 15 Mar 2017 01:19:58 GMT

{
    "totalCount": 5,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesActive": 0,
            "licensesQualified": 5,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesActive": 0,
            "licensesQualified": 2,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
