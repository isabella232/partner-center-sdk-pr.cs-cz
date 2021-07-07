---
title: Vytvořit objednávku zákazníka pro nepřímý prodejce
description: Naučte se používat rozhraní API partnerského centra k vytvoření objednávky pro zákazníka nepřímého prodejce. Článek obsahuje požadavky, kroky a příklady.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253ba2289ea1f58e7d8eaa960d7d0daaa887f0d
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973535"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="acc2d-104">Vytvoření objednávky pro zákazníka nepřímého prodejce</span><span class="sxs-lookup"><span data-stu-id="acc2d-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="acc2d-105">Jak vytvořit objednávku pro zákazníka nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="acc2d-105">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acc2d-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="acc2d-106">Prerequisites</span></span>

- <span data-ttu-id="acc2d-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="acc2d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="acc2d-108">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="acc2d-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="acc2d-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="acc2d-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="acc2d-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="acc2d-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="acc2d-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="acc2d-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="acc2d-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="acc2d-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="acc2d-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="acc2d-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="acc2d-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="acc2d-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="acc2d-115">Identifikátor nabídky položky, která se má koupit</span><span class="sxs-lookup"><span data-stu-id="acc2d-115">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="acc2d-116">Identifikátor tenanta nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="acc2d-116">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="acc2d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="acc2d-117">C\#</span></span>

<span data-ttu-id="acc2d-118">Chcete-li vytvořit objednávku pro zákazníka nepřímého prodejce:</span><span class="sxs-lookup"><span data-stu-id="acc2d-118">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="acc2d-119">Získejte kolekci nepřímých prodejců, kteří mají relaci s přihlášeným partnerem.</span><span class="sxs-lookup"><span data-stu-id="acc2d-119">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="acc2d-120">Získat místní proměnnou na položku v kolekci, která odpovídá ID nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="acc2d-120">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="acc2d-121">Tento krok vám pomůže při vytváření objednávky získat přístup k vlastnosti [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) prodejce.</span><span class="sxs-lookup"><span data-stu-id="acc2d-121">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="acc2d-122">Vytvořte instanci objektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) a nastavte vlastnost [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) na identifikátor zákazníka, aby bylo možné záznam zákazníka zaznamenat.</span><span class="sxs-lookup"><span data-stu-id="acc2d-122">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="acc2d-123">Vytvořte seznam objektů [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) a přiřaďte seznam k vlastnosti [**položky řádku**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) objednávky.</span><span class="sxs-lookup"><span data-stu-id="acc2d-123">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="acc2d-124">Každá položka řádku objednávky obsahuje informace o nákupu pro jednu nabídku.</span><span class="sxs-lookup"><span data-stu-id="acc2d-124">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="acc2d-125">Nezapomeňte v každé položce řádku naplnit vlastnost [**PARTNERIDONRECORD**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) číslem MPN nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="acc2d-125">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="acc2d-126">Musíte mít aspoň jednu položku řádku objednávky.</span><span class="sxs-lookup"><span data-stu-id="acc2d-126">You must have at least one order line item.</span></span>

5. <span data-ttu-id="acc2d-127">Získejte rozhraní k seřazení operací voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, které zákazníka identifikují, a potom načtěte rozhraní z vlastnosti [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .</span><span class="sxs-lookup"><span data-stu-id="acc2d-127">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="acc2d-128">Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) vytvořte objednávku.</span><span class="sxs-lookup"><span data-stu-id="acc2d-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="acc2d-129">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="acc2d-129">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="acc2d-130">**ukázka**: [konzola test app](console-test-app.md)**Project**: **třída** pro ukázkové sady SDK partnerského centra: PlaceOrderForCustomer. cs</span><span class="sxs-lookup"><span data-stu-id="acc2d-130">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="acc2d-131">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="acc2d-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="acc2d-132">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="acc2d-132">Request syntax</span></span>

| <span data-ttu-id="acc2d-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="acc2d-133">Method</span></span>   | <span data-ttu-id="acc2d-134">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="acc2d-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="acc2d-135">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="acc2d-135">**POST**</span></span> | <span data-ttu-id="acc2d-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="acc2d-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="acc2d-137">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="acc2d-137">URI parameters</span></span>

<span data-ttu-id="acc2d-138">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="acc2d-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="acc2d-139">Název</span><span class="sxs-lookup"><span data-stu-id="acc2d-139">Name</span></span>        | <span data-ttu-id="acc2d-140">Typ</span><span class="sxs-lookup"><span data-stu-id="acc2d-140">Type</span></span>   | <span data-ttu-id="acc2d-141">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="acc2d-141">Required</span></span> | <span data-ttu-id="acc2d-142">Popis</span><span class="sxs-lookup"><span data-stu-id="acc2d-142">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="acc2d-143">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="acc2d-143">customer-id</span></span> | <span data-ttu-id="acc2d-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-144">string</span></span> | <span data-ttu-id="acc2d-145">Yes</span><span class="sxs-lookup"><span data-stu-id="acc2d-145">Yes</span></span>      | <span data-ttu-id="acc2d-146">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="acc2d-146">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="acc2d-147">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="acc2d-147">Request headers</span></span>

