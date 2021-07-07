---
title: Vytvoření předplatného pro produkty z komerčního tržiště
description: Vývojáři můžou vytvořit a spravovat předplatné pro produkty z komerčního tržiště pomocí rozhraní API partnerského centra.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ae2e4b0a1ffa2e63e68864887093673e32079d9f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973362"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a><span data-ttu-id="e7312-103">Vytvoření předplatného pro produkty z komerčního tržiště</span><span class="sxs-lookup"><span data-stu-id="e7312-103">Create a subscription for commercial marketplace products</span></span>

<span data-ttu-id="e7312-104">Předplatné pro produkty komerčního tržiště můžete vytvořit pomocí rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e7312-104">You can create a subscription for commercial marketplace products using Partner Center APIs.</span></span> <span data-ttu-id="e7312-105">Musíte [získat seznam nabídek pro trh](#get-a-list-of-offers-for-a-market), [vytvořit a odeslat objednávku](#create-and-submit-an-order) pro předplatné komerčního tržiště a pak [načíst aktivační odkaz](#get-activation-link).</span><span class="sxs-lookup"><span data-stu-id="e7312-105">You must [get a list of offers for a market](#get-a-list-of-offers-for-a-market), [create and submit an order](#create-and-submit-an-order) for a commercial marketplace subscription, then [retrieve an activation link](#get-activation-link).</span></span>

