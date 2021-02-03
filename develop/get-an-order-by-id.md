---
title: Získání objednávky podle ID
description: Získá zdroj objednávky, který odpovídá ID zákazníka a objednávky.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 0a39d7142e5bf97f9fb345416964d4ed6bb935ad
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767041"
---
# <a name="get-an-order-by-id"></a><span data-ttu-id="bd69f-103">Získání objednávky podle ID</span><span class="sxs-lookup"><span data-stu-id="bd69f-103">Get an order by ID</span></span>

<span data-ttu-id="bd69f-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="bd69f-104">**Applies to:**</span></span>

- <span data-ttu-id="bd69f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="bd69f-105">Partner Center</span></span>
- <span data-ttu-id="bd69f-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="bd69f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="bd69f-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="bd69f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="bd69f-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bd69f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bd69f-109">Získá zdroj [objednávky](order-resources.md) , který odpovídá ID zákazníka a objednávky.</span><span class="sxs-lookup"><span data-stu-id="bd69f-109">Gets an [Order](order-resources.md) resource that matches the customer and order ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd69f-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bd69f-110">Prerequisites</span></span>

- <span data-ttu-id="bd69f-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bd69f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bd69f-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="bd69f-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="bd69f-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bd69f-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="bd69f-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="bd69f-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="bd69f-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="bd69f-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="bd69f-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="bd69f-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="bd69f-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="bd69f-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="bd69f-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bd69f-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="bd69f-119">ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="bd69f-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="bd69f-120">C\#</span><span class="sxs-lookup"><span data-stu-id="bd69f-120">C\#</span></span>

<span data-ttu-id="bd69f-121">Postup získání objednávky zákazníka podle ID:</span><span class="sxs-lookup"><span data-stu-id="bd69f-121">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="bd69f-122">Použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="bd69f-122">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="bd69f-123">Zavolejte vlastnost [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) , za níž následuje metoda [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="bd69f-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.</span></span>
3. <span data-ttu-id="bd69f-124">Volejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span><span class="sxs-lookup"><span data-stu-id="bd69f-124">Call [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

<span data-ttu-id="bd69f-125">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bd69f-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bd69f-126">**Projekt**: PartnerSDK. FeatureSample **Třída**: GetOrder.cs</span><span class="sxs-lookup"><span data-stu-id="bd69f-126">**Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs</span></span>

## <a name="java"></a><span data-ttu-id="bd69f-127">Java</span><span class="sxs-lookup"><span data-stu-id="bd69f-127">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="bd69f-128">Postup získání objednávky zákazníka podle ID:</span><span class="sxs-lookup"><span data-stu-id="bd69f-128">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="bd69f-129">Použijte svou funkci **IAggregatePartner. GetCustomers** a zavolejte funkci **byId ()** .</span><span class="sxs-lookup"><span data-stu-id="bd69f-129">Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.</span></span>

2. <span data-ttu-id="bd69f-130">Zavolejte funkci **GetOrders** , následovanou funkcí **byID ()** .</span><span class="sxs-lookup"><span data-stu-id="bd69f-130">Call the **getOrders** function, followed by the **byID()** function once more.</span></span>
3. <span data-ttu-id="bd69f-131">Zavolejte funkci **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="bd69f-131">Call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a><span data-ttu-id="bd69f-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd69f-132">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="bd69f-133">Pokud chcete získat objednávku zákazníka podle ID, spusťte příkaz [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) a zadejte parametry **CustomerID** a **ČísloObjednávky** .</span><span class="sxs-lookup"><span data-stu-id="bd69f-133">To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** parameters.</span></span>

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a><span data-ttu-id="bd69f-134">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="bd69f-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bd69f-135">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="bd69f-135">Request syntax</span></span>

| <span data-ttu-id="bd69f-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="bd69f-136">Method</span></span>  | <span data-ttu-id="bd69f-137">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="bd69f-137">Request URI</span></span>                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bd69f-138">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="bd69f-138">**GET**</span></span> | <span data-ttu-id="bd69f-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{ID-for-Order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bd69f-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="bd69f-140">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="bd69f-140">URI parameters</span></span>

<span data-ttu-id="bd69f-141">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání objednávky podle ID.</span><span class="sxs-lookup"><span data-stu-id="bd69f-141">This table lists the required query parameters to get an order by ID.</span></span>

| <span data-ttu-id="bd69f-142">Název</span><span class="sxs-lookup"><span data-stu-id="bd69f-142">Name</span></span>                   | <span data-ttu-id="bd69f-143">Typ</span><span class="sxs-lookup"><span data-stu-id="bd69f-143">Type</span></span>     | <span data-ttu-id="bd69f-144">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="bd69f-144">Required</span></span> | <span data-ttu-id="bd69f-145">Popis</span><span class="sxs-lookup"><span data-stu-id="bd69f-145">Description</span></span>                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| <span data-ttu-id="bd69f-146">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="bd69f-146">customer-tenant-id</span></span>     | <span data-ttu-id="bd69f-147">řetězec</span><span class="sxs-lookup"><span data-stu-id="bd69f-147">string</span></span>   | <span data-ttu-id="bd69f-148">Yes</span><span class="sxs-lookup"><span data-stu-id="bd69f-148">Yes</span></span>      | <span data-ttu-id="bd69f-149">Řetězec ve formátu GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="bd69f-149">A GUID formatted string corresponding to the customer.</span></span> |
| <span data-ttu-id="bd69f-150">ID pro objednávku</span><span class="sxs-lookup"><span data-stu-id="bd69f-150">id-for-order</span></span>           | <span data-ttu-id="bd69f-151">řetězec</span><span class="sxs-lookup"><span data-stu-id="bd69f-151">string</span></span>   | <span data-ttu-id="bd69f-152">Yes</span><span class="sxs-lookup"><span data-stu-id="bd69f-152">Yes</span></span>      | <span data-ttu-id="bd69f-153">Řetězec odpovídající ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="bd69f-153">A string corresponding to the order ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="bd69f-154">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="bd69f-154">Request headers</span></span>

<span data-ttu-id="bd69f-155">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bd69f-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bd69f-156">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="bd69f-156">Request body</span></span>

<span data-ttu-id="bd69f-157">Žádné</span><span class="sxs-lookup"><span data-stu-id="bd69f-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bd69f-158">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bd69f-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="bd69f-159">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="bd69f-159">REST response</span></span>

<span data-ttu-id="bd69f-160">V případě úspěchu tato metoda vrátí prostředek [objednávky](order-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="bd69f-160">If successful, this method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bd69f-161">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="bd69f-161">Response success and error codes</span></span>

<span data-ttu-id="bd69f-162">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="bd69f-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bd69f-163">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="bd69f-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bd69f-164">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bd69f-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bd69f-165">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bd69f-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
