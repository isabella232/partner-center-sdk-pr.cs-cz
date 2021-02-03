---
title: Změna fakturačního cyklu
description: Naučte se aktualizovat předplatné zákazníka na měsíční nebo roční fakturaci pomocí rozhraní API partnerského centra. Můžete to provést taky z řídicího panelu partnerského centra.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767114"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="e2cb5-104">Změna fakturačního cyklu zákaznického předplatného</span><span class="sxs-lookup"><span data-stu-id="e2cb5-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="e2cb5-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="e2cb5-105">**Applies to:**</span></span>

- <span data-ttu-id="e2cb5-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e2cb5-106">Partner Center</span></span>
- <span data-ttu-id="e2cb5-107">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e2cb5-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e2cb5-108">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="e2cb5-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e2cb5-109">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e2cb5-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e2cb5-110">Aktualizuje [objednávku](order-resources.md) z měsíčního na roční fakturace nebo z roční na měsíční fakturaci.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-110">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="e2cb5-111">Na řídicím panelu partnerského centra můžete tuto operaci provést přechodem na stránku s podrobnostmi o předplatném zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-111">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="e2cb5-112">Po tomto případě se zobrazí možnost definující aktuální fakturační cyklus pro předplatné s možností změny a odeslání.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-112">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="e2cb5-113">**Mimo rozsah** tohoto článku:</span><span class="sxs-lookup"><span data-stu-id="e2cb5-113">**Out of scope** for this article:</span></span>

- <span data-ttu-id="e2cb5-114">Změna fakturačního cyklu pro zkušební verze</span><span class="sxs-lookup"><span data-stu-id="e2cb5-114">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="e2cb5-115">Změna fakturačních cyklů pro jakékoli neroční nabídky za období (měsíčně, 6 let) & předplatných Azure</span><span class="sxs-lookup"><span data-stu-id="e2cb5-115">Changing the billing cycles for any non-annual term offers (monthly, 6-year) & Azure subscriptions</span></span>
- <span data-ttu-id="e2cb5-116">Změna fakturačních cyklů pro neaktivní předplatná</span><span class="sxs-lookup"><span data-stu-id="e2cb5-116">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="e2cb5-117">Změna fakturačních cyklů pro odběry založené na licencích Microsoft online služby</span><span class="sxs-lookup"><span data-stu-id="e2cb5-117">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2cb5-118">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e2cb5-118">Prerequisites</span></span>

- <span data-ttu-id="e2cb5-119">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e2cb5-119">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e2cb5-120">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-120">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e2cb5-121">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e2cb5-121">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e2cb5-122">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-122">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e2cb5-123">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-123">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e2cb5-124">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-124">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e2cb5-125">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e2cb5-125">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e2cb5-126">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e2cb5-126">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e2cb5-127">ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-127">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="e2cb5-128">C\#</span><span class="sxs-lookup"><span data-stu-id="e2cb5-128">C\#</span></span>

<span data-ttu-id="e2cb5-129">Chcete-li změnit četnost fakturačního cyklu, aktualizujte vlastnost [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) .</span><span class="sxs-lookup"><span data-stu-id="e2cb5-129">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a><span data-ttu-id="e2cb5-130">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e2cb5-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e2cb5-131">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e2cb5-131">Request syntax</span></span>

| <span data-ttu-id="e2cb5-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="e2cb5-132">Method</span></span>    | <span data-ttu-id="e2cb5-133">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e2cb5-133">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e2cb5-134">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="e2cb5-134">**PATCH**</span></span> | <span data-ttu-id="e2cb5-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e2cb5-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e2cb5-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e2cb5-136">URI parameter</span></span>

<span data-ttu-id="e2cb5-137">Tato tabulka uvádí požadovaný parametr dotazu pro změnu množství předplatného.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-137">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="e2cb5-138">Název</span><span class="sxs-lookup"><span data-stu-id="e2cb5-138">Name</span></span>                   | <span data-ttu-id="e2cb5-139">Typ</span><span class="sxs-lookup"><span data-stu-id="e2cb5-139">Type</span></span> | <span data-ttu-id="e2cb5-140">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e2cb5-140">Required</span></span> | <span data-ttu-id="e2cb5-141">Popis</span><span class="sxs-lookup"><span data-stu-id="e2cb5-141">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="e2cb5-142">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="e2cb5-142">**customer-tenant-id**</span></span> | <span data-ttu-id="e2cb5-143">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="e2cb5-143">GUID</span></span> |    <span data-ttu-id="e2cb5-144">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-144">Y</span></span>     | <span data-ttu-id="e2cb5-145">IDENTIFIKÁTOR zákazníka s formátováním **ID tenanta** , který identifikuje zákazníka</span><span class="sxs-lookup"><span data-stu-id="e2cb5-145">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="e2cb5-146">**ID objednávky**</span><span class="sxs-lookup"><span data-stu-id="e2cb5-146">**order-id**</span></span>           | <span data-ttu-id="e2cb5-147">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="e2cb5-147">GUID</span></span> |    <span data-ttu-id="e2cb5-148">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-148">Y</span></span>     | <span data-ttu-id="e2cb5-149">Identifikátor objednávky</span><span class="sxs-lookup"><span data-stu-id="e2cb5-149">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="e2cb5-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e2cb5-150">Request headers</span></span>

