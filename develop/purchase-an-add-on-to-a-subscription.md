---
title: Nákup doplňku k předplatnému
description: Jak zakoupit doplněk do stávajícího předplatného.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766970"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="88333-103">Nákup doplňku k předplatnému</span><span class="sxs-lookup"><span data-stu-id="88333-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="88333-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="88333-104">**Applies To**</span></span>

- <span data-ttu-id="88333-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="88333-105">Partner Center</span></span>
- <span data-ttu-id="88333-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="88333-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="88333-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="88333-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="88333-108">Jak zakoupit doplněk do stávajícího předplatného.</span><span class="sxs-lookup"><span data-stu-id="88333-108">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88333-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="88333-109">Prerequisites</span></span>

- <span data-ttu-id="88333-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="88333-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="88333-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="88333-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="88333-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="88333-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="88333-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="88333-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="88333-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="88333-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="88333-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="88333-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="88333-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="88333-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="88333-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="88333-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="88333-118">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="88333-118">A subscription ID.</span></span> <span data-ttu-id="88333-119">Toto je stávající předplatné, pro které se má koupit nabídka doplňku.</span><span class="sxs-lookup"><span data-stu-id="88333-119">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="88333-120">ID nabídky, která identifikuje nabídku doplňku k nákupu.</span><span class="sxs-lookup"><span data-stu-id="88333-120">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="88333-121">Nákup doplňku prostřednictvím kódu</span><span class="sxs-lookup"><span data-stu-id="88333-121">Purchasing an add-on through code</span></span>

<span data-ttu-id="88333-122">Když si nakoupíte doplněk k předplatnému, které aktualizujete původní pořadí předplatného, s pořadím pro doplněk.</span><span class="sxs-lookup"><span data-stu-id="88333-122">When you purchase an add-on to a subscription you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="88333-123">V následujícím seznamu je KódZákazníka ID zákazníka, subscriptionId je ID předplatného a addOnOfferId je ID nabídky pro doplněk.</span><span class="sxs-lookup"><span data-stu-id="88333-123">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="88333-124">Tady je postup:</span><span class="sxs-lookup"><span data-stu-id="88333-124">Here are the steps:</span></span>

1.  <span data-ttu-id="88333-125">Získejte rozhraní pro operace pro předplatné.</span><span class="sxs-lookup"><span data-stu-id="88333-125">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="88333-126">Pomocí tohoto rozhraní můžete vytvořit instanci objektu předplatného.</span><span class="sxs-lookup"><span data-stu-id="88333-126">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="88333-127">Tím získáte podrobnosti o nadřazeném předplatném, včetně ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="88333-127">This gets you the parent subscription details, including the order id.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="88333-128">Vytvoří instanci objektu New [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) .</span><span class="sxs-lookup"><span data-stu-id="88333-128">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="88333-129">Tato instance objednávky se používá k aktualizaci původního pořadí používaného k zakoupení předplatného.</span><span class="sxs-lookup"><span data-stu-id="88333-129">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="88333-130">Přidejte jednu položku řádku do objednávky, která představuje doplněk.</span><span class="sxs-lookup"><span data-stu-id="88333-130">Add a single line item to the order that represents the add-on.</span></span>
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

4.  <span data-ttu-id="88333-131">Aktualizuje původní pořadí pro předplatné s novým pořadím pro doplněk.</span><span class="sxs-lookup"><span data-stu-id="88333-131">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="88333-132">C\#</span><span class="sxs-lookup"><span data-stu-id="88333-132">C\#</span></span>