<span data-ttu-id="acc2d-148">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="acc2d-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="acc2d-149">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="acc2d-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="acc2d-150">Objednávka</span><span class="sxs-lookup"><span data-stu-id="acc2d-150">Order</span></span>

<span data-ttu-id="acc2d-151">Tato tabulka popisuje vlastnosti **objednávky** v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="acc2d-151">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="acc2d-152">Název</span><span class="sxs-lookup"><span data-stu-id="acc2d-152">Name</span></span> | <span data-ttu-id="acc2d-153">Typ</span><span class="sxs-lookup"><span data-stu-id="acc2d-153">Type</span></span> | <span data-ttu-id="acc2d-154">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="acc2d-154">Required</span></span> | <span data-ttu-id="acc2d-155">Popis</span><span class="sxs-lookup"><span data-stu-id="acc2d-155">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="acc2d-156">id</span><span class="sxs-lookup"><span data-stu-id="acc2d-156">id</span></span> | <span data-ttu-id="acc2d-157">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-157">string</span></span> | <span data-ttu-id="acc2d-158">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-158">No</span></span> | <span data-ttu-id="acc2d-159">Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="acc2d-159">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="acc2d-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="acc2d-160">referenceCustomerId</span></span> | <span data-ttu-id="acc2d-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-161">string</span></span> | <span data-ttu-id="acc2d-162">Yes</span><span class="sxs-lookup"><span data-stu-id="acc2d-162">Yes</span></span> | <span data-ttu-id="acc2d-163">Identifikátor zákazníka.</span><span class="sxs-lookup"><span data-stu-id="acc2d-163">The customer identifier.</span></span> |
| <span data-ttu-id="acc2d-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="acc2d-164">billingCycle</span></span> | <span data-ttu-id="acc2d-165">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-165">string</span></span> | <span data-ttu-id="acc2d-166">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-166">No</span></span> | <span data-ttu-id="acc2d-167">Frekvence, s jakou se má partner fakturovat v této objednávce</span><span class="sxs-lookup"><span data-stu-id="acc2d-167">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="acc2d-168">Výchozí hodnota je &quot; měsíčně &quot; a po úspěšném vytvoření objednávky se použije.</span><span class="sxs-lookup"><span data-stu-id="acc2d-168">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="acc2d-169">Podporované hodnoty jsou názvy členů nalezené v [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="acc2d-169">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="acc2d-170">Poznámka: funkce každoroční fakturace zatím není obecně dostupná.</span><span class="sxs-lookup"><span data-stu-id="acc2d-170">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="acc2d-171">Brzy se přiblíží podpora pro roční fakturaci.</span><span class="sxs-lookup"><span data-stu-id="acc2d-171">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="acc2d-172">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="acc2d-172">lineItems</span></span> | <span data-ttu-id="acc2d-173">pole objektů</span><span class="sxs-lookup"><span data-stu-id="acc2d-173">array of objects</span></span> | <span data-ttu-id="acc2d-174">Yes</span><span class="sxs-lookup"><span data-stu-id="acc2d-174">Yes</span></span> | <span data-ttu-id="acc2d-175">Pole prostředků [**OrderLineItem**](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="acc2d-175">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="acc2d-176">creationDate</span><span class="sxs-lookup"><span data-stu-id="acc2d-176">creationDate</span></span> | <span data-ttu-id="acc2d-177">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-177">string</span></span> | <span data-ttu-id="acc2d-178">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-178">No</span></span> | <span data-ttu-id="acc2d-179">Datum vytvoření objednávky ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="acc2d-179">The date the order was created, in date-time format.</span></span> <span data-ttu-id="acc2d-180">Použito po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="acc2d-180">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="acc2d-181">atributy</span><span class="sxs-lookup"><span data-stu-id="acc2d-181">attributes</span></span> | <span data-ttu-id="acc2d-182">object</span><span class="sxs-lookup"><span data-stu-id="acc2d-182">object</span></span> | <span data-ttu-id="acc2d-183">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-183">No</span></span> | <span data-ttu-id="acc2d-184">Obsahuje "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="acc2d-184">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="acc2d-185">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="acc2d-185">OrderLineItem</span></span>

<span data-ttu-id="acc2d-186">Tato tabulka popisuje vlastnosti **OrderLineItem** v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="acc2d-186">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="acc2d-187">Název</span><span class="sxs-lookup"><span data-stu-id="acc2d-187">Name</span></span> | <span data-ttu-id="acc2d-188">Typ</span><span class="sxs-lookup"><span data-stu-id="acc2d-188">Type</span></span> | <span data-ttu-id="acc2d-189">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="acc2d-189">Required</span></span> | <span data-ttu-id="acc2d-190">Popis</span><span class="sxs-lookup"><span data-stu-id="acc2d-190">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="acc2d-191">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="acc2d-191">lineItemNumber</span></span> | <span data-ttu-id="acc2d-192">int</span><span class="sxs-lookup"><span data-stu-id="acc2d-192">int</span></span> | <span data-ttu-id="acc2d-193">Yes</span><span class="sxs-lookup"><span data-stu-id="acc2d-193">Yes</span></span> | <span data-ttu-id="acc2d-194">Každá položka řádku v kolekci získá jedinečné číslo řádku, počítáno od 0 do Count-1.</span><span class="sxs-lookup"><span data-stu-id="acc2d-194">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="acc2d-195">Hodnotami OfferId</span><span class="sxs-lookup"><span data-stu-id="acc2d-195">offerId</span></span> | <span data-ttu-id="acc2d-196">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-196">string</span></span> | <span data-ttu-id="acc2d-197">Yes</span><span class="sxs-lookup"><span data-stu-id="acc2d-197">Yes</span></span> | <span data-ttu-id="acc2d-198">Identifikátor nabídky</span><span class="sxs-lookup"><span data-stu-id="acc2d-198">The offer identifier.</span></span> |
| <span data-ttu-id="acc2d-199">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="acc2d-199">subscriptionId</span></span> | <span data-ttu-id="acc2d-200">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-200">string</span></span> | <span data-ttu-id="acc2d-201">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-201">No</span></span> | <span data-ttu-id="acc2d-202">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="acc2d-202">The subscription identifier.</span></span> |
| <span data-ttu-id="acc2d-203">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="acc2d-203">parentSubscriptionId</span></span> | <span data-ttu-id="acc2d-204">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-204">string</span></span> | <span data-ttu-id="acc2d-205">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-205">No</span></span> | <span data-ttu-id="acc2d-206">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="acc2d-206">Optional.</span></span> <span data-ttu-id="acc2d-207">ID nadřazeného odběru v nabídce doplňku</span><span class="sxs-lookup"><span data-stu-id="acc2d-207">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="acc2d-208">Platí pouze pro opravu.</span><span class="sxs-lookup"><span data-stu-id="acc2d-208">Applies to PATCH only.</span></span> |
| <span data-ttu-id="acc2d-209">friendlyName</span><span class="sxs-lookup"><span data-stu-id="acc2d-209">friendlyName</span></span> | <span data-ttu-id="acc2d-210">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-210">string</span></span> | <span data-ttu-id="acc2d-211">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-211">No</span></span> | <span data-ttu-id="acc2d-212">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="acc2d-212">Optional.</span></span> <span data-ttu-id="acc2d-213">Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost.</span><span class="sxs-lookup"><span data-stu-id="acc2d-213">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="acc2d-214">quantity</span><span class="sxs-lookup"><span data-stu-id="acc2d-214">quantity</span></span> | <span data-ttu-id="acc2d-215">int</span><span class="sxs-lookup"><span data-stu-id="acc2d-215">int</span></span> | <span data-ttu-id="acc2d-216">Yes</span><span class="sxs-lookup"><span data-stu-id="acc2d-216">Yes</span></span> | <span data-ttu-id="acc2d-217">Počet licencí pro předplatné založené na licencích.</span><span class="sxs-lookup"><span data-stu-id="acc2d-217">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="acc2d-218">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="acc2d-218">partnerIdOnRecord</span></span> | <span data-ttu-id="acc2d-219">řetězec</span><span class="sxs-lookup"><span data-stu-id="acc2d-219">string</span></span> | <span data-ttu-id="acc2d-220">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-220">No</span></span> | <span data-ttu-id="acc2d-221">Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **nepřímého prodejce** (nikdy ID nepřímého poskytovatele).</span><span class="sxs-lookup"><span data-stu-id="acc2d-221">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="acc2d-222">To zajišťuje správné účetnictví pro motivaci.</span><span class="sxs-lookup"><span data-stu-id="acc2d-222">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="acc2d-223">**Nepodaří-li se poskytnout ID programu MPN pro prodejce nezpůsobí selhání objednávky. Prodejce však není zaznamenán a v důsledku toho nemůžou výpočty s nesekvencí zahrnovat prodej.**</span><span class="sxs-lookup"><span data-stu-id="acc2d-223">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="acc2d-224">atributy</span><span class="sxs-lookup"><span data-stu-id="acc2d-224">attributes</span></span> | <span data-ttu-id="acc2d-225">object</span><span class="sxs-lookup"><span data-stu-id="acc2d-225">object</span></span> | <span data-ttu-id="acc2d-226">No</span><span class="sxs-lookup"><span data-stu-id="acc2d-226">No</span></span> | <span data-ttu-id="acc2d-227">Obsahuje "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="acc2d-227">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="acc2d-228">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="acc2d-228">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
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

## <a name="rest-response"></a><span data-ttu-id="acc2d-229">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="acc2d-229">REST response</span></span>

<span data-ttu-id="acc2d-230">V případě úspěchu obsahuje tělo odpovědi vyplněný prostředek [objednávky](order-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="acc2d-230">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="acc2d-231">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="acc2d-231">Response success and error codes</span></span>

<span data-ttu-id="acc2d-232">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="acc2d-232">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="acc2d-233">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="acc2d-233">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="acc2d-234">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="acc2d-234">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="acc2d-235">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="acc2d-235">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