<span data-ttu-id="e2cb5-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e2cb5-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e2cb5-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e2cb5-152">Request body</span></span>

<span data-ttu-id="e2cb5-153">V následujících tabulkách jsou popsány vlastnosti v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-153">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="e2cb5-154">Objednávka</span><span class="sxs-lookup"><span data-stu-id="e2cb5-154">Order</span></span>

| <span data-ttu-id="e2cb5-155">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="e2cb5-155">Property</span></span>           | <span data-ttu-id="e2cb5-156">Typ</span><span class="sxs-lookup"><span data-stu-id="e2cb5-156">Type</span></span>             | <span data-ttu-id="e2cb5-157">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e2cb5-157">Required</span></span> | <span data-ttu-id="e2cb5-158">Popis</span><span class="sxs-lookup"><span data-stu-id="e2cb5-158">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="e2cb5-159">Id</span><span class="sxs-lookup"><span data-stu-id="e2cb5-159">Id</span></span>                 | <span data-ttu-id="e2cb5-160">řetězec</span><span class="sxs-lookup"><span data-stu-id="e2cb5-160">string</span></span>           |    <span data-ttu-id="e2cb5-161">N</span><span class="sxs-lookup"><span data-stu-id="e2cb5-161">N</span></span>     | <span data-ttu-id="e2cb5-162">Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky</span><span class="sxs-lookup"><span data-stu-id="e2cb5-162">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="e2cb5-163">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="e2cb5-163">ReferenceCustomerId</span></span> | <span data-ttu-id="e2cb5-164">řetězec</span><span class="sxs-lookup"><span data-stu-id="e2cb5-164">string</span></span>           |    <span data-ttu-id="e2cb5-165">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-165">Y</span></span>     | <span data-ttu-id="e2cb5-166">Identifikátor zákazníka</span><span class="sxs-lookup"><span data-stu-id="e2cb5-166">The customer identifier</span></span>                                                    |
| <span data-ttu-id="e2cb5-167">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="e2cb5-167">BillingCycle</span></span>       | <span data-ttu-id="e2cb5-168">řetězec</span><span class="sxs-lookup"><span data-stu-id="e2cb5-168">string</span></span>           |    <span data-ttu-id="e2cb5-169">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-169">Y</span></span>     | <span data-ttu-id="e2cb5-170">Určuje četnost, s jakou se má partner fakturovat v této objednávce.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="e2cb5-171">Podporované hodnoty jsou názvy členů nalezené v [BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="e2cb5-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="e2cb5-172">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="e2cb5-172">LineItems</span></span>          | <span data-ttu-id="e2cb5-173">pole objektů</span><span class="sxs-lookup"><span data-stu-id="e2cb5-173">array of objects</span></span> |    <span data-ttu-id="e2cb5-174">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-174">Y</span></span>     | <span data-ttu-id="e2cb5-175">Pole prostředků [OrderLineItem](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="e2cb5-175">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="e2cb5-176">CreationDate</span><span class="sxs-lookup"><span data-stu-id="e2cb5-176">CreationDate</span></span>       | <span data-ttu-id="e2cb5-177">datetime</span><span class="sxs-lookup"><span data-stu-id="e2cb5-177">datetime</span></span>         |    <span data-ttu-id="e2cb5-178">N</span><span class="sxs-lookup"><span data-stu-id="e2cb5-178">N</span></span>     | <span data-ttu-id="e2cb5-179">Datum vytvoření objednávky ve formátu data a času</span><span class="sxs-lookup"><span data-stu-id="e2cb5-179">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="e2cb5-180">Atributy</span><span class="sxs-lookup"><span data-stu-id="e2cb5-180">Attributes</span></span>         | <span data-ttu-id="e2cb5-181">Objekt</span><span class="sxs-lookup"><span data-stu-id="e2cb5-181">Object</span></span>           |    <span data-ttu-id="e2cb5-182">N</span><span class="sxs-lookup"><span data-stu-id="e2cb5-182">N</span></span>     | <span data-ttu-id="e2cb5-183">Obsahuje ObjectType: "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="e2cb5-183">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="e2cb5-184">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="e2cb5-184">OrderLineItem</span></span>

