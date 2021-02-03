---
title: Získání dat o využití pro předplatné podle měřiče
description: Pomocí kolekce prostředků MeterUsageRecord můžete získat záznamy o využití měřičů zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766800"
---
# <a name="get-usage-data-for-subscription-by-meter"></a><span data-ttu-id="e2f20-103">Získání dat o využití pro předplatné podle měřiče</span><span class="sxs-lookup"><span data-stu-id="e2f20-103">Get usage data for subscription by meter</span></span>

<span data-ttu-id="e2f20-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="e2f20-104">**Applies to:**</span></span>

- <span data-ttu-id="e2f20-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e2f20-105">Partner Center</span></span>
- <span data-ttu-id="e2f20-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="e2f20-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e2f20-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e2f20-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e2f20-108">Pomocí kolekce prostředků **MeterUsageRecord** můžete získat záznamy o využití měřičů zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="e2f20-108">You can use the **MeterUsageRecord** resource collection to get meter usage records of a customer for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="e2f20-109">Tato kolekce prostředků představuje agregovaný součet pro každý měřič pro aktuální fakturační cyklus v rámci celého plánu Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f20-109">This resource collection represents an aggregated total for each meter for the current billing cycle, across your entire Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2f20-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e2f20-110">Prerequisites</span></span>

- <span data-ttu-id="e2f20-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e2f20-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e2f20-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="e2f20-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e2f20-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e2f20-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e2f20-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e2f20-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e2f20-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e2f20-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e2f20-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e2f20-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e2f20-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e2f20-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e2f20-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e2f20-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e2f20-119">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="e2f20-119">A subscription ID</span></span>

