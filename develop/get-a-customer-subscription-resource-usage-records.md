---
title: Získat data o využití pro předplatné podle prostředku
description: Pomocí prostředku ResourceUsageRecord můžete získat záznamy o využití prostředků zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e815430730dd7182380e9efd1fea80f9e84d2ce7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766798"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="0f59d-103">Získat data o využití pro předplatné podle prostředku</span><span class="sxs-lookup"><span data-stu-id="0f59d-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="0f59d-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="0f59d-104">**Applies to:**</span></span>

- <span data-ttu-id="0f59d-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0f59d-105">Partner Center</span></span>
- <span data-ttu-id="0f59d-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="0f59d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0f59d-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0f59d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0f59d-108">Tento článek popisuje, jak získat prostředek **ResourceUsageRecord** .</span><span class="sxs-lookup"><span data-stu-id="0f59d-108">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="0f59d-109">Tento prostředek představuje agregovaný součet za měsíc pro jednotlivé prostředky zřízené v plánu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f59d-109">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="0f59d-110">Tento prostředek můžete použít k získání záznamů o využití prostředků zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="0f59d-110">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="0f59d-111">Toto rozhraní API vrací data, která nebyla dříve k dispozici prostřednictvím rozhraní API útraty Azure.</span><span class="sxs-lookup"><span data-stu-id="0f59d-111">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="0f59d-112">*Tato trasa nepodporuje odběry Microsoft Azure (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="0f59d-112">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f59d-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0f59d-113">Prerequisites</span></span>

- <span data-ttu-id="0f59d-114">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0f59d-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0f59d-115">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="0f59d-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0f59d-116">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0f59d-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0f59d-117">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0f59d-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0f59d-118">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="0f59d-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0f59d-119">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="0f59d-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0f59d-120">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="0f59d-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0f59d-121">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0f59d-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0f59d-122">Identifikátor předplatného</span><span class="sxs-lookup"><span data-stu-id="0f59d-122">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="0f59d-123">C\#</span><span class="sxs-lookup"><span data-stu-id="0f59d-123">C\#</span></span>

<span data-ttu-id="0f59d-124">Postup získání záznamů o využití prostředků zákazníka pro konkrétní službu nebo prostředek Azure během aktuálního fakturačního období:</span><span class="sxs-lookup"><span data-stu-id="0f59d-124">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="0f59d-125">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="0f59d-125">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="0f59d-126">Zavolejte vlastnost Subscriptions a také **UsageRecords** a pak vlastnost **Resources (prostředky** ).</span><span class="sxs-lookup"><span data-stu-id="0f59d-126">Call the Subscriptions property, as well as **UsageRecords**, then the **Resources** property.</span></span> <span data-ttu-id="0f59d-127">Dokončete voláním metod Get () nebo GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="0f59d-127">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="0f59d-128">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="0f59d-128">For an example, see the following:</span></span>

- <span data-ttu-id="0f59d-129">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="0f59d-129">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="0f59d-130">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="0f59d-130">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="0f59d-131">Třída: **GetSubscriptionUsageRecordsByResource.cs**</span><span class="sxs-lookup"><span data-stu-id="0f59d-131">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="0f59d-132">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0f59d-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0f59d-133">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0f59d-133">Request syntax</span></span>

| <span data-ttu-id="0f59d-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="0f59d-134">Method</span></span>  | <span data-ttu-id="0f59d-135">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0f59d-135">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0f59d-136">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="0f59d-136">**GET**</span></span> | <span data-ttu-id="0f59d-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/resourceusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0f59d-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="0f59d-138">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="0f59d-138">URI parameters</span></span>

<span data-ttu-id="0f59d-139">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o využití ohodnocených zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="0f59d-139">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="0f59d-140">Název</span><span class="sxs-lookup"><span data-stu-id="0f59d-140">Name</span></span>                   | <span data-ttu-id="0f59d-141">Typ</span><span class="sxs-lookup"><span data-stu-id="0f59d-141">Type</span></span>     | <span data-ttu-id="0f59d-142">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0f59d-142">Required</span></span> | <span data-ttu-id="0f59d-143">Popis</span><span class="sxs-lookup"><span data-stu-id="0f59d-143">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="0f59d-144">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="0f59d-144">**customer-tenant-id**</span></span> | <span data-ttu-id="0f59d-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="0f59d-145">**guid**</span></span> | <span data-ttu-id="0f59d-146">Y</span><span class="sxs-lookup"><span data-stu-id="0f59d-146">Y</span></span>        | <span data-ttu-id="0f59d-147">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="0f59d-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="0f59d-148">**ID předplatného**</span><span class="sxs-lookup"><span data-stu-id="0f59d-148">**subscription-id**</span></span>    | <span data-ttu-id="0f59d-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="0f59d-149">**guid**</span></span> | <span data-ttu-id="0f59d-150">Y</span><span class="sxs-lookup"><span data-stu-id="0f59d-150">Y</span></span>        | <span data-ttu-id="0f59d-151">Identifikátor GUID odpovídající identifikátoru [prostředku předplatného](subscription-resources.md#subscription)partnerského centra, který představuje předplatné Microsoft Azure (MS-AZR-0145P) nebo plán Azure.</span><span class="sxs-lookup"><span data-stu-id="0f59d-151">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="0f59d-152">*V části plánování prostředků předplatného Azure zadejte **ID plánu** jako **ID předplatného** v této trase.*</span><span class="sxs-lookup"><span data-stu-id="0f59d-152">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0f59d-153">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0f59d-153">Request headers</span></span>

<span data-ttu-id="0f59d-154">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0f59d-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0f59d-155">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0f59d-155">Request body</span></span>

<span data-ttu-id="0f59d-156">Žádné</span><span class="sxs-lookup"><span data-stu-id="0f59d-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0f59d-157">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0f59d-157">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="0f59d-158">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0f59d-158">REST response</span></span>

<span data-ttu-id="0f59d-159">V případě úspěchu tato metoda vrátí prostředek **PagedResourceCollection \<ResourceUsageRecord>** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="0f59d-159">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0f59d-160">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0f59d-160">Response success and error codes</span></span>

<span data-ttu-id="0f59d-161">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0f59d-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0f59d-162">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0f59d-162">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="0f59d-163">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0f59d-163">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0f59d-164">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0f59d-164">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
