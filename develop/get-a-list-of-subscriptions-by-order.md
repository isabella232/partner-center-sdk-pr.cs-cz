---
title: Získání seznamu předplatných podle objednávky
description: Získá kolekci prostředků předplatného, které odpovídají danému pořadí.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 011a92500d0c7ed44f86030febd1ea83be2c6474
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873951"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="3edf7-103">Získání seznamu předplatných podle objednávky</span><span class="sxs-lookup"><span data-stu-id="3edf7-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="3edf7-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3edf7-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3edf7-105">Získá kolekci prostředků [předplatného,](subscription-resources.md) které odpovídají danému pořadí.</span><span class="sxs-lookup"><span data-stu-id="3edf7-105">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3edf7-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3edf7-106">Prerequisites</span></span>

- <span data-ttu-id="3edf7-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3edf7-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3edf7-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="3edf7-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3edf7-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3edf7-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3edf7-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="3edf7-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3edf7-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="3edf7-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3edf7-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="3edf7-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3edf7-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3edf7-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3edf7-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3edf7-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3edf7-115">ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="3edf7-115">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="3edf7-116">C\#</span><span class="sxs-lookup"><span data-stu-id="3edf7-116">C\#</span></span>

<span data-ttu-id="3edf7-117">Pokud chcete získat seznam předplatných podle objednávky, použijte kolekci **IAggregatePartner.Customers** a zavolejte **metodu ById().**</span><span class="sxs-lookup"><span data-stu-id="3edf7-117">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="3edf7-118">Potom zavolejte [**vlastnost Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a pak **metodu ByOrder().**</span><span class="sxs-lookup"><span data-stu-id="3edf7-118">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="3edf7-119">Dokončete [**voláním metody Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync)</span><span class="sxs-lookup"><span data-stu-id="3edf7-119">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="3edf7-120">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3edf7-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3edf7-121">**Project:** PartnerSDK.FeatureSample **– třída:** SubscriptionsByOrder.cs</span><span class="sxs-lookup"><span data-stu-id="3edf7-121">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3edf7-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="3edf7-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3edf7-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="3edf7-123">Request syntax</span></span>

| <span data-ttu-id="3edf7-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="3edf7-124">Method</span></span>  | <span data-ttu-id="3edf7-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3edf7-125">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3edf7-126">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="3edf7-126">**GET**</span></span> | <span data-ttu-id="3edf7-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions?order \_ id={id-for-order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3edf7-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3edf7-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="3edf7-128">URI parameter</span></span>

<span data-ttu-id="3edf7-129">Tato tabulka uvádí požadovaný parametr dotazu pro získání všech předplatných.</span><span class="sxs-lookup"><span data-stu-id="3edf7-129">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="3edf7-130">Název</span><span class="sxs-lookup"><span data-stu-id="3edf7-130">Name</span></span>                   | <span data-ttu-id="3edf7-131">Typ</span><span class="sxs-lookup"><span data-stu-id="3edf7-131">Type</span></span>     | <span data-ttu-id="3edf7-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3edf7-132">Required</span></span> | <span data-ttu-id="3edf7-133">Popis</span><span class="sxs-lookup"><span data-stu-id="3edf7-133">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="3edf7-134">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="3edf7-134">**customer-tenant-id**</span></span> | <span data-ttu-id="3edf7-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="3edf7-135">**guid**</span></span> | <span data-ttu-id="3edf7-136">Y</span><span class="sxs-lookup"><span data-stu-id="3edf7-136">Y</span></span>        | <span data-ttu-id="3edf7-137">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="3edf7-137">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="3edf7-138">**id-for-order**</span><span class="sxs-lookup"><span data-stu-id="3edf7-138">**id-for-order**</span></span>       | <span data-ttu-id="3edf7-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="3edf7-139">**guid**</span></span> | <span data-ttu-id="3edf7-140">Y</span><span class="sxs-lookup"><span data-stu-id="3edf7-140">Y</span></span>        | <span data-ttu-id="3edf7-141">Identifikátor GUID odpovídající objednávce.</span><span class="sxs-lookup"><span data-stu-id="3edf7-141">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="3edf7-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="3edf7-142">Request headers</span></span>

<span data-ttu-id="3edf7-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3edf7-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3edf7-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="3edf7-144">Request body</span></span>

<span data-ttu-id="3edf7-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="3edf7-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3edf7-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="3edf7-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="3edf7-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3edf7-147">REST response</span></span>

<span data-ttu-id="3edf7-148">V případě úspěchu tato metoda vrátí kolekci [prostředků předplatného](subscription-resources.md) v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="3edf7-148">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3edf7-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="3edf7-149">Response success and error codes</span></span>

<span data-ttu-id="3edf7-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="3edf7-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3edf7-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="3edf7-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3edf7-152">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3edf7-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3edf7-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="3edf7-153">Response example</span></span>

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
