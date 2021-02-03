---
title: Vytvořit objednávku zákazníka pro nepřímý prodejce
description: Naučte se používat rozhraní API partnerského centra k vytvoření objednávky pro zákazníka nepřímého prodejce. Článek zahrnuje požadavky, kroky a Exmaples.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767134"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="06439-104">Vytvoření objednávky pro zákazníka nepřímého prodejce</span><span class="sxs-lookup"><span data-stu-id="06439-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="06439-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="06439-105">**Applies to:**</span></span>

- <span data-ttu-id="06439-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="06439-106">Partner Center</span></span>

<span data-ttu-id="06439-107">Jak vytvořit objednávku pro zákazníka nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="06439-107">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06439-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="06439-108">Prerequisites</span></span>

- <span data-ttu-id="06439-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="06439-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="06439-110">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="06439-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="06439-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="06439-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="06439-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="06439-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="06439-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="06439-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="06439-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="06439-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="06439-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="06439-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="06439-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="06439-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="06439-117">Identifikátor nabídky položky, která se má koupit</span><span class="sxs-lookup"><span data-stu-id="06439-117">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="06439-118">Identifikátor tenanta nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="06439-118">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="06439-119">C\#</span><span class="sxs-lookup"><span data-stu-id="06439-119">C\#</span></span>

<span data-ttu-id="06439-120">Chcete-li vytvořit objednávku pro zákazníka nepřímého prodejce:</span><span class="sxs-lookup"><span data-stu-id="06439-120">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="06439-121">Získejte kolekci nepřímých prodejců, kteří mají relaci s přihlášeným partnerem.</span><span class="sxs-lookup"><span data-stu-id="06439-121">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="06439-122">Získat místní proměnnou na položku v kolekci, která odpovídá ID nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="06439-122">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="06439-123">Tento krok vám pomůže při vytváření objednávky získat přístup k vlastnosti [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) prodejce.</span><span class="sxs-lookup"><span data-stu-id="06439-123">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="06439-124">Vytvořte instanci objektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) a nastavte vlastnost [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) na identifikátor zákazníka, aby bylo možné záznam zákazníka zaznamenat.</span><span class="sxs-lookup"><span data-stu-id="06439-124">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="06439-125">Vytvořte seznam objektů [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) a přiřaďte seznam k vlastnosti [**položky řádku**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) objednávky.</span><span class="sxs-lookup"><span data-stu-id="06439-125">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="06439-126">Každá položka řádku objednávky obsahuje informace o nákupu pro jednu nabídku.</span><span class="sxs-lookup"><span data-stu-id="06439-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="06439-127">Nezapomeňte v každé položce řádku naplnit vlastnost [**PARTNERIDONRECORD**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) číslem MPN nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="06439-127">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="06439-128">Musíte mít aspoň jednu položku řádku objednávky.</span><span class="sxs-lookup"><span data-stu-id="06439-128">You must have at least one order line item.</span></span>

5. <span data-ttu-id="06439-129">Získejte rozhraní k seřazení operací voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, které zákazníka identifikují, a potom načtěte rozhraní z vlastnosti [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .</span><span class="sxs-lookup"><span data-stu-id="06439-129">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="06439-130">Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) vytvořte objednávku.</span><span class="sxs-lookup"><span data-stu-id="06439-130">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="06439-131">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="06439-131">C\# example</span></span>

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

<span data-ttu-id="06439-132">**Ukázka**:**projekt** [aplikace testů konzoly](console-test-app.md): ukázkové **třídy** SDK pro partnerských Center: PlaceOrderForCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="06439-132">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="06439-133">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="06439-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="06439-134">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="06439-134">Request syntax</span></span>

| <span data-ttu-id="06439-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="06439-135">Method</span></span>   | <span data-ttu-id="06439-136">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="06439-136">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="06439-137">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="06439-137">**POST**</span></span> | <span data-ttu-id="06439-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="06439-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="06439-139">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="06439-139">URI parameters</span></span>

<span data-ttu-id="06439-140">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="06439-140">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="06439-141">Název</span><span class="sxs-lookup"><span data-stu-id="06439-141">Name</span></span>        | <span data-ttu-id="06439-142">Typ</span><span class="sxs-lookup"><span data-stu-id="06439-142">Type</span></span>   | <span data-ttu-id="06439-143">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="06439-143">Required</span></span> | <span data-ttu-id="06439-144">Popis</span><span class="sxs-lookup"><span data-stu-id="06439-144">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="06439-145">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="06439-145">customer-id</span></span> | <span data-ttu-id="06439-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-146">string</span></span> | <span data-ttu-id="06439-147">Yes</span><span class="sxs-lookup"><span data-stu-id="06439-147">Yes</span></span>      | <span data-ttu-id="06439-148">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="06439-148">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="06439-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="06439-149">Request headers</span></span>

<span data-ttu-id="06439-150">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="06439-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="06439-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="06439-151">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="06439-152">Objednávka</span><span class="sxs-lookup"><span data-stu-id="06439-152">Order</span></span>

