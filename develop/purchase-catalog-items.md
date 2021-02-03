---
title: Nákup položek katalogu
description: Jak zakoupit položky katalogu pomocí rozhraní API partnerského centra
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2b3a34cdb6b29cb7eaaf5d977e4588f538fff09
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766712"
---
# <a name="purchase-catalog-items"></a><span data-ttu-id="9ea29-103">Nákup položek katalogu</span><span class="sxs-lookup"><span data-stu-id="9ea29-103">Purchase catalog items</span></span>

<span data-ttu-id="9ea29-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="9ea29-104">**Applies To**</span></span>

- <span data-ttu-id="9ea29-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="9ea29-105">Partner Center</span></span>

<span data-ttu-id="9ea29-106">Následující scénář ukazuje obecný proces nákupu položek z katalogu pomocí rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="9ea29-106">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="9ea29-107">Zjišťování</span><span class="sxs-lookup"><span data-stu-id="9ea29-107">Discovery</span></span>

<span data-ttu-id="9ea29-108">Vyberte produkty a SKU a ověřte jejich dostupnost pomocí následujících modelů rozhraní API partnerského centra:</span><span class="sxs-lookup"><span data-stu-id="9ea29-108">Select products and SKUs and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="9ea29-109">[Produkt](product-resources.md#product) – seskupovací konstrukce pro kupní zboží nebo služby.</span><span class="sxs-lookup"><span data-stu-id="9ea29-109">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="9ea29-110">Produkt sám o sobě není položkou, která je k nákupu.</span><span class="sxs-lookup"><span data-stu-id="9ea29-110">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="9ea29-111">[SKU](product-resources.md#sku) – skladová jednotka (SKU), která je v rámci produktu kupní.</span><span class="sxs-lookup"><span data-stu-id="9ea29-111">[SKU](product-resources.md#sku) - A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="9ea29-112">Tyto prvky jsou znázorněny v různých tvarech produktu.</span><span class="sxs-lookup"><span data-stu-id="9ea29-112">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="9ea29-113">[Dostupnost](product-resources.md#availability) – konfigurace, v níž je k dispozici skladová položka k nákupu (například země, měna a oborové segmenty).</span><span class="sxs-lookup"><span data-stu-id="9ea29-113">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency and industry segment).</span></span>

<span data-ttu-id="9ea29-114">Pokud chcete položku zakoupit z katalogu, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="9ea29-114">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="9ea29-115">Identifikujte a načtěte produkt a SKU, které chcete koupit.</span><span class="sxs-lookup"><span data-stu-id="9ea29-115">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="9ea29-116">Získat seznam produktů</span><span class="sxs-lookup"><span data-stu-id="9ea29-116">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="9ea29-117">Získat produkt s použitím ID produktu</span><span class="sxs-lookup"><span data-stu-id="9ea29-117">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="9ea29-118">Získat seznam SKU pro produkt</span><span class="sxs-lookup"><span data-stu-id="9ea29-118">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="9ea29-119">Získání SKU pomocí ID SKU</span><span class="sxs-lookup"><span data-stu-id="9ea29-119">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="9ea29-120">Zkontroluje inventář SKU.</span><span class="sxs-lookup"><span data-stu-id="9ea29-120">Check the inventory for a SKU.</span></span> <span data-ttu-id="9ea29-121">Tento krok je potřeba jenom pro skladové položky, které jsou označené hodnotou **InventoryCheck** ve vlastnosti [purchasePrerequisites](product-resources.md#sku) .</span><span class="sxs-lookup"><span data-stu-id="9ea29-121">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="9ea29-122">Kontrola inventáře</span><span class="sxs-lookup"><span data-stu-id="9ea29-122">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="9ea29-123">Načtěte [dostupnost](product-resources.md#availability) pro [skladovou](product-resources.md#sku)položku.</span><span class="sxs-lookup"><span data-stu-id="9ea29-123">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="9ea29-124">Při zadávání objednávky budete potřebovat **CatalogItemIdi** dostupnosti.</span><span class="sxs-lookup"><span data-stu-id="9ea29-124">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="9ea29-125">Chcete-li získat tuto hodnotu, použijte jednu z následujících rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="9ea29-125">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="9ea29-126">Získat seznam dostupnosti pro SKU</span><span class="sxs-lookup"><span data-stu-id="9ea29-126">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="9ea29-127">Získání dostupnosti pomocí ID dostupnosti</span><span class="sxs-lookup"><span data-stu-id="9ea29-127">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="9ea29-128">Odeslání objednávky</span><span class="sxs-lookup"><span data-stu-id="9ea29-128">Order submission</span></span>

<span data-ttu-id="9ea29-129">Chcete-li odeslat své pořadí položek katalogu, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="9ea29-129">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="9ea29-130">Vytvořte [košík](cart-resources.md) pro uložení kolekce položek katalogu, které máte v úmyslu koupit.</span><span class="sxs-lookup"><span data-stu-id="9ea29-130">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="9ea29-131">Při vytváření košíku se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-131">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="9ea29-132">Vytvoření nákupního košíku</span><span class="sxs-lookup"><span data-stu-id="9ea29-132">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="9ea29-133">Aktualizace nákupního košíku</span><span class="sxs-lookup"><span data-stu-id="9ea29-133">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="9ea29-134">Podívejte se na košík.</span><span class="sxs-lookup"><span data-stu-id="9ea29-134">Check out the cart.</span></span> <span data-ttu-id="9ea29-135">Při rezervaci vozíku dojde k vytvoření [objednávky](order-resources.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-135">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="9ea29-136">Rezervace košíku</span><span class="sxs-lookup"><span data-stu-id="9ea29-136">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="9ea29-137">Získat podrobnosti objednávky</span><span class="sxs-lookup"><span data-stu-id="9ea29-137">Get order details</span></span>

<span data-ttu-id="9ea29-138">Podrobnosti o jednotlivých objednávkách můžete načíst pomocí ID objednávky nebo získat seznam objednávek pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9ea29-138">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="9ea29-139">Mezi časem odeslání objednávky a jejím zobrazením v seznamu objednávek zákazníka nastane zpoždění až 15 minut.</span><span class="sxs-lookup"><span data-stu-id="9ea29-139">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="9ea29-140">Podrobnosti o jednotlivých objednávkách pomocí ID objednávek získáte v tématu [získání objednávky podle ID](get-an-order-by-id.md) .</span><span class="sxs-lookup"><span data-stu-id="9ea29-140">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="9ea29-141">V tématu [získání všech objednávek zákazníka](get-all-of-a-customer-s-orders.md) získáte seznam objednávek pro zákazníka pomocí zákaznického ID.</span><span class="sxs-lookup"><span data-stu-id="9ea29-141">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="9ea29-142">V tématu [získání seznamu objednávek podle zákazníka a fakturačního cyklu](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) můžete získat seznam objednávek pro zákazníka podle [typu fakturačního cyklu](product-resources.md#billingcycletype) , což vám umožní vypsat objednávky položek katalogu (jednorázové poplatky) a roční nebo měsíční Fakturované objednávky samostatně.</span><span class="sxs-lookup"><span data-stu-id="9ea29-142">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="9ea29-143">Správa životního cyklu</span><span class="sxs-lookup"><span data-stu-id="9ea29-143">Lifecycle management</span></span>

<span data-ttu-id="9ea29-144">V rámci správy životního cyklu položek katalogu v partnerském centru můžete načíst informace o vašich [nárokech](entitlement-resources.md)na položky katalogu a získat podrobnosti o rezervacích pomocí ID objednávky rezervace.</span><span class="sxs-lookup"><span data-stu-id="9ea29-144">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="9ea29-145">Příklady toho, jak to udělat, najdete v tématu [získání nároků](get-a-collection-of-entitlements.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-145">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="9ea29-146">Faktura a odsouhlasení</span><span class="sxs-lookup"><span data-stu-id="9ea29-146">Invoice and reconciliation</span></span>

<span data-ttu-id="9ea29-147">V následujících scénářích se dozvíte, jak programově zobrazit [faktury](invoice-resources.md)zákazníka a získat bilanci a souhrny účtů, které zahrnují jednorázové poplatky za katalogové položky.</span><span class="sxs-lookup"><span data-stu-id="9ea29-147">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="9ea29-148">Zůstatek a platba</span><span class="sxs-lookup"><span data-stu-id="9ea29-148">Balance and payment</span></span>

<span data-ttu-id="9ea29-149">Pokud chcete získat aktuální zůstatek k účtu ve vašem výchozím typu měny, který je saldem poplatků za periodické i jednorázové (položky katalogu), podívejte se na téma [získání aktuálního zůstatku účtu](get-the-reseller-s-current-account-balance.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-149">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="9ea29-150">Zůstatek a platba na více měn</span><span class="sxs-lookup"><span data-stu-id="9ea29-150">Multi-currency balance and payment</span></span>

<span data-ttu-id="9ea29-151">K získání aktuálního zůstatku účtu a shromáždění souhrnů faktury, které obsahují souhrn faktury s pravidelným i jednorázovým poplatkem pro každý typ měny vašeho zákazníka, najdete informace v tématu [získání souhrnů faktury](get-invoice-summaries.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-151">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="9ea29-152">Faktury</span><span class="sxs-lookup"><span data-stu-id="9ea29-152">Invoices</span></span>

<span data-ttu-id="9ea29-153">Chcete-li získat kolekci faktur, které zobrazují jak opakované, tak jednorázové poplatky, přečtěte si téma [získání kolekce faktur](get-a-collection-of-invoices.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-153">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="9ea29-154">Jedna faktura</span><span class="sxs-lookup"><span data-stu-id="9ea29-154">Single Invoice</span></span>

<span data-ttu-id="9ea29-155">Pokud chcete načíst konkrétní fakturu pomocí ID faktury, přečtěte si téma [získání faktury podle ID](get-invoice-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-155">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="9ea29-156">Párován</span><span class="sxs-lookup"><span data-stu-id="9ea29-156">Reconciliation</span></span>

<span data-ttu-id="9ea29-157">Chcete-li získat kolekci podrobností o položce řádku faktury (položky řádku odsouhlasení) pro konkrétní ID faktury, přečtěte si téma [získání položek řádků faktury](get-invoiceline-items.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-157">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="9ea29-158">Stažení faktury jako PDF</span><span class="sxs-lookup"><span data-stu-id="9ea29-158">Download an invoice as a PDF</span></span>

<span data-ttu-id="9ea29-159">Chcete-li načíst výpis faktury ve formátu PDF pomocí ID faktury, přečtěte si téma [získání výpisu faktury](get-invoice-statement.md).</span><span class="sxs-lookup"><span data-stu-id="9ea29-159">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
