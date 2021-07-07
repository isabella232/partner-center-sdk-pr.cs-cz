---
title: Vytvoření košíku s doplňky
description: Naučte se používat Partnerské centrum API k přidání objednávky zákazníka s doplňky prostřednictvím košíku. Článek obsahuje požadavky a kroky pro vytvoření košíku s doplňky.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 513a9607b9194c36253630c91de9622325317c3a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973753"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="813e4-104">Vytvoření košíku s doplňky k objednávce zákazníka</span><span class="sxs-lookup"><span data-stu-id="813e4-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="813e4-105">Doplňky si můžete koupit prostřednictvím košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-105">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="813e4-106">Další informace o tom, co je aktuálně k dispozici k prodeji, najdete v tématu Nabídky partnerů [v Cloud Solution Provider programu](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="813e4-106">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="813e4-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="813e4-107">Prerequisites</span></span>

- <span data-ttu-id="813e4-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="813e4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="813e4-109">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="813e4-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="813e4-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="813e4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="813e4-111">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="813e4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="813e4-112">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="813e4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="813e4-113">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="813e4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="813e4-114">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="813e4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="813e4-115">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="813e4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="813e4-116">C\#</span><span class="sxs-lookup"><span data-stu-id="813e4-116">C\#</span></span>

<span data-ttu-id="813e4-117">Košík umožňuje nákup základní nabídky a odpovídajících doplňků.</span><span class="sxs-lookup"><span data-stu-id="813e4-117">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="813e4-118">Při vytváření košíku postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="813e4-118">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="813e4-119">Vytvoření instance objektu [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart)</span><span class="sxs-lookup"><span data-stu-id="813e4-119">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="813e4-120">Vytvořte seznam objektů [**CartLineItem,**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) které představují základní nabídky, a přiřaďte tento seznam k vlastnosti [**LineItems košíku.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)</span><span class="sxs-lookup"><span data-stu-id="813e4-120">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects that represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="813e4-121">Pod řádkovou položkou košíku každé základní nabídky naplňte seznam **AddOnItems** jinými objekty **CartLineItem,** které představují doplněk, který bude zakoupen na základě této základní nabídky.</span><span class="sxs-lookup"><span data-stu-id="813e4-121">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="813e4-122">Získejte rozhraní pro operace košíku pomocí [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) k volání metody [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka a načtením rozhraní z vlastnosti **Cart.**</span><span class="sxs-lookup"><span data-stu-id="813e4-122">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="813e4-123">Nakonec zavolejte [**metodu Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) a vytvořte košík.</span><span class="sxs-lookup"><span data-stu-id="813e4-123">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="813e4-124">Příklad \# jazyka C</span><span class="sxs-lookup"><span data-stu-id="813e4-124">C\# example</span></span>

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

<span data-ttu-id="813e4-125">Postupujte podle těchto kroků a vytvořte košík, který umožní nákup doplňků pro stávající základní předplatná:</span><span class="sxs-lookup"><span data-stu-id="813e4-125">Follow these steps to create a cart that will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="813e4-126">Vytvořte košík **s** novým **CartLineItem** obsahujícím ID předplatného ve vlastnosti **ProvisioningContext** s klíčem ParentSubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="813e4-126">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="813e4-127">Zavolejte **metodu Create** nebo **CreateAsync.**</span><span class="sxs-lookup"><span data-stu-id="813e4-127">Call the **Create** or **CreateAsync** method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="813e4-128">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="813e4-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="813e4-129">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="813e4-129">Request syntax</span></span>

| <span data-ttu-id="813e4-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="813e4-130">Method</span></span>   | <span data-ttu-id="813e4-131">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="813e4-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="813e4-132">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="813e4-132">**POST**</span></span> | <span data-ttu-id="813e4-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="813e4-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="813e4-134">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="813e4-134">URI parameter</span></span>

<span data-ttu-id="813e4-135">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="813e4-135">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="813e4-136">Název</span><span class="sxs-lookup"><span data-stu-id="813e4-136">Name</span></span>            | <span data-ttu-id="813e4-137">Typ</span><span class="sxs-lookup"><span data-stu-id="813e4-137">Type</span></span>     | <span data-ttu-id="813e4-138">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="813e4-138">Required</span></span> | <span data-ttu-id="813e4-139">Popis</span><span class="sxs-lookup"><span data-stu-id="813e4-139">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="813e4-140">**id zákazníka**</span><span class="sxs-lookup"><span data-stu-id="813e4-140">**customer-id**</span></span> | <span data-ttu-id="813e4-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="813e4-141">string</span></span>   | <span data-ttu-id="813e4-142">Yes</span><span class="sxs-lookup"><span data-stu-id="813e4-142">Yes</span></span>      | <span data-ttu-id="813e4-143">Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="813e4-143">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="813e4-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="813e4-144">Request headers</span></span>

<span data-ttu-id="813e4-145">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="813e4-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="813e4-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="813e4-146">Request body</span></span>

<span data-ttu-id="813e4-147">Tato tabulka popisuje vlastnosti [Cart](cart-resources.md) (Košík) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="813e4-147">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="813e4-148">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="813e4-148">Property</span></span>              | <span data-ttu-id="813e4-149">Typ</span><span class="sxs-lookup"><span data-stu-id="813e4-149">Type</span></span>             | <span data-ttu-id="813e4-150">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="813e4-150">Required</span></span>        | <span data-ttu-id="813e4-151">Popis</span><span class="sxs-lookup"><span data-stu-id="813e4-151">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="813e4-152">id</span><span class="sxs-lookup"><span data-stu-id="813e4-152">id</span></span>                    | <span data-ttu-id="813e4-153">řetězec</span><span class="sxs-lookup"><span data-stu-id="813e4-153">string</span></span>           | <span data-ttu-id="813e4-154">No</span><span class="sxs-lookup"><span data-stu-id="813e4-154">No</span></span>              | <span data-ttu-id="813e4-155">Identifikátor košíku, který se dodá po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-155">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="813e4-156">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="813e4-156">creationTimeStamp</span></span>     | <span data-ttu-id="813e4-157">DateTime</span><span class="sxs-lookup"><span data-stu-id="813e4-157">DateTime</span></span>         | <span data-ttu-id="813e4-158">No</span><span class="sxs-lookup"><span data-stu-id="813e4-158">No</span></span>              | <span data-ttu-id="813e4-159">Datum vytvoření košíku ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="813e4-159">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="813e4-160">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-160">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="813e4-161">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="813e4-161">lastModifiedTimeStamp</span></span> | <span data-ttu-id="813e4-162">DateTime</span><span class="sxs-lookup"><span data-stu-id="813e4-162">DateTime</span></span>         | <span data-ttu-id="813e4-163">No</span><span class="sxs-lookup"><span data-stu-id="813e4-163">No</span></span>              | <span data-ttu-id="813e4-164">Datum poslední aktualizace košíku ve formátu data a času</span><span class="sxs-lookup"><span data-stu-id="813e4-164">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="813e4-165">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-165">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="813e4-166">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="813e4-166">expirationTimeStamp</span></span>   | <span data-ttu-id="813e4-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="813e4-167">DateTime</span></span>         | <span data-ttu-id="813e4-168">No</span><span class="sxs-lookup"><span data-stu-id="813e4-168">No</span></span>              | <span data-ttu-id="813e4-169">Datum, kdy vyprší platnost košíku ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="813e4-169">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="813e4-170">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-170">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="813e4-171">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="813e4-171">lastModifiedUser</span></span>      | <span data-ttu-id="813e4-172">řetězec</span><span class="sxs-lookup"><span data-stu-id="813e4-172">string</span></span>           | <span data-ttu-id="813e4-173">No</span><span class="sxs-lookup"><span data-stu-id="813e4-173">No</span></span>              | <span data-ttu-id="813e4-174">Uživatel, který naposledy aktualizoval košík</span><span class="sxs-lookup"><span data-stu-id="813e4-174">The user who last updated the cart.</span></span> <span data-ttu-id="813e4-175">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-175">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="813e4-176">položky řádku</span><span class="sxs-lookup"><span data-stu-id="813e4-176">lineItems</span></span>             | <span data-ttu-id="813e4-177">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="813e4-177">Array of objects</span></span> | <span data-ttu-id="813e4-178">Yes</span><span class="sxs-lookup"><span data-stu-id="813e4-178">Yes</span></span>             | <span data-ttu-id="813e4-179">Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="813e4-179">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="813e4-180">Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="813e4-180">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="813e4-181">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="813e4-181">Property</span></span>             | <span data-ttu-id="813e4-182">Typ</span><span class="sxs-lookup"><span data-stu-id="813e4-182">Type</span></span>                             | <span data-ttu-id="813e4-183">Description</span><span class="sxs-lookup"><span data-stu-id="813e4-183">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="813e4-184">id</span><span class="sxs-lookup"><span data-stu-id="813e4-184">id</span></span>                   | <span data-ttu-id="813e4-185">řetězec</span><span class="sxs-lookup"><span data-stu-id="813e4-185">string</span></span>                           | <span data-ttu-id="813e4-186">Jedinečný identifikátor řádkové položky košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-186">A unique identifier for a cart line item.</span></span> <span data-ttu-id="813e4-187">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-187">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="813e4-188">id katalogu</span><span class="sxs-lookup"><span data-stu-id="813e4-188">catalogId</span></span>            | <span data-ttu-id="813e4-189">řetězec</span><span class="sxs-lookup"><span data-stu-id="813e4-189">string</span></span>                           | <span data-ttu-id="813e4-190">Identifikátor položky katalogu.</span><span class="sxs-lookup"><span data-stu-id="813e4-190">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="813e4-191">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="813e4-191">friendlyName</span></span>         | <span data-ttu-id="813e4-192">řetězec</span><span class="sxs-lookup"><span data-stu-id="813e4-192">string</span></span>                           | <span data-ttu-id="813e4-193">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="813e4-193">Optional.</span></span> <span data-ttu-id="813e4-194">Popisný název položky definované partnerem, který pomáhá jednoznačně rozpoznat.</span><span class="sxs-lookup"><span data-stu-id="813e4-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="813e4-195">quantity</span><span class="sxs-lookup"><span data-stu-id="813e4-195">quantity</span></span>             | <span data-ttu-id="813e4-196">int</span><span class="sxs-lookup"><span data-stu-id="813e4-196">int</span></span>                              | <span data-ttu-id="813e4-197">Počet licencí nebo instancí</span><span class="sxs-lookup"><span data-stu-id="813e4-197">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="813e4-198">currencyCode</span><span class="sxs-lookup"><span data-stu-id="813e4-198">currencyCode</span></span>         | <span data-ttu-id="813e4-199">řetězec</span><span class="sxs-lookup"><span data-stu-id="813e4-199">string</span></span>                           | <span data-ttu-id="813e4-200">Kód měny</span><span class="sxs-lookup"><span data-stu-id="813e4-200">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="813e4-201">billingCycle</span><span class="sxs-lookup"><span data-stu-id="813e4-201">billingCycle</span></span>         | <span data-ttu-id="813e4-202">Objekt</span><span class="sxs-lookup"><span data-stu-id="813e4-202">Object</span></span>                           | <span data-ttu-id="813e4-203">Typ fakturačního cyklu nastaveného pro aktuální období.</span><span class="sxs-lookup"><span data-stu-id="813e4-203">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="813e4-204">členům</span><span class="sxs-lookup"><span data-stu-id="813e4-204">participants</span></span>         | <span data-ttu-id="813e4-205">Seznam párů řetězců objektů</span><span class="sxs-lookup"><span data-stu-id="813e4-205">List of Object String pairs</span></span>      | <span data-ttu-id="813e4-206">Kolekce PartnerId na záznamu (MPN ID) na nákupu.</span><span class="sxs-lookup"><span data-stu-id="813e4-206">A collection of PartnerId on Record (MPN ID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="813e4-207">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="813e4-207">provisioningContext</span></span>  | <span data-ttu-id="813e4-208">Řetězec<slovníku, řetězec></span><span class="sxs-lookup"><span data-stu-id="813e4-208">Dictionary<string, string></span></span>       | <span data-ttu-id="813e4-209">Kontext použitý ke zřízení nabídky.</span><span class="sxs-lookup"><span data-stu-id="813e4-209">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="813e4-210">pořadí</span><span class="sxs-lookup"><span data-stu-id="813e4-210">orderGroup</span></span>           | <span data-ttu-id="813e4-211">řetězec</span><span class="sxs-lookup"><span data-stu-id="813e4-211">string</span></span>                           | <span data-ttu-id="813e4-212">Skupina, která označuje, které položky lze umístit dohromady.</span><span class="sxs-lookup"><span data-stu-id="813e4-212">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="813e4-213">addonItems</span><span class="sxs-lookup"><span data-stu-id="813e4-213">addonItems</span></span>           | <span data-ttu-id="813e4-214">Seznam objektů **CartLineItem**</span><span class="sxs-lookup"><span data-stu-id="813e4-214">List of **CartLineItem** objects</span></span> | <span data-ttu-id="813e4-215">Kolekce položek řádků košíku pro doplňky, které budou koupeny k základnímu předplatnému, které je výsledkem nákupu položky řádku nadřazeného košíku.</span><span class="sxs-lookup"><span data-stu-id="813e4-215">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="813e4-216">error</span><span class="sxs-lookup"><span data-stu-id="813e4-216">error</span></span>                | <span data-ttu-id="813e4-217">Objekt</span><span class="sxs-lookup"><span data-stu-id="813e4-217">Object</span></span>                           | <span data-ttu-id="813e4-218">Používá se po vytvoření košíku, pokud dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="813e4-218">Applied after cart is created if there is an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="813e4-219">Příklad požadavku (nové základní předplatné)</span><span class="sxs-lookup"><span data-stu-id="813e4-219">Request example (new base subscription)</span></span>

<span data-ttu-id="813e4-220">Následující příklad REST ukazuje, jak vytvořit košík s položkami doplňku pro nové základní předplatné.</span><span class="sxs-lookup"><span data-stu-id="813e4-220">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

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

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="813e4-221">Příklad požadavku (stávající základní předplatné)</span><span class="sxs-lookup"><span data-stu-id="813e4-221">Request example (existing base subscription)</span></span>

<span data-ttu-id="813e4-222">Následující příklad REST ukazuje, jak připojit doplňky ke stávajícímu základnímu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="813e4-222">The following REST example shows how to append add-ons to an existing base subscription.</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="813e4-223">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="813e4-223">REST response</span></span>

<span data-ttu-id="813e4-224">V případě úspěchu tato metoda vrátí prostředek vyplněné [vozíku](cart-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="813e4-224">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="813e4-225">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="813e4-225">Response success and error codes</span></span>

<span data-ttu-id="813e4-226">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="813e4-226">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="813e4-227">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="813e4-227">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="813e4-228">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="813e4-228">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="813e4-229">Příklad odpovědi (nové základní předplatné)</span><span class="sxs-lookup"><span data-stu-id="813e4-229">Response example (new base subscription)</span></span>

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

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="813e4-230">Příklad odpovědi (stávající základní předplatné)</span><span class="sxs-lookup"><span data-stu-id="813e4-230">Response example (existing base subscription)</span></span>

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
