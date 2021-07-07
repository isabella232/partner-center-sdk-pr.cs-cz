---
title: Získání aktivačního odkazu podle položky řádku objednávky
description: Získá odkaz na aktivaci předplatného podle řádkové položky objednávky.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: aa02a5a5b4a281b96e32ee6d239cc440cf8af4ec
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760772"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="5dd02-103">Získání aktivačního odkazu podle položky řádku objednávky</span><span class="sxs-lookup"><span data-stu-id="5dd02-103">Get activation link by order line item</span></span>

<span data-ttu-id="5dd02-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5dd02-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5dd02-105">Získá odkaz na aktivaci předplatného komerčního marketplace podle čísla položky řádku objednávky.</span><span class="sxs-lookup"><span data-stu-id="5dd02-105">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="5dd02-106">Na řídicím panelu Partnerské centrum můžete tuto operaci provést  výběrem  konkrétního předplatného v části Předplatné na hlavní stránce nebo výběrem odkazu Přejít na web **Publisher** vedle předplatného aktivovat na stránce Předplatná. </span><span class="sxs-lookup"><span data-stu-id="5dd02-106">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5dd02-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5dd02-107">Prerequisites</span></span>

- <span data-ttu-id="5dd02-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5dd02-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5dd02-109">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="5dd02-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5dd02-110">Dokončená objednávka s produktem, který vyžaduje aktivaci.</span><span class="sxs-lookup"><span data-stu-id="5dd02-110">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="5dd02-111">C\#</span><span class="sxs-lookup"><span data-stu-id="5dd02-111">C\#</span></span>

<span data-ttu-id="5dd02-112">Pokud chcete získat aktivační odkaz na řádkové položky, použijte kolekci [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s vybraným ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5dd02-112">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="5dd02-113">Potom zavolejte [**vlastnost Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a [**metodu ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) se zadaným  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span><span class="sxs-lookup"><span data-stu-id="5dd02-113">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="5dd02-114">Potom zavolejte [**metodu LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) s **byId()** s identifikátorem čísla položky řádku.</span><span class="sxs-lookup"><span data-stu-id="5dd02-114">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="5dd02-115">Nakonec zavolejte **metodu ActivationLinks().**</span><span class="sxs-lookup"><span data-stu-id="5dd02-115">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="5dd02-116">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="5dd02-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5dd02-117">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="5dd02-117">Request syntax</span></span>

| <span data-ttu-id="5dd02-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="5dd02-118">Method</span></span>  | <span data-ttu-id="5dd02-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5dd02-119">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5dd02-120">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="5dd02-120">**GET**</span></span> | <span data-ttu-id="5dd02-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5dd02-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5dd02-122">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5dd02-122">Request headers</span></span>

<span data-ttu-id="5dd02-123">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5dd02-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5dd02-124">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="5dd02-124">Request body</span></span>

<span data-ttu-id="5dd02-125">Žádné</span><span class="sxs-lookup"><span data-stu-id="5dd02-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5dd02-126">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="5dd02-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="5dd02-127">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5dd02-127">REST response</span></span>

<span data-ttu-id="5dd02-128">V případě úspěchu vrátí tato [](customer-resources.md#customer) metoda v textu odpovědi kolekci prostředků zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5dd02-128">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5dd02-129">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="5dd02-129">Response success and error codes</span></span>

<span data-ttu-id="5dd02-130">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5dd02-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5dd02-131">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="5dd02-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5dd02-132">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5dd02-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5dd02-133">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="5dd02-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
