---
title: Nákup doplňku k předplatnému
description: Jak zakoupit doplněk do stávajícího předplatného.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8b700a2ad41a37ca0ad745f3e7767449974b18a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547678"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="29714-103">Nákup doplňku k předplatnému</span><span class="sxs-lookup"><span data-stu-id="29714-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="29714-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="29714-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="29714-105">Jak zakoupit doplněk do stávajícího předplatného.</span><span class="sxs-lookup"><span data-stu-id="29714-105">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29714-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="29714-106">Prerequisites</span></span>

- <span data-ttu-id="29714-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="29714-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="29714-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="29714-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="29714-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="29714-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="29714-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="29714-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="29714-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="29714-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="29714-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="29714-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="29714-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="29714-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="29714-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="29714-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="29714-115">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="29714-115">A subscription ID.</span></span> <span data-ttu-id="29714-116">Toto je stávající předplatné, pro které se má koupit nabídka doplňku.</span><span class="sxs-lookup"><span data-stu-id="29714-116">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="29714-117">ID nabídky, která identifikuje nabídku doplňku k nákupu.</span><span class="sxs-lookup"><span data-stu-id="29714-117">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="29714-118">Nákup doplňku prostřednictvím kódu</span><span class="sxs-lookup"><span data-stu-id="29714-118">Purchasing an add-on through code</span></span>

<span data-ttu-id="29714-119">Při nákupu doplňku k předplatnému se aktualizuje původní pořadí předplatného s pořadím pro doplněk.</span><span class="sxs-lookup"><span data-stu-id="29714-119">When you purchase an add-on to a subscription, you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="29714-120">V následujícím seznamu je KódZákazníka ID zákazníka, subscriptionId je ID předplatného a addOnOfferId je ID nabídky pro doplněk.</span><span class="sxs-lookup"><span data-stu-id="29714-120">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="29714-121">Tady je postup:</span><span class="sxs-lookup"><span data-stu-id="29714-121">Here are the steps:</span></span>

1.  <span data-ttu-id="29714-122">Získejte rozhraní pro operace pro předplatné.</span><span class="sxs-lookup"><span data-stu-id="29714-122">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="29714-123">Pomocí tohoto rozhraní můžete vytvořit instanci objektu předplatného.</span><span class="sxs-lookup"><span data-stu-id="29714-123">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="29714-124">Tím získáte podrobnosti o nadřazeném předplatném, včetně ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="29714-124">This gets you the parent subscription details, including the order ID.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="29714-125">Vytvoří instanci objektu New [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) .</span><span class="sxs-lookup"><span data-stu-id="29714-125">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="29714-126">Tato instance objednávky se používá k aktualizaci původního pořadí používaného k zakoupení předplatného.</span><span class="sxs-lookup"><span data-stu-id="29714-126">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="29714-127">Přidejte do pořadí, který představuje doplněk, jednu položku s jedním řádkem.</span><span class="sxs-lookup"><span data-stu-id="29714-127">Add a single-line item to the order that represents the add-on.</span></span>
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  <span data-ttu-id="29714-128">Aktualizuje původní pořadí pro předplatné s novým pořadím pro doplněk.</span><span class="sxs-lookup"><span data-stu-id="29714-128">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="29714-129">C\#</span><span class="sxs-lookup"><span data-stu-id="29714-129">C\#</span></span>