<span data-ttu-id="e2f20-120">*Tato nová trasa je ekvivalentní k `subscriptions/{subscription-id}/usagerecords/resources` , což bude i nadále fungovat jenom pro předplatná Microsoft Azure (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="e2f20-120">*This new route is equivalent to `subscriptions/{subscription-id}/usagerecords/resources`, which will continue to function only for Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span> <span data-ttu-id="e2f20-121">Tato nová trasa bude podporovat předplatná Microsoft Azure (MS-AZR-0145P) i plány Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f20-121">This new route will support both Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span> <span data-ttu-id="e2f20-122">Chcete-li získat tyto informace pro plán Azure, musíte přepnout do této nové trasy.</span><span class="sxs-lookup"><span data-stu-id="e2f20-122">In order to get this information for your Azure plan, you need to switch to this new route.</span></span> <span data-ttu-id="e2f20-123">Kromě vlastností uvedených v následujících částech je odpověď stejná jako u staré trasy.</span><span class="sxs-lookup"><span data-stu-id="e2f20-123">Other than the properties mentioned in the following sections, the response is the same as the old route.</span></span>

## <a name="c"></a><span data-ttu-id="e2f20-124">C\#</span><span class="sxs-lookup"><span data-stu-id="e2f20-124">C\#</span></span>

<span data-ttu-id="e2f20-125">Postup získání záznamů využití měřiče zákazníka pro konkrétní službu nebo prostředek Azure během aktuálního fakturačního období:</span><span class="sxs-lookup"><span data-stu-id="e2f20-125">To get meter usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="e2f20-126">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="e2f20-126">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="e2f20-127">Zavolejte vlastnost Subscriptions a pak vlastnost **měřiče** ( **UsageRecords**).</span><span class="sxs-lookup"><span data-stu-id="e2f20-127">Call the Subscriptions property, and **UsageRecords**, then the **Meters** property.</span></span> <span data-ttu-id="e2f20-128">Dokončete voláním metod Get () nebo GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="e2f20-128">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

<span data-ttu-id="e2f20-129">Příklad naleznete v následující ukázce:</span><span class="sxs-lookup"><span data-stu-id="e2f20-129">For an example, see the following sample:</span></span>

- <span data-ttu-id="e2f20-130">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e2f20-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e2f20-131">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="e2f20-131">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="e2f20-132">Třída: **GetSubscriptionUsageRecordsByMeter.cs**</span><span class="sxs-lookup"><span data-stu-id="e2f20-132">Class: **GetSubscriptionUsageRecordsByMeter.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e2f20-133">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e2f20-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e2f20-134">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e2f20-134">Request syntax</span></span>

| <span data-ttu-id="e2f20-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="e2f20-135">Method</span></span>  | <span data-ttu-id="e2f20-136">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e2f20-136">Request URI</span></span>                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e2f20-137">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="e2f20-137">**GET**</span></span> | <span data-ttu-id="e2f20-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/meterusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e2f20-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="e2f20-139">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="e2f20-139">URI parameters</span></span>

<span data-ttu-id="e2f20-140">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o využití ohodnocených zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="e2f20-140">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="e2f20-141">Název</span><span class="sxs-lookup"><span data-stu-id="e2f20-141">Name</span></span>                   | <span data-ttu-id="e2f20-142">Typ</span><span class="sxs-lookup"><span data-stu-id="e2f20-142">Type</span></span>     | <span data-ttu-id="e2f20-143">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e2f20-143">Required</span></span> | <span data-ttu-id="e2f20-144">Popis</span><span class="sxs-lookup"><span data-stu-id="e2f20-144">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="e2f20-145">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="e2f20-145">**customer-tenant-id**</span></span> | <span data-ttu-id="e2f20-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="e2f20-146">**guid**</span></span> | <span data-ttu-id="e2f20-147">Y</span><span class="sxs-lookup"><span data-stu-id="e2f20-147">Y</span></span>        | <span data-ttu-id="e2f20-148">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="e2f20-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="e2f20-149">**ID předplatného**</span><span class="sxs-lookup"><span data-stu-id="e2f20-149">**subscription-id**</span></span>    | <span data-ttu-id="e2f20-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="e2f20-150">**guid**</span></span> | <span data-ttu-id="e2f20-151">Y</span><span class="sxs-lookup"><span data-stu-id="e2f20-151">Y</span></span>        | <span data-ttu-id="e2f20-152">Identifikátor GUID odpovídající identifikátoru [prostředku předplatného](subscription-resources.md#subscription)partnerského centra, který představuje předplatné Microsoft Azure (MS-AZR-0145P) nebo plán Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f20-152">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="e2f20-153">*V části plánování prostředků předplatného Azure zadejte **ID plánu** jako **ID předplatného** v této trase.*</span><span class="sxs-lookup"><span data-stu-id="e2f20-153">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e2f20-154">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e2f20-154">Request headers</span></span>

<span data-ttu-id="e2f20-155">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e2f20-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e2f20-156">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e2f20-156">Request body</span></span>

<span data-ttu-id="e2f20-157">Žádné</span><span class="sxs-lookup"><span data-stu-id="e2f20-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e2f20-158">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e2f20-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="e2f20-159">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e2f20-159">REST response</span></span>

<span data-ttu-id="e2f20-160">V případě úspěchu tato metoda vrátí prostředek **PagedResourceCollection \<MeterUsageRecord>** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e2f20-160">If successful, this method returns a **PagedResourceCollection\<MeterUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e2f20-161">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e2f20-161">Response success and error codes</span></span>

<span data-ttu-id="e2f20-162">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e2f20-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e2f20-163">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e2f20-163">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="e2f20-164">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e2f20-164">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="e2f20-165">Příklad odpovědi pro předplatná Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="e2f20-165">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="e2f20-166">V tomto příkladu si zákazník koupil **145P Azure PayG**.</span><span class="sxs-lookup"><span data-stu-id="e2f20-166">In this example, the customer purchased **145P Azure PayG**.</span></span>

<span data-ttu-id="e2f20-167">*Pro zákazníky s předplatným Microsoft Azure (MS-AZR-0145P) nedojde k žádné změně v odpovědi rozhraní API.*</span><span class="sxs-lookup"><span data-stu-id="e2f20-167">*For customers with a Microsoft Azure (MS-AZR-0145P) subscription, there will be no change to API response.*</span></span>

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
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="e2f20-168">Příklad odpovědi REST pro plán Azure</span><span class="sxs-lookup"><span data-stu-id="e2f20-168">REST response example for Azure plan</span></span>

<span data-ttu-id="e2f20-169">V tomto příkladu si zákazník koupil plán Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f20-169">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="e2f20-170">*Pro zákazníky s plány Azure jsou v odpovědi rozhraní API tyto změny:*</span><span class="sxs-lookup"><span data-stu-id="e2f20-170">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="e2f20-171">**currencyLocale** se nahrazuje **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="e2f20-171">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="e2f20-172">**usdTotalCost** je nové pole.</span><span class="sxs-lookup"><span data-stu-id="e2f20-172">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
