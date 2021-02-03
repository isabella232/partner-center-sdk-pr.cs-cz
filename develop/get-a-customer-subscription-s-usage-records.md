---
title: Získání všech záznamů o využití předplatných pro zákazníka
description: Pomocí kolekce prostředků SubscriptionMonthlyUsageRecord můžete získat záznamy o využití předplatných pro zákazníka konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 765ea16ff58b462d83ae3b8764b8b34c3ef804dc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766799"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="e0d6d-103">Získání záznamů o využití předplatných pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="e0d6d-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="e0d6d-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="e0d6d-104">**Applies to:**</span></span>

- <span data-ttu-id="e0d6d-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e0d6d-105">Partner Center</span></span>
- <span data-ttu-id="e0d6d-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="e0d6d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e0d6d-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e0d6d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e0d6d-108">Pomocí kolekce prostředků **SubscriptionMonthlyUsageRecord** můžete získat záznamy o využití předplatných pro zákazníka konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-108">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="e0d6d-109">Tento prostředek představuje všechna předplatná pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-109">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="e0d6d-110">U zákazníka s plánem Azure tento prostředek vrátí seznam těchto plánů (ne individuálních předplatných Azure).</span><span class="sxs-lookup"><span data-stu-id="e0d6d-110">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0d6d-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e0d6d-111">Prerequisites</span></span>

- <span data-ttu-id="e0d6d-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e0d6d-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e0d6d-113">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e0d6d-114">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e0d6d-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e0d6d-115">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e0d6d-116">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e0d6d-117">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e0d6d-118">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e0d6d-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e0d6d-119">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e0d6d-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e0d6d-120">C\#</span><span class="sxs-lookup"><span data-stu-id="e0d6d-120">C\#</span></span>

<span data-ttu-id="e0d6d-121">Získání záznamů o využití předplatných pro zákazníka konkrétní služby nebo prostředku Azure během aktuálního fakturačního období:</span><span class="sxs-lookup"><span data-stu-id="e0d6d-121">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period.:</span></span>

1. <span data-ttu-id="e0d6d-122">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="e0d6d-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="e0d6d-123">Pak zavolejte vlastnost **Subscriptions** a také vlastnost **UsageRecords** .</span><span class="sxs-lookup"><span data-stu-id="e0d6d-123">Then call the **Subscriptions** property, as well as **UsageRecords** property.</span></span> <span data-ttu-id="e0d6d-124">Dokončete voláním metod Get () nebo GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="e0d6d-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="e0d6d-125">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="e0d6d-125">For an example, see the following:</span></span>

- <span data-ttu-id="e0d6d-126">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e0d6d-127">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="e0d6d-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="e0d6d-128">Třída: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="e0d6d-128">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e0d6d-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e0d6d-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e0d6d-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e0d6d-130">Request syntax</span></span>

| <span data-ttu-id="e0d6d-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="e0d6d-131">Method</span></span>  | <span data-ttu-id="e0d6d-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e0d6d-132">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e0d6d-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="e0d6d-133">**GET**</span></span> | <span data-ttu-id="e0d6d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e0d6d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e0d6d-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e0d6d-135">URI parameter</span></span>

<span data-ttu-id="e0d6d-136">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o využití ohodnocených zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-136">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="e0d6d-137">Název</span><span class="sxs-lookup"><span data-stu-id="e0d6d-137">Name</span></span>                   | <span data-ttu-id="e0d6d-138">Typ</span><span class="sxs-lookup"><span data-stu-id="e0d6d-138">Type</span></span>     | <span data-ttu-id="e0d6d-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e0d6d-139">Required</span></span> | <span data-ttu-id="e0d6d-140">Popis</span><span class="sxs-lookup"><span data-stu-id="e0d6d-140">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="e0d6d-141">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="e0d6d-141">**customer-tenant-id**</span></span> | <span data-ttu-id="e0d6d-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="e0d6d-142">**guid**</span></span> | <span data-ttu-id="e0d6d-143">Y</span><span class="sxs-lookup"><span data-stu-id="e0d6d-143">Y</span></span>        | <span data-ttu-id="e0d6d-144">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-144">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e0d6d-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e0d6d-145">Request headers</span></span>

<span data-ttu-id="e0d6d-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e0d6d-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e0d6d-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e0d6d-147">Request body</span></span>

<span data-ttu-id="e0d6d-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="e0d6d-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e0d6d-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e0d6d-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="e0d6d-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e0d6d-150">REST response</span></span>

<span data-ttu-id="e0d6d-151">V případě úspěchu tato metoda vrátí prostředek **SubscriptionMonthlyUsageRecord** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-151">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e0d6d-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e0d6d-152">Response success and error codes</span></span>

<span data-ttu-id="e0d6d-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e0d6d-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-154">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="e0d6d-155">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e0d6d-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="e0d6d-156">Příklad odpovědi pro předplatná Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="e0d6d-156">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="e0d6d-157">V tomto příkladu si zákazník koupil nabídku **145P Azure PayG** .</span><span class="sxs-lookup"><span data-stu-id="e0d6d-157">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="e0d6d-158">*Pro zákazníky s předplatnými Microsoft Azure (MS-AZR-0145P) nedojde k žádné změně v odpovědi rozhraní API.*</span><span class="sxs-lookup"><span data-stu-id="e0d6d-158">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="e0d6d-159">Příklad odpovědi REST pro plán Azure</span><span class="sxs-lookup"><span data-stu-id="e0d6d-159">REST response example for Azure plan</span></span>

<span data-ttu-id="e0d6d-160">V tomto příkladu si zákazník koupil plán Azure.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-160">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="e0d6d-161">*Pro zákazníky s plány Azure jsou v odpovědi rozhraní API tyto změny:*</span><span class="sxs-lookup"><span data-stu-id="e0d6d-161">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="e0d6d-162">**currencyLocale** se nahrazuje **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="e0d6d-162">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="e0d6d-163">**usdTotalCost** je nové pole.</span><span class="sxs-lookup"><span data-stu-id="e0d6d-163">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 2,
    "items": [
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-7d58-6654-69fa-0797198155d3",
            "id": "11111111-7d58-6654-69fa-0797198155d3",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        },
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "id": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
