---
title: Získání všech objednávek zákazníka
description: Získá kolekci všech objednávek pro zadaného zákazníka.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e8f23e90cbb5afb45e519e2c58fd0d3b9ea2de6a
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760296"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="2f3f8-103">Získání všech objednávek zákazníka</span><span class="sxs-lookup"><span data-stu-id="2f3f8-103">Get all of a customer's orders</span></span>

<span data-ttu-id="2f3f8-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2f3f8-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2f3f8-105">Získá kolekci všech objednávek pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-105">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="2f3f8-106">Mezi časem, kdy je objednávka odeslána a kdy se objeví v kolekci objednávek zákazníka, je zpoždění až 15 minut.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f3f8-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2f3f8-107">Prerequisites</span></span>

- <span data-ttu-id="2f3f8-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2f3f8-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2f3f8-109">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2f3f8-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2f3f8-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2f3f8-111">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2f3f8-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2f3f8-112">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="2f3f8-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2f3f8-113">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="2f3f8-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2f3f8-114">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2f3f8-115">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2f3f8-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2f3f8-116">C\#</span><span class="sxs-lookup"><span data-stu-id="2f3f8-116">C\#</span></span>

<span data-ttu-id="2f3f8-117">Získání kolekce všech objednávek zákazníka:</span><span class="sxs-lookup"><span data-stu-id="2f3f8-117">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="2f3f8-118">Použijte kolekci [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="2f3f8-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="2f3f8-119">Zavolejte [**vlastnost Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a pak metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="2f3f8-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="2f3f8-120">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2f3f8-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2f3f8-121">**Project:** PartnerSDK.FeatureSamples **– třída:** GetOrders.cs</span><span class="sxs-lookup"><span data-stu-id="2f3f8-121">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2f3f8-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="2f3f8-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2f3f8-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="2f3f8-123">Request syntax</span></span>

| <span data-ttu-id="2f3f8-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="2f3f8-124">Method</span></span>  | <span data-ttu-id="2f3f8-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2f3f8-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2f3f8-126">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="2f3f8-126">**GET**</span></span> | <span data-ttu-id="2f3f8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2f3f8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="2f3f8-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2f3f8-128">URI parameter</span></span>

<span data-ttu-id="2f3f8-129">K získání všech objednávek použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-129">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="2f3f8-130">Název</span><span class="sxs-lookup"><span data-stu-id="2f3f8-130">Name</span></span>                   | <span data-ttu-id="2f3f8-131">Typ</span><span class="sxs-lookup"><span data-stu-id="2f3f8-131">Type</span></span>     | <span data-ttu-id="2f3f8-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="2f3f8-132">Required</span></span> | <span data-ttu-id="2f3f8-133">Popis</span><span class="sxs-lookup"><span data-stu-id="2f3f8-133">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="2f3f8-134">customer-tenant-id</span><span class="sxs-lookup"><span data-stu-id="2f3f8-134">customer-tenant-id</span></span>     | <span data-ttu-id="2f3f8-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="2f3f8-135">string</span></span>   | <span data-ttu-id="2f3f8-136">Yes</span><span class="sxs-lookup"><span data-stu-id="2f3f8-136">Yes</span></span>      | <span data-ttu-id="2f3f8-137">Řetězec ve formátu GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-137">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="2f3f8-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2f3f8-138">Request headers</span></span>

<span data-ttu-id="2f3f8-139">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2f3f8-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2f3f8-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2f3f8-140">Request body</span></span>

<span data-ttu-id="2f3f8-141">Žádné</span><span class="sxs-lookup"><span data-stu-id="2f3f8-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2f3f8-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="2f3f8-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="2f3f8-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2f3f8-143">REST response</span></span>

<span data-ttu-id="2f3f8-144">V případě úspěchu tato metoda vrátí kolekci [prostředků Order](order-resources.md) v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-144">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2f3f8-145">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="2f3f8-145">Response success and error codes</span></span>

<span data-ttu-id="2f3f8-146">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2f3f8-147">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="2f3f8-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2f3f8-148">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2f3f8-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2f3f8-149">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="2f3f8-149">Response example</span></span>

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
