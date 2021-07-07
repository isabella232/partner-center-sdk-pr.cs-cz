---
title: Vytvoření objednávky zákazníka
description: Naučte se používat Partnerské centrum API k vytvoření objednávky pro zákazníka. Článek obsahuje požadavky, kroky a příklady.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3a86a99f43bdeec5e4c560ab59e1924b76c0636
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973536"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="fddac-104">Vytvoření objednávky pro zákazníka pomocí Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="fddac-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="fddac-105">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fddac-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fddac-106">Vytvoření objednávky **produktů rezervovaných instancí virtuálních** počítače Azure se *vztahuje pouze* na:</span><span class="sxs-lookup"><span data-stu-id="fddac-106">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="fddac-107">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="fddac-107">Partner Center</span></span>

<span data-ttu-id="fddac-108">Informace o tom, co je aktuálně k dispozici k prodeji, najdete v tématu Nabídky partnerů [v Cloud Solution Provider programu](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="fddac-108">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fddac-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fddac-109">Prerequisites</span></span>

- <span data-ttu-id="fddac-110">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fddac-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fddac-111">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="fddac-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fddac-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fddac-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fddac-113">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="fddac-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fddac-114">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="fddac-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fddac-115">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="fddac-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fddac-116">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fddac-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fddac-117">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fddac-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fddac-118">Identifikátor nabídky.</span><span class="sxs-lookup"><span data-stu-id="fddac-118">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="fddac-119">C\#</span><span class="sxs-lookup"><span data-stu-id="fddac-119">C\#</span></span>

<span data-ttu-id="fddac-120">Vytvoření objednávky pro zákazníka:</span><span class="sxs-lookup"><span data-stu-id="fddac-120">To create an order for a customer:</span></span>

1. <span data-ttu-id="fddac-121">Vytvořte instanci objektu [**Order**](order-resources.md) a nastavte vlastnost **ReferenceCustomerID** na ID zákazníka pro zaznamenání zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fddac-121">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="fddac-122">Vytvořte seznam objektů [**OrderLineItem**](order-resources.md#orderlineitem) a přiřaďte ho k vlastnosti **LineItems** objednávky.</span><span class="sxs-lookup"><span data-stu-id="fddac-122">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="fddac-123">Každá položka řádku objednávky obsahuje informace o nákupu pro jednu nabídku.</span><span class="sxs-lookup"><span data-stu-id="fddac-123">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="fddac-124">Musíte mít alespoň jednu řádkovou položku objednávky.</span><span class="sxs-lookup"><span data-stu-id="fddac-124">You must have at least one order line item.</span></span>

3. <span data-ttu-id="fddac-125">Získání rozhraní pro řazení operací.</span><span class="sxs-lookup"><span data-stu-id="fddac-125">Obtain an interface to order operations.</span></span> <span data-ttu-id="fddac-126">Nejprve zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fddac-126">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="fddac-127">Dále načtěte rozhraní z [**vlastnosti Orders.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)</span><span class="sxs-lookup"><span data-stu-id="fddac-127">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="fddac-128">Zavolejte [**metodu Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) a předejte [**objekt Order.**](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="fddac-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="fddac-129">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fddac-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fddac-130">**Project:** SDK pro Partnerské centrum Samples **Class:** CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="fddac-130">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fddac-131">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="fddac-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fddac-132">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="fddac-132">Request syntax</span></span>

| <span data-ttu-id="fddac-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="fddac-133">Method</span></span>   | <span data-ttu-id="fddac-134">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fddac-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="fddac-135">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="fddac-135">**POST**</span></span> | <span data-ttu-id="fddac-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fddac-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="fddac-137">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="fddac-137">URI parameters</span></span>

<span data-ttu-id="fddac-138">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="fddac-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="fddac-139">Název</span><span class="sxs-lookup"><span data-stu-id="fddac-139">Name</span></span>        | <span data-ttu-id="fddac-140">Typ</span><span class="sxs-lookup"><span data-stu-id="fddac-140">Type</span></span>   | <span data-ttu-id="fddac-141">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fddac-141">Required</span></span> | <span data-ttu-id="fddac-142">Popis</span><span class="sxs-lookup"><span data-stu-id="fddac-142">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="fddac-143">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="fddac-143">customer-id</span></span> | <span data-ttu-id="fddac-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-144">string</span></span> | <span data-ttu-id="fddac-145">Yes</span><span class="sxs-lookup"><span data-stu-id="fddac-145">Yes</span></span>      | <span data-ttu-id="fddac-146">Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fddac-146">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fddac-147">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fddac-147">Request headers</span></span>

<span data-ttu-id="fddac-148">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fddac-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fddac-149">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fddac-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="fddac-150">Objednávka</span><span class="sxs-lookup"><span data-stu-id="fddac-150">Order</span></span>

<span data-ttu-id="fddac-151">Tato tabulka popisuje [vlastnosti Order](order-resources.md) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="fddac-151">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="fddac-152">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fddac-152">Property</span></span>             | <span data-ttu-id="fddac-153">Typ</span><span class="sxs-lookup"><span data-stu-id="fddac-153">Type</span></span>                        | <span data-ttu-id="fddac-154">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fddac-154">Required</span></span>                        | <span data-ttu-id="fddac-155">Popis</span><span class="sxs-lookup"><span data-stu-id="fddac-155">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="fddac-156">id</span><span class="sxs-lookup"><span data-stu-id="fddac-156">id</span></span>                   | <span data-ttu-id="fddac-157">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-157">string</span></span>                      | <span data-ttu-id="fddac-158">No</span><span class="sxs-lookup"><span data-stu-id="fddac-158">No</span></span>                              | <span data-ttu-id="fddac-159">Identifikátor objednávky zadaný po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="fddac-159">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="fddac-160">referenčníCustomerId</span><span class="sxs-lookup"><span data-stu-id="fddac-160">referenceCustomerId</span></span>  | <span data-ttu-id="fddac-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-161">string</span></span>                      | <span data-ttu-id="fddac-162">No</span><span class="sxs-lookup"><span data-stu-id="fddac-162">No</span></span>                              | <span data-ttu-id="fddac-163">Identifikátor zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fddac-163">The customer identifier.</span></span> |
| <span data-ttu-id="fddac-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="fddac-164">billingCycle</span></span>         | <span data-ttu-id="fddac-165">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-165">string</span></span>                      | <span data-ttu-id="fddac-166">No</span><span class="sxs-lookup"><span data-stu-id="fddac-166">No</span></span>                              | <span data-ttu-id="fddac-167">Určuje frekvenci, s jakou se partner účtuje za tuto objednávku.</span><span class="sxs-lookup"><span data-stu-id="fddac-167">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="fddac-168">Podporované hodnoty jsou názvy členů, které najdete v [části BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="fddac-168">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="fddac-169">Výchozí hodnota je "Měsíčně" nebo "OneTime" při vytváření objednávky.</span><span class="sxs-lookup"><span data-stu-id="fddac-169">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="fddac-170">Toto pole se použije při úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="fddac-170">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="fddac-171">položky řádku</span><span class="sxs-lookup"><span data-stu-id="fddac-171">lineItems</span></span>            | <span data-ttu-id="fddac-172">pole prostředků [OrderLineItem](order-resources.md#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="fddac-172">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="fddac-173">Yes</span><span class="sxs-lookup"><span data-stu-id="fddac-173">Yes</span></span>      | <span data-ttu-id="fddac-174">Itemized list of the offers the customer is purchasing including the quantity.</span><span class="sxs-lookup"><span data-stu-id="fddac-174">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="fddac-175">currencyCode</span><span class="sxs-lookup"><span data-stu-id="fddac-175">currencyCode</span></span>         | <span data-ttu-id="fddac-176">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-176">string</span></span>                      | <span data-ttu-id="fddac-177">No</span><span class="sxs-lookup"><span data-stu-id="fddac-177">No</span></span>                              | <span data-ttu-id="fddac-178">Jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="fddac-178">Read-only.</span></span> <span data-ttu-id="fddac-179">Měna použitá při zadávání objednávky.</span><span class="sxs-lookup"><span data-stu-id="fddac-179">The currency used when placing the order.</span></span> <span data-ttu-id="fddac-180">Použije se při úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="fddac-180">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="fddac-181">datum vytvoření</span><span class="sxs-lookup"><span data-stu-id="fddac-181">creationDate</span></span>         | <span data-ttu-id="fddac-182">datetime</span><span class="sxs-lookup"><span data-stu-id="fddac-182">datetime</span></span>                    | <span data-ttu-id="fddac-183">No</span><span class="sxs-lookup"><span data-stu-id="fddac-183">No</span></span>                              | <span data-ttu-id="fddac-184">Jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="fddac-184">Read-only.</span></span> <span data-ttu-id="fddac-185">Datum vytvoření objednávky ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="fddac-185">The date the order was created, in date-time format.</span></span> <span data-ttu-id="fddac-186">Použije se při úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="fddac-186">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="fddac-187">status</span><span class="sxs-lookup"><span data-stu-id="fddac-187">status</span></span>               | <span data-ttu-id="fddac-188">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-188">string</span></span>                      | <span data-ttu-id="fddac-189">No</span><span class="sxs-lookup"><span data-stu-id="fddac-189">No</span></span>                              | <span data-ttu-id="fddac-190">Jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="fddac-190">Read-only.</span></span> <span data-ttu-id="fddac-191">Stav objednávky</span><span class="sxs-lookup"><span data-stu-id="fddac-191">The status of the order.</span></span>  <span data-ttu-id="fddac-192">Podporované hodnoty jsou názvy členů, které najdete v [OrderStatus](order-resources.md#orderstatus).</span><span class="sxs-lookup"><span data-stu-id="fddac-192">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="fddac-193">Odkazy</span><span class="sxs-lookup"><span data-stu-id="fddac-193">links</span></span>                | [<span data-ttu-id="fddac-194">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="fddac-194">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="fddac-195">No</span><span class="sxs-lookup"><span data-stu-id="fddac-195">No</span></span>                              | <span data-ttu-id="fddac-196">Propojení prostředků odpovídající objednávce</span><span class="sxs-lookup"><span data-stu-id="fddac-196">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="fddac-197">atributy</span><span class="sxs-lookup"><span data-stu-id="fddac-197">attributes</span></span>           | [<span data-ttu-id="fddac-198">Atributy prostředků</span><span class="sxs-lookup"><span data-stu-id="fddac-198">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="fddac-199">No</span><span class="sxs-lookup"><span data-stu-id="fddac-199">No</span></span>                              | <span data-ttu-id="fddac-200">Atributy metadat odpovídající order.</span><span class="sxs-lookup"><span data-stu-id="fddac-200">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="fddac-201">OrderLineItem (PoložkaŘádku Objednávky)</span><span class="sxs-lookup"><span data-stu-id="fddac-201">OrderLineItem</span></span>

<span data-ttu-id="fddac-202">Tato tabulka popisuje vlastnosti [OrderLineItem](order-resources.md#orderlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="fddac-202">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="fddac-203">Záznam partnerIdOnRecord by měl být poskytnut pouze v případě, že nepřímý poskytovatel zadá objednávku jménem nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="fddac-203">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="fddac-204">Slouží k uložení ID Microsoft Partner Network nepřímého prodejce (nikdy ID nepřímého poskytovatele).</span><span class="sxs-lookup"><span data-stu-id="fddac-204">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="fddac-205">Název</span><span class="sxs-lookup"><span data-stu-id="fddac-205">Name</span></span>                 | <span data-ttu-id="fddac-206">Typ</span><span class="sxs-lookup"><span data-stu-id="fddac-206">Type</span></span>   | <span data-ttu-id="fddac-207">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fddac-207">Required</span></span> | <span data-ttu-id="fddac-208">Popis</span><span class="sxs-lookup"><span data-stu-id="fddac-208">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fddac-209">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="fddac-209">lineItemNumber</span></span>       | <span data-ttu-id="fddac-210">int</span><span class="sxs-lookup"><span data-stu-id="fddac-210">int</span></span>    | <span data-ttu-id="fddac-211">Yes</span><span class="sxs-lookup"><span data-stu-id="fddac-211">Yes</span></span>      | <span data-ttu-id="fddac-212">Každá položka řádku v kolekci získá jedinečné číslo řádku, počítá se od 0 do count-1.</span><span class="sxs-lookup"><span data-stu-id="fddac-212">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="fddac-213">ID nabídky</span><span class="sxs-lookup"><span data-stu-id="fddac-213">offerId</span></span>              | <span data-ttu-id="fddac-214">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-214">string</span></span> | <span data-ttu-id="fddac-215">Yes</span><span class="sxs-lookup"><span data-stu-id="fddac-215">Yes</span></span>      | <span data-ttu-id="fddac-216">Identifikátor nabídky.</span><span class="sxs-lookup"><span data-stu-id="fddac-216">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="fddac-217">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="fddac-217">subscriptionId</span></span>       | <span data-ttu-id="fddac-218">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-218">string</span></span> | <span data-ttu-id="fddac-219">No</span><span class="sxs-lookup"><span data-stu-id="fddac-219">No</span></span>       | <span data-ttu-id="fddac-220">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="fddac-220">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="fddac-221">PARENTSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="fddac-221">parentSubscriptionId</span></span> | <span data-ttu-id="fddac-222">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-222">string</span></span> | <span data-ttu-id="fddac-223">No</span><span class="sxs-lookup"><span data-stu-id="fddac-223">No</span></span>       | <span data-ttu-id="fddac-224">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="fddac-224">Optional.</span></span> <span data-ttu-id="fddac-225">ID nadřazeného předplatného v nabídce doplňku.</span><span class="sxs-lookup"><span data-stu-id="fddac-225">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="fddac-226">Platí jenom pro PATCH.</span><span class="sxs-lookup"><span data-stu-id="fddac-226">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="fddac-227">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="fddac-227">friendlyName</span></span>         | <span data-ttu-id="fddac-228">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-228">string</span></span> | <span data-ttu-id="fddac-229">No</span><span class="sxs-lookup"><span data-stu-id="fddac-229">No</span></span>       | <span data-ttu-id="fddac-230">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="fddac-230">Optional.</span></span> <span data-ttu-id="fddac-231">Popisný název předplatného definovaného partnerem, který pomáhá jednoznačně rozpoznat.</span><span class="sxs-lookup"><span data-stu-id="fddac-231">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="fddac-232">quantity</span><span class="sxs-lookup"><span data-stu-id="fddac-232">quantity</span></span>             | <span data-ttu-id="fddac-233">int</span><span class="sxs-lookup"><span data-stu-id="fddac-233">int</span></span>    | <span data-ttu-id="fddac-234">Yes</span><span class="sxs-lookup"><span data-stu-id="fddac-234">Yes</span></span>      | <span data-ttu-id="fddac-235">Počet licencí pro předplatné založené na licencích.</span><span class="sxs-lookup"><span data-stu-id="fddac-235">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="fddac-236">id partneraZáznam</span><span class="sxs-lookup"><span data-stu-id="fddac-236">partnerIdOnRecord</span></span>    | <span data-ttu-id="fddac-237">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-237">string</span></span> | <span data-ttu-id="fddac-238">No</span><span class="sxs-lookup"><span data-stu-id="fddac-238">No</span></span>       | <span data-ttu-id="fddac-239">Když nepřímý poskytovatel zadá objednávku jménem nepřímého prodejce, zadejte do tohoto pole pouze ID MPN nepřímého prodejce **(nikdy** ID nepřímého poskytovatele).</span><span class="sxs-lookup"><span data-stu-id="fddac-239">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="fddac-240">Tím se zajistí správné účtování pobídek.</span><span class="sxs-lookup"><span data-stu-id="fddac-240">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="fddac-241">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="fddac-241">provisioningContext</span></span>  | <span data-ttu-id="fddac-242">Slovníkový<řetězec, řetězec></span><span class="sxs-lookup"><span data-stu-id="fddac-242">Dictionary<string, string></span></span>                | <span data-ttu-id="fddac-243">No</span><span class="sxs-lookup"><span data-stu-id="fddac-243">No</span></span>       |  <span data-ttu-id="fddac-244">Informace vyžadované pro zřizování některých položek v katalogu.</span><span class="sxs-lookup"><span data-stu-id="fddac-244">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="fddac-245">Vlastnost provisioningVariables ve SKU určuje, které vlastnosti jsou vyžadovány pro konkrétní položky v katalogu.</span><span class="sxs-lookup"><span data-stu-id="fddac-245">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="fddac-246">Odkazy</span><span class="sxs-lookup"><span data-stu-id="fddac-246">links</span></span>                | [<span data-ttu-id="fddac-247">OrderLineItemLinks</span><span class="sxs-lookup"><span data-stu-id="fddac-247">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="fddac-248">No</span><span class="sxs-lookup"><span data-stu-id="fddac-248">No</span></span>       |  <span data-ttu-id="fddac-249">Jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="fddac-249">Read-only.</span></span> <span data-ttu-id="fddac-250">Propojení prostředků odpovídající položce řádku Order (Objednávka).</span><span class="sxs-lookup"><span data-stu-id="fddac-250">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="fddac-251">atributy</span><span class="sxs-lookup"><span data-stu-id="fddac-251">attributes</span></span>           | [<span data-ttu-id="fddac-252">Atributy prostředků</span><span class="sxs-lookup"><span data-stu-id="fddac-252">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="fddac-253">No</span><span class="sxs-lookup"><span data-stu-id="fddac-253">No</span></span>       | <span data-ttu-id="fddac-254">Atributy metadat odpovídající OrderLineItem.</span><span class="sxs-lookup"><span data-stu-id="fddac-254">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="fddac-255">renewsTo</span><span class="sxs-lookup"><span data-stu-id="fddac-255">renewsTo</span></span>             | <span data-ttu-id="fddac-256">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="fddac-256">Array of objects</span></span>                          | <span data-ttu-id="fddac-257">No</span><span class="sxs-lookup"><span data-stu-id="fddac-257">No</span></span>    |<span data-ttu-id="fddac-258">Pole prostředků [RenewsTo.](order-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="fddac-258">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="fddac-259">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="fddac-259">RenewsTo</span></span>

<span data-ttu-id="fddac-260">Tato tabulka popisuje vlastnosti [RenewsTo](order-resources.md#renewsto) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="fddac-260">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="fddac-261">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fddac-261">Property</span></span>              | <span data-ttu-id="fddac-262">Typ</span><span class="sxs-lookup"><span data-stu-id="fddac-262">Type</span></span>             | <span data-ttu-id="fddac-263">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fddac-263">Required</span></span>        | <span data-ttu-id="fddac-264">Popis</span><span class="sxs-lookup"><span data-stu-id="fddac-264">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fddac-265">termDuration</span><span class="sxs-lookup"><span data-stu-id="fddac-265">termDuration</span></span>          | <span data-ttu-id="fddac-266">řetězec</span><span class="sxs-lookup"><span data-stu-id="fddac-266">string</span></span>           | <span data-ttu-id="fddac-267">No</span><span class="sxs-lookup"><span data-stu-id="fddac-267">No</span></span>              | <span data-ttu-id="fddac-268">Reprezentace doby trvání období prodloužení podle ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="fddac-268">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="fddac-269">Aktuální podporované hodnoty jsou **P1M (1** měsíc) a **P1Y** (1 rok).</span><span class="sxs-lookup"><span data-stu-id="fddac-269">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="fddac-270">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fddac-270">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="fddac-271">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fddac-271">REST response</span></span>

<span data-ttu-id="fddac-272">V případě úspěchu vrátí metoda [v textu](order-resources.md) odpovědi prostředek Order.</span><span class="sxs-lookup"><span data-stu-id="fddac-272">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fddac-273">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="fddac-273">Response success and error codes</span></span>

<span data-ttu-id="fddac-274">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fddac-274">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fddac-275">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="fddac-275">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fddac-276">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fddac-276">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fddac-277">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fddac-277">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
