---
title: Zrušení předplatného na komerčním marketplace
description: Zjistěte, jak pomocí Partnerské centrum API zrušit prostředek předplatného komerčního marketplace, který odpovídá ID zákazníka a předplatného.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 95fa265a3c103d1ec55066f12a3ede7fdb2d0170
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974280"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="57267-103">Zrušení předplatného komerčního marketplace pomocí Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="57267-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="57267-104">Tento článek popisuje, jak můžete pomocí Partnerské centrum API zrušit prostředek předplatného komerčního [marketplace,](subscription-resources.md) který odpovídá ID zákazníka a předplatného.</span><span class="sxs-lookup"><span data-stu-id="57267-104">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57267-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="57267-105">Prerequisites</span></span>

- <span data-ttu-id="57267-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="57267-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="57267-107">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="57267-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="57267-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="57267-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="57267-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="57267-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="57267-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="57267-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="57267-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="57267-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="57267-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="57267-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="57267-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="57267-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="57267-114">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="57267-114">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="57267-115">Partnerské centrum řídicího panelu</span><span class="sxs-lookup"><span data-stu-id="57267-115">Partner Center dashboard method</span></span>

<span data-ttu-id="57267-116">Zrušení předplatného komerčního marketplace na řídicím panelu Partnerské centrum marketplace:</span><span class="sxs-lookup"><span data-stu-id="57267-116">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="57267-117">[Vyberte zákazníka.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="57267-117">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="57267-118">Vyberte předplatné, které chcete zrušit.</span><span class="sxs-lookup"><span data-stu-id="57267-118">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="57267-119">Zvolte možnost **Zrušit předplatné** a pak vyberte **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="57267-119">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="57267-120">C\#</span><span class="sxs-lookup"><span data-stu-id="57267-120">C\#</span></span>

<span data-ttu-id="57267-121">Zrušení předplatného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="57267-121">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="57267-122">[Získejte předplatné podle ID](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="57267-122">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="57267-123">Změňte vlastnost [**Status předplatného.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)</span><span class="sxs-lookup"><span data-stu-id="57267-123">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="57267-124">Informace o **stavových kódech** najdete v tématu [Výčet SubscriptionStatus.](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)</span><span class="sxs-lookup"><span data-stu-id="57267-124">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="57267-125">Po provedení změny použijte kolekci **`IAggregatePartner.Customers`** a zavolejte **metodu ById().**</span><span class="sxs-lookup"><span data-stu-id="57267-125">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="57267-126">Zavolejte [**vlastnost Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a pak [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="57267-126">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="57267-127">Zavolejte **metodu Patch().**</span><span class="sxs-lookup"><span data-stu-id="57267-127">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="57267-128">Ukázková testovací aplikace konzoly</span><span class="sxs-lookup"><span data-stu-id="57267-128">Sample console test app</span></span>

<span data-ttu-id="57267-129">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="57267-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="57267-130">**Project:** PartnerSDK.FeatureSample **– třída:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="57267-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="57267-131">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="57267-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="57267-132">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="57267-132">Request syntax</span></span>

| <span data-ttu-id="57267-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="57267-133">Method</span></span>    | <span data-ttu-id="57267-134">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="57267-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="57267-135">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="57267-135">**PATCH**</span></span> | <span data-ttu-id="57267-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{id-pro-předplatné} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="57267-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="57267-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="57267-137">URI parameter</span></span>

<span data-ttu-id="57267-138">Tato tabulka uvádí požadovaný parametr dotazu pro pozastavení odběru.</span><span class="sxs-lookup"><span data-stu-id="57267-138">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="57267-139">Název</span><span class="sxs-lookup"><span data-stu-id="57267-139">Name</span></span>                    | <span data-ttu-id="57267-140">Typ</span><span class="sxs-lookup"><span data-stu-id="57267-140">Type</span></span>     | <span data-ttu-id="57267-141">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="57267-141">Required</span></span> | <span data-ttu-id="57267-142">Popis</span><span class="sxs-lookup"><span data-stu-id="57267-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="57267-143">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="57267-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="57267-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="57267-144">**guid**</span></span> | <span data-ttu-id="57267-145">Y</span><span class="sxs-lookup"><span data-stu-id="57267-145">Y</span></span>        | <span data-ttu-id="57267-146">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="57267-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="57267-147">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="57267-147">**id-for-subscription**</span></span> | <span data-ttu-id="57267-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="57267-148">**guid**</span></span> | <span data-ttu-id="57267-149">Y</span><span class="sxs-lookup"><span data-stu-id="57267-149">Y</span></span>        | <span data-ttu-id="57267-150">Identifikátor GUID odpovídající předplatnému.</span><span class="sxs-lookup"><span data-stu-id="57267-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="57267-151">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="57267-151">Request headers</span></span>

<span data-ttu-id="57267-152">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="57267-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="57267-153">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="57267-153">Request body</span></span>

<span data-ttu-id="57267-154">V textu **požadavku** se vyžaduje úplný prostředek předplatného.</span><span class="sxs-lookup"><span data-stu-id="57267-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="57267-155">Ujistěte **se, že byla** aktualizována vlastnost Status.</span><span class="sxs-lookup"><span data-stu-id="57267-155">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="57267-156">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="57267-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [{
        "type": "Full",
        "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
    }],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "publisherName": "publisher Name",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {"objectType": "Subscription"},
}
```

## <a name="rest-response"></a><span data-ttu-id="57267-157">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="57267-157">REST response</span></span>

<span data-ttu-id="57267-158">V případě úspěchu tato [](subscription-resources.md) metoda vrátí v textu odpovědi odstraněné vlastnosti prostředku předplatného.</span><span class="sxs-lookup"><span data-stu-id="57267-158">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="57267-159">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="57267-159">Response success and error codes</span></span>

<span data-ttu-id="57267-160">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="57267-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="57267-161">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="57267-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="57267-162">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="57267-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="57267-163">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="57267-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1322
Content-Type: application/json; charset=utf-8
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
X-Locale: en-US

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [
        {
            "type": "Full",
            "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
        }
    ],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "links": {
        "product": {
            "uri": "/products/DZH318Z0BXWC?country=US",
            "method": "GET",
            "headers": []
        },
        "sku": {
            "uri": "/products/DZH318Z0BXWC/skus/0001?country=US",
            "method": "GET",
            "headers": []
        },
        "availability": {
            "uri": "/products/DZH318Z0BXWC/skus/0001/availabilities/DZH318Z0BMJX?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/5921f00a-32c0-4457-aaa1-e8018c650895/subscriptions/6e7aa601-629e-461b-8933-0898c3cc3c7c",
            "method": "GET",
            "headers": []
        }
    },
    "publisherName": "publishe rName",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {
        "etag": "",
        "objectType": "Subscription"
    }
}
```
