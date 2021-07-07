---
title: Nákup položek katalogu
description: Jak zakoupit položky katalogu pomocí rozhraní API partnerského centra
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3e0deedff194b1c836d9266c2201a2b3a52cc1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445353"
---
# <a name="purchase-catalog-items"></a><span data-ttu-id="47598-103">Nákup položek katalogu</span><span class="sxs-lookup"><span data-stu-id="47598-103">Purchase catalog items</span></span>

<span data-ttu-id="47598-104">Následující scénář ukazuje obecný proces nákupu položek z katalogu pomocí rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="47598-104">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="47598-105">Zjišťování</span><span class="sxs-lookup"><span data-stu-id="47598-105">Discovery</span></span>

<span data-ttu-id="47598-106">Vyberte produkty a skladové jednotky (SKU) a ověřte jejich dostupnost pomocí následujících modelů rozhraní API partnerského centra:</span><span class="sxs-lookup"><span data-stu-id="47598-106">Select products and Stock Keeping Units (SKUs) and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="47598-107">[Produkt](product-resources.md#product) – seskupovací konstrukce pro kupní zboží nebo služby.</span><span class="sxs-lookup"><span data-stu-id="47598-107">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="47598-108">Produkt sám o sobě není položkou, která je k nákupu.</span><span class="sxs-lookup"><span data-stu-id="47598-108">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="47598-109">[SKU](product-resources.md#sku) – skladová SKU v rámci produktu.</span><span class="sxs-lookup"><span data-stu-id="47598-109">[SKU](product-resources.md#sku) - A purchasable SKU under a product.</span></span> <span data-ttu-id="47598-110">Tyto prvky jsou znázorněny v různých tvarech produktu.</span><span class="sxs-lookup"><span data-stu-id="47598-110">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="47598-111">[Dostupnost](product-resources.md#availability) – konfigurace, v níž je k DISpozici SKU k nákupu (například země, měna a odvětví).</span><span class="sxs-lookup"><span data-stu-id="47598-111">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency, and industry segment).</span></span>

<span data-ttu-id="47598-112">Pokud chcete položku zakoupit z katalogu, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="47598-112">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="47598-113">Identifikujte a načtěte produkt a SKU, které chcete koupit.</span><span class="sxs-lookup"><span data-stu-id="47598-113">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="47598-114">Získat seznam produktů</span><span class="sxs-lookup"><span data-stu-id="47598-114">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="47598-115">Získat produkt s použitím ID produktu</span><span class="sxs-lookup"><span data-stu-id="47598-115">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="47598-116">Získat seznam SKU pro produkt</span><span class="sxs-lookup"><span data-stu-id="47598-116">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="47598-117">Získání SKU pomocí ID SKU</span><span class="sxs-lookup"><span data-stu-id="47598-117">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="47598-118">Zkontroluje inventář SKU.</span><span class="sxs-lookup"><span data-stu-id="47598-118">Check the inventory for a SKU.</span></span> <span data-ttu-id="47598-119">Tento krok je potřeba jenom pro skladové položky, které jsou označené hodnotou **InventoryCheck** ve vlastnosti [purchasePrerequisites](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="47598-119">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="47598-120">Kontrola inventáře</span><span class="sxs-lookup"><span data-stu-id="47598-120">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="47598-121">Načtěte [dostupnost](product-resources.md#availability) pro [skladovou](product-resources.md#sku)položku.</span><span class="sxs-lookup"><span data-stu-id="47598-121">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="47598-122">Při zadávání objednávky budete potřebovat **CatalogItemIdi** dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="47598-122">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="47598-123">Chcete-li získat tuto hodnotu, použijte jednu z následujících rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="47598-123">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="47598-124">Získat seznam dostupnosti pro SKU</span><span class="sxs-lookup"><span data-stu-id="47598-124">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="47598-125">Získání dostupnosti pomocí ID dostupnosti</span><span class="sxs-lookup"><span data-stu-id="47598-125">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="47598-126">Odeslání objednávky</span><span class="sxs-lookup"><span data-stu-id="47598-126">Order submission</span></span>

<span data-ttu-id="47598-127">Chcete-li odeslat své pořadí položek katalogu, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="47598-127">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="47598-128">Vytvořte [košík](cart-resources.md) pro uložení kolekce položek katalogu, které máte v úmyslu koupit.</span><span class="sxs-lookup"><span data-stu-id="47598-128">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="47598-129">Při vytváření košíku se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="47598-129">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="47598-130">Vytvoření nákupního košíku</span><span class="sxs-lookup"><span data-stu-id="47598-130">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="47598-131">Aktualizace nákupního košíku</span><span class="sxs-lookup"><span data-stu-id="47598-131">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="47598-132">Podívejte se na košík.</span><span class="sxs-lookup"><span data-stu-id="47598-132">Check out the cart.</span></span> <span data-ttu-id="47598-133">Při rezervaci vozíku dojde k vytvoření [objednávky](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="47598-133">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="47598-134">Rezervace košíku</span><span class="sxs-lookup"><span data-stu-id="47598-134">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="47598-135">Získat podrobnosti objednávky</span><span class="sxs-lookup"><span data-stu-id="47598-135">Get order details</span></span>

<span data-ttu-id="47598-136">Podrobnosti o jednotlivých objednávkách můžete načíst pomocí ID objednávky nebo získat seznam objednávek pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="47598-136">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="47598-137">Mezi časem odeslání objednávky a jejím zobrazením v seznamu objednávek zákazníka nastane zpoždění až 15 minut.</span><span class="sxs-lookup"><span data-stu-id="47598-137">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="47598-138">Podrobnosti o jednotlivých objednávkách pomocí ID objednávek získáte v tématu [získání objednávky podle ID](get-an-order-by-id.md) .</span><span class="sxs-lookup"><span data-stu-id="47598-138">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="47598-139">V tématu [získání všech objednávek zákazníka](get-all-of-a-customer-s-orders.md) získáte seznam objednávek pro zákazníka pomocí zákaznického ID.</span><span class="sxs-lookup"><span data-stu-id="47598-139">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="47598-140">V tématu [získání seznamu objednávek podle zákazníka a fakturačního cyklu](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) můžete získat seznam objednávek pro zákazníka podle [typu fakturačního cyklu](product-resources.md#billingcycletype) , což vám umožní vypsat objednávky položek katalogu (jednorázové poplatky) a roční nebo měsíční Fakturované objednávky samostatně.</span><span class="sxs-lookup"><span data-stu-id="47598-140">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="47598-141">Správa životního cyklu</span><span class="sxs-lookup"><span data-stu-id="47598-141">Lifecycle management</span></span>

<span data-ttu-id="47598-142">V rámci správy životního cyklu položek katalogu v partnerském centru můžete načíst informace o vašich [nárokech](entitlement-resources.md)na položky katalogu a získat podrobnosti o rezervacích pomocí ID objednávky rezervace.</span><span class="sxs-lookup"><span data-stu-id="47598-142">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="47598-143">Příklady toho, jak to udělat, najdete v tématu [získání nároků](get-a-collection-of-entitlements.md).</span><span class="sxs-lookup"><span data-stu-id="47598-143">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="47598-144">Faktura a odsouhlasení</span><span class="sxs-lookup"><span data-stu-id="47598-144">Invoice and reconciliation</span></span>

<span data-ttu-id="47598-145">V následujících scénářích se dozvíte, jak programově zobrazit [faktury](invoice-resources.md)zákazníka a získat bilanci a souhrny účtů, které zahrnují jednorázové poplatky za katalogové položky.</span><span class="sxs-lookup"><span data-stu-id="47598-145">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="47598-146">Zůstatek a platba</span><span class="sxs-lookup"><span data-stu-id="47598-146">Balance and payment</span></span>

<span data-ttu-id="47598-147">Pokud chcete získat aktuální zůstatek k účtu ve vašem výchozím typu měny, který je saldem poplatků za periodické i jednorázové (položky katalogu), podívejte se na téma [získání aktuálního zůstatku účtu](get-the-reseller-s-current-account-balance.md).</span><span class="sxs-lookup"><span data-stu-id="47598-147">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="47598-148">Zůstatek a platba na více měn</span><span class="sxs-lookup"><span data-stu-id="47598-148">Multi-currency balance and payment</span></span>

<span data-ttu-id="47598-149">K získání aktuálního zůstatku účtu a shromáždění souhrnů faktury, které obsahují souhrn faktury s pravidelným i jednorázovým poplatkem pro každý typ měny vašeho zákazníka, najdete informace v tématu [získání souhrnů faktury](get-invoice-summaries.md).</span><span class="sxs-lookup"><span data-stu-id="47598-149">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="47598-150">Faktury</span><span class="sxs-lookup"><span data-stu-id="47598-150">Invoices</span></span>

<span data-ttu-id="47598-151">Chcete-li získat kolekci faktur, které zobrazují jak opakované, tak jednorázové poplatky, přečtěte si téma [získání kolekce faktur](get-a-collection-of-invoices.md).</span><span class="sxs-lookup"><span data-stu-id="47598-151">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="47598-152">Jedna faktura</span><span class="sxs-lookup"><span data-stu-id="47598-152">Single Invoice</span></span>

<span data-ttu-id="47598-153">Pokud chcete načíst konkrétní fakturu pomocí ID faktury, přečtěte si téma [získání faktury podle ID](get-invoice-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="47598-153">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="47598-154">Párován</span><span class="sxs-lookup"><span data-stu-id="47598-154">Reconciliation</span></span>

<span data-ttu-id="47598-155">Chcete-li získat kolekci podrobností o položce řádku faktury (položky řádku odsouhlasení) pro konkrétní ID faktury, přečtěte si téma [získání položek řádků faktury](get-invoiceline-items.md).</span><span class="sxs-lookup"><span data-stu-id="47598-155">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="47598-156">Stažení faktury jako PDF</span><span class="sxs-lookup"><span data-stu-id="47598-156">Download an invoice as a PDF</span></span>

<span data-ttu-id="47598-157">Chcete-li načíst výpis faktury ve formátu PDF pomocí ID faktury, přečtěte si téma [získání výpisu faktury](get-invoice-statement.md).</span><span class="sxs-lookup"><span data-stu-id="47598-157">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