<span data-ttu-id="06439-153">Tato tabulka popisuje vlastnosti **objednávky** v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="06439-153">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="06439-154">Název</span><span class="sxs-lookup"><span data-stu-id="06439-154">Name</span></span> | <span data-ttu-id="06439-155">Typ</span><span class="sxs-lookup"><span data-stu-id="06439-155">Type</span></span> | <span data-ttu-id="06439-156">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="06439-156">Required</span></span> | <span data-ttu-id="06439-157">Popis</span><span class="sxs-lookup"><span data-stu-id="06439-157">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="06439-158">id</span><span class="sxs-lookup"><span data-stu-id="06439-158">id</span></span> | <span data-ttu-id="06439-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-159">string</span></span> | <span data-ttu-id="06439-160">No</span><span class="sxs-lookup"><span data-stu-id="06439-160">No</span></span> | <span data-ttu-id="06439-161">Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="06439-161">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="06439-162">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="06439-162">referenceCustomerId</span></span> | <span data-ttu-id="06439-163">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-163">string</span></span> | <span data-ttu-id="06439-164">Yes</span><span class="sxs-lookup"><span data-stu-id="06439-164">Yes</span></span> | <span data-ttu-id="06439-165">Identifikátor zákazníka.</span><span class="sxs-lookup"><span data-stu-id="06439-165">The customer identifier.</span></span> |
| <span data-ttu-id="06439-166">billingCycle</span><span class="sxs-lookup"><span data-stu-id="06439-166">billingCycle</span></span> | <span data-ttu-id="06439-167">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-167">string</span></span> | <span data-ttu-id="06439-168">No</span><span class="sxs-lookup"><span data-stu-id="06439-168">No</span></span> | <span data-ttu-id="06439-169">Frekvence, s jakou se má partner fakturovat v této objednávce</span><span class="sxs-lookup"><span data-stu-id="06439-169">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="06439-170">Výchozí hodnota je &quot; měsíčně &quot; a po úspěšném vytvoření objednávky se použije.</span><span class="sxs-lookup"><span data-stu-id="06439-170">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="06439-171">Podporované hodnoty jsou názvy členů nalezené v [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="06439-171">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="06439-172">Poznámka: funkce každoroční fakturace zatím není obecně dostupná.</span><span class="sxs-lookup"><span data-stu-id="06439-172">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="06439-173">Brzy se přiblíží podpora pro roční fakturaci.</span><span class="sxs-lookup"><span data-stu-id="06439-173">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="06439-174">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="06439-174">lineItems</span></span> | <span data-ttu-id="06439-175">pole objektů</span><span class="sxs-lookup"><span data-stu-id="06439-175">array of objects</span></span> | <span data-ttu-id="06439-176">Yes</span><span class="sxs-lookup"><span data-stu-id="06439-176">Yes</span></span> | <span data-ttu-id="06439-177">Pole prostředků [**OrderLineItem**](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="06439-177">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="06439-178">creationDate</span><span class="sxs-lookup"><span data-stu-id="06439-178">creationDate</span></span> | <span data-ttu-id="06439-179">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-179">string</span></span> | <span data-ttu-id="06439-180">No</span><span class="sxs-lookup"><span data-stu-id="06439-180">No</span></span> | <span data-ttu-id="06439-181">Datum vytvoření objednávky ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="06439-181">The date the order was created, in date-time format.</span></span> <span data-ttu-id="06439-182">Použito po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="06439-182">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="06439-183">atributy</span><span class="sxs-lookup"><span data-stu-id="06439-183">attributes</span></span> | <span data-ttu-id="06439-184">object</span><span class="sxs-lookup"><span data-stu-id="06439-184">object</span></span> | <span data-ttu-id="06439-185">No</span><span class="sxs-lookup"><span data-stu-id="06439-185">No</span></span> | <span data-ttu-id="06439-186">Obsahuje "ObjectType": "Order".</span><span class="sxs-lookup"><span data-stu-id="06439-186">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="06439-187">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="06439-187">OrderLineItem</span></span>