<span data-ttu-id="29714-130">Chcete-li zakoupit doplněk, Začněte získáním rozhraní pro operace předplatného voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, který identifikuje zákazníka, a pomocí metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pro identifikaci předplatného, které obsahuje nabídku doplňku.</span><span class="sxs-lookup"><span data-stu-id="29714-130">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="29714-131">Použijte toto [**rozhraní**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) k načtení podrobností o předplatném voláním [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="29714-131">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="29714-132">Podrobnosti o předplatném obsahují ID objednávky pořadí předplatného, což je pořadí, v jakém se má doplněk aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="29714-132">The subscription details contain the order ID of the subscription order, which is the order to be updated with the add-on.</span></span>

<span data-ttu-id="29714-133">Dále vytvořte instanci objektu New [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) a naplňte ji jednou instancí [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) , která obsahuje informace pro identifikaci doplňku, jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="29714-133">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="29714-134">Pomocí tohoto nového objektu aktualizujete pořadí předplatného pomocí doplňku.</span><span class="sxs-lookup"><span data-stu-id="29714-134">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="29714-135">Nakonec zavolejte metodu [**patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) a aktualizujte pořadí předplatného, a to po prvním identifikaci zákazníka pomocí [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) a ORDER by Order [**. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span><span class="sxs-lookup"><span data-stu-id="29714-135">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

<span data-ttu-id="29714-136">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="29714-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="29714-137">**Project**: **třída** microsoft Partner SDK samples: AddSubscriptionAddOn. cs</span><span class="sxs-lookup"><span data-stu-id="29714-137">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="29714-138">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="29714-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="29714-139">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="29714-139">Request syntax</span></span>

| <span data-ttu-id="29714-140">Metoda</span><span class="sxs-lookup"><span data-stu-id="29714-140">Method</span></span>    | <span data-ttu-id="29714-141">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="29714-141">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="29714-142">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="29714-142">**PATCH**</span></span> | <span data-ttu-id="29714-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="29714-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="29714-144">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="29714-144">URI parameters</span></span>

<span data-ttu-id="29714-145">K identifikaci zákazníka a objednávky použijte následující parametry.</span><span class="sxs-lookup"><span data-stu-id="29714-145">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="29714-146">Název</span><span class="sxs-lookup"><span data-stu-id="29714-146">Name</span></span>                   | <span data-ttu-id="29714-147">Typ</span><span class="sxs-lookup"><span data-stu-id="29714-147">Type</span></span>     | <span data-ttu-id="29714-148">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="29714-148">Required</span></span> | <span data-ttu-id="29714-149">Popis</span><span class="sxs-lookup"><span data-stu-id="29714-149">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="29714-150">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="29714-150">**customer-tenant-id**</span></span> | <span data-ttu-id="29714-151">**guid**</span><span class="sxs-lookup"><span data-stu-id="29714-151">**guid**</span></span> | <span data-ttu-id="29714-152">Y</span><span class="sxs-lookup"><span data-stu-id="29714-152">Y</span></span>        | <span data-ttu-id="29714-153">Hodnota je identifikátor **zákazníka (zákazníka** ), který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="29714-153">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="29714-154">**ID objednávky**</span><span class="sxs-lookup"><span data-stu-id="29714-154">**order-id**</span></span>           | <span data-ttu-id="29714-155">**guid**</span><span class="sxs-lookup"><span data-stu-id="29714-155">**guid**</span></span> | <span data-ttu-id="29714-156">Y</span><span class="sxs-lookup"><span data-stu-id="29714-156">Y</span></span>        | <span data-ttu-id="29714-157">Identifikátor objednávky.</span><span class="sxs-lookup"><span data-stu-id="29714-157">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="29714-158">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="29714-158">Request headers</span></span>

<span data-ttu-id="29714-159">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="29714-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="29714-160">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="29714-160">Request body</span></span>

<span data-ttu-id="29714-161">V následujících tabulkách jsou popsány vlastnosti v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="29714-161">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="29714-162">Objednávka</span><span class="sxs-lookup"><span data-stu-id="29714-162">Order</span></span>

| <span data-ttu-id="29714-163">Název</span><span class="sxs-lookup"><span data-stu-id="29714-163">Name</span></span>                | <span data-ttu-id="29714-164">Typ</span><span class="sxs-lookup"><span data-stu-id="29714-164">Type</span></span>             | <span data-ttu-id="29714-165">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="29714-165">Required</span></span> | <span data-ttu-id="29714-166">Popis</span><span class="sxs-lookup"><span data-stu-id="29714-166">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="29714-167">Id</span><span class="sxs-lookup"><span data-stu-id="29714-167">Id</span></span>                  | <span data-ttu-id="29714-168">řetězec</span><span class="sxs-lookup"><span data-stu-id="29714-168">string</span></span>           | <span data-ttu-id="29714-169">N</span><span class="sxs-lookup"><span data-stu-id="29714-169">N</span></span>        | <span data-ttu-id="29714-170">ID objednávky</span><span class="sxs-lookup"><span data-stu-id="29714-170">The order ID.</span></span>                                        |
| <span data-ttu-id="29714-171">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="29714-171">ReferenceCustomerId</span></span> | <span data-ttu-id="29714-172">řetězec</span><span class="sxs-lookup"><span data-stu-id="29714-172">string</span></span>           | <span data-ttu-id="29714-173">Y</span><span class="sxs-lookup"><span data-stu-id="29714-173">Y</span></span>        | <span data-ttu-id="29714-174">ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="29714-174">The customer ID.</span></span>                                     |
| <span data-ttu-id="29714-175">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="29714-175">LineItems</span></span>           | <span data-ttu-id="29714-176">pole objektů</span><span class="sxs-lookup"><span data-stu-id="29714-176">array of objects</span></span> | <span data-ttu-id="29714-177">Y</span><span class="sxs-lookup"><span data-stu-id="29714-177">Y</span></span>        | <span data-ttu-id="29714-178">Pole objektů [OrderLineItem](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="29714-178">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="29714-179">CreationDate</span><span class="sxs-lookup"><span data-stu-id="29714-179">CreationDate</span></span>        | <span data-ttu-id="29714-180">řetězec</span><span class="sxs-lookup"><span data-stu-id="29714-180">string</span></span>           | <span data-ttu-id="29714-181">N</span><span class="sxs-lookup"><span data-stu-id="29714-181">N</span></span>        | <span data-ttu-id="29714-182">Datum vytvoření objednávky ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="29714-182">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="29714-183">Atributy</span><span class="sxs-lookup"><span data-stu-id="29714-183">Attributes</span></span>          | <span data-ttu-id="29714-184">object</span><span class="sxs-lookup"><span data-stu-id="29714-184">object</span></span>           | <span data-ttu-id="29714-185">N</span><span class="sxs-lookup"><span data-stu-id="29714-185">N</span></span>        | <span data-ttu-id="29714-186">Obsahuje "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="29714-186">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="29714-187">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="29714-187">OrderLineItem</span></span>

| <span data-ttu-id="29714-188">Název</span><span class="sxs-lookup"><span data-stu-id="29714-188">Name</span></span>                 | <span data-ttu-id="29714-189">Typ</span><span class="sxs-lookup"><span data-stu-id="29714-189">Type</span></span>   | <span data-ttu-id="29714-190">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="29714-190">Required</span></span> | <span data-ttu-id="29714-191">Popis</span><span class="sxs-lookup"><span data-stu-id="29714-191">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="29714-192">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="29714-192">LineItemNumber</span></span>       | <span data-ttu-id="29714-193">číslo</span><span class="sxs-lookup"><span data-stu-id="29714-193">number</span></span> | <span data-ttu-id="29714-194">Y</span><span class="sxs-lookup"><span data-stu-id="29714-194">Y</span></span>        | <span data-ttu-id="29714-195">Číslo položky řádku začínající na 0.</span><span class="sxs-lookup"><span data-stu-id="29714-195">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="29714-196">Hodnotami OfferId</span><span class="sxs-lookup"><span data-stu-id="29714-196">OfferId</span></span>              | <span data-ttu-id="29714-197">řetězec</span><span class="sxs-lookup"><span data-stu-id="29714-197">string</span></span> | <span data-ttu-id="29714-198">Y</span><span class="sxs-lookup"><span data-stu-id="29714-198">Y</span></span>        | <span data-ttu-id="29714-199">ID nabídky doplňku</span><span class="sxs-lookup"><span data-stu-id="29714-199">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="29714-200">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="29714-200">SubscriptionId</span></span>       | <span data-ttu-id="29714-201">řetězec</span><span class="sxs-lookup"><span data-stu-id="29714-201">string</span></span> | <span data-ttu-id="29714-202">N</span><span class="sxs-lookup"><span data-stu-id="29714-202">N</span></span>        | <span data-ttu-id="29714-203">ID zakoupeného předplatného doplňku.</span><span class="sxs-lookup"><span data-stu-id="29714-203">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="29714-204">ID nadřazeného odběru</span><span class="sxs-lookup"><span data-stu-id="29714-204">ParentSubscriptionId</span></span> | <span data-ttu-id="29714-205">řetězec</span><span class="sxs-lookup"><span data-stu-id="29714-205">string</span></span> | <span data-ttu-id="29714-206">Y</span><span class="sxs-lookup"><span data-stu-id="29714-206">Y</span></span>        | <span data-ttu-id="29714-207">ID nadřazeného předplatného, které má nabídku doplňku.</span><span class="sxs-lookup"><span data-stu-id="29714-207">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="29714-208">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="29714-208">FriendlyName</span></span>         | <span data-ttu-id="29714-209">řetězec</span><span class="sxs-lookup"><span data-stu-id="29714-209">string</span></span> | <span data-ttu-id="29714-210">N</span><span class="sxs-lookup"><span data-stu-id="29714-210">N</span></span>        | <span data-ttu-id="29714-211">Popisný název této řádkové položky.</span><span class="sxs-lookup"><span data-stu-id="29714-211">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="29714-212">Množství</span><span class="sxs-lookup"><span data-stu-id="29714-212">Quantity</span></span>             | <span data-ttu-id="29714-213">číslo</span><span class="sxs-lookup"><span data-stu-id="29714-213">number</span></span> | <span data-ttu-id="29714-214">Y</span><span class="sxs-lookup"><span data-stu-id="29714-214">Y</span></span>        | <span data-ttu-id="29714-215">Počet licencí</span><span class="sxs-lookup"><span data-stu-id="29714-215">The number of licenses.</span></span>                                      |
| <span data-ttu-id="29714-216">Id partneraZáznam</span><span class="sxs-lookup"><span data-stu-id="29714-216">PartnerIdOnRecord</span></span>    | <span data-ttu-id="29714-217">řetězec</span><span class="sxs-lookup"><span data-stu-id="29714-217">string</span></span> | <span data-ttu-id="29714-218">N</span><span class="sxs-lookup"><span data-stu-id="29714-218">N</span></span>        | <span data-ttu-id="29714-219">ID MPN záznamu partnera.</span><span class="sxs-lookup"><span data-stu-id="29714-219">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="29714-220">Atributy</span><span class="sxs-lookup"><span data-stu-id="29714-220">Attributes</span></span>           | <span data-ttu-id="29714-221">object</span><span class="sxs-lookup"><span data-stu-id="29714-221">object</span></span> | <span data-ttu-id="29714-222">N</span><span class="sxs-lookup"><span data-stu-id="29714-222">N</span></span>        | <span data-ttu-id="29714-223">Obsahuje "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="29714-223">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="29714-224">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="29714-224">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="29714-225">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="29714-225">REST response</span></span>

<span data-ttu-id="29714-226">V případě úspěchu vrátí tato metoda v textu odpovědi aktualizované pořadí odběru.</span><span class="sxs-lookup"><span data-stu-id="29714-226">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="29714-227">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="29714-227">Response success and error codes</span></span>

<span data-ttu-id="29714-228">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="29714-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="29714-229">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="29714-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="29714-230">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="29714-230">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="29714-231">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="29714-231">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```
