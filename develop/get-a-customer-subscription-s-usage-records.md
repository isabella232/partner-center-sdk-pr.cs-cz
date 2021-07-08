---
title: Získání všech záznamů o využití předplatných pro zákazníka
description: Kolekci prostředků SubscriptionMonthlyUsageRecord můžete použít k získání záznamů o využití předplatného pro zákazníka konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 976abd86f34c1c27184f277ffc89fbc65f16bb37
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874682"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="56d13-103">Získání záznamů o využití předplatného pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="56d13-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="56d13-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="56d13-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="56d13-105">Kolekci prostředků **SubscriptionMonthlyUsageRecord** můžete použít k získání záznamů o využití předplatného pro zákazníka konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="56d13-105">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="56d13-106">Tento prostředek představuje všechna předplatná zákazníka.</span><span class="sxs-lookup"><span data-stu-id="56d13-106">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="56d13-107">Pro zákazníka s plánem Azure tento prostředek vrátí seznam těchto plánů (ne jednotlivá předplatná Azure).</span><span class="sxs-lookup"><span data-stu-id="56d13-107">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56d13-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="56d13-108">Prerequisites</span></span>

- <span data-ttu-id="56d13-109">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="56d13-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="56d13-110">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="56d13-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="56d13-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="56d13-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="56d13-112">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="56d13-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="56d13-113">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="56d13-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="56d13-114">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="56d13-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="56d13-115">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="56d13-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="56d13-116">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="56d13-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="56d13-117">C\#</span><span class="sxs-lookup"><span data-stu-id="56d13-117">C\#</span></span>

<span data-ttu-id="56d13-118">Pokud chcete získat záznamy o využití předplatného pro zákazníka konkrétní služby nebo prostředku Azure během aktuálního fakturačního období, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="56d13-118">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period, do the following steps:</span></span>

1. <span data-ttu-id="56d13-119">K volání metody **ById()** použijte kolekci **IAggregatePartner.Customers.**</span><span class="sxs-lookup"><span data-stu-id="56d13-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="56d13-120">Potom zavolejte **vlastnost Subscriptions** a **vlastnost UsageRecords.**</span><span class="sxs-lookup"><span data-stu-id="56d13-120">Then call the **Subscriptions** property and the **UsageRecords** property.</span></span> <span data-ttu-id="56d13-121">Dokončete voláním metod Get() nebo GetAsync().</span><span class="sxs-lookup"><span data-stu-id="56d13-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="56d13-122">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="56d13-122">For an example, see the following:</span></span>

- <span data-ttu-id="56d13-123">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="56d13-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="56d13-124">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="56d13-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="56d13-125">Třída: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="56d13-125">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="56d13-126">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="56d13-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="56d13-127">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="56d13-127">Request syntax</span></span>

| <span data-ttu-id="56d13-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="56d13-128">Method</span></span>  | <span data-ttu-id="56d13-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="56d13-129">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="56d13-130">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="56d13-130">**GET**</span></span> | <span data-ttu-id="56d13-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="56d13-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="56d13-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="56d13-132">URI parameter</span></span>

<span data-ttu-id="56d13-133">Tato tabulka uvádí požadovaný parametr dotazu k získání informací o hodnocených využitích zákazníka.</span><span class="sxs-lookup"><span data-stu-id="56d13-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="56d13-134">Název</span><span class="sxs-lookup"><span data-stu-id="56d13-134">Name</span></span>                   | <span data-ttu-id="56d13-135">Typ</span><span class="sxs-lookup"><span data-stu-id="56d13-135">Type</span></span>     | <span data-ttu-id="56d13-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="56d13-136">Required</span></span> | <span data-ttu-id="56d13-137">Popis</span><span class="sxs-lookup"><span data-stu-id="56d13-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="56d13-138">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="56d13-138">**customer-tenant-id**</span></span> | <span data-ttu-id="56d13-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="56d13-139">**guid**</span></span> | <span data-ttu-id="56d13-140">Y</span><span class="sxs-lookup"><span data-stu-id="56d13-140">Y</span></span>        | <span data-ttu-id="56d13-141">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="56d13-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="56d13-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="56d13-142">Request headers</span></span>

<span data-ttu-id="56d13-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="56d13-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="56d13-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="56d13-144">Request body</span></span>

<span data-ttu-id="56d13-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="56d13-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="56d13-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="56d13-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="56d13-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="56d13-147">REST response</span></span>

<span data-ttu-id="56d13-148">V případě úspěchu vrátí tato metoda v textu odpovědi prostředek **SubscriptionMonthlyUsageRecord.**</span><span class="sxs-lookup"><span data-stu-id="56d13-148">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="56d13-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="56d13-149">Response success and error codes</span></span>

<span data-ttu-id="56d13-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="56d13-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="56d13-151">Ke čtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="56d13-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="56d13-152">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="56d13-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="56d13-153">Příklad odpovědi Microsoft Azure předplatných (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="56d13-153">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="56d13-154">V tomto příkladu zákazník zakoupil nabídku **azure payg 145P.**</span><span class="sxs-lookup"><span data-stu-id="56d13-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="56d13-155">*U zákazníků Microsoft Azure předplatných (MS-AZR-0145P) se v odpovědi rozhraní API nezmění.*</span><span class="sxs-lookup"><span data-stu-id="56d13-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="56d13-156">Příklad odpovědi REST pro plán Azure</span><span class="sxs-lookup"><span data-stu-id="56d13-156">REST response example for Azure plan</span></span>

<span data-ttu-id="56d13-157">V tomto příkladu zákazník zakoupil plán Azure.</span><span class="sxs-lookup"><span data-stu-id="56d13-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="56d13-158">*U zákazníků s plány Azure došlo v odpovědi rozhraní API k následujícím změnám:*</span><span class="sxs-lookup"><span data-stu-id="56d13-158">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="56d13-159">**currencyLocale** se nahradí **kódem měny**</span><span class="sxs-lookup"><span data-stu-id="56d13-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="56d13-160">**usdTotalCost** je nové pole</span><span class="sxs-lookup"><span data-stu-id="56d13-160">**usdTotalCost** is a new field</span></span>

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