<span data-ttu-id="88333-133">Chcete-li zakoupit doplněk, Začněte získáním rozhraní pro operace předplatného voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, který identifikuje zákazníka, a pomocí metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pro identifikaci předplatného, které obsahuje nabídku doplňku.</span><span class="sxs-lookup"><span data-stu-id="88333-133">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="88333-134">Použijte toto [**rozhraní**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) k načtení podrobností o předplatném voláním [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="88333-134">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="88333-135">Proč potřebujete podrobnosti o předplatném?</span><span class="sxs-lookup"><span data-stu-id="88333-135">Why do you need the subscription details?</span></span> <span data-ttu-id="88333-136">Protože potřebujete ID objednávky pořadí předplatného.</span><span class="sxs-lookup"><span data-stu-id="88333-136">Because you need the order id of the subscription order.</span></span> <span data-ttu-id="88333-137">To je pořadí, v jakém se má doplněk aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="88333-137">That's the order to be updated with the add-on.</span></span>

<span data-ttu-id="88333-138">Dále vytvořte instanci objektu New [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) a naplňte ji jednou instancí [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) , která obsahuje informace pro identifikaci doplňku, jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="88333-138">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="88333-139">Pomocí tohoto nového objektu aktualizujete pořadí předplatného pomocí doplňku.</span><span class="sxs-lookup"><span data-stu-id="88333-139">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="88333-140">Nakonec zavolejte metodu [**patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) a aktualizujte pořadí předplatného, a to po prvním identifikaci zákazníka pomocí [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) a ORDER by Order [**. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span><span class="sxs-lookup"><span data-stu-id="88333-140">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

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

<span data-ttu-id="88333-141">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="88333-141">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="88333-142">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: AddSubscriptionAddOn.cs</span><span class="sxs-lookup"><span data-stu-id="88333-142">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="88333-143">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="88333-143">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="88333-144">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="88333-144">Request syntax</span></span>

| <span data-ttu-id="88333-145">Metoda</span><span class="sxs-lookup"><span data-stu-id="88333-145">Method</span></span>    | <span data-ttu-id="88333-146">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="88333-146">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="88333-147">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="88333-147">**PATCH**</span></span> | <span data-ttu-id="88333-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="88333-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="88333-149">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="88333-149">URI parameters</span></span>

<span data-ttu-id="88333-150">K identifikaci zákazníka a objednávky použijte následující parametry.</span><span class="sxs-lookup"><span data-stu-id="88333-150">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="88333-151">Název</span><span class="sxs-lookup"><span data-stu-id="88333-151">Name</span></span>                   | <span data-ttu-id="88333-152">Typ</span><span class="sxs-lookup"><span data-stu-id="88333-152">Type</span></span>     | <span data-ttu-id="88333-153">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="88333-153">Required</span></span> | <span data-ttu-id="88333-154">Popis</span><span class="sxs-lookup"><span data-stu-id="88333-154">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="88333-155">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="88333-155">**customer-tenant-id**</span></span> | <span data-ttu-id="88333-156">**guid**</span><span class="sxs-lookup"><span data-stu-id="88333-156">**guid**</span></span> | <span data-ttu-id="88333-157">Y</span><span class="sxs-lookup"><span data-stu-id="88333-157">Y</span></span>        | <span data-ttu-id="88333-158">Hodnota je identifikátor **zákazníka (zákazníka** ), který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="88333-158">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="88333-159">**ID objednávky**</span><span class="sxs-lookup"><span data-stu-id="88333-159">**order-id**</span></span>           | <span data-ttu-id="88333-160">**guid**</span><span class="sxs-lookup"><span data-stu-id="88333-160">**guid**</span></span> | <span data-ttu-id="88333-161">Y</span><span class="sxs-lookup"><span data-stu-id="88333-161">Y</span></span>        | <span data-ttu-id="88333-162">Identifikátor objednávky.</span><span class="sxs-lookup"><span data-stu-id="88333-162">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="88333-163">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="88333-163">Request headers</span></span>

<span data-ttu-id="88333-164">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="88333-164">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="88333-165">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="88333-165">Request body</span></span>

<span data-ttu-id="88333-166">V následujících tabulkách jsou popsány vlastnosti v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="88333-166">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="88333-167">Objednávka</span><span class="sxs-lookup"><span data-stu-id="88333-167">Order</span></span>

| <span data-ttu-id="88333-168">Název</span><span class="sxs-lookup"><span data-stu-id="88333-168">Name</span></span>                | <span data-ttu-id="88333-169">Typ</span><span class="sxs-lookup"><span data-stu-id="88333-169">Type</span></span>             | <span data-ttu-id="88333-170">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="88333-170">Required</span></span> | <span data-ttu-id="88333-171">Popis</span><span class="sxs-lookup"><span data-stu-id="88333-171">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="88333-172">Id</span><span class="sxs-lookup"><span data-stu-id="88333-172">Id</span></span>                  | <span data-ttu-id="88333-173">řetězec</span><span class="sxs-lookup"><span data-stu-id="88333-173">string</span></span>           | <span data-ttu-id="88333-174">N</span><span class="sxs-lookup"><span data-stu-id="88333-174">N</span></span>        | <span data-ttu-id="88333-175">ID objednávky</span><span class="sxs-lookup"><span data-stu-id="88333-175">The order ID.</span></span>                                        |
| <span data-ttu-id="88333-176">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="88333-176">ReferenceCustomerId</span></span> | <span data-ttu-id="88333-177">řetězec</span><span class="sxs-lookup"><span data-stu-id="88333-177">string</span></span>           | <span data-ttu-id="88333-178">Y</span><span class="sxs-lookup"><span data-stu-id="88333-178">Y</span></span>        | <span data-ttu-id="88333-179">ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="88333-179">The customer ID.</span></span>                                     |
| <span data-ttu-id="88333-180">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="88333-180">LineItems</span></span>           | <span data-ttu-id="88333-181">pole objektů</span><span class="sxs-lookup"><span data-stu-id="88333-181">array of objects</span></span> | <span data-ttu-id="88333-182">Y</span><span class="sxs-lookup"><span data-stu-id="88333-182">Y</span></span>        | <span data-ttu-id="88333-183">Pole objektů [OrderLineItem](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="88333-183">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="88333-184">CreationDate</span><span class="sxs-lookup"><span data-stu-id="88333-184">CreationDate</span></span>        | <span data-ttu-id="88333-185">řetězec</span><span class="sxs-lookup"><span data-stu-id="88333-185">string</span></span>           | <span data-ttu-id="88333-186">N</span><span class="sxs-lookup"><span data-stu-id="88333-186">N</span></span>        | <span data-ttu-id="88333-187">Datum vytvoření objednávky ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="88333-187">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="88333-188">Atributy</span><span class="sxs-lookup"><span data-stu-id="88333-188">Attributes</span></span>          | <span data-ttu-id="88333-189">object</span><span class="sxs-lookup"><span data-stu-id="88333-189">object</span></span>           | <span data-ttu-id="88333-190">N</span><span class="sxs-lookup"><span data-stu-id="88333-190">N</span></span>        | <span data-ttu-id="88333-191">Obsahuje "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="88333-191">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="88333-192">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="88333-192">OrderLineItem</span></span>

| <span data-ttu-id="88333-193">Název</span><span class="sxs-lookup"><span data-stu-id="88333-193">Name</span></span>                 | <span data-ttu-id="88333-194">Typ</span><span class="sxs-lookup"><span data-stu-id="88333-194">Type</span></span>   | <span data-ttu-id="88333-195">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="88333-195">Required</span></span> | <span data-ttu-id="88333-196">Popis</span><span class="sxs-lookup"><span data-stu-id="88333-196">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="88333-197">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="88333-197">LineItemNumber</span></span>       | <span data-ttu-id="88333-198">číslo</span><span class="sxs-lookup"><span data-stu-id="88333-198">number</span></span> | <span data-ttu-id="88333-199">Y</span><span class="sxs-lookup"><span data-stu-id="88333-199">Y</span></span>        | <span data-ttu-id="88333-200">Číslo položky řádku začínající na 0.</span><span class="sxs-lookup"><span data-stu-id="88333-200">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="88333-201">Hodnotami OfferId</span><span class="sxs-lookup"><span data-stu-id="88333-201">OfferId</span></span>              | <span data-ttu-id="88333-202">řetězec</span><span class="sxs-lookup"><span data-stu-id="88333-202">string</span></span> | <span data-ttu-id="88333-203">Y</span><span class="sxs-lookup"><span data-stu-id="88333-203">Y</span></span>        | <span data-ttu-id="88333-204">ID nabídky doplňku</span><span class="sxs-lookup"><span data-stu-id="88333-204">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="88333-205">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="88333-205">SubscriptionId</span></span>       | <span data-ttu-id="88333-206">řetězec</span><span class="sxs-lookup"><span data-stu-id="88333-206">string</span></span> | <span data-ttu-id="88333-207">N</span><span class="sxs-lookup"><span data-stu-id="88333-207">N</span></span>        | <span data-ttu-id="88333-208">ID zakoupeného předplatného doplňku.</span><span class="sxs-lookup"><span data-stu-id="88333-208">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="88333-209">ParentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="88333-209">ParentSubscriptionId</span></span> | <span data-ttu-id="88333-210">řetězec</span><span class="sxs-lookup"><span data-stu-id="88333-210">string</span></span> | <span data-ttu-id="88333-211">Y</span><span class="sxs-lookup"><span data-stu-id="88333-211">Y</span></span>        | <span data-ttu-id="88333-212">ID nadřazeného předplatného, které má nabídku doplňku.</span><span class="sxs-lookup"><span data-stu-id="88333-212">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="88333-213">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="88333-213">FriendlyName</span></span>         | <span data-ttu-id="88333-214">řetězec</span><span class="sxs-lookup"><span data-stu-id="88333-214">string</span></span> | <span data-ttu-id="88333-215">N</span><span class="sxs-lookup"><span data-stu-id="88333-215">N</span></span>        | <span data-ttu-id="88333-216">Popisný název této položky řádku</span><span class="sxs-lookup"><span data-stu-id="88333-216">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="88333-217">Množství</span><span class="sxs-lookup"><span data-stu-id="88333-217">Quantity</span></span>             | <span data-ttu-id="88333-218">číslo</span><span class="sxs-lookup"><span data-stu-id="88333-218">number</span></span> | <span data-ttu-id="88333-219">Y</span><span class="sxs-lookup"><span data-stu-id="88333-219">Y</span></span>        | <span data-ttu-id="88333-220">Počet licencí.</span><span class="sxs-lookup"><span data-stu-id="88333-220">The number of licenses.</span></span>                                      |
| <span data-ttu-id="88333-221">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="88333-221">PartnerIdOnRecord</span></span>    | <span data-ttu-id="88333-222">řetězec</span><span class="sxs-lookup"><span data-stu-id="88333-222">string</span></span> | <span data-ttu-id="88333-223">N</span><span class="sxs-lookup"><span data-stu-id="88333-223">N</span></span>        | <span data-ttu-id="88333-224">ID MPN partnera záznamu</span><span class="sxs-lookup"><span data-stu-id="88333-224">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="88333-225">Atributy</span><span class="sxs-lookup"><span data-stu-id="88333-225">Attributes</span></span>           | <span data-ttu-id="88333-226">object</span><span class="sxs-lookup"><span data-stu-id="88333-226">object</span></span> | <span data-ttu-id="88333-227">N</span><span class="sxs-lookup"><span data-stu-id="88333-227">N</span></span>        | <span data-ttu-id="88333-228">Obsahuje "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="88333-228">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="88333-229">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="88333-229">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="88333-230">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="88333-230">REST response</span></span>

<span data-ttu-id="88333-231">V případě úspěchu tato metoda vrátí aktualizované pořadí předplatného v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="88333-231">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="88333-232">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="88333-232">Response success and error codes</span></span>

<span data-ttu-id="88333-233">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="88333-233">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="88333-234">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="88333-234">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="88333-235">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="88333-235">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="88333-236">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="88333-236">Response example</span></span>

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