<span data-ttu-id="06439-188">Tato tabulka popisuje vlastnosti **OrderLineItem** v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="06439-188">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="06439-189">Název</span><span class="sxs-lookup"><span data-stu-id="06439-189">Name</span></span> | <span data-ttu-id="06439-190">Typ</span><span class="sxs-lookup"><span data-stu-id="06439-190">Type</span></span> | <span data-ttu-id="06439-191">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="06439-191">Required</span></span> | <span data-ttu-id="06439-192">Popis</span><span class="sxs-lookup"><span data-stu-id="06439-192">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="06439-193">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="06439-193">lineItemNumber</span></span> | <span data-ttu-id="06439-194">int</span><span class="sxs-lookup"><span data-stu-id="06439-194">int</span></span> | <span data-ttu-id="06439-195">Yes</span><span class="sxs-lookup"><span data-stu-id="06439-195">Yes</span></span> | <span data-ttu-id="06439-196">Každá položka řádku v kolekci získá jedinečné číslo řádku, počítáno od 0 do Count-1.</span><span class="sxs-lookup"><span data-stu-id="06439-196">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="06439-197">Hodnotami OfferId</span><span class="sxs-lookup"><span data-stu-id="06439-197">offerId</span></span> | <span data-ttu-id="06439-198">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-198">string</span></span> | <span data-ttu-id="06439-199">Yes</span><span class="sxs-lookup"><span data-stu-id="06439-199">Yes</span></span> | <span data-ttu-id="06439-200">Identifikátor nabídky</span><span class="sxs-lookup"><span data-stu-id="06439-200">The offer identifier.</span></span> |
| <span data-ttu-id="06439-201">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="06439-201">subscriptionId</span></span> | <span data-ttu-id="06439-202">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-202">string</span></span> | <span data-ttu-id="06439-203">No</span><span class="sxs-lookup"><span data-stu-id="06439-203">No</span></span> | <span data-ttu-id="06439-204">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="06439-204">The subscription identifier.</span></span> |
| <span data-ttu-id="06439-205">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="06439-205">parentSubscriptionId</span></span> | <span data-ttu-id="06439-206">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-206">string</span></span> | <span data-ttu-id="06439-207">No</span><span class="sxs-lookup"><span data-stu-id="06439-207">No</span></span> | <span data-ttu-id="06439-208">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="06439-208">Optional.</span></span> <span data-ttu-id="06439-209">ID nadřazeného odběru v nabídce doplňku</span><span class="sxs-lookup"><span data-stu-id="06439-209">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="06439-210">Platí pouze pro opravu.</span><span class="sxs-lookup"><span data-stu-id="06439-210">Applies to PATCH only.</span></span> |
| <span data-ttu-id="06439-211">friendlyName</span><span class="sxs-lookup"><span data-stu-id="06439-211">friendlyName</span></span> | <span data-ttu-id="06439-212">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-212">string</span></span> | <span data-ttu-id="06439-213">No</span><span class="sxs-lookup"><span data-stu-id="06439-213">No</span></span> | <span data-ttu-id="06439-214">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="06439-214">Optional.</span></span> <span data-ttu-id="06439-215">Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost.</span><span class="sxs-lookup"><span data-stu-id="06439-215">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="06439-216">quantity</span><span class="sxs-lookup"><span data-stu-id="06439-216">quantity</span></span> | <span data-ttu-id="06439-217">int</span><span class="sxs-lookup"><span data-stu-id="06439-217">int</span></span> | <span data-ttu-id="06439-218">Yes</span><span class="sxs-lookup"><span data-stu-id="06439-218">Yes</span></span> | <span data-ttu-id="06439-219">Počet licencí pro předplatné založené na licencích.</span><span class="sxs-lookup"><span data-stu-id="06439-219">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="06439-220">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="06439-220">partnerIdOnRecord</span></span> | <span data-ttu-id="06439-221">řetězec</span><span class="sxs-lookup"><span data-stu-id="06439-221">string</span></span> | <span data-ttu-id="06439-222">No</span><span class="sxs-lookup"><span data-stu-id="06439-222">No</span></span> | <span data-ttu-id="06439-223">Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **nepřímého prodejce** (nikdy ID nepřímého poskytovatele).</span><span class="sxs-lookup"><span data-stu-id="06439-223">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="06439-224">To zajišťuje správné účetnictví pro motivaci.</span><span class="sxs-lookup"><span data-stu-id="06439-224">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="06439-225">**Nepodaří-li se poskytnout ID programu MPN pro prodejce nezpůsobí selhání objednávky. Prodejce však není zaznamenán a v důsledku toho nemůžou výpočty s nesekvencí zahrnovat prodej.**</span><span class="sxs-lookup"><span data-stu-id="06439-225">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="06439-226">atributy</span><span class="sxs-lookup"><span data-stu-id="06439-226">attributes</span></span> | <span data-ttu-id="06439-227">object</span><span class="sxs-lookup"><span data-stu-id="06439-227">object</span></span> | <span data-ttu-id="06439-228">No</span><span class="sxs-lookup"><span data-stu-id="06439-228">No</span></span> | <span data-ttu-id="06439-229">Obsahuje "ObjectType": "OrderLineItem".</span><span class="sxs-lookup"><span data-stu-id="06439-229">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="06439-230">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="06439-230">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="06439-231">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="06439-231">REST response</span></span>

<span data-ttu-id="06439-232">V případě úspěchu obsahuje tělo odpovědi vyplněný prostředek [objednávky](order-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="06439-232">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="06439-233">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="06439-233">Response success and error codes</span></span>

<span data-ttu-id="06439-234">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="06439-234">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="06439-235">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="06439-235">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="06439-236">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="06439-236">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="06439-237">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="06439-237">Response example</span></span>

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
