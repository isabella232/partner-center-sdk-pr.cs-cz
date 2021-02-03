---
title: Získání všech objednávek zákazníka
description: Získá kolekci všech objednávek pro zadaného zákazníka.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4d71cd138421704d94a55a9fe21e074d92638815
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766993"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="68882-103">Získání všech objednávek zákazníka</span><span class="sxs-lookup"><span data-stu-id="68882-103">Get all of a customer's orders</span></span>

<span data-ttu-id="68882-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="68882-104">**Applies to:**</span></span>

- <span data-ttu-id="68882-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="68882-105">Partner Center</span></span>
- <span data-ttu-id="68882-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="68882-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="68882-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="68882-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="68882-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="68882-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="68882-109">Získá kolekci všech objednávek pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="68882-109">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="68882-110">Mezi časem odeslání objednávky a jejím zobrazením v kolekci objednávek zákazníka dojde k prodlevě až 15 minut.</span><span class="sxs-lookup"><span data-stu-id="68882-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68882-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="68882-111">Prerequisites</span></span>

- <span data-ttu-id="68882-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="68882-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="68882-113">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="68882-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="68882-114">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="68882-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="68882-115">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="68882-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="68882-116">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="68882-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="68882-117">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="68882-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="68882-118">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="68882-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="68882-119">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="68882-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="68882-120">C\#</span><span class="sxs-lookup"><span data-stu-id="68882-120">C\#</span></span>

<span data-ttu-id="68882-121">Získání kolekce všech objednávek zákazníka:</span><span class="sxs-lookup"><span data-stu-id="68882-121">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="68882-122">Použijte svou kolekci [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="68882-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="68882-123">Zavolejte vlastnost [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) , následovanou metodami [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="68882-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="68882-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="68882-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="68882-125">**Projekt**: PartnerSDK. FeatureSamples **Třída**: GetOrders.cs</span><span class="sxs-lookup"><span data-stu-id="68882-125">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="68882-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="68882-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="68882-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="68882-127">Request syntax</span></span>

| <span data-ttu-id="68882-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="68882-128">Method</span></span>  | <span data-ttu-id="68882-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="68882-129">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="68882-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="68882-130">**GET**</span></span> | <span data-ttu-id="68882-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="68882-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="68882-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="68882-132">URI parameter</span></span>

<span data-ttu-id="68882-133">K získání všech objednávek použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="68882-133">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="68882-134">Název</span><span class="sxs-lookup"><span data-stu-id="68882-134">Name</span></span>                   | <span data-ttu-id="68882-135">Typ</span><span class="sxs-lookup"><span data-stu-id="68882-135">Type</span></span>     | <span data-ttu-id="68882-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="68882-136">Required</span></span> | <span data-ttu-id="68882-137">Popis</span><span class="sxs-lookup"><span data-stu-id="68882-137">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="68882-138">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="68882-138">customer-tenant-id</span></span>     | <span data-ttu-id="68882-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="68882-139">string</span></span>   | <span data-ttu-id="68882-140">Yes</span><span class="sxs-lookup"><span data-stu-id="68882-140">Yes</span></span>      | <span data-ttu-id="68882-141">Řetězec ve formátu GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="68882-141">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="68882-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="68882-142">Request headers</span></span>

<span data-ttu-id="68882-143">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="68882-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="68882-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="68882-144">Request body</span></span>

<span data-ttu-id="68882-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="68882-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="68882-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="68882-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="68882-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="68882-147">REST response</span></span>

<span data-ttu-id="68882-148">V případě úspěchu tato metoda vrátí kolekci prostředků [Order](order-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="68882-148">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="68882-149">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="68882-149">Response success and error codes</span></span>

<span data-ttu-id="68882-150">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="68882-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="68882-151">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="68882-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="68882-152">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="68882-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="68882-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="68882-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
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
            "id": "eeba9d00-7b46-443a-917e-22887a8fc993",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "E59159FC-6F67-4599-B3CB-17FF4020F643",
                    "subscriptionId": "DB8C695B-1C3C-4C55-B697-771503DD46BF",
                    "friendlyName": "Azure Active Directory Premium P2",
                    "quantity": 1,
                    "links": {
                        "subscription": {
                            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/84A661C4-E949-4BD2-A560-ED7766FCAF2B/skus/E59159FC-6F67-4599-B3CB-17FF4020F643",
                            "method": "GET",
                            "headers": []
                        },
                        "provisioningStatus": {
                            "uri": "/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF/provisioningstatus",
                            "method": "GET",
                            "headers": []
                        }
                    }
            ],
            "creationDate": "2018-03-06T17:37:05.253-08:00",
            "status": "completed",
            "links": {
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/eeba9d00-7b46-443a-917e-22887a8fc993",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "etag": "eyJpZCI6ImVlYmE5ZDAwLTdiNDYtNDQzYS05MTdlLTIyODg3YThmYzk5MyIsInZlcnNpb24iOjF9",
                "objectType": "Order"
            }
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
         "objectType": "Collection"
    }
}
```
