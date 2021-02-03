---
title: Vytvoření objednávky zákazníka
description: Naučte se používat rozhraní API partnerského centra k vytvoření objednávky pro zákazníka. Článek obsahuje požadavky, kroky a příklady.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767126"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="9f58f-104">Vytvoření objednávky pro zákazníka pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="9f58f-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="9f58f-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="9f58f-105">**Applies to:**</span></span>

- <span data-ttu-id="9f58f-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="9f58f-106">Partner Center</span></span>
- <span data-ttu-id="9f58f-107">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="9f58f-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9f58f-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9f58f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9f58f-109">Vytvoření **objednávky pro rezervované instance virtuálních počítačů Azure** se týká *jenom* těchto produktů:</span><span class="sxs-lookup"><span data-stu-id="9f58f-109">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="9f58f-110">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="9f58f-110">Partner Center</span></span>

<span data-ttu-id="9f58f-111">Informace o tom, co je aktuálně k dispozici pro prodej, najdete v tématu [partnerské nabídky v programu Cloud Solution Provider](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="9f58f-111">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f58f-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9f58f-112">Prerequisites</span></span>

- <span data-ttu-id="9f58f-113">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9f58f-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9f58f-114">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="9f58f-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9f58f-115">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9f58f-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9f58f-116">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="9f58f-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9f58f-117">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="9f58f-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9f58f-118">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="9f58f-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9f58f-119">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="9f58f-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9f58f-120">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9f58f-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9f58f-121">Identifikátor nabídky</span><span class="sxs-lookup"><span data-stu-id="9f58f-121">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="9f58f-122">C\#</span><span class="sxs-lookup"><span data-stu-id="9f58f-122">C\#</span></span>

<span data-ttu-id="9f58f-123">Vytvoření objednávky pro zákazníka:</span><span class="sxs-lookup"><span data-stu-id="9f58f-123">To create an order for a customer:</span></span>

1. <span data-ttu-id="9f58f-124">Vytvořte instanci objektu [**Order**](order-resources.md) a nastavte vlastnost **ReferenceCustomerID** na ID zákazníka pro záznam zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9f58f-124">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="9f58f-125">Vytvořte seznam objektů [**OrderLineItem**](order-resources.md#orderlineitem) a přiřaďte seznam k vlastnosti **položky řádku** objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-125">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="9f58f-126">Každá položka řádku objednávky obsahuje informace o nákupu pro jednu nabídku.</span><span class="sxs-lookup"><span data-stu-id="9f58f-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="9f58f-127">Musíte mít aspoň jednu položku řádku objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-127">You must have at least one order line item.</span></span>

3. <span data-ttu-id="9f58f-128">Získejte rozhraní k seřazení operací.</span><span class="sxs-lookup"><span data-stu-id="9f58f-128">Obtain an interface to order operations.</span></span> <span data-ttu-id="9f58f-129">Nejdřív zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, abyste zákazníka identifikovali.</span><span class="sxs-lookup"><span data-stu-id="9f58f-129">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="9f58f-130">Dále načtěte rozhraní z vlastnosti [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .</span><span class="sxs-lookup"><span data-stu-id="9f58f-130">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="9f58f-131">Zavolejte metodu [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) a předejte objekt [**Order**](order-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="9f58f-131">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

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

<span data-ttu-id="9f58f-132">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9f58f-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9f58f-133">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="9f58f-133">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9f58f-134">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="9f58f-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9f58f-135">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="9f58f-135">Request syntax</span></span>

| <span data-ttu-id="9f58f-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="9f58f-136">Method</span></span>   | <span data-ttu-id="9f58f-137">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9f58f-137">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="9f58f-138">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="9f58f-138">**POST**</span></span> | <span data-ttu-id="9f58f-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9f58f-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="9f58f-140">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="9f58f-140">URI parameters</span></span>

<span data-ttu-id="9f58f-141">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="9f58f-141">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="9f58f-142">Název</span><span class="sxs-lookup"><span data-stu-id="9f58f-142">Name</span></span>        | <span data-ttu-id="9f58f-143">Typ</span><span class="sxs-lookup"><span data-stu-id="9f58f-143">Type</span></span>   | <span data-ttu-id="9f58f-144">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9f58f-144">Required</span></span> | <span data-ttu-id="9f58f-145">Popis</span><span class="sxs-lookup"><span data-stu-id="9f58f-145">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="9f58f-146">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="9f58f-146">customer-id</span></span> | <span data-ttu-id="9f58f-147">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-147">string</span></span> | <span data-ttu-id="9f58f-148">Yes</span><span class="sxs-lookup"><span data-stu-id="9f58f-148">Yes</span></span>      | <span data-ttu-id="9f58f-149">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9f58f-149">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9f58f-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9f58f-150">Request headers</span></span>

<span data-ttu-id="9f58f-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9f58f-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9f58f-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9f58f-152">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="9f58f-153">Objednávka</span><span class="sxs-lookup"><span data-stu-id="9f58f-153">Order</span></span>

<span data-ttu-id="9f58f-154">Tato tabulka popisuje vlastnosti [objednávky](order-resources.md) v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="9f58f-154">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="9f58f-155">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="9f58f-155">Property</span></span>             | <span data-ttu-id="9f58f-156">Typ</span><span class="sxs-lookup"><span data-stu-id="9f58f-156">Type</span></span>                        | <span data-ttu-id="9f58f-157">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9f58f-157">Required</span></span>                        | <span data-ttu-id="9f58f-158">Popis</span><span class="sxs-lookup"><span data-stu-id="9f58f-158">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="9f58f-159">id</span><span class="sxs-lookup"><span data-stu-id="9f58f-159">id</span></span>                   | <span data-ttu-id="9f58f-160">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-160">string</span></span>                      | <span data-ttu-id="9f58f-161">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-161">No</span></span>                              | <span data-ttu-id="9f58f-162">Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-162">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="9f58f-163">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="9f58f-163">referenceCustomerId</span></span>  | <span data-ttu-id="9f58f-164">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-164">string</span></span>                      | <span data-ttu-id="9f58f-165">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-165">No</span></span>                              | <span data-ttu-id="9f58f-166">Identifikátor zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9f58f-166">The customer identifier.</span></span> |
| <span data-ttu-id="9f58f-167">billingCycle</span><span class="sxs-lookup"><span data-stu-id="9f58f-167">billingCycle</span></span>         | <span data-ttu-id="9f58f-168">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-168">string</span></span>                      | <span data-ttu-id="9f58f-169">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-169">No</span></span>                              | <span data-ttu-id="9f58f-170">Určuje četnost, s jakou se má partner fakturovat v této objednávce.</span><span class="sxs-lookup"><span data-stu-id="9f58f-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="9f58f-171">Podporované hodnoty jsou názvy členů nalezené v [BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="9f58f-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="9f58f-172">Výchozí hodnota je "Month" nebo "jednorázová" při vytváření objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-172">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="9f58f-173">Toto pole se použije po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-173">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="9f58f-174">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="9f58f-174">lineItems</span></span>            | <span data-ttu-id="9f58f-175">pole prostředků [OrderLineItem](order-resources.md#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="9f58f-175">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="9f58f-176">Yes</span><span class="sxs-lookup"><span data-stu-id="9f58f-176">Yes</span></span>      | <span data-ttu-id="9f58f-177">Seznam položek nabídek, které zákazník kupuje, včetně množství.</span><span class="sxs-lookup"><span data-stu-id="9f58f-177">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="9f58f-178">currencyCode</span><span class="sxs-lookup"><span data-stu-id="9f58f-178">currencyCode</span></span>         | <span data-ttu-id="9f58f-179">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-179">string</span></span>                      | <span data-ttu-id="9f58f-180">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-180">No</span></span>                              | <span data-ttu-id="9f58f-181">Jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="9f58f-181">Read-only.</span></span> <span data-ttu-id="9f58f-182">Měna použitá při umístění objednávky</span><span class="sxs-lookup"><span data-stu-id="9f58f-182">The currency used when placing the order.</span></span> <span data-ttu-id="9f58f-183">Použito po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-183">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="9f58f-184">creationDate</span><span class="sxs-lookup"><span data-stu-id="9f58f-184">creationDate</span></span>         | <span data-ttu-id="9f58f-185">datetime</span><span class="sxs-lookup"><span data-stu-id="9f58f-185">datetime</span></span>                    | <span data-ttu-id="9f58f-186">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-186">No</span></span>                              | <span data-ttu-id="9f58f-187">Jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="9f58f-187">Read-only.</span></span> <span data-ttu-id="9f58f-188">Datum vytvoření objednávky ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="9f58f-188">The date the order was created, in date-time format.</span></span> <span data-ttu-id="9f58f-189">Použito po úspěšném vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-189">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="9f58f-190">status</span><span class="sxs-lookup"><span data-stu-id="9f58f-190">status</span></span>               | <span data-ttu-id="9f58f-191">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-191">string</span></span>                      | <span data-ttu-id="9f58f-192">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-192">No</span></span>                              | <span data-ttu-id="9f58f-193">Jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="9f58f-193">Read-only.</span></span> <span data-ttu-id="9f58f-194">Stav objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-194">The status of the order.</span></span>  <span data-ttu-id="9f58f-195">Podporované hodnoty jsou názvy členů nalezené v [OrderStatus](order-resources.md#orderstatus).</span><span class="sxs-lookup"><span data-stu-id="9f58f-195">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="9f58f-196">odkazy</span><span class="sxs-lookup"><span data-stu-id="9f58f-196">links</span></span>                | [<span data-ttu-id="9f58f-197">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="9f58f-197">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="9f58f-198">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-198">No</span></span>                              | <span data-ttu-id="9f58f-199">Odkazy na prostředky odpovídající objednávce.</span><span class="sxs-lookup"><span data-stu-id="9f58f-199">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="9f58f-200">atributy</span><span class="sxs-lookup"><span data-stu-id="9f58f-200">attributes</span></span>           | [<span data-ttu-id="9f58f-201">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="9f58f-201">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="9f58f-202">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-202">No</span></span>                              | <span data-ttu-id="9f58f-203">Atributy metadat odpovídající pořadí.</span><span class="sxs-lookup"><span data-stu-id="9f58f-203">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="9f58f-204">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="9f58f-204">OrderLineItem</span></span>

<span data-ttu-id="9f58f-205">Tato tabulka popisuje vlastnosti [OrderLineItem](order-resources.md#orderlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="9f58f-205">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="9f58f-206">PartnerIdOnRecord by měla být poskytnuta pouze v případě, že nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="9f58f-206">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="9f58f-207">Slouží k ukládání Microsoft Partner Network ID nepřímých prodejců (nikdy ID nepřímého poskytovatele).</span><span class="sxs-lookup"><span data-stu-id="9f58f-207">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="9f58f-208">Název</span><span class="sxs-lookup"><span data-stu-id="9f58f-208">Name</span></span>                 | <span data-ttu-id="9f58f-209">Typ</span><span class="sxs-lookup"><span data-stu-id="9f58f-209">Type</span></span>   | <span data-ttu-id="9f58f-210">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9f58f-210">Required</span></span> | <span data-ttu-id="9f58f-211">Popis</span><span class="sxs-lookup"><span data-stu-id="9f58f-211">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9f58f-212">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="9f58f-212">lineItemNumber</span></span>       | <span data-ttu-id="9f58f-213">int</span><span class="sxs-lookup"><span data-stu-id="9f58f-213">int</span></span>    | <span data-ttu-id="9f58f-214">Yes</span><span class="sxs-lookup"><span data-stu-id="9f58f-214">Yes</span></span>      | <span data-ttu-id="9f58f-215">Každá položka řádku v kolekci získá jedinečné číslo řádku, počítáno od 0 do Count-1.</span><span class="sxs-lookup"><span data-stu-id="9f58f-215">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="9f58f-216">Hodnotami OfferId</span><span class="sxs-lookup"><span data-stu-id="9f58f-216">offerId</span></span>              | <span data-ttu-id="9f58f-217">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-217">string</span></span> | <span data-ttu-id="9f58f-218">Yes</span><span class="sxs-lookup"><span data-stu-id="9f58f-218">Yes</span></span>      | <span data-ttu-id="9f58f-219">Identifikátor nabídky</span><span class="sxs-lookup"><span data-stu-id="9f58f-219">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="9f58f-220">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="9f58f-220">subscriptionId</span></span>       | <span data-ttu-id="9f58f-221">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-221">string</span></span> | <span data-ttu-id="9f58f-222">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-222">No</span></span>       | <span data-ttu-id="9f58f-223">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="9f58f-223">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="9f58f-224">parentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="9f58f-224">parentSubscriptionId</span></span> | <span data-ttu-id="9f58f-225">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-225">string</span></span> | <span data-ttu-id="9f58f-226">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-226">No</span></span>       | <span data-ttu-id="9f58f-227">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="9f58f-227">Optional.</span></span> <span data-ttu-id="9f58f-228">ID nadřazeného odběru v nabídce doplňku</span><span class="sxs-lookup"><span data-stu-id="9f58f-228">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="9f58f-229">Platí pouze pro opravu.</span><span class="sxs-lookup"><span data-stu-id="9f58f-229">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="9f58f-230">friendlyName</span><span class="sxs-lookup"><span data-stu-id="9f58f-230">friendlyName</span></span>         | <span data-ttu-id="9f58f-231">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-231">string</span></span> | <span data-ttu-id="9f58f-232">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-232">No</span></span>       | <span data-ttu-id="9f58f-233">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="9f58f-233">Optional.</span></span> <span data-ttu-id="9f58f-234">Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost.</span><span class="sxs-lookup"><span data-stu-id="9f58f-234">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="9f58f-235">quantity</span><span class="sxs-lookup"><span data-stu-id="9f58f-235">quantity</span></span>             | <span data-ttu-id="9f58f-236">int</span><span class="sxs-lookup"><span data-stu-id="9f58f-236">int</span></span>    | <span data-ttu-id="9f58f-237">Yes</span><span class="sxs-lookup"><span data-stu-id="9f58f-237">Yes</span></span>      | <span data-ttu-id="9f58f-238">Počet licencí pro předplatné založené na licencích.</span><span class="sxs-lookup"><span data-stu-id="9f58f-238">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="9f58f-239">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="9f58f-239">partnerIdOnRecord</span></span>    | <span data-ttu-id="9f58f-240">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-240">string</span></span> | <span data-ttu-id="9f58f-241">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-241">No</span></span>       | <span data-ttu-id="9f58f-242">Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **nepřímého prodejce** (nikdy ID nepřímého poskytovatele).</span><span class="sxs-lookup"><span data-stu-id="9f58f-242">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="9f58f-243">To zajišťuje správné účetnictví pro motivaci.</span><span class="sxs-lookup"><span data-stu-id="9f58f-243">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="9f58f-244">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="9f58f-244">provisioningContext</span></span>  | <span data-ttu-id="9f58f-245">Řetězec<slovníku, řetězec></span><span class="sxs-lookup"><span data-stu-id="9f58f-245">Dictionary<string, string></span></span>                | <span data-ttu-id="9f58f-246">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-246">No</span></span>       |  <span data-ttu-id="9f58f-247">Informace požadované pro zřizování některých položek v katalogu.</span><span class="sxs-lookup"><span data-stu-id="9f58f-247">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="9f58f-248">Vlastnost provisioningVariables v SKU indikuje, které vlastnosti jsou požadovány pro konkrétní položky v katalogu.</span><span class="sxs-lookup"><span data-stu-id="9f58f-248">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="9f58f-249">odkazy</span><span class="sxs-lookup"><span data-stu-id="9f58f-249">links</span></span>                | [<span data-ttu-id="9f58f-250">OrderLineItemLinks</span><span class="sxs-lookup"><span data-stu-id="9f58f-250">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="9f58f-251">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-251">No</span></span>       |  <span data-ttu-id="9f58f-252">Jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="9f58f-252">Read-only.</span></span> <span data-ttu-id="9f58f-253">Odkazy na prostředky odpovídající položce řádku objednávky.</span><span class="sxs-lookup"><span data-stu-id="9f58f-253">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="9f58f-254">atributy</span><span class="sxs-lookup"><span data-stu-id="9f58f-254">attributes</span></span>           | [<span data-ttu-id="9f58f-255">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="9f58f-255">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="9f58f-256">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-256">No</span></span>       | <span data-ttu-id="9f58f-257">Atributy metadat odpovídající OrderLineItem.</span><span class="sxs-lookup"><span data-stu-id="9f58f-257">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="9f58f-258">renewsTo</span><span class="sxs-lookup"><span data-stu-id="9f58f-258">renewsTo</span></span>             | <span data-ttu-id="9f58f-259">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="9f58f-259">Array of objects</span></span>                          | <span data-ttu-id="9f58f-260">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-260">No</span></span>    |<span data-ttu-id="9f58f-261">Pole prostředků [RenewsTo](order-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="9f58f-261">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="9f58f-262">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="9f58f-262">RenewsTo</span></span>

<span data-ttu-id="9f58f-263">Tato tabulka popisuje vlastnosti [RenewsTo](order-resources.md#renewsto) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="9f58f-263">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="9f58f-264">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="9f58f-264">Property</span></span>              | <span data-ttu-id="9f58f-265">Typ</span><span class="sxs-lookup"><span data-stu-id="9f58f-265">Type</span></span>             | <span data-ttu-id="9f58f-266">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9f58f-266">Required</span></span>        | <span data-ttu-id="9f58f-267">Popis</span><span class="sxs-lookup"><span data-stu-id="9f58f-267">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9f58f-268">termDuration</span><span class="sxs-lookup"><span data-stu-id="9f58f-268">termDuration</span></span>          | <span data-ttu-id="9f58f-269">řetězec</span><span class="sxs-lookup"><span data-stu-id="9f58f-269">string</span></span>           | <span data-ttu-id="9f58f-270">No</span><span class="sxs-lookup"><span data-stu-id="9f58f-270">No</span></span>              | <span data-ttu-id="9f58f-271">ISO 8601 představuje dobu trvání období obnovy.</span><span class="sxs-lookup"><span data-stu-id="9f58f-271">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="9f58f-272">Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok).</span><span class="sxs-lookup"><span data-stu-id="9f58f-272">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="9f58f-273">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9f58f-273">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9f58f-274">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9f58f-274">REST response</span></span>

<span data-ttu-id="9f58f-275">V případě úspěchu metoda vrátí zdroj [objednávky](order-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9f58f-275">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9f58f-276">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="9f58f-276">Response success and error codes</span></span>

<span data-ttu-id="9f58f-277">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9f58f-277">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9f58f-278">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="9f58f-278">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9f58f-279">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9f58f-279">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9f58f-280">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9f58f-280">Response example</span></span>

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
