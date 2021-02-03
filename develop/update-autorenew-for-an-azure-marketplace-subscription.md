---
title: Aktualizace automatického obnovení pro předplatné na komerčním marketplace
description: Aktualizujte vlastnost autorenew pro prostředek předplatného, který odpovídá ID zákazníka a předplatného.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dccec57901ea4ea429b74044e3b6c28178c43f6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766946"
---
# <a name="update-autorenew-for-a-commercial-marketplace-subscription"></a><span data-ttu-id="b1e47-103">Aktualizace automatického obnovení pro předplatné na komerčním marketplace</span><span class="sxs-lookup"><span data-stu-id="b1e47-103">Update autorenew for a commercial marketplace subscription</span></span>

<span data-ttu-id="b1e47-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="b1e47-104">**Applies To**</span></span>

- <span data-ttu-id="b1e47-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b1e47-105">Partner Center</span></span>

<span data-ttu-id="b1e47-106">Aktualizujte vlastnost autorenew pro zdroj [předplatného](subscription-resources.md) komerčního tržiště, který odpovídá ID zákazníka a předplatného.</span><span class="sxs-lookup"><span data-stu-id="b1e47-106">Update the autorenew property for a commercial marketplace [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

<span data-ttu-id="b1e47-107">Na řídicím panelu partnerského centra se tato operace provádí prvním [výběrem zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="b1e47-107">In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="b1e47-108">Pak vyberte předplatné, které chcete aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="b1e47-108">Then, select the subscription that you wish to update.</span></span> <span data-ttu-id="b1e47-109">Nakonec přepněte možnost **automatického obnovení** a pak vyberte **Odeslat**.</span><span class="sxs-lookup"><span data-stu-id="b1e47-109">Finally, toggle the **Auto-renew** option, then select **Submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1e47-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b1e47-110">Prerequisites</span></span>

- <span data-ttu-id="b1e47-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b1e47-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b1e47-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="b1e47-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b1e47-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b1e47-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b1e47-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b1e47-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b1e47-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b1e47-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b1e47-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b1e47-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b1e47-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b1e47-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b1e47-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b1e47-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b1e47-119">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="b1e47-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="b1e47-120">C\#</span><span class="sxs-lookup"><span data-stu-id="b1e47-120">C\#</span></span>

<span data-ttu-id="b1e47-121">Pokud chcete aktualizovat předplatné zákazníka, nejdřív [získejte předplatné](get-a-subscription-by-id.md)a pak nastavte vlastnost [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) tohoto předplatného.</span><span class="sxs-lookup"><span data-stu-id="b1e47-121">To update a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) property.</span></span> <span data-ttu-id="b1e47-122">Po provedení změny použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="b1e47-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="b1e47-123">Poté zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a potom metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="b1e47-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="b1e47-124">Potom dokončete voláním metody **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="b1e47-124">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

// turn off auto renew.
selectedSubscription.AutoRenewEnabled = false;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="b1e47-125">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1e47-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b1e47-126">**Projekt**: PartnerSDK. FeatureSample **Třída**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="b1e47-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b1e47-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b1e47-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b1e47-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b1e47-128">Request syntax</span></span>

| <span data-ttu-id="b1e47-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="b1e47-129">Method</span></span>    | <span data-ttu-id="b1e47-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b1e47-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b1e47-131">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="b1e47-131">**PATCH**</span></span> | <span data-ttu-id="b1e47-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b1e47-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b1e47-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b1e47-133">URI parameter</span></span>

<span data-ttu-id="b1e47-134">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro pozastavení předplatného.</span><span class="sxs-lookup"><span data-stu-id="b1e47-134">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="b1e47-135">Název</span><span class="sxs-lookup"><span data-stu-id="b1e47-135">Name</span></span>                    | <span data-ttu-id="b1e47-136">Typ</span><span class="sxs-lookup"><span data-stu-id="b1e47-136">Type</span></span>     | <span data-ttu-id="b1e47-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b1e47-137">Required</span></span> | <span data-ttu-id="b1e47-138">Popis</span><span class="sxs-lookup"><span data-stu-id="b1e47-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="b1e47-139">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="b1e47-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="b1e47-140">**HLAVNÍCH**</span><span class="sxs-lookup"><span data-stu-id="b1e47-140">**GUID**</span></span> | <span data-ttu-id="b1e47-141">Y</span><span class="sxs-lookup"><span data-stu-id="b1e47-141">Y</span></span>        | <span data-ttu-id="b1e47-142">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="b1e47-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="b1e47-143">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="b1e47-143">**id-for-subscription**</span></span> | <span data-ttu-id="b1e47-144">**HLAVNÍCH**</span><span class="sxs-lookup"><span data-stu-id="b1e47-144">**GUID**</span></span> | <span data-ttu-id="b1e47-145">Y</span><span class="sxs-lookup"><span data-stu-id="b1e47-145">Y</span></span>        | <span data-ttu-id="b1e47-146">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="b1e47-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b1e47-147">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b1e47-147">Request headers</span></span>

<span data-ttu-id="b1e47-148">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b1e47-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b1e47-149">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b1e47-149">Request body</span></span>

<span data-ttu-id="b1e47-150">V textu žádosti se vyžaduje kompletní prostředek **odběru** komerčního tržiště.</span><span class="sxs-lookup"><span data-stu-id="b1e47-150">A full commercial marketplace **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="b1e47-151">Ujistěte se, že se vlastnost **AutoRenewEnabled** aktualizovala.</span><span class="sxs-lookup"><span data-stu-id="b1e47-151">Ensure that the **AutoRenewEnabled** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="b1e47-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b1e47-152">Request example</span></span>

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
    "status": "active",
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

## <a name="rest-response"></a><span data-ttu-id="b1e47-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b1e47-153">REST response</span></span>

<span data-ttu-id="b1e47-154">V případě úspěchu tato metoda vrátí aktualizované vlastnosti prostředku [předplatného](subscription-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b1e47-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b1e47-155">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b1e47-155">Response success and error codes</span></span>

<span data-ttu-id="b1e47-156">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b1e47-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b1e47-157">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b1e47-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b1e47-158">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b1e47-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b1e47-159">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b1e47-159">Response example</span></span>

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
    "status": "active",
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
