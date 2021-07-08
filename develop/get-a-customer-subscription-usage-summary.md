---
title: Získání souhrnu využití pro předplatné zákazníka
description: Pomocí prostředku SubscriptionUsageSummary můžete získat souhrn využití předplatného pro konkrétní službu nebo prostředek Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 362e72e1b54a62a114564d4dc48a082bcdeea012
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874665"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="58f3f-103">Získání souhrnu využití pro předplatné zákazníka</span><span class="sxs-lookup"><span data-stu-id="58f3f-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="58f3f-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="58f3f-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="58f3f-105">K získání souhrnu využití předplatného pro zákazníka můžete použít prostředek **SubscriptionUsageSummary.**</span><span class="sxs-lookup"><span data-stu-id="58f3f-105">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="58f3f-106">Tento prostředek představuje souhrn využití předplatného konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="58f3f-106">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58f3f-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="58f3f-107">Prerequisites</span></span>

- <span data-ttu-id="58f3f-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="58f3f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="58f3f-109">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="58f3f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="58f3f-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="58f3f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="58f3f-111">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="58f3f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="58f3f-112">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="58f3f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="58f3f-113">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="58f3f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="58f3f-114">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="58f3f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="58f3f-115">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="58f3f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="58f3f-116">Identifikátor předplatného</span><span class="sxs-lookup"><span data-stu-id="58f3f-116">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="58f3f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="58f3f-117">C\#</span></span>

<span data-ttu-id="58f3f-118">Získání souhrnu využití předplatného pro předplatné zákazníka:</span><span class="sxs-lookup"><span data-stu-id="58f3f-118">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="58f3f-119">K volání metody **ById()** použijte kolekci **IAggregatePartner.Customers.**</span><span class="sxs-lookup"><span data-stu-id="58f3f-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="58f3f-120">Potom zavolejte vlastnost Subscriptions a **vlastnost UsageSummary.**</span><span class="sxs-lookup"><span data-stu-id="58f3f-120">Then call the Subscriptions property and the **UsageSummary** property.</span></span> <span data-ttu-id="58f3f-121">Dokončete voláním metod Get() nebo GetAsync().</span><span class="sxs-lookup"><span data-stu-id="58f3f-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="58f3f-122">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="58f3f-122">For an example, see the following:</span></span>

- <span data-ttu-id="58f3f-123">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="58f3f-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="58f3f-124">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="58f3f-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="58f3f-125">Třída: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="58f3f-125">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="58f3f-126">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="58f3f-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="58f3f-127">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="58f3f-127">Request syntax</span></span>

| <span data-ttu-id="58f3f-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="58f3f-128">Method</span></span>  | <span data-ttu-id="58f3f-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="58f3f-129">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="58f3f-130">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="58f3f-130">**GET**</span></span> | <span data-ttu-id="58f3f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{ID_předplatného}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="58f3f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="58f3f-132">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="58f3f-132">URI parameters</span></span>

<span data-ttu-id="58f3f-133">Tato tabulka obsahuje seznam požadovaných parametrů dotazu k získání informací o hodnocených využitích zákazníka.</span><span class="sxs-lookup"><span data-stu-id="58f3f-133">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="58f3f-134">Název</span><span class="sxs-lookup"><span data-stu-id="58f3f-134">Name</span></span>                   | <span data-ttu-id="58f3f-135">Typ</span><span class="sxs-lookup"><span data-stu-id="58f3f-135">Type</span></span>     | <span data-ttu-id="58f3f-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="58f3f-136">Required</span></span> | <span data-ttu-id="58f3f-137">Popis</span><span class="sxs-lookup"><span data-stu-id="58f3f-137">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="58f3f-138">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="58f3f-138">**customer-tenant-id**</span></span> | <span data-ttu-id="58f3f-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="58f3f-139">**guid**</span></span> | <span data-ttu-id="58f3f-140">Y</span><span class="sxs-lookup"><span data-stu-id="58f3f-140">Y</span></span>        | <span data-ttu-id="58f3f-141">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="58f3f-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="58f3f-142">**id předplatného**</span><span class="sxs-lookup"><span data-stu-id="58f3f-142">**subscription-id**</span></span>    | <span data-ttu-id="58f3f-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="58f3f-143">**guid**</span></span> | <span data-ttu-id="58f3f-144">Y</span><span class="sxs-lookup"><span data-stu-id="58f3f-144">Y</span></span>        | <span data-ttu-id="58f3f-145">Identifikátor GUID odpovídající identifikátoru předplatného.</span><span class="sxs-lookup"><span data-stu-id="58f3f-145">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="58f3f-146">U plánu Azure je to identifikátor odpovídajícího prostředku předplatného [Partnerské centrum,](subscription-resources.md#subscription)který představuje plán Azure.</span><span class="sxs-lookup"><span data-stu-id="58f3f-146">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="58f3f-147">*V případě prostředků předplatného plánu Azure zadejte **id plánu** jako **ID předplatného** v této trase.*</span><span class="sxs-lookup"><span data-stu-id="58f3f-147">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="58f3f-148">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="58f3f-148">Request headers</span></span>

<span data-ttu-id="58f3f-149">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="58f3f-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="58f3f-150">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="58f3f-150">Request body</span></span>

<span data-ttu-id="58f3f-151">Žádné</span><span class="sxs-lookup"><span data-stu-id="58f3f-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="58f3f-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="58f3f-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="58f3f-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="58f3f-153">REST response</span></span>

<span data-ttu-id="58f3f-154">V případě úspěchu vrátí tato metoda v textu odpovědi prostředek **SubscriptionUsageSummary.**</span><span class="sxs-lookup"><span data-stu-id="58f3f-154">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="58f3f-155">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="58f3f-155">Response success and error codes</span></span>

<span data-ttu-id="58f3f-156">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="58f3f-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="58f3f-157">Ke čtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="58f3f-157">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="58f3f-158">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="58f3f-158">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="58f3f-159">Příklad odpovědi Microsoft Azure předplatných (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="58f3f-159">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="58f3f-160">V tomto příkladu zákazník zakoupil nabídku **azure payg 145P.**</span><span class="sxs-lookup"><span data-stu-id="58f3f-160">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="58f3f-161">*U zákazníků Microsoft Azure předplatných (MS-AZR-0145P) se v odpovědi rozhraní API nezmění.*</span><span class="sxs-lookup"><span data-stu-id="58f3f-161">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="58f3f-162">Příklad odpovědi REST pro plán Azure</span><span class="sxs-lookup"><span data-stu-id="58f3f-162">REST response example for Azure plan</span></span>

<span data-ttu-id="58f3f-163">V tomto příkladu zákazník zakoupil plán Azure.</span><span class="sxs-lookup"><span data-stu-id="58f3f-163">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="58f3f-164">*Pro zákazníky s plány Azure existují následující změny odpovědí rozhraní API:*</span><span class="sxs-lookup"><span data-stu-id="58f3f-164">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="58f3f-165">**currencyLocale** se nahradí **kódem měny**</span><span class="sxs-lookup"><span data-stu-id="58f3f-165">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="58f3f-166">**usdTotalCost** je nové pole</span><span class="sxs-lookup"><span data-stu-id="58f3f-166">**usdTotalCost** is a new field</span></span>

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