| <span data-ttu-id="e2cb5-185">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="e2cb5-185">Property</span></span>             | <span data-ttu-id="e2cb5-186">Typ</span><span class="sxs-lookup"><span data-stu-id="e2cb5-186">Type</span></span>   | <span data-ttu-id="e2cb5-187">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e2cb5-187">Required</span></span> | <span data-ttu-id="e2cb5-188">Popis</span><span class="sxs-lookup"><span data-stu-id="e2cb5-188">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="e2cb5-189">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="e2cb5-189">LineItemNumber</span></span>       | <span data-ttu-id="e2cb5-190">číslo</span><span class="sxs-lookup"><span data-stu-id="e2cb5-190">number</span></span> |    <span data-ttu-id="e2cb5-191">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-191">Y</span></span>     | <span data-ttu-id="e2cb5-192">Číslo položky řádku začínající na 0</span><span class="sxs-lookup"><span data-stu-id="e2cb5-192">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="e2cb5-193">Hodnotami OfferId</span><span class="sxs-lookup"><span data-stu-id="e2cb5-193">OfferId</span></span>              | <span data-ttu-id="e2cb5-194">řetězec</span><span class="sxs-lookup"><span data-stu-id="e2cb5-194">string</span></span> |    <span data-ttu-id="e2cb5-195">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-195">Y</span></span>     | <span data-ttu-id="e2cb5-196">ID nabídky</span><span class="sxs-lookup"><span data-stu-id="e2cb5-196">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="e2cb5-197">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="e2cb5-197">SubscriptionId</span></span>       | <span data-ttu-id="e2cb5-198">řetězec</span><span class="sxs-lookup"><span data-stu-id="e2cb5-198">string</span></span> |    <span data-ttu-id="e2cb5-199">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-199">Y</span></span>     | <span data-ttu-id="e2cb5-200">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="e2cb5-200">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="e2cb5-201">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="e2cb5-201">FriendlyName</span></span>         | <span data-ttu-id="e2cb5-202">řetězec</span><span class="sxs-lookup"><span data-stu-id="e2cb5-202">string</span></span> |    <span data-ttu-id="e2cb5-203">N</span><span class="sxs-lookup"><span data-stu-id="e2cb5-203">N</span></span>     | <span data-ttu-id="e2cb5-204">Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost</span><span class="sxs-lookup"><span data-stu-id="e2cb5-204">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="e2cb5-205">Množství</span><span class="sxs-lookup"><span data-stu-id="e2cb5-205">Quantity</span></span>             | <span data-ttu-id="e2cb5-206">číslo</span><span class="sxs-lookup"><span data-stu-id="e2cb5-206">number</span></span> |    <span data-ttu-id="e2cb5-207">Y</span><span class="sxs-lookup"><span data-stu-id="e2cb5-207">Y</span></span>     | <span data-ttu-id="e2cb5-208">Počet licencí nebo instancí</span><span class="sxs-lookup"><span data-stu-id="e2cb5-208">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="e2cb5-209">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="e2cb5-209">PartnerIdOnRecord</span></span>    | <span data-ttu-id="e2cb5-210">řetězec</span><span class="sxs-lookup"><span data-stu-id="e2cb5-210">string</span></span> |    <span data-ttu-id="e2cb5-211">N</span><span class="sxs-lookup"><span data-stu-id="e2cb5-211">N</span></span>     | <span data-ttu-id="e2cb5-212">ID MPN partnera záznamu</span><span class="sxs-lookup"><span data-stu-id="e2cb5-212">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="e2cb5-213">Atributy</span><span class="sxs-lookup"><span data-stu-id="e2cb5-213">Attributes</span></span>           | <span data-ttu-id="e2cb5-214">Objekt</span><span class="sxs-lookup"><span data-stu-id="e2cb5-214">Object</span></span> |    <span data-ttu-id="e2cb5-215">N</span><span class="sxs-lookup"><span data-stu-id="e2cb5-215">N</span></span>     | <span data-ttu-id="e2cb5-216">Obsahuje ObjectType: "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="e2cb5-216">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="e2cb5-217">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e2cb5-217">Request example</span></span>

<span data-ttu-id="e2cb5-218">Aktualizace na roční fakturaci</span><span class="sxs-lookup"><span data-stu-id="e2cb5-218">Update to annual billing</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
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

## <a name="rest-response"></a><span data-ttu-id="e2cb5-219">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e2cb5-219">REST response</span></span>

<span data-ttu-id="e2cb5-220">V případě úspěchu tato metoda vrátí aktualizované pořadí předplatného v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-220">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e2cb5-221">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e2cb5-221">Response success and error codes</span></span>

<span data-ttu-id="e2cb5-222">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-222">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e2cb5-223">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e2cb5-223">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e2cb5-224">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e2cb5-224">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e2cb5-225">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e2cb5-225">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "Annual",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```