---
title: Získání seznamu objednávek podle typu fakturačního cyklu a zákazníka
description: Získá kolekci prostředků objednávky pro zadaný typ zákazníka a fakturačního cyklu.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c52a556887dba065c4ccd1a82d6223624d0ad1f2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874223"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="676d6-103">Získání seznamu objednávek podle typu fakturačního cyklu a zákazníka</span><span class="sxs-lookup"><span data-stu-id="676d6-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="676d6-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="676d6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="676d6-105">Získá kolekci prostředků objednávky, které odpovídají danému typu zákazníka a fakturačního cyklu.</span><span class="sxs-lookup"><span data-stu-id="676d6-105">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="676d6-106">Mezi časem odeslání objednávky a jejím zobrazením v kolekci objednávek zákazníka dojde k prodlevě až 15 minut.</span><span class="sxs-lookup"><span data-stu-id="676d6-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="676d6-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="676d6-107">Prerequisites</span></span>

- <span data-ttu-id="676d6-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="676d6-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="676d6-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="676d6-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="676d6-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="676d6-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="676d6-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="676d6-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="676d6-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="676d6-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="676d6-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="676d6-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="676d6-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="676d6-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="676d6-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="676d6-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="676d6-116">C\#</span><span class="sxs-lookup"><span data-stu-id="676d6-116">C\#</span></span>

<span data-ttu-id="676d6-117">Získání kolekce objednávek zákazníka:</span><span class="sxs-lookup"><span data-stu-id="676d6-117">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="676d6-118">Použijte svou kolekci [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s vybraným ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="676d6-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="676d6-119">Zavolejte vlastnost [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a metodu **ByBillingCycleType ()** s vaším zadaným  [**BillingCycleType**](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="676d6-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="676d6-120">Zavolejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="676d6-120">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="676d6-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="676d6-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="676d6-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="676d6-122">Request syntax</span></span>

| <span data-ttu-id="676d6-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="676d6-123">Method</span></span>  | <span data-ttu-id="676d6-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="676d6-124">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="676d6-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="676d6-125">**GET**</span></span> | <span data-ttu-id="676d6-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders? billingType = {účtování-cyklus-typ} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="676d6-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="676d6-127">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="676d6-127">URI parameters</span></span>

<span data-ttu-id="676d6-128">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání kolekce objednávek podle ID zákazníka a typu fakturačního cyklu.</span><span class="sxs-lookup"><span data-stu-id="676d6-128">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="676d6-129">Název</span><span class="sxs-lookup"><span data-stu-id="676d6-129">Name</span></span>                   | <span data-ttu-id="676d6-130">Typ</span><span class="sxs-lookup"><span data-stu-id="676d6-130">Type</span></span>     | <span data-ttu-id="676d6-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="676d6-131">Required</span></span> | <span data-ttu-id="676d6-132">Popis</span><span class="sxs-lookup"><span data-stu-id="676d6-132">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="676d6-133">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="676d6-133">customer-tenant-id</span></span>     | <span data-ttu-id="676d6-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="676d6-134">string</span></span>   | <span data-ttu-id="676d6-135">Yes</span><span class="sxs-lookup"><span data-stu-id="676d6-135">Yes</span></span>      | <span data-ttu-id="676d6-136">Řetězec ve formátu GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="676d6-136">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="676d6-137">fakturace-cyklus – typ</span><span class="sxs-lookup"><span data-stu-id="676d6-137">billing-cycle-type</span></span>     | <span data-ttu-id="676d6-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="676d6-138">string</span></span>   | <span data-ttu-id="676d6-139">No</span><span class="sxs-lookup"><span data-stu-id="676d6-139">No</span></span>       | <span data-ttu-id="676d6-140">Řetězec odpovídající typu fakturačního cyklu.</span><span class="sxs-lookup"><span data-stu-id="676d6-140">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="676d6-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="676d6-141">Request headers</span></span>

<span data-ttu-id="676d6-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="676d6-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="676d6-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="676d6-143">Request body</span></span>

<span data-ttu-id="676d6-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="676d6-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="676d6-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="676d6-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="676d6-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="676d6-146">REST response</span></span>

<span data-ttu-id="676d6-147">V případě úspěchu tato metoda vrátí kolekci prostředků [Order](order-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="676d6-147">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="676d6-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="676d6-148">Response success and error codes</span></span>

<span data-ttu-id="676d6-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="676d6-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="676d6-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="676d6-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="676d6-151">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="676d6-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="676d6-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="676d6-152">Response example</span></span>

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
