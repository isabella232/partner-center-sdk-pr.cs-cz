---
title: Vytvoření košíku
description: Naučte se používat rozhraní API partnerského centra k přidání objednávky pro zákazníka na vozík. Téma obsahuje informace o tom, jak vytvořit vozík a všechny požadované součásti.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a1c559b415a7d42af4e904e09795f92aed7f125f
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767127"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="fd65d-104">Vytvoření košíku s objednávkou zákazníka</span><span class="sxs-lookup"><span data-stu-id="fd65d-104">Create a cart with a customer order</span></span>

<span data-ttu-id="fd65d-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="fd65d-105">**Applies to:**</span></span>

- <span data-ttu-id="fd65d-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="fd65d-106">Partner Center</span></span>
- <span data-ttu-id="fd65d-107">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="fd65d-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="fd65d-108">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="fd65d-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fd65d-109">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fd65d-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fd65d-110">Můžete přidat objednávku pro zákazníka na vozík.</span><span class="sxs-lookup"><span data-stu-id="fd65d-110">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="fd65d-111">Další informace o tom, co je aktuálně k dispozici pro prodej, najdete [v tématu partnerské nabídky v programu Cloud Solution Provider](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="fd65d-111">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd65d-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fd65d-112">Prerequisites</span></span>

- <span data-ttu-id="fd65d-113">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fd65d-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fd65d-114">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="fd65d-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fd65d-115">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fd65d-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fd65d-116">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fd65d-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fd65d-117">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="fd65d-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fd65d-118">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="fd65d-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fd65d-119">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="fd65d-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fd65d-120">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fd65d-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="fd65d-121">C\#</span><span class="sxs-lookup"><span data-stu-id="fd65d-121">C\#</span></span>

<span data-ttu-id="fd65d-122">Vytvoření objednávky pro zákazníka:</span><span class="sxs-lookup"><span data-stu-id="fd65d-122">To create an order for a customer:</span></span>

1. <span data-ttu-id="fd65d-123">Vytvoří instanci objektu košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-123">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="fd65d-124">Vytvořte seznam objektů **CartLineItem** a přiřaďte seznam k vlastnosti položky řádku košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-124">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="fd65d-125">Každá položka řádku vozíku obsahuje informace o nákupu pro jeden produkt.</span><span class="sxs-lookup"><span data-stu-id="fd65d-125">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="fd65d-126">Musíte mít aspoň jednu položku řádku košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-126">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="fd65d-127">Získejte rozhraní k zavozíkování operací voláním metody **IAggregatePartner. Customers. ById** s ID zákazníka, které zákazníka identifikuje, a následným načtením rozhraní z vlastnosti **košíku** .</span><span class="sxs-lookup"><span data-stu-id="fd65d-127">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="fd65d-128">Voláním metody **Create** nebo **CreateAsync** vytvořte košík.</span><span class="sxs-lookup"><span data-stu-id="fd65d-128">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="fd65d-129">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="fd65d-129">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a><span data-ttu-id="fd65d-130">Java</span><span class="sxs-lookup"><span data-stu-id="fd65d-130">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="fd65d-131">Vytvoření objednávky pro zákazníka:</span><span class="sxs-lookup"><span data-stu-id="fd65d-131">To create an order for a customer:</span></span>

1. <span data-ttu-id="fd65d-132">Vytvoří instanci objektu košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-132">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="fd65d-133">Vytvoří seznam objektů **CartLineItem** a přiřadí seznam k položkám na řádku košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-133">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="fd65d-134">Každá položka řádku vozíku obsahuje informace o nákupu pro jeden produkt.</span><span class="sxs-lookup"><span data-stu-id="fd65d-134">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="fd65d-135">Musíte mít aspoň jednu položku řádku košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-135">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="fd65d-136">Získejte rozhraní k zavozíkování operací voláním funkce **IAggregatePartner. GetCustomers (). byId** s ID zákazníka pro identifikaci zákazníka a následným načtením rozhraní z funkce **getkošík** .</span><span class="sxs-lookup"><span data-stu-id="fd65d-136">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="fd65d-137">Chcete-li vytvořit košík, zavolejte funkci **Create** .</span><span class="sxs-lookup"><span data-stu-id="fd65d-137">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="fd65d-138">Příklad Java</span><span class="sxs-lookup"><span data-stu-id="fd65d-138">Java example</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a><span data-ttu-id="fd65d-139">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd65d-139">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="fd65d-140">Vytvoření objednávky pro zákazníka:</span><span class="sxs-lookup"><span data-stu-id="fd65d-140">To create an order for a customer:</span></span>

1. <span data-ttu-id="fd65d-141">Vytvoří instanci objektu košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-141">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="fd65d-142">Vytvoří seznam objektů **CartLineItem** a přiřadí seznam k položkám na řádku košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-142">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="fd65d-143">Každá položka řádku vozíku obsahuje informace o nákupu pro jeden produkt.</span><span class="sxs-lookup"><span data-stu-id="fd65d-143">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="fd65d-144">Musíte mít aspoň jednu položku řádku košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-144">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="fd65d-145">Spuštěním příkazu [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) vytvořte košík.</span><span class="sxs-lookup"><span data-stu-id="fd65d-145">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a><span data-ttu-id="fd65d-146">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fd65d-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fd65d-147">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fd65d-147">Request syntax</span></span>

| <span data-ttu-id="fd65d-148">Metoda</span><span class="sxs-lookup"><span data-stu-id="fd65d-148">Method</span></span>   | <span data-ttu-id="fd65d-149">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fd65d-149">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fd65d-150">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="fd65d-150">**POST**</span></span> | <span data-ttu-id="fd65d-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fd65d-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="fd65d-152">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fd65d-152">URI parameter</span></span>

<span data-ttu-id="fd65d-153">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="fd65d-153">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="fd65d-154">Název</span><span class="sxs-lookup"><span data-stu-id="fd65d-154">Name</span></span>            | <span data-ttu-id="fd65d-155">Typ</span><span class="sxs-lookup"><span data-stu-id="fd65d-155">Type</span></span>     | <span data-ttu-id="fd65d-156">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fd65d-156">Required</span></span> | <span data-ttu-id="fd65d-157">Popis</span><span class="sxs-lookup"><span data-stu-id="fd65d-157">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="fd65d-158">**ID zákazníka**</span><span class="sxs-lookup"><span data-stu-id="fd65d-158">**customer-id**</span></span> | <span data-ttu-id="fd65d-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-159">string</span></span>   | <span data-ttu-id="fd65d-160">Yes</span><span class="sxs-lookup"><span data-stu-id="fd65d-160">Yes</span></span>      | <span data-ttu-id="fd65d-161">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fd65d-161">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="fd65d-162">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fd65d-162">Request headers</span></span>

<span data-ttu-id="fd65d-163">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fd65d-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fd65d-164">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fd65d-164">Request body</span></span>

<span data-ttu-id="fd65d-165">Tato tabulka popisuje vlastnosti [košíku](cart-resources.md) v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="fd65d-165">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="fd65d-166">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fd65d-166">Property</span></span>              | <span data-ttu-id="fd65d-167">Typ</span><span class="sxs-lookup"><span data-stu-id="fd65d-167">Type</span></span>             | <span data-ttu-id="fd65d-168">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fd65d-168">Required</span></span>        | <span data-ttu-id="fd65d-169">Popis</span><span class="sxs-lookup"><span data-stu-id="fd65d-169">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fd65d-170">id</span><span class="sxs-lookup"><span data-stu-id="fd65d-170">id</span></span>                    | <span data-ttu-id="fd65d-171">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-171">string</span></span>           | <span data-ttu-id="fd65d-172">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-172">No</span></span>              | <span data-ttu-id="fd65d-173">Identifikátor košíku, který se zadal po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-173">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="fd65d-174">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="fd65d-174">creationTimeStamp</span></span>     | <span data-ttu-id="fd65d-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="fd65d-175">DateTime</span></span>         | <span data-ttu-id="fd65d-176">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-176">No</span></span>              | <span data-ttu-id="fd65d-177">Datum, kdy byl košík vytvořen, ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="fd65d-177">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="fd65d-178">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-178">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="fd65d-179">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="fd65d-179">lastModifiedTimeStamp</span></span> | <span data-ttu-id="fd65d-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="fd65d-180">DateTime</span></span>         | <span data-ttu-id="fd65d-181">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-181">No</span></span>              | <span data-ttu-id="fd65d-182">Datum poslední aktualizace košíku ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="fd65d-182">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="fd65d-183">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-183">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="fd65d-184">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="fd65d-184">expirationTimeStamp</span></span>   | <span data-ttu-id="fd65d-185">DateTime</span><span class="sxs-lookup"><span data-stu-id="fd65d-185">DateTime</span></span>         | <span data-ttu-id="fd65d-186">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-186">No</span></span>              | <span data-ttu-id="fd65d-187">Datum, kdy vyprší platnost košíku, ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="fd65d-187">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="fd65d-188">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-188">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="fd65d-189">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="fd65d-189">lastModifiedUser</span></span>      | <span data-ttu-id="fd65d-190">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-190">string</span></span>           | <span data-ttu-id="fd65d-191">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-191">No</span></span>              | <span data-ttu-id="fd65d-192">Uživatel, který kartu naposledy aktualizoval.</span><span class="sxs-lookup"><span data-stu-id="fd65d-192">The user who last updated the cart.</span></span> <span data-ttu-id="fd65d-193">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-193">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="fd65d-194">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="fd65d-194">lineItems</span></span>             | <span data-ttu-id="fd65d-195">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="fd65d-195">Array of objects</span></span> | <span data-ttu-id="fd65d-196">Yes</span><span class="sxs-lookup"><span data-stu-id="fd65d-196">Yes</span></span>             | <span data-ttu-id="fd65d-197">Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="fd65d-197">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="fd65d-198">Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-198">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="fd65d-199">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fd65d-199">Property</span></span>       |            <span data-ttu-id="fd65d-200">Typ</span><span class="sxs-lookup"><span data-stu-id="fd65d-200">Type</span></span>             | <span data-ttu-id="fd65d-201">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fd65d-201">Required</span></span> |                                                                                         <span data-ttu-id="fd65d-202">Popis</span><span class="sxs-lookup"><span data-stu-id="fd65d-202">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="fd65d-203">id</span><span class="sxs-lookup"><span data-stu-id="fd65d-203">id</span></span>          |           <span data-ttu-id="fd65d-204">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-204">string</span></span>            |    <span data-ttu-id="fd65d-205">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-205">No</span></span>    |                                                     <span data-ttu-id="fd65d-206">Jedinečný identifikátor položky řádku košíku</span><span class="sxs-lookup"><span data-stu-id="fd65d-206">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="fd65d-207">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-207">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="fd65d-208">catalogId</span><span class="sxs-lookup"><span data-stu-id="fd65d-208">catalogId</span></span>      |           <span data-ttu-id="fd65d-209">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-209">string</span></span>            |   <span data-ttu-id="fd65d-210">Yes</span><span class="sxs-lookup"><span data-stu-id="fd65d-210">Yes</span></span>    |                                                                                <span data-ttu-id="fd65d-211">Identifikátor položky katalogu</span><span class="sxs-lookup"><span data-stu-id="fd65d-211">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="fd65d-212">friendlyName</span><span class="sxs-lookup"><span data-stu-id="fd65d-212">friendlyName</span></span>     |           <span data-ttu-id="fd65d-213">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-213">string</span></span>            |    <span data-ttu-id="fd65d-214">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-214">No</span></span>    |                                                    <span data-ttu-id="fd65d-215">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="fd65d-215">Optional.</span></span> <span data-ttu-id="fd65d-216">Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.</span><span class="sxs-lookup"><span data-stu-id="fd65d-216">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="fd65d-217">quantity</span><span class="sxs-lookup"><span data-stu-id="fd65d-217">quantity</span></span>       |             <span data-ttu-id="fd65d-218">int</span><span class="sxs-lookup"><span data-stu-id="fd65d-218">int</span></span>             |   <span data-ttu-id="fd65d-219">Yes</span><span class="sxs-lookup"><span data-stu-id="fd65d-219">Yes</span></span>    |                                                                            <span data-ttu-id="fd65d-220">Počet licencí nebo instancí.</span><span class="sxs-lookup"><span data-stu-id="fd65d-220">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="fd65d-221">currencyCode</span><span class="sxs-lookup"><span data-stu-id="fd65d-221">currencyCode</span></span>     |           <span data-ttu-id="fd65d-222">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-222">string</span></span>            |    <span data-ttu-id="fd65d-223">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-223">No</span></span>    |                                                                                     <span data-ttu-id="fd65d-224">Kód měny.</span><span class="sxs-lookup"><span data-stu-id="fd65d-224">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="fd65d-225">billingCycle</span><span class="sxs-lookup"><span data-stu-id="fd65d-225">billingCycle</span></span>     |           <span data-ttu-id="fd65d-226">Objekt</span><span class="sxs-lookup"><span data-stu-id="fd65d-226">Object</span></span>            |   <span data-ttu-id="fd65d-227">Yes</span><span class="sxs-lookup"><span data-stu-id="fd65d-227">Yes</span></span>    |                                                                    <span data-ttu-id="fd65d-228">Typ fakturačního cyklu nastaveného pro aktuální období.</span><span class="sxs-lookup"><span data-stu-id="fd65d-228">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="fd65d-229">členům</span><span class="sxs-lookup"><span data-stu-id="fd65d-229">participants</span></span>     | <span data-ttu-id="fd65d-230">Seznam párů řetězců objektů</span><span class="sxs-lookup"><span data-stu-id="fd65d-230">List of Object String pairs</span></span> |    <span data-ttu-id="fd65d-231">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-231">No</span></span>    |                                                                <span data-ttu-id="fd65d-232">Kolekce PartnerId na záznamu (MPNID) na nákupu.</span><span class="sxs-lookup"><span data-stu-id="fd65d-232">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="fd65d-233">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="fd65d-233">provisioningContext</span></span> | <span data-ttu-id="fd65d-234">Řetězec<slovníku, řetězec></span><span class="sxs-lookup"><span data-stu-id="fd65d-234">Dictionary<string, string></span></span>  |    <span data-ttu-id="fd65d-235">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-235">No</span></span>    | <span data-ttu-id="fd65d-236">Informace požadované pro zřizování některých položek v katalogu.</span><span class="sxs-lookup"><span data-stu-id="fd65d-236">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="fd65d-237">Vlastnost provisioningVariables v SKU indikuje, které vlastnosti jsou požadovány pro konkrétní položky v katalogu.</span><span class="sxs-lookup"><span data-stu-id="fd65d-237">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="fd65d-238">pořadí</span><span class="sxs-lookup"><span data-stu-id="fd65d-238">orderGroup</span></span>      |           <span data-ttu-id="fd65d-239">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-239">string</span></span>            |    <span data-ttu-id="fd65d-240">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-240">No</span></span>    |                                                                   <span data-ttu-id="fd65d-241">Skupina, která označuje, které položky lze umístit dohromady.</span><span class="sxs-lookup"><span data-stu-id="fd65d-241">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="fd65d-242">error</span><span class="sxs-lookup"><span data-stu-id="fd65d-242">error</span></span>        |           <span data-ttu-id="fd65d-243">Objekt</span><span class="sxs-lookup"><span data-stu-id="fd65d-243">Object</span></span>            |    <span data-ttu-id="fd65d-244">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-244">No</span></span>    |                                                                     <span data-ttu-id="fd65d-245">Používá se po vytvoření košíku v případě chyby.</span><span class="sxs-lookup"><span data-stu-id="fd65d-245">Applied after cart is created in case of an error.</span></span>                                                                      |
|     <span data-ttu-id="fd65d-246">renewsTo</span><span class="sxs-lookup"><span data-stu-id="fd65d-246">renewsTo</span></span>        | <span data-ttu-id="fd65d-247">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="fd65d-247">Array of objects</span></span>            |    <span data-ttu-id="fd65d-248">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-248">No</span></span>    |                                                    <span data-ttu-id="fd65d-249">Pole prostředků [RenewsTo](cart-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="fd65d-249">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="fd65d-250">Tato tabulka popisuje vlastnosti [RenewsTo](cart-resources.md#renewsto) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="fd65d-250">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="fd65d-251">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fd65d-251">Property</span></span>              | <span data-ttu-id="fd65d-252">Typ</span><span class="sxs-lookup"><span data-stu-id="fd65d-252">Type</span></span>             | <span data-ttu-id="fd65d-253">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fd65d-253">Required</span></span>        | <span data-ttu-id="fd65d-254">Popis</span><span class="sxs-lookup"><span data-stu-id="fd65d-254">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fd65d-255">termDuration</span><span class="sxs-lookup"><span data-stu-id="fd65d-255">termDuration</span></span>          | <span data-ttu-id="fd65d-256">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd65d-256">string</span></span>           | <span data-ttu-id="fd65d-257">No</span><span class="sxs-lookup"><span data-stu-id="fd65d-257">No</span></span>              | <span data-ttu-id="fd65d-258">ISO 8601 představuje dobu trvání období obnovy.</span><span class="sxs-lookup"><span data-stu-id="fd65d-258">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="fd65d-259">Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok).</span><span class="sxs-lookup"><span data-stu-id="fd65d-259">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="fd65d-260">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fd65d-260">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="fd65d-261">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fd65d-261">REST response</span></span>

<span data-ttu-id="fd65d-262">V případě úspěchu tato metoda vrátí prostředek vyplněné [vozíku](cart-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="fd65d-262">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fd65d-263">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fd65d-263">Response success and error codes</span></span>

<span data-ttu-id="fd65d-264">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fd65d-264">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fd65d-265">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fd65d-265">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fd65d-266">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fd65d-266">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fd65d-267">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fd65d-267">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
