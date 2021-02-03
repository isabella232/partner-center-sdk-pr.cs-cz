---
title: Zrušení předplatného na komerčním marketplace
description: Naučte se používat rozhraní API partnerského centra ke zrušení předplatného komerčního tržiště, který odpovídá ID zákazníka a předplatného.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38708c17b31e39a5e7c436e0d76b4ebabbc3a801
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767110"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="62e81-103">Zrušení předplatného komerčního tržiště pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="62e81-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="62e81-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="62e81-104">**Applies to:**</span></span>

- <span data-ttu-id="62e81-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="62e81-105">Partner Center</span></span>

<span data-ttu-id="62e81-106">Tento článek popisuje, jak můžete pomocí rozhraní API partnerského centra zrušit komerční prostředek [předplatného](subscription-resources.md) Marketplace, který odpovídá ID zákazníka a předplatného.</span><span class="sxs-lookup"><span data-stu-id="62e81-106">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62e81-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="62e81-107">Prerequisites</span></span>

- <span data-ttu-id="62e81-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="62e81-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="62e81-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="62e81-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="62e81-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="62e81-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="62e81-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="62e81-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="62e81-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="62e81-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="62e81-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="62e81-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="62e81-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="62e81-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="62e81-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="62e81-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="62e81-116">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="62e81-116">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="62e81-117">Metoda řídicího panelu partnerského centra</span><span class="sxs-lookup"><span data-stu-id="62e81-117">Partner Center dashboard method</span></span>

<span data-ttu-id="62e81-118">Zrušení předplatného komerčního tržiště na řídicím panelu partnerského centra:</span><span class="sxs-lookup"><span data-stu-id="62e81-118">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="62e81-119">[Vyberte zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="62e81-119">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="62e81-120">Vyberte předplatné, které chcete zrušit.</span><span class="sxs-lookup"><span data-stu-id="62e81-120">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="62e81-121">Zvolte možnost **zrušit odběr** a pak vyberte **Odeslat**.</span><span class="sxs-lookup"><span data-stu-id="62e81-121">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="62e81-122">C\#</span><span class="sxs-lookup"><span data-stu-id="62e81-122">C\#</span></span>

<span data-ttu-id="62e81-123">Zrušení předplatného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="62e81-123">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="62e81-124">[Získá předplatné podle ID](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="62e81-124">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="62e81-125">Změňte vlastnost [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) odběru.</span><span class="sxs-lookup"><span data-stu-id="62e81-125">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="62e81-126">Informace o **stavových** kódech naleznete v tématu [SubscriptionStatus Enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="62e81-126">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="62e81-127">Po provedení změny použijte **`IAggregatePartner.Customers`** kolekci a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="62e81-127">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="62e81-128">Zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , za kterou následuje metoda [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="62e81-128">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="62e81-129">Zavolejte metodu **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="62e81-129">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="62e81-130">Ukázková aplikace pro testování konzoly</span><span class="sxs-lookup"><span data-stu-id="62e81-130">Sample console test app</span></span>

<span data-ttu-id="62e81-131">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="62e81-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="62e81-132">**Projekt**: PartnerSDK. FeatureSample **Třída**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="62e81-132">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="62e81-133">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="62e81-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="62e81-134">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="62e81-134">Request syntax</span></span>

| <span data-ttu-id="62e81-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="62e81-135">Method</span></span>    | <span data-ttu-id="62e81-136">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="62e81-136">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="62e81-137">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="62e81-137">**PATCH**</span></span> | <span data-ttu-id="62e81-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="62e81-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="62e81-139">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="62e81-139">URI parameter</span></span>

<span data-ttu-id="62e81-140">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro pozastavení předplatného.</span><span class="sxs-lookup"><span data-stu-id="62e81-140">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="62e81-141">Název</span><span class="sxs-lookup"><span data-stu-id="62e81-141">Name</span></span>                    | <span data-ttu-id="62e81-142">Typ</span><span class="sxs-lookup"><span data-stu-id="62e81-142">Type</span></span>     | <span data-ttu-id="62e81-143">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="62e81-143">Required</span></span> | <span data-ttu-id="62e81-144">Popis</span><span class="sxs-lookup"><span data-stu-id="62e81-144">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="62e81-145">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="62e81-145">**customer-tenant-id**</span></span>  | <span data-ttu-id="62e81-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="62e81-146">**guid**</span></span> | <span data-ttu-id="62e81-147">Y</span><span class="sxs-lookup"><span data-stu-id="62e81-147">Y</span></span>        | <span data-ttu-id="62e81-148">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="62e81-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="62e81-149">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="62e81-149">**id-for-subscription**</span></span> | <span data-ttu-id="62e81-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="62e81-150">**guid**</span></span> | <span data-ttu-id="62e81-151">Y</span><span class="sxs-lookup"><span data-stu-id="62e81-151">Y</span></span>        | <span data-ttu-id="62e81-152">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="62e81-152">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="62e81-153">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="62e81-153">Request headers</span></span>

<span data-ttu-id="62e81-154">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="62e81-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="62e81-155">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="62e81-155">Request body</span></span>

<span data-ttu-id="62e81-156">V těle žádosti se vyžaduje prostředek s úplným **předplatným** .</span><span class="sxs-lookup"><span data-stu-id="62e81-156">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="62e81-157">Ujistěte se, že se vlastnost **status** aktualizovala.</span><span class="sxs-lookup"><span data-stu-id="62e81-157">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="62e81-158">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="62e81-158">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="62e81-159">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="62e81-159">REST response</span></span>

<span data-ttu-id="62e81-160">V případě úspěchu vrátí tato metoda v těle odpovědi vlastnosti prostředku odstraněné [odběry](subscription-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="62e81-160">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="62e81-161">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="62e81-161">Response success and error codes</span></span>

<span data-ttu-id="62e81-162">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="62e81-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="62e81-163">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="62e81-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="62e81-164">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="62e81-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="62e81-165">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="62e81-165">Response example</span></span>

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
