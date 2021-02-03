---
title: Získat záznamy o využití pro všechny zákazníky
description: Pomocí kolekce prostředků CustomerMonthlyUsageRecord můžete získat záznamy o využití pro všechny zákazníky, kteří si zakoupili konkrétní službu nebo prostředek Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: da829a6de3690a9b1117ce9dfa58fbe381cafd81
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766804"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="b3948-103">Získat záznamy o využití pro všechny zákazníky</span><span class="sxs-lookup"><span data-stu-id="b3948-103">Get usage records for all customers</span></span>

<span data-ttu-id="b3948-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="b3948-104">**Applies to:**</span></span>

- <span data-ttu-id="b3948-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b3948-105">Partner Center</span></span>
- <span data-ttu-id="b3948-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="b3948-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b3948-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b3948-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b3948-108">Partneři můžou pomocí kolekce prostředků **CustomerMonthlyUsageRecord** získat záznamy o využití pro všechny své zákazníky.</span><span class="sxs-lookup"><span data-stu-id="b3948-108">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="b3948-109">Tento prostředek představuje záznamy o využití pro všechny zákazníky.</span><span class="sxs-lookup"><span data-stu-id="b3948-109">This resource represents usage records for all customers.</span></span> <span data-ttu-id="b3948-110">Který zahrnuje zákazníky s předplatným Microsoft Azure (MS-AZR-0145P) nebo plánem Azure.</span><span class="sxs-lookup"><span data-stu-id="b3948-110">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3948-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b3948-111">Prerequisites</span></span>

- <span data-ttu-id="b3948-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b3948-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b3948-113">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b3948-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b3948-114">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b3948-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b3948-115">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b3948-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b3948-116">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b3948-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b3948-117">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b3948-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b3948-118">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b3948-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b3948-119">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b3948-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b3948-120">C\#</span><span class="sxs-lookup"><span data-stu-id="b3948-120">C\#</span></span>

<span data-ttu-id="b3948-121">Chcete-li získat všechny záznamy o využití pro všechny zákazníky, kteří si zakoupili určitou službu nebo prostředek Azure během aktuálního fakturačního období:</span><span class="sxs-lookup"><span data-stu-id="b3948-121">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="b3948-122">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="b3948-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="b3948-123">Zavolejte vlastnost **UsageRecords** a potom zavolejte metodu **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="b3948-123">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="b3948-124">Příklad naleznete v následující ukázce:</span><span class="sxs-lookup"><span data-stu-id="b3948-124">For an example, see the following sample:</span></span>

- <span data-ttu-id="b3948-125">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="b3948-125">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="b3948-126">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="b3948-126">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="b3948-127">Třída: **GetCustomerUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="b3948-127">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="b3948-128">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b3948-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b3948-129">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b3948-129">Request syntax</span></span>

| <span data-ttu-id="b3948-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="b3948-130">Method</span></span>  | <span data-ttu-id="b3948-131">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b3948-131">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="b3948-132">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b3948-132">**GET**</span></span> | <span data-ttu-id="b3948-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b3948-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b3948-134">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b3948-134">Request headers</span></span>

<span data-ttu-id="b3948-135">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b3948-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b3948-136">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b3948-136">Request body</span></span>

<span data-ttu-id="b3948-137">Žádné</span><span class="sxs-lookup"><span data-stu-id="b3948-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b3948-138">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b3948-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="b3948-139">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b3948-139">REST response</span></span>

<span data-ttu-id="b3948-140">V případě úspěchu tato metoda vrátí prostředek **CustomerMonthlyUsageRecord** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b3948-140">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b3948-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b3948-141">Response success and error codes</span></span>

<span data-ttu-id="b3948-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b3948-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b3948-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b3948-143">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="b3948-144">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b3948-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b3948-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b3948-145">Response example</span></span>

<span data-ttu-id="b3948-146">Pomocí vlastnosti- **upgrade** můžete identifikovat zákazníky, kteří mají plán Azure.</span><span class="sxs-lookup"><span data-stu-id="b3948-146">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="b3948-147">Pokud je hodnota pro **upgrade** **pravdivá**, znamená to, že zákazníci mají plány Azure.</span><span class="sxs-lookup"><span data-stu-id="b3948-147">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 25,
    "items": [
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "customerSpendingBudget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": false,
            "resourceId": "11111111-1843-4b3b-872f-206e08a08e51",
            "id": "11111111-1843-4b3b-872f-206e08a08e51",
            "resourceName": "LEGACY AZURE CUSTOMER SE",
            "name": "LEGACY AZURE CUSTOMER SE",
            "totalCost": 0,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-08-01T23:00:16.57+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "amount": 20,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 602.84,
            "isUpgraded": true,
            "resourceId": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "id": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "resourceName": "Modern Azure Customer SE",
            "name": "Modern Azure Customer SE",
            "totalCost": 120.5682999999995904716,
            "currencyCode": "SEK",
            "usdTotalCost": 12.39999999999999985235,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": true,
            "resourceId": "11111111-5892-4326-8541-9da1fdb233fb",
            "id": "11111111-5892-4326-8541-9da1fdb233fb",
            "resourceName": "Test_Test_MA20190829_14",
            "name": "Test_Test_MA20190829_14",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
           {
            "budget": {
                "amount": 97,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 28.08,
            "isUpgraded": true,
            "resourceId": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "id": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "resourceName": "Modern Azure Customer UK",
            "name": "Modern Azure Customer UK",
            "totalCost": 27.23292827625710931604,
            "currencyCode": "GBP",
            "usdTotalCost": 33.280000000000001044,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
