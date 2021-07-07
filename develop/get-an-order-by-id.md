---
title: Získání objednávky podle ID
description: Získá zdroj objednávky, který odpovídá ID zákazníka a objednávky.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2cb2822935113fe1c5337b4ffc899fccff333d2f
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760177"
---
# <a name="get-an-order-by-id"></a><span data-ttu-id="60487-103">Získání objednávky podle ID</span><span class="sxs-lookup"><span data-stu-id="60487-103">Get an order by ID</span></span>

<span data-ttu-id="60487-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="60487-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="60487-105">Získá zdroj [objednávky](order-resources.md) , který odpovídá ID zákazníka a objednávky.</span><span class="sxs-lookup"><span data-stu-id="60487-105">Gets an [Order](order-resources.md) resource that matches the customer and order ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60487-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="60487-106">Prerequisites</span></span>

- <span data-ttu-id="60487-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="60487-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="60487-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="60487-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="60487-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="60487-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="60487-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="60487-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="60487-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="60487-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="60487-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="60487-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="60487-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="60487-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="60487-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="60487-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="60487-115">ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="60487-115">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="60487-116">C\#</span><span class="sxs-lookup"><span data-stu-id="60487-116">C\#</span></span>

<span data-ttu-id="60487-117">Postup získání objednávky zákazníka podle ID:</span><span class="sxs-lookup"><span data-stu-id="60487-117">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="60487-118">Použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="60487-118">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="60487-119">Zavolejte vlastnost [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) , za níž následuje metoda [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="60487-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.</span></span>
3. <span data-ttu-id="60487-120">Volejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span><span class="sxs-lookup"><span data-stu-id="60487-120">Call [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

<span data-ttu-id="60487-121">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="60487-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="60487-122">**Project**: PartnerSDK. FeatureSample **třída**: getorder. cs</span><span class="sxs-lookup"><span data-stu-id="60487-122">**Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs</span></span>

## <a name="java"></a><span data-ttu-id="60487-123">Java</span><span class="sxs-lookup"><span data-stu-id="60487-123">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="60487-124">Postup získání objednávky zákazníka podle ID:</span><span class="sxs-lookup"><span data-stu-id="60487-124">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="60487-125">Použijte svou funkci **IAggregatePartner. GetCustomers** a zavolejte funkci **byId ()** .</span><span class="sxs-lookup"><span data-stu-id="60487-125">Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.</span></span>

2. <span data-ttu-id="60487-126">Zavolejte funkci **GetOrders** , následovanou funkcí **byID ()** .</span><span class="sxs-lookup"><span data-stu-id="60487-126">Call the **getOrders** function, followed by the **byID()** function once more.</span></span>
3. <span data-ttu-id="60487-127">Zavolejte funkci **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="60487-127">Call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a><span data-ttu-id="60487-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60487-128">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="60487-129">Pokud chcete získat objednávku zákazníka podle ID, spusťte příkaz [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) a zadejte parametry **CustomerID** a **ČísloObjednávky** .</span><span class="sxs-lookup"><span data-stu-id="60487-129">To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** parameters.</span></span>

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a><span data-ttu-id="60487-130">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="60487-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="60487-131">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="60487-131">Request syntax</span></span>

| <span data-ttu-id="60487-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="60487-132">Method</span></span>  | <span data-ttu-id="60487-133">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="60487-133">Request URI</span></span>                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="60487-134">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="60487-134">**GET**</span></span> | <span data-ttu-id="60487-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{ID-for-Order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="60487-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="60487-136">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="60487-136">URI parameters</span></span>

<span data-ttu-id="60487-137">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání objednávky podle ID.</span><span class="sxs-lookup"><span data-stu-id="60487-137">This table lists the required query parameters to get an order by ID.</span></span>

| <span data-ttu-id="60487-138">Název</span><span class="sxs-lookup"><span data-stu-id="60487-138">Name</span></span>                   | <span data-ttu-id="60487-139">Typ</span><span class="sxs-lookup"><span data-stu-id="60487-139">Type</span></span>     | <span data-ttu-id="60487-140">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="60487-140">Required</span></span> | <span data-ttu-id="60487-141">Popis</span><span class="sxs-lookup"><span data-stu-id="60487-141">Description</span></span>                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| <span data-ttu-id="60487-142">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="60487-142">customer-tenant-id</span></span>     | <span data-ttu-id="60487-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="60487-143">string</span></span>   | <span data-ttu-id="60487-144">Yes</span><span class="sxs-lookup"><span data-stu-id="60487-144">Yes</span></span>      | <span data-ttu-id="60487-145">Řetězec ve formátu GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="60487-145">A GUID formatted string corresponding to the customer.</span></span> |
| <span data-ttu-id="60487-146">ID pro objednávku</span><span class="sxs-lookup"><span data-stu-id="60487-146">id-for-order</span></span>           | <span data-ttu-id="60487-147">řetězec</span><span class="sxs-lookup"><span data-stu-id="60487-147">string</span></span>   | <span data-ttu-id="60487-148">Yes</span><span class="sxs-lookup"><span data-stu-id="60487-148">Yes</span></span>      | <span data-ttu-id="60487-149">Řetězec odpovídající ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="60487-149">A string corresponding to the order ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="60487-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="60487-150">Request headers</span></span>

<span data-ttu-id="60487-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="60487-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="60487-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="60487-152">Request body</span></span>

<span data-ttu-id="60487-153">Žádné</span><span class="sxs-lookup"><span data-stu-id="60487-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="60487-154">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="60487-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="60487-155">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="60487-155">REST response</span></span>

<span data-ttu-id="60487-156">V případě úspěchu tato metoda vrátí prostředek [objednávky](order-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="60487-156">If successful, this method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="60487-157">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="60487-157">Response success and error codes</span></span>

<span data-ttu-id="60487-158">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="60487-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="60487-159">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="60487-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="60487-160">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="60487-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="60487-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="60487-161">Response example</span></span>

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
