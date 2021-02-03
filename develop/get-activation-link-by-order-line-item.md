---
title: Získání aktivačního odkazu podle položky řádku objednávky
description: Načte odkaz na aktivaci předplatného podle pořadí položek řádku.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c0e84888870571cf6bd21306f527863f2aa7ee85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766840"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="9921b-103">Získání aktivačního odkazu podle položky řádku objednávky</span><span class="sxs-lookup"><span data-stu-id="9921b-103">Get activation link by order line item</span></span>

<span data-ttu-id="9921b-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="9921b-104">**Applies To**</span></span>

- <span data-ttu-id="9921b-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="9921b-105">Partner Center</span></span>
- <span data-ttu-id="9921b-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="9921b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9921b-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="9921b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9921b-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9921b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9921b-109">Získá odkaz na aktivaci předplatného komerčního webu Marketplace číslem položky řádku objednávky.</span><span class="sxs-lookup"><span data-stu-id="9921b-109">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="9921b-110">Na řídicím panelu partnerského centra můžete tuto operaci provést výběrem **konkrétního předplatného** na **hlavní** stránce nebo výběrem odkazu **Přejít na web vydavatele** vedle předplatného, které chcete aktivovat na stránce **předplatná** .</span><span class="sxs-lookup"><span data-stu-id="9921b-110">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9921b-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9921b-111">Prerequisites</span></span>

- <span data-ttu-id="9921b-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9921b-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9921b-113">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="9921b-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9921b-114">Bylo dokončeno pořadí s produktem, který vyžaduje aktivaci.</span><span class="sxs-lookup"><span data-stu-id="9921b-114">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="9921b-115">C\#</span><span class="sxs-lookup"><span data-stu-id="9921b-115">C\#</span></span>

<span data-ttu-id="9921b-116">Chcete-li získat aktivační odkaz na řádkovou položku, použijte svou kolekci [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s vybraným ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9921b-116">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="9921b-117">Pak zavolejte vlastnost [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) se zadaným pořadím  [**ČísloObjednávky**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span><span class="sxs-lookup"><span data-stu-id="9921b-117">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="9921b-118">Pak zavolejte [**položky řádku**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) s metodou **ById ()** s identifikátorem položky řádku.</span><span class="sxs-lookup"><span data-stu-id="9921b-118">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="9921b-119">Nakonec zavolejte metodu **ActivationLinks ()** .</span><span class="sxs-lookup"><span data-stu-id="9921b-119">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="9921b-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="9921b-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9921b-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="9921b-121">Request syntax</span></span>

| <span data-ttu-id="9921b-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="9921b-122">Method</span></span>  | <span data-ttu-id="9921b-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9921b-123">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9921b-124">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="9921b-124">**GET**</span></span> | <span data-ttu-id="9921b-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Orders/{OrderID}/LineItems/{lineItemNumber}/activationlinks HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9921b-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9921b-126">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9921b-126">Request headers</span></span>

<span data-ttu-id="9921b-127">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9921b-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9921b-128">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9921b-128">Request body</span></span>

<span data-ttu-id="9921b-129">Žádné</span><span class="sxs-lookup"><span data-stu-id="9921b-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9921b-130">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9921b-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="9921b-131">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9921b-131">REST response</span></span>

<span data-ttu-id="9921b-132">V případě úspěchu tato metoda vrátí kolekci [zákaznických](customer-resources.md#customer) prostředků v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9921b-132">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9921b-133">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="9921b-133">Response success and error codes</span></span>

<span data-ttu-id="9921b-134">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9921b-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9921b-135">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="9921b-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9921b-136">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9921b-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9921b-137">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9921b-137">Response example</span></span>

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
