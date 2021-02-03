---
title: Získání seznamu předplatných podle objednávky
description: Získá kolekci prostředků předplatného, které odpovídají danému pořadí.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 56b9c80021cace03976d410b2a6cd4c0eee18398
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766935"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="d0056-103">Získání seznamu předplatných podle objednávky</span><span class="sxs-lookup"><span data-stu-id="d0056-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="d0056-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="d0056-104">**Applies To**</span></span>

- <span data-ttu-id="d0056-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d0056-105">Partner Center</span></span>
- <span data-ttu-id="d0056-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d0056-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d0056-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="d0056-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d0056-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d0056-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d0056-109">Získá kolekci prostředků [předplatného](subscription-resources.md) , které odpovídají danému pořadí.</span><span class="sxs-lookup"><span data-stu-id="d0056-109">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0056-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d0056-110">Prerequisites</span></span>

- <span data-ttu-id="d0056-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d0056-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d0056-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="d0056-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d0056-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d0056-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d0056-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="d0056-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d0056-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="d0056-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d0056-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="d0056-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d0056-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="d0056-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d0056-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d0056-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d0056-119">ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="d0056-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="d0056-120">C\#</span><span class="sxs-lookup"><span data-stu-id="d0056-120">C\#</span></span>

<span data-ttu-id="d0056-121">Chcete-li získat seznam předplatných podle pořadí, použijte svoji **IAggregatePartner. Customers** Collection a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="d0056-121">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="d0056-122">Poté zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a potom metodu **ByOrder ()** .</span><span class="sxs-lookup"><span data-stu-id="d0056-122">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="d0056-123">Dokončete voláním metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span><span class="sxs-lookup"><span data-stu-id="d0056-123">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="d0056-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d0056-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d0056-125">**Projekt**: PartnerSDK. FeatureSample **Třída**: SubscriptionsByOrder.cs</span><span class="sxs-lookup"><span data-stu-id="d0056-125">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d0056-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d0056-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d0056-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d0056-127">Request syntax</span></span>

| <span data-ttu-id="d0056-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="d0056-128">Method</span></span>  | <span data-ttu-id="d0056-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d0056-129">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d0056-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="d0056-130">**GET**</span></span> | <span data-ttu-id="d0056-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions? \_ ID objednávky = {ID pro objednávku} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d0056-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d0056-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d0056-132">URI parameter</span></span>

<span data-ttu-id="d0056-133">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech předplatných.</span><span class="sxs-lookup"><span data-stu-id="d0056-133">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="d0056-134">Název</span><span class="sxs-lookup"><span data-stu-id="d0056-134">Name</span></span>                   | <span data-ttu-id="d0056-135">Typ</span><span class="sxs-lookup"><span data-stu-id="d0056-135">Type</span></span>     | <span data-ttu-id="d0056-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d0056-136">Required</span></span> | <span data-ttu-id="d0056-137">Popis</span><span class="sxs-lookup"><span data-stu-id="d0056-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="d0056-138">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="d0056-138">**customer-tenant-id**</span></span> | <span data-ttu-id="d0056-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="d0056-139">**guid**</span></span> | <span data-ttu-id="d0056-140">Y</span><span class="sxs-lookup"><span data-stu-id="d0056-140">Y</span></span>        | <span data-ttu-id="d0056-141">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="d0056-141">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="d0056-142">**ID pro objednávku**</span><span class="sxs-lookup"><span data-stu-id="d0056-142">**id-for-order**</span></span>       | <span data-ttu-id="d0056-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="d0056-143">**guid**</span></span> | <span data-ttu-id="d0056-144">Y</span><span class="sxs-lookup"><span data-stu-id="d0056-144">Y</span></span>        | <span data-ttu-id="d0056-145">Identifikátor GUID odpovídající objednávce.</span><span class="sxs-lookup"><span data-stu-id="d0056-145">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="d0056-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d0056-146">Request headers</span></span>

<span data-ttu-id="d0056-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d0056-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d0056-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d0056-148">Request body</span></span>

<span data-ttu-id="d0056-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="d0056-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d0056-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d0056-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="d0056-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d0056-151">REST response</span></span>

<span data-ttu-id="d0056-152">V případě úspěchu tato metoda vrátí kolekci prostředků [předplatného](subscription-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="d0056-152">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d0056-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d0056-153">Response success and error codes</span></span>

<span data-ttu-id="d0056-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d0056-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d0056-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d0056-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d0056-156">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d0056-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d0056-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d0056-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 25 Nov 2015 05:50:45 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "Myofferpurchase",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "{id-for-order}",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
