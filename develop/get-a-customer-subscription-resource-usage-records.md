---
title: Získat data o využití pro předplatné podle prostředku
description: Pomocí prostředku ResourceUsageRecord můžete získat záznamy o využití prostředků zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 50edb9de1d09363b242c080a76c683732f05a5de
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874835"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="faa79-103">Získat data o využití pro předplatné podle prostředku</span><span class="sxs-lookup"><span data-stu-id="faa79-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="faa79-104">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="faa79-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="faa79-105">Tento článek popisuje, jak získat prostředek **ResourceUsageRecord** .</span><span class="sxs-lookup"><span data-stu-id="faa79-105">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="faa79-106">Tento prostředek představuje agregovaný součet za měsíc pro jednotlivé prostředky zřízené v plánu Azure.</span><span class="sxs-lookup"><span data-stu-id="faa79-106">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="faa79-107">Tento prostředek můžete použít k získání záznamů o využití prostředků zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="faa79-107">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="faa79-108">Toto rozhraní API vrací data, která nebyla dříve k dispozici prostřednictvím rozhraní API útraty Azure.</span><span class="sxs-lookup"><span data-stu-id="faa79-108">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="faa79-109">*tato trasa nepodporuje odběry Microsoft Azure (MS-AZR-0145P).*</span><span class="sxs-lookup"><span data-stu-id="faa79-109">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faa79-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="faa79-110">Prerequisites</span></span>

- <span data-ttu-id="faa79-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="faa79-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="faa79-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="faa79-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="faa79-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="faa79-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="faa79-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="faa79-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="faa79-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="faa79-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="faa79-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="faa79-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="faa79-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="faa79-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="faa79-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="faa79-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="faa79-119">Identifikátor předplatného</span><span class="sxs-lookup"><span data-stu-id="faa79-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="faa79-120">C\#</span><span class="sxs-lookup"><span data-stu-id="faa79-120">C\#</span></span>

<span data-ttu-id="faa79-121">Postup získání záznamů o využití prostředků zákazníka pro konkrétní službu nebo prostředek Azure během aktuálního fakturačního období:</span><span class="sxs-lookup"><span data-stu-id="faa79-121">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="faa79-122">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="faa79-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="faa79-123">Zavolejte vlastnost Subscriptions a **UsageRecords** a potom vlastnost **Resources** .</span><span class="sxs-lookup"><span data-stu-id="faa79-123">Call the Subscriptions property and **UsageRecords**, and then the **Resources** property.</span></span> <span data-ttu-id="faa79-124">Dokončete voláním metod Get () nebo GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="faa79-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="faa79-125">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="faa79-125">For an example, see the following:</span></span>

- <span data-ttu-id="faa79-126">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="faa79-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="faa79-127">Project: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="faa79-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="faa79-128">Třída: **GetSubscriptionUsageRecordsByResource. cs**</span><span class="sxs-lookup"><span data-stu-id="faa79-128">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="faa79-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="faa79-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="faa79-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="faa79-130">Request syntax</span></span>

| <span data-ttu-id="faa79-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="faa79-131">Method</span></span>  | <span data-ttu-id="faa79-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="faa79-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="faa79-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="faa79-133">**GET**</span></span> | <span data-ttu-id="faa79-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/resourceusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="faa79-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="faa79-135">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="faa79-135">URI parameters</span></span>

<span data-ttu-id="faa79-136">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o využití ohodnocených zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="faa79-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="faa79-137">Název</span><span class="sxs-lookup"><span data-stu-id="faa79-137">Name</span></span>                   | <span data-ttu-id="faa79-138">Typ</span><span class="sxs-lookup"><span data-stu-id="faa79-138">Type</span></span>     | <span data-ttu-id="faa79-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="faa79-139">Required</span></span> | <span data-ttu-id="faa79-140">Popis</span><span class="sxs-lookup"><span data-stu-id="faa79-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="faa79-141">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="faa79-141">**customer-tenant-id**</span></span> | <span data-ttu-id="faa79-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="faa79-142">**guid**</span></span> | <span data-ttu-id="faa79-143">Y</span><span class="sxs-lookup"><span data-stu-id="faa79-143">Y</span></span>        | <span data-ttu-id="faa79-144">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="faa79-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="faa79-145">**ID předplatného**</span><span class="sxs-lookup"><span data-stu-id="faa79-145">**subscription-id**</span></span>    | <span data-ttu-id="faa79-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="faa79-146">**guid**</span></span> | <span data-ttu-id="faa79-147">Y</span><span class="sxs-lookup"><span data-stu-id="faa79-147">Y</span></span>        | <span data-ttu-id="faa79-148">identifikátor GUID odpovídající identifikátoru [prostředku předplatného](subscription-resources.md#subscription)partnerského centra, který představuje předplatné Microsoft Azure (MS-AZR-0145P) nebo plán Azure.</span><span class="sxs-lookup"><span data-stu-id="faa79-148">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="faa79-149">*V části plánování prostředků předplatného Azure zadejte **ID plánu** jako **ID předplatného** v této trase.*</span><span class="sxs-lookup"><span data-stu-id="faa79-149">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="faa79-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="faa79-150">Request headers</span></span>

<span data-ttu-id="faa79-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="faa79-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="faa79-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="faa79-152">Request body</span></span>

<span data-ttu-id="faa79-153">Žádné</span><span class="sxs-lookup"><span data-stu-id="faa79-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="faa79-154">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="faa79-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="faa79-155">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="faa79-155">REST response</span></span>

<span data-ttu-id="faa79-156">V případě úspěchu tato metoda vrátí prostředek **PagedResourceCollection \<ResourceUsageRecord>** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="faa79-156">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="faa79-157">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="faa79-157">Response success and error codes</span></span>

<span data-ttu-id="faa79-158">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="faa79-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="faa79-159">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="faa79-159">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="faa79-160">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="faa79-160">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="faa79-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="faa79-161">Response example</span></span>

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
