---
title: Vytvoření košíku s doplňky
description: Naučte se používat rozhraní API partnerského centra k přidání objednávky zákazníka s doplňky prostřednictvím košíku. Článek sdílí požadavky a kroky k vytvoření košíku s doplňky.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767128"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="a0560-104">Vytvoření košíku s doplňky pro objednávku zákazníka</span><span class="sxs-lookup"><span data-stu-id="a0560-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="a0560-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="a0560-105">**Applies to:**</span></span>

- <span data-ttu-id="a0560-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="a0560-106">Partner Center</span></span>

<span data-ttu-id="a0560-107">Přidané doplňky můžete koupit prostřednictvím košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-107">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="a0560-108">Další informace o tom, co je aktuálně k dispozici pro prodej, najdete [v tématu partnerské nabídky v programu Cloud Solution Provider](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="a0560-108">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0560-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a0560-109">Prerequisites</span></span>

- <span data-ttu-id="a0560-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a0560-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a0560-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="a0560-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a0560-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a0560-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a0560-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="a0560-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a0560-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="a0560-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a0560-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="a0560-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a0560-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="a0560-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a0560-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a0560-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="a0560-118">C\#</span><span class="sxs-lookup"><span data-stu-id="a0560-118">C\#</span></span>

<span data-ttu-id="a0560-119">Vozík umožňuje zakoupit základní nabídku a její odpovídající doplňky.</span><span class="sxs-lookup"><span data-stu-id="a0560-119">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="a0560-120">Pomocí těchto kroků vytvořte košík:</span><span class="sxs-lookup"><span data-stu-id="a0560-120">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="a0560-121">Vytvoří instanci objektu [**košíku**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) .</span><span class="sxs-lookup"><span data-stu-id="a0560-121">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="a0560-122">Vytvořte seznam objektů [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) , které představují základní nabídky, a přiřaďte seznam k vlastnosti [**položky řádku**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-122">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects which represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="a0560-123">V rámci položky řádku košíku základní nabídky vyplňte seznam **AddOnItems** dalšími objekty **CartLineItem** , které každý z nich představují doplněk, který bude koupen na základě této základní nabídky.</span><span class="sxs-lookup"><span data-stu-id="a0560-123">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="a0560-124">Získejte rozhraní pro operace na vozíku pomocí [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) k volání metody [**ICustomerCollection. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka a následnému načtení rozhraní z vlastnosti **košíku** .</span><span class="sxs-lookup"><span data-stu-id="a0560-124">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="a0560-125">Nakonec voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) vytvořte košík.</span><span class="sxs-lookup"><span data-stu-id="a0560-125">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="a0560-126">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="a0560-126">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

<span data-ttu-id="a0560-127">Pomocí těchto kroků můžete vytvořit košík, který umožní nákup doplňků u stávajících základních předplatných:</span><span class="sxs-lookup"><span data-stu-id="a0560-127">Follow these steps to create a cart which will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="a0560-128">Vytvořte **košík** s novým **CartLineItem** , který obsahuje ID předplatného ve vlastnosti **ProvisioningContext** s klíčem "ParentSubscriptionId".</span><span class="sxs-lookup"><span data-stu-id="a0560-128">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="a0560-129">Zavolejte metodu **Create** nebo **CreateAsync** .</span><span class="sxs-lookup"><span data-stu-id="a0560-129">Call the **Create** or **CreateAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a><span data-ttu-id="a0560-130">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="a0560-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a0560-131">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="a0560-131">Request syntax</span></span>

| <span data-ttu-id="a0560-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="a0560-132">Method</span></span>   | <span data-ttu-id="a0560-133">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a0560-133">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a0560-134">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="a0560-134">**POST**</span></span> | <span data-ttu-id="a0560-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a0560-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="a0560-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a0560-136">URI parameter</span></span>

<span data-ttu-id="a0560-137">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="a0560-137">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="a0560-138">Název</span><span class="sxs-lookup"><span data-stu-id="a0560-138">Name</span></span>            | <span data-ttu-id="a0560-139">Typ</span><span class="sxs-lookup"><span data-stu-id="a0560-139">Type</span></span>     | <span data-ttu-id="a0560-140">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a0560-140">Required</span></span> | <span data-ttu-id="a0560-141">Popis</span><span class="sxs-lookup"><span data-stu-id="a0560-141">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="a0560-142">**ID zákazníka**</span><span class="sxs-lookup"><span data-stu-id="a0560-142">**customer-id**</span></span> | <span data-ttu-id="a0560-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0560-143">string</span></span>   | <span data-ttu-id="a0560-144">Yes</span><span class="sxs-lookup"><span data-stu-id="a0560-144">Yes</span></span>      | <span data-ttu-id="a0560-145">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a0560-145">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="a0560-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a0560-146">Request headers</span></span>

<span data-ttu-id="a0560-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a0560-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a0560-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a0560-148">Request body</span></span>

<span data-ttu-id="a0560-149">Tato tabulka popisuje vlastnosti [košíku](cart-resources.md) v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="a0560-149">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="a0560-150">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a0560-150">Property</span></span>              | <span data-ttu-id="a0560-151">Typ</span><span class="sxs-lookup"><span data-stu-id="a0560-151">Type</span></span>             | <span data-ttu-id="a0560-152">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a0560-152">Required</span></span>        | <span data-ttu-id="a0560-153">Popis</span><span class="sxs-lookup"><span data-stu-id="a0560-153">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a0560-154">id</span><span class="sxs-lookup"><span data-stu-id="a0560-154">id</span></span>                    | <span data-ttu-id="a0560-155">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0560-155">string</span></span>           | <span data-ttu-id="a0560-156">No</span><span class="sxs-lookup"><span data-stu-id="a0560-156">No</span></span>              | <span data-ttu-id="a0560-157">Identifikátor košíku, který se zadal po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-157">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="a0560-158">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="a0560-158">creationTimeStamp</span></span>     | <span data-ttu-id="a0560-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0560-159">DateTime</span></span>         | <span data-ttu-id="a0560-160">No</span><span class="sxs-lookup"><span data-stu-id="a0560-160">No</span></span>              | <span data-ttu-id="a0560-161">Datum, kdy byl košík vytvořen, ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="a0560-161">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="a0560-162">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-162">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="a0560-163">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="a0560-163">lastModifiedTimeStamp</span></span> | <span data-ttu-id="a0560-164">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0560-164">DateTime</span></span>         | <span data-ttu-id="a0560-165">No</span><span class="sxs-lookup"><span data-stu-id="a0560-165">No</span></span>              | <span data-ttu-id="a0560-166">Datum poslední aktualizace košíku ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="a0560-166">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="a0560-167">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-167">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="a0560-168">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="a0560-168">expirationTimeStamp</span></span>   | <span data-ttu-id="a0560-169">DateTime</span><span class="sxs-lookup"><span data-stu-id="a0560-169">DateTime</span></span>         | <span data-ttu-id="a0560-170">No</span><span class="sxs-lookup"><span data-stu-id="a0560-170">No</span></span>              | <span data-ttu-id="a0560-171">Datum, kdy vyprší platnost košíku, ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="a0560-171">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="a0560-172">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-172">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="a0560-173">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="a0560-173">lastModifiedUser</span></span>      | <span data-ttu-id="a0560-174">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0560-174">string</span></span>           | <span data-ttu-id="a0560-175">No</span><span class="sxs-lookup"><span data-stu-id="a0560-175">No</span></span>              | <span data-ttu-id="a0560-176">Uživatel, který kartu naposledy aktualizoval.</span><span class="sxs-lookup"><span data-stu-id="a0560-176">The user who last updated the cart.</span></span> <span data-ttu-id="a0560-177">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-177">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="a0560-178">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="a0560-178">lineItems</span></span>             | <span data-ttu-id="a0560-179">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="a0560-179">Array of objects</span></span> | <span data-ttu-id="a0560-180">Yes</span><span class="sxs-lookup"><span data-stu-id="a0560-180">Yes</span></span>             | <span data-ttu-id="a0560-181">Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="a0560-181">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="a0560-182">Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="a0560-182">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="a0560-183">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a0560-183">Property</span></span>             | <span data-ttu-id="a0560-184">Typ</span><span class="sxs-lookup"><span data-stu-id="a0560-184">Type</span></span>                             | <span data-ttu-id="a0560-185">Description</span><span class="sxs-lookup"><span data-stu-id="a0560-185">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a0560-186">id</span><span class="sxs-lookup"><span data-stu-id="a0560-186">id</span></span>                   | <span data-ttu-id="a0560-187">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0560-187">string</span></span>                           | <span data-ttu-id="a0560-188">Jedinečný identifikátor položky řádku košíku</span><span class="sxs-lookup"><span data-stu-id="a0560-188">A unique identifier for a cart line item.</span></span> <span data-ttu-id="a0560-189">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-189">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="a0560-190">catalogId</span><span class="sxs-lookup"><span data-stu-id="a0560-190">catalogId</span></span>            | <span data-ttu-id="a0560-191">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0560-191">string</span></span>                           | <span data-ttu-id="a0560-192">Identifikátor položky katalogu</span><span class="sxs-lookup"><span data-stu-id="a0560-192">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="a0560-193">friendlyName</span><span class="sxs-lookup"><span data-stu-id="a0560-193">friendlyName</span></span>         | <span data-ttu-id="a0560-194">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0560-194">string</span></span>                           | <span data-ttu-id="a0560-195">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="a0560-195">Optional.</span></span> <span data-ttu-id="a0560-196">Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.</span><span class="sxs-lookup"><span data-stu-id="a0560-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="a0560-197">quantity</span><span class="sxs-lookup"><span data-stu-id="a0560-197">quantity</span></span>             | <span data-ttu-id="a0560-198">int</span><span class="sxs-lookup"><span data-stu-id="a0560-198">int</span></span>                              | <span data-ttu-id="a0560-199">Počet licencí nebo instancí.</span><span class="sxs-lookup"><span data-stu-id="a0560-199">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="a0560-200">currencyCode</span><span class="sxs-lookup"><span data-stu-id="a0560-200">currencyCode</span></span>         | <span data-ttu-id="a0560-201">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0560-201">string</span></span>                           | <span data-ttu-id="a0560-202">Kód měny.</span><span class="sxs-lookup"><span data-stu-id="a0560-202">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="a0560-203">billingCycle</span><span class="sxs-lookup"><span data-stu-id="a0560-203">billingCycle</span></span>         | <span data-ttu-id="a0560-204">Objekt</span><span class="sxs-lookup"><span data-stu-id="a0560-204">Object</span></span>                           | <span data-ttu-id="a0560-205">Typ fakturačního cyklu nastaveného pro aktuální období.</span><span class="sxs-lookup"><span data-stu-id="a0560-205">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="a0560-206">členům</span><span class="sxs-lookup"><span data-stu-id="a0560-206">participants</span></span>         | <span data-ttu-id="a0560-207">Seznam párů řetězců objektů</span><span class="sxs-lookup"><span data-stu-id="a0560-207">List of Object String pairs</span></span>      | <span data-ttu-id="a0560-208">Kolekce PartnerId na záznamu (MPNID) na nákupu.</span><span class="sxs-lookup"><span data-stu-id="a0560-208">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="a0560-209">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="a0560-209">provisioningContext</span></span>  | <span data-ttu-id="a0560-210">Řetězec<slovníku, řetězec></span><span class="sxs-lookup"><span data-stu-id="a0560-210">Dictionary<string, string></span></span>       | <span data-ttu-id="a0560-211">Kontext použitý ke zřízení nabídky.</span><span class="sxs-lookup"><span data-stu-id="a0560-211">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="a0560-212">pořadí</span><span class="sxs-lookup"><span data-stu-id="a0560-212">orderGroup</span></span>           | <span data-ttu-id="a0560-213">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0560-213">string</span></span>                           | <span data-ttu-id="a0560-214">Skupina, která označuje, které položky lze umístit dohromady.</span><span class="sxs-lookup"><span data-stu-id="a0560-214">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="a0560-215">addonItems</span><span class="sxs-lookup"><span data-stu-id="a0560-215">addonItems</span></span>           | <span data-ttu-id="a0560-216">Seznam objektů **CartLineItem**</span><span class="sxs-lookup"><span data-stu-id="a0560-216">List of **CartLineItem** objects</span></span> | <span data-ttu-id="a0560-217">Kolekce položek řádků košíku pro doplňky, které budou koupeny k základnímu předplatnému, které je výsledkem nákupu položky řádku nadřazeného košíku.</span><span class="sxs-lookup"><span data-stu-id="a0560-217">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="a0560-218">error</span><span class="sxs-lookup"><span data-stu-id="a0560-218">error</span></span>                | <span data-ttu-id="a0560-219">Objekt</span><span class="sxs-lookup"><span data-stu-id="a0560-219">Object</span></span>                           | <span data-ttu-id="a0560-220">Používá se po vytvoření košíku v případě chyby.</span><span class="sxs-lookup"><span data-stu-id="a0560-220">Applied after cart is created in case of an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="a0560-221">Příklad požadavku (nové základní předplatné)</span><span class="sxs-lookup"><span data-stu-id="a0560-221">Request example (new base subscription)</span></span>

<span data-ttu-id="a0560-222">Následující příklad REST ukazuje, jak vytvořit košík s položkami doplňku pro nové základní předplatné.</span><span class="sxs-lookup"><span data-stu-id="a0560-222">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="a0560-223">Příklad požadavku (stávající základní předplatné)</span><span class="sxs-lookup"><span data-stu-id="a0560-223">Request example (existing base subscription)</span></span>

<span data-ttu-id="a0560-224">Následující příklad REST ukazuje, jak připojit doplňky ke stávajícímu základnímu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="a0560-224">The following REST example show how to append add-ons to an existing base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="a0560-225">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a0560-225">REST response</span></span>

<span data-ttu-id="a0560-226">V případě úspěchu tato metoda vrátí prostředek vyplněné [vozíku](cart-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="a0560-226">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="a0560-227">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="a0560-227">Response success and error codes</span></span>

<span data-ttu-id="a0560-228">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a0560-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a0560-229">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="a0560-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a0560-230">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a0560-230">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="a0560-231">Příklad odpovědi (nové základní předplatné)</span><span class="sxs-lookup"><span data-stu-id="a0560-231">Response example (new base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="a0560-232">Příklad odpovědi (stávající základní předplatné)</span><span class="sxs-lookup"><span data-stu-id="a0560-232">Response example (existing base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
