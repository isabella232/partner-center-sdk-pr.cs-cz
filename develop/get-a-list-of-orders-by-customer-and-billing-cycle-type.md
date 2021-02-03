---
title: Získání seznamu objednávek podle typu fakturačního cyklu a zákazníka
description: Získá kolekci prostředků objednávky pro zadaný typ zákazníka a fakturačního cyklu.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 43fe08b0791851f915e2b39a25394db5ffd022ca
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766930"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="cda7f-103">Získání seznamu objednávek podle typu fakturačního cyklu a zákazníka</span><span class="sxs-lookup"><span data-stu-id="cda7f-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="cda7f-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="cda7f-104">**Applies to:**</span></span>

- <span data-ttu-id="cda7f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="cda7f-105">Partner Center</span></span>
- <span data-ttu-id="cda7f-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="cda7f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cda7f-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="cda7f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cda7f-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cda7f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cda7f-109">Získá kolekci prostředků objednávky, které odpovídají danému typu zákazníka a fakturačního cyklu.</span><span class="sxs-lookup"><span data-stu-id="cda7f-109">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="cda7f-110">Mezi časem odeslání objednávky a jejím zobrazením v kolekci objednávek zákazníka dojde k prodlevě až 15 minut.</span><span class="sxs-lookup"><span data-stu-id="cda7f-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cda7f-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="cda7f-111">Prerequisites</span></span>

- <span data-ttu-id="cda7f-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cda7f-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cda7f-113">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="cda7f-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cda7f-114">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cda7f-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cda7f-115">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="cda7f-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cda7f-116">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="cda7f-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cda7f-117">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="cda7f-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cda7f-118">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="cda7f-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cda7f-119">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cda7f-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="cda7f-120">C\#</span><span class="sxs-lookup"><span data-stu-id="cda7f-120">C\#</span></span>

<span data-ttu-id="cda7f-121">Získání kolekce objednávek zákazníka:</span><span class="sxs-lookup"><span data-stu-id="cda7f-121">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="cda7f-122">Použijte svou kolekci [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s vybraným ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="cda7f-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="cda7f-123">Zavolejte vlastnost [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a metodu **ByBillingCycleType ()** s vaším zadaným  [**BillingCycleType**](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="cda7f-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="cda7f-124">Zavolejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="cda7f-124">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="cda7f-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="cda7f-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cda7f-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="cda7f-126">Request syntax</span></span>

| <span data-ttu-id="cda7f-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="cda7f-127">Method</span></span>  | <span data-ttu-id="cda7f-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="cda7f-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cda7f-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="cda7f-129">**GET**</span></span> | <span data-ttu-id="cda7f-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders? billingType = {účtování-cyklus-typ} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cda7f-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="cda7f-131">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="cda7f-131">URI parameters</span></span>

<span data-ttu-id="cda7f-132">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání kolekce objednávek podle ID zákazníka a typu fakturačního cyklu.</span><span class="sxs-lookup"><span data-stu-id="cda7f-132">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="cda7f-133">Název</span><span class="sxs-lookup"><span data-stu-id="cda7f-133">Name</span></span>                   | <span data-ttu-id="cda7f-134">Typ</span><span class="sxs-lookup"><span data-stu-id="cda7f-134">Type</span></span>     | <span data-ttu-id="cda7f-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="cda7f-135">Required</span></span> | <span data-ttu-id="cda7f-136">Popis</span><span class="sxs-lookup"><span data-stu-id="cda7f-136">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="cda7f-137">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="cda7f-137">customer-tenant-id</span></span>     | <span data-ttu-id="cda7f-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="cda7f-138">string</span></span>   | <span data-ttu-id="cda7f-139">Yes</span><span class="sxs-lookup"><span data-stu-id="cda7f-139">Yes</span></span>      | <span data-ttu-id="cda7f-140">Řetězec ve formátu GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="cda7f-140">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="cda7f-141">fakturace-cyklus – typ</span><span class="sxs-lookup"><span data-stu-id="cda7f-141">billing-cycle-type</span></span>     | <span data-ttu-id="cda7f-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="cda7f-142">string</span></span>   | <span data-ttu-id="cda7f-143">No</span><span class="sxs-lookup"><span data-stu-id="cda7f-143">No</span></span>       | <span data-ttu-id="cda7f-144">Řetězec odpovídající typu fakturačního cyklu.</span><span class="sxs-lookup"><span data-stu-id="cda7f-144">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="cda7f-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="cda7f-145">Request headers</span></span>

<span data-ttu-id="cda7f-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cda7f-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cda7f-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="cda7f-147">Request body</span></span>

<span data-ttu-id="cda7f-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="cda7f-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cda7f-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="cda7f-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="cda7f-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="cda7f-150">REST response</span></span>

<span data-ttu-id="cda7f-151">V případě úspěchu tato metoda vrátí kolekci prostředků [Order](order-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="cda7f-151">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cda7f-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="cda7f-152">Response success and error codes</span></span>

<span data-ttu-id="cda7f-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="cda7f-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cda7f-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="cda7f-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cda7f-155">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cda7f-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cda7f-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="cda7f-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 97fa8b4f-6576-4cd9-dd19-ac7c97a023a7
MS-RequestId: 3c6a034c-82ee-4095-d50f-9b530a415f1f
MS-CV: nb4/b3Yl2keY0eYR.0
MS-ServerId: 202010607
Date: Thu, 15 Mar 2018 20:44:40 GMT

{
    "totalCount": 2,
    "items": [
        {
            "id": "9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4B:000Z:DZH318Z0DSPL",
                    "friendlyName": "Reserved_VM_Instance_Standard_D1_AP_East_1_Year",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4B/skus/000Z?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T02:17:15.6455674Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Order"
            }
        },
        {
            "id": "s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4Z:002P:DZH318Z0CL2D",
                    "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_3_Years",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4Z/skus/002P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T01:42:36.8440279Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": { "objectType": "Order" }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType":
        "Collection"
    }
}
```