<span data-ttu-id="e7312-106">Můžete také [provádět správu životního cyklu](#lifecycle-management) a [spravovat faktury](#invoice-and-reconciliation) pro tyto odběry.</span><span class="sxs-lookup"><span data-stu-id="e7312-106">You can also [perform lifecycle management](#lifecycle-management) and [manage invoices](#invoice-and-reconciliation) for these subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7312-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e7312-107">Prerequisites</span></span>

* <span data-ttu-id="e7312-108">Přihlašovací údaje pro [ověření partnerského centra](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e7312-108">[Partner Center authentication](partner-center-authentication.md) credentials.</span></span> <span data-ttu-id="e7312-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e7312-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>
* <span data-ttu-id="e7312-110">Identifikátor zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e7312-110">The customer identifier.</span></span> <span data-ttu-id="e7312-111">Pokud nemáte identifikátor zákazníka, postupujte podle kroků v části [získání seznamu zákazníků](get-a-list-of-customers.md).</span><span class="sxs-lookup"><span data-stu-id="e7312-111">If you don't have a customer's identifier, follow the steps in [Get a list of customers](get-a-list-of-customers.md).</span></span> <span data-ttu-id="e7312-112">Případně se přihlaste do partnerského centra, vyberte zákazníka ze seznamu zákazníků, vyberte možnost **účet** a uložte své **ID společnosti Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e7312-112">Alternatively, sign in to Partner Center, choose the customer from the list of customers, select **Account**, then save their **Microsoft ID**.</span></span>

## <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="e7312-113">Získání seznamu nabídek pro trh</span><span class="sxs-lookup"><span data-stu-id="e7312-113">Get a list of offers for a market</span></span>

<span data-ttu-id="e7312-114">Dostupné nabídky pro trh můžete vyhledat pomocí následujících modelů rozhraní API partnerského centra:</span><span class="sxs-lookup"><span data-stu-id="e7312-114">You can check the available offers for a market using the following Partner Center API models:</span></span>

* <span data-ttu-id="e7312-115">**[Produkt](product-resources.md#product)**: seskupovací konstrukce pro kupní zboží nebo služby.</span><span class="sxs-lookup"><span data-stu-id="e7312-115">**[Product](product-resources.md#product)**: A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="e7312-116">Produkt sám o sobě není položka, která je k nákupu.</span><span class="sxs-lookup"><span data-stu-id="e7312-116">A product itself isn't a purchasable item.</span></span>
* <span data-ttu-id="e7312-117">**[SKU](product-resources.md#sku)**: kupní jednotka (SKU) na skladě v rámci produktu.</span><span class="sxs-lookup"><span data-stu-id="e7312-117">**[SKU](product-resources.md#sku)**: A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="e7312-118">Tyto prvky jsou znázorněny v různých tvarech produktu.</span><span class="sxs-lookup"><span data-stu-id="e7312-118">These represent the different shapes of the product.</span></span>
* <span data-ttu-id="e7312-119">**[Dostupnost](product-resources.md#availability)**: konfigurace, ve které je k DISpozici SKU k nákupu (například země, Měna nebo odvětví odvětví).</span><span class="sxs-lookup"><span data-stu-id="e7312-119">**[Availability](product-resources.md#availability)**: A configuration in which a SKU is available for purchase (such as country, currency, or industry segment).</span></span>

<span data-ttu-id="e7312-120">Než zakoupíte rezervaci Azure, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="e7312-120">Before you purchase an Azure reservation, complete the following steps:</span></span>

1. <span data-ttu-id="e7312-121">Identifikujte a načtěte produkt a SKU, které chcete koupit.</span><span class="sxs-lookup"><span data-stu-id="e7312-121">Identify and retrieve the product and SKU that you want to purchase.</span></span> <span data-ttu-id="e7312-122">Pokud už znáte ID produktu a ID skladové položky, vyberte je.</span><span class="sxs-lookup"><span data-stu-id="e7312-122">If you already know the Product ID and SKU ID, select them.</span></span>

    * [<span data-ttu-id="e7312-123">Získat seznam produktů</span><span class="sxs-lookup"><span data-stu-id="e7312-123">Get a list of products</span></span>](get-a-list-of-products.md)
    * [<span data-ttu-id="e7312-124">Získat produkt s použitím ID produktu</span><span class="sxs-lookup"><span data-stu-id="e7312-124">Get a product using the product ID</span></span>](get-a-product-by-id.md)
    * [<span data-ttu-id="e7312-125">Získat seznam SKU pro produkt</span><span class="sxs-lookup"><span data-stu-id="e7312-125">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
    * [<span data-ttu-id="e7312-126">Získání SKU pomocí ID SKU</span><span class="sxs-lookup"><span data-stu-id="e7312-126">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

    > [!NOTE]
    > <span data-ttu-id="e7312-127">Produkty z komerčního tržiště můžete identifikovat jejich **ProductType** vlastností **"Azure"** a jejich vlastností **podtypu** **"SaaS"**.</span><span class="sxs-lookup"><span data-stu-id="e7312-127">You can identify commercial marketplace products by their **ProductType** property of **"Azure"** and their **SubType** property of **"SaaS"**.</span></span>

2. <span data-ttu-id="e7312-128">Pokud jsou skladové jednotky označené **InventoryCheck** podmínkou, podívejte se na [inventář skladové](check-inventory.md)položky.</span><span class="sxs-lookup"><span data-stu-id="e7312-128">If the SKUs are tagged with an **InventoryCheck** prerequisite, [check the inventory for a SKU](check-inventory.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e7312-129">V tuto chvíli nejsou k dispozici žádné produkty z komerčního tržiště, které podporují kontrolu inventáře nebo jsou označené **InventoryCheck** požadavky.</span><span class="sxs-lookup"><span data-stu-id="e7312-129">At this time, there are no commercial marketplace products that support inventory check or are tagged with an **InventoryCheck** prerequisite.</span></span>

3. <span data-ttu-id="e7312-130">Načtěte dostupnost pro SKLADOVOU položku.</span><span class="sxs-lookup"><span data-stu-id="e7312-130">Retrieve the availability for the SKU.</span></span> <span data-ttu-id="e7312-131">Při umísťování objednávky budete potřebovat **CatalogItemId** dostupnost, kterou můžete načíst prostřednictvím následujících rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="e7312-131">You will need the **CatalogItemId** of the availability when placing the order, which you can retrieve through the following APIs:</span></span>

    * [<span data-ttu-id="e7312-132">Získat seznam dostupnosti pro SKU</span><span class="sxs-lookup"><span data-stu-id="e7312-132">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
    * [<span data-ttu-id="e7312-133">Získání dostupnosti pomocí ID dostupnosti</span><span class="sxs-lookup"><span data-stu-id="e7312-133">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a><span data-ttu-id="e7312-134">Vytvoření a odeslání objednávky</span><span class="sxs-lookup"><span data-stu-id="e7312-134">Create and submit an order</span></span>

<span data-ttu-id="e7312-135">K odeslání vaší objednávky rezervace Azure použijte tento postup:</span><span class="sxs-lookup"><span data-stu-id="e7312-135">To submit your Azure reservation order, follow these steps:</span></span>

1. <span data-ttu-id="e7312-136">[Vytvořte košík](create-a-cart.md) pro uložení kolekce položek katalogu, které máte v úmyslu koupit.</span><span class="sxs-lookup"><span data-stu-id="e7312-136">[Create a cart](create-a-cart.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="e7312-137">Při vytváření [košíku](cart-resources.md#cart)se [položky řádku vozíku](cart-resources.md#cartlineitem) automaticky seskupují podle toho, co se dá koupit společně ve stejném [pořadí](order-resources.md#order).</span><span class="sxs-lookup"><span data-stu-id="e7312-137">When you create a [cart](cart-resources.md#cart), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [order](order-resources.md#order).</span></span> <span data-ttu-id="e7312-138">(Můžete také [Aktualizovat košík](update-a-cart.md).)</span><span class="sxs-lookup"><span data-stu-id="e7312-138">(You can also [update a cart](update-a-cart.md).)</span></span>
2. <span data-ttu-id="e7312-139">[Podívejte se na košík](checkout-a-cart.md), který má za následek vytvoření [objednávky](order-resources.md#order).</span><span class="sxs-lookup"><span data-stu-id="e7312-139">[Check out the cart](checkout-a-cart.md), which results in the creation of an [order](order-resources.md#order).</span></span>

### <a name="get-order-details"></a><span data-ttu-id="e7312-140">Získat podrobnosti objednávky</span><span class="sxs-lookup"><span data-stu-id="e7312-140">Get order details</span></span>

<span data-ttu-id="e7312-141">[Pomocí ID objednávky můžete načíst podrobnosti o jednotlivých objednávkách](get-an-order-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="e7312-141">You can [retrieve the details of an individual order using the order ID](get-an-order-by-id.md).</span></span> <span data-ttu-id="e7312-142">Můžete také [načíst seznam všech objednávek pro konkrétního zákazníka](get-all-of-a-customer-s-orders.md).</span><span class="sxs-lookup"><span data-stu-id="e7312-142">You can also [retrieve a list of all orders for a specific customer](get-all-of-a-customer-s-orders.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e7312-143">Po odeslání objednávky dojde k prodlevě až 15 minut, než se objednávka objeví v seznamu objednávek zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e7312-143">After an order is submitted, there is a delay of up to 15 minutes before the order appears in that customer's order list.</span></span>

## <a name="get-activation-link"></a><span data-ttu-id="e7312-144">Získat aktivační odkaz</span><span class="sxs-lookup"><span data-stu-id="e7312-144">Get activation link</span></span>

<span data-ttu-id="e7312-145">Partner nebo zákazník musí aktivovat odběry Azure Marketplace produktů.</span><span class="sxs-lookup"><span data-stu-id="e7312-145">The partner or customer must activate subscriptions to Azure Marketplace products.</span></span> <span data-ttu-id="e7312-146">Můžete [získat aktivační odkaz podle položky řádku objednávky](get-activation-link-by-order-line-item.md).</span><span class="sxs-lookup"><span data-stu-id="e7312-146">You can [get an activation link by order line item](get-activation-link-by-order-line-item.md).</span></span> <span data-ttu-id="e7312-147">Můžete taky [získat předplatné podle ID](get-a-subscription-by-id.md)a potom **vytvořit jeho vlastnost Links** a vytvořit tak aktivační odkaz.</span><span class="sxs-lookup"><span data-stu-id="e7312-147">You can also [get a subscription by ID](get-a-subscription-by-id.md), then enumerate its **Links** property to create an activation link.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="e7312-148">Správa životního cyklu</span><span class="sxs-lookup"><span data-stu-id="e7312-148">Lifecycle management</span></span>

<span data-ttu-id="e7312-149">Životní cyklus předplatných můžete spravovat na komerční produkty z webu Marketplace pomocí následujících metod:</span><span class="sxs-lookup"><span data-stu-id="e7312-149">You can manage the lifecycle of your subscriptions to commercial marketplace products using the following methods:</span></span>

* [<span data-ttu-id="e7312-150">Zrušení předplatného na komerčním marketplace</span><span class="sxs-lookup"><span data-stu-id="e7312-150">Cancel a commercial marketplace subscription</span></span>](cancel-an-azure-marketplace-subscription.md)
* [<span data-ttu-id="e7312-151">Povolení nebo zakázání autorenew pro předplatné komerčního tržiště</span><span class="sxs-lookup"><span data-stu-id="e7312-151">Enable or disable autorenew for a commercial marketplace subscription</span></span>](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a><span data-ttu-id="e7312-152">Správa množství</span><span class="sxs-lookup"><span data-stu-id="e7312-152">Quantity management</span></span>

<span data-ttu-id="e7312-153">Množství předplatného komerčního tržiště musí být v mezích definovaných přiřazenými [SKU](product-resources.md#sku) (viz atributy **minimumQuantity** a **maximumQuantity** ).</span><span class="sxs-lookup"><span data-stu-id="e7312-153">The quantity of a commercial marketplace subscription must be within the limits defined by its associated [SKU](product-resources.md#sku) (see the **minimumQuantity** and **maximumQuantity** attributes).</span></span> <span data-ttu-id="e7312-154">Pokud chcete aktualizovat množství předplatného komerčního tržiště, použijte tuto metodu:</span><span class="sxs-lookup"><span data-stu-id="e7312-154">To update the quantity of a commercial marketplace subscription, use the following method:</span></span>

* [<span data-ttu-id="e7312-155">Změna objemu předplatného</span><span class="sxs-lookup"><span data-stu-id="e7312-155">Change the quantity of a subscription</span></span>](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="e7312-156">Faktura a odsouhlasení</span><span class="sxs-lookup"><span data-stu-id="e7312-156">Invoice and reconciliation</span></span>

<span data-ttu-id="e7312-157">Pomocí následujících metod můžete spravovat [faktury](invoice-resources.md) zákazníků (včetně poplatků za předplatné z komerčních produktů na webu Marketplace):</span><span class="sxs-lookup"><span data-stu-id="e7312-157">You can manage customer [invoices](invoice-resources.md) (including charges for subscriptions to commercial marketplace products) using the following methods:</span></span>

* [<span data-ttu-id="e7312-158">Získat položky řádkové spotřeby pro komerční web na faktuře</span><span class="sxs-lookup"><span data-stu-id="e7312-158">Get invoice billed commercial marketplace consumption line items</span></span>](get-invoice-billed-consumption-lineitems.md)
* [<span data-ttu-id="e7312-159">Získání odkazů na odhad faktury</span><span class="sxs-lookup"><span data-stu-id="e7312-159">Get invoice estimate links</span></span>](get-invoice-estimate-links.md)
* [<span data-ttu-id="e7312-160">Získat faktury za položky na řádcích spotřeby na komerční web Marketplace</span><span class="sxs-lookup"><span data-stu-id="e7312-160">Get invoice unbilled commercial marketplace consumption line items</span></span>](get-invoice-unbilled-consumption-lineitems.md)
* [<span data-ttu-id="e7312-161">Získat nefakturovatelné položky řádku odsouhlasení faktury</span><span class="sxs-lookup"><span data-stu-id="e7312-161">Get invoice unbilled reconciliation line items</span></span>](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a><span data-ttu-id="e7312-162">Test pomocí účtu izolovaného prostoru pro integraci</span><span class="sxs-lookup"><span data-stu-id="e7312-162">Test using integration sandbox account</span></span>

<span data-ttu-id="e7312-163">V produkčním prostředí, po vytvoření odběru pro komerční produkty SaaS na webu Marketplace, je potřeba načíst přizpůsobený aktivační odkaz z partnerského centra a přejít na web vydavatele, aby se proces instalace dokončil.</span><span class="sxs-lookup"><span data-stu-id="e7312-163">In production, after you have created a subscription to commercial marketplace SaaS products, you need to retrieve a personalized activation link from Partner Center and visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="e7312-164">Fakturace předplatného se zahájí až po dokončení instalace.</span><span class="sxs-lookup"><span data-stu-id="e7312-164">Subscription billing will begin only after setup is complete.</span></span>

<span data-ttu-id="e7312-165">V prostředí izolovaného prostoru (sandbox) CSP není k dispozici žádná integrace s nezávislými prodejci softwaru.</span><span class="sxs-lookup"><span data-stu-id="e7312-165">In the CSP sandbox environment, there is no integration with ISVs.</span></span> <span data-ttu-id="e7312-166">Pokud se pokusíte načíst aktivační odkaz z partnerského centra, vrátí se fiktivní odkaz.</span><span class="sxs-lookup"><span data-stu-id="e7312-166">If you try to retrieve an activation link from Partner Center, a dummy link will be returned.</span></span> <span data-ttu-id="e7312-167">Tento fiktivní odkaz nelze použít k dokončení procesu instalace na webu vydavatele.</span><span class="sxs-lookup"><span data-stu-id="e7312-167">You cannot use this dummy link to complete the setup process at the publisher's site.</span></span> <span data-ttu-id="e7312-168">Pokud chcete pomocí účtu izolovaného prostoru (sandbox) testovat účtování předplatných do komerčních produktů SaaS na webu Marketplace, použijte k aktivaci předplatného následující metodu.</span><span class="sxs-lookup"><span data-stu-id="e7312-168">To use the integration sandbox account to test billing for subscriptions to commercial marketplace SaaS products, use the following method to activate the subscription instead.</span></span> <span data-ttu-id="e7312-169">Fakturace předplatného se zahájí po úspěšné aktivaci:</span><span class="sxs-lookup"><span data-stu-id="e7312-169">Subscription billing will begin after successful activation:</span></span>

* [<span data-ttu-id="e7312-170">Aktivace předplatného izolovaného prostoru pro produkty z komerčního tržiště</span><span class="sxs-lookup"><span data-stu-id="e7312-170">Activate a sandbox subscription for commercial marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

