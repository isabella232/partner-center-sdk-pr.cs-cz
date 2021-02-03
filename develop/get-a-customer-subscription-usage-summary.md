---
title: Získat Souhrn využití pro předplatné zákazníka
description: Pomocí prostředku SubscriptionUsageSummary můžete v aktuálním fakturačním období získat Souhrn využití předplatných konkrétní služby nebo prostředku Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30334b6f08829eccf0693b566c11f94cb3ece976
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766797"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="802e3-103">Získat Souhrn využití pro předplatné zákazníka</span><span class="sxs-lookup"><span data-stu-id="802e3-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="802e3-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="802e3-104">**Applies to:**</span></span>

- <span data-ttu-id="802e3-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="802e3-105">Partner Center</span></span>
- <span data-ttu-id="802e3-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="802e3-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="802e3-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="802e3-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="802e3-108">Pomocí prostředku **SubscriptionUsageSummary** můžete získat Souhrn využití předplatných pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="802e3-108">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="802e3-109">Tento prostředek představuje souhrn využití předplatných konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="802e3-109">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="802e3-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="802e3-110">Prerequisites</span></span>

- <span data-ttu-id="802e3-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="802e3-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="802e3-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="802e3-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="802e3-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="802e3-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="802e3-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="802e3-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="802e3-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="802e3-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="802e3-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="802e3-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="802e3-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="802e3-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="802e3-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="802e3-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="802e3-119">Identifikátor předplatného</span><span class="sxs-lookup"><span data-stu-id="802e3-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="802e3-120">C\#</span><span class="sxs-lookup"><span data-stu-id="802e3-120">C\#</span></span>

<span data-ttu-id="802e3-121">Získání souhrnu využití předplatného pro předplatné zákazníka:</span><span class="sxs-lookup"><span data-stu-id="802e3-121">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="802e3-122">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="802e3-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="802e3-123">Pak zavolejte vlastnost Subscriptions a také vlastnost **UsageSummary** .</span><span class="sxs-lookup"><span data-stu-id="802e3-123">Then call the Subscriptions property, as well as **UsageSummary** property.</span></span> <span data-ttu-id="802e3-124">Dokončete voláním metod Get () nebo GetAsync ().</span><span class="sxs-lookup"><span data-stu-id="802e3-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="802e3-125">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="802e3-125">For an example, see the following:</span></span>

- <span data-ttu-id="802e3-126">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="802e3-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="802e3-127">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="802e3-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="802e3-128">Třída: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="802e3-128">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="802e3-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="802e3-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="802e3-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="802e3-130">Request syntax</span></span>

| <span data-ttu-id="802e3-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="802e3-131">Method</span></span>  | <span data-ttu-id="802e3-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="802e3-132">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="802e3-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="802e3-133">**GET**</span></span> | <span data-ttu-id="802e3-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="802e3-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="802e3-135">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="802e3-135">URI parameters</span></span>

<span data-ttu-id="802e3-136">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o využití ohodnocených zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="802e3-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="802e3-137">Název</span><span class="sxs-lookup"><span data-stu-id="802e3-137">Name</span></span>                   | <span data-ttu-id="802e3-138">Typ</span><span class="sxs-lookup"><span data-stu-id="802e3-138">Type</span></span>     | <span data-ttu-id="802e3-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="802e3-139">Required</span></span> | <span data-ttu-id="802e3-140">Popis</span><span class="sxs-lookup"><span data-stu-id="802e3-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="802e3-141">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="802e3-141">**customer-tenant-id**</span></span> | <span data-ttu-id="802e3-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="802e3-142">**guid**</span></span> | <span data-ttu-id="802e3-143">Y</span><span class="sxs-lookup"><span data-stu-id="802e3-143">Y</span></span>        | <span data-ttu-id="802e3-144">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="802e3-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="802e3-145">**ID předplatného**</span><span class="sxs-lookup"><span data-stu-id="802e3-145">**subscription-id**</span></span>    | <span data-ttu-id="802e3-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="802e3-146">**guid**</span></span> | <span data-ttu-id="802e3-147">Y</span><span class="sxs-lookup"><span data-stu-id="802e3-147">Y</span></span>        | <span data-ttu-id="802e3-148">Identifikátor GUID odpovídající identifikátoru předplatného.</span><span class="sxs-lookup"><span data-stu-id="802e3-148">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="802e3-149">Pro plán Azure se jedná o identifikátor odpovídajícího [prostředku pro předplatné](subscription-resources.md#subscription)partnerského centra, který představuje plán Azure.</span><span class="sxs-lookup"><span data-stu-id="802e3-149">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="802e3-150">*V části plánování prostředků předplatného Azure zadejte **ID plánu** jako **ID předplatného** v této trase.*</span><span class="sxs-lookup"><span data-stu-id="802e3-150">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="802e3-151">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="802e3-151">Request headers</span></span>

<span data-ttu-id="802e3-152">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="802e3-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="802e3-153">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="802e3-153">Request body</span></span>

<span data-ttu-id="802e3-154">Žádné</span><span class="sxs-lookup"><span data-stu-id="802e3-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="802e3-155">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="802e3-155">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="802e3-156">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="802e3-156">REST response</span></span>

<span data-ttu-id="802e3-157">V případě úspěchu tato metoda vrátí prostředek **SubscriptionUsageSummary** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="802e3-157">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="802e3-158">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="802e3-158">Response success and error codes</span></span>

<span data-ttu-id="802e3-159">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="802e3-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="802e3-160">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="802e3-160">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="802e3-161">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="802e3-161">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="802e3-162">Příklad odpovědi pro předplatná Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="802e3-162">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="802e3-163">V tomto příkladu si zákazník koupil nabídku **145P Azure PayG** .</span><span class="sxs-lookup"><span data-stu-id="802e3-163">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="802e3-164">*Pro zákazníky s předplatnými Microsoft Azure (MS-AZR-0145P) nedojde k žádné změně v odpovědi rozhraní API.*</span><span class="sxs-lookup"><span data-stu-id="802e3-164">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="802e3-165">Příklad odpovědi REST pro plán Azure</span><span class="sxs-lookup"><span data-stu-id="802e3-165">REST response example for Azure plan</span></span>

<span data-ttu-id="802e3-166">V tomto příkladu si zákazník koupil plán Azure.</span><span class="sxs-lookup"><span data-stu-id="802e3-166">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="802e3-167">*Pro zákazníky s plány Azure jsou k dispozici následující změny odezvy rozhraní API:*</span><span class="sxs-lookup"><span data-stu-id="802e3-167">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="802e3-168">**currencyLocale** se nahrazuje **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="802e3-168">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="802e3-169">**usdTotalCost** je nové pole.</span><span class="sxs-lookup"><span data-stu-id="802e3-169">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
