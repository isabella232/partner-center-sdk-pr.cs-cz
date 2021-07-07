---
title: Změna fakturačního cyklu
description: Naučte se aktualizovat předplatné zákazníka na měsíční nebo roční fakturaci pomocí rozhraní API partnerského centra. Můžete to provést taky z řídicího panelu partnerského centra.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 435309229e2cb038c936028943f4c2cf27b032a7
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974110"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="be14e-104">Změna fakturačního cyklu zákaznického předplatného</span><span class="sxs-lookup"><span data-stu-id="be14e-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="be14e-105">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="be14e-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="be14e-106">Aktualizuje [objednávku](order-resources.md) z měsíčního na roční fakturace nebo z roční na měsíční fakturaci.</span><span class="sxs-lookup"><span data-stu-id="be14e-106">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="be14e-107">Na řídicím panelu partnerského centra můžete tuto operaci provést přechodem na stránku s podrobnostmi o předplatném zákazníka.</span><span class="sxs-lookup"><span data-stu-id="be14e-107">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="be14e-108">Po tomto případě se zobrazí možnost definující aktuální fakturační cyklus pro předplatné s možností změny a odeslání.</span><span class="sxs-lookup"><span data-stu-id="be14e-108">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="be14e-109">**Mimo rozsah** tohoto článku:</span><span class="sxs-lookup"><span data-stu-id="be14e-109">**Out of scope** for this article:</span></span>

- <span data-ttu-id="be14e-110">Změna fakturačního cyklu pro zkušební verze</span><span class="sxs-lookup"><span data-stu-id="be14e-110">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="be14e-111">Změna fakturačních cyklů pro jakékoli neroční nabídky (měsíčně, šest let) & předplatných Azure</span><span class="sxs-lookup"><span data-stu-id="be14e-111">Changing the billing cycles for any non-annual term offers (monthly, six-year) & Azure subscriptions</span></span>
- <span data-ttu-id="be14e-112">Změna fakturačních cyklů pro neaktivní předplatná</span><span class="sxs-lookup"><span data-stu-id="be14e-112">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="be14e-113">Změna fakturačních cyklů pro odběry založené na licencích Microsoft online služby</span><span class="sxs-lookup"><span data-stu-id="be14e-113">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be14e-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="be14e-114">Prerequisites</span></span>

- <span data-ttu-id="be14e-115">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="be14e-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="be14e-116">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="be14e-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="be14e-117">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="be14e-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="be14e-118">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="be14e-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="be14e-119">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="be14e-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="be14e-120">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="be14e-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="be14e-121">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="be14e-121">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="be14e-122">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="be14e-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="be14e-123">ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="be14e-123">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="be14e-124">C\#</span><span class="sxs-lookup"><span data-stu-id="be14e-124">C\#</span></span>

<span data-ttu-id="be14e-125">Chcete-li změnit četnost fakturačního cyklu, aktualizujte vlastnost [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) .</span><span class="sxs-lookup"><span data-stu-id="be14e-125">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="be14e-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="be14e-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="be14e-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="be14e-127">Request syntax</span></span>

| <span data-ttu-id="be14e-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="be14e-128">Method</span></span>    | <span data-ttu-id="be14e-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="be14e-129">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="be14e-130">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="be14e-130">**PATCH**</span></span> | <span data-ttu-id="be14e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="be14e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="be14e-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="be14e-132">URI parameter</span></span>

<span data-ttu-id="be14e-133">Tato tabulka uvádí požadovaný parametr dotazu pro změnu množství předplatného.</span><span class="sxs-lookup"><span data-stu-id="be14e-133">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="be14e-134">Název</span><span class="sxs-lookup"><span data-stu-id="be14e-134">Name</span></span>                   | <span data-ttu-id="be14e-135">Typ</span><span class="sxs-lookup"><span data-stu-id="be14e-135">Type</span></span> | <span data-ttu-id="be14e-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="be14e-136">Required</span></span> | <span data-ttu-id="be14e-137">Popis</span><span class="sxs-lookup"><span data-stu-id="be14e-137">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="be14e-138">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="be14e-138">**customer-tenant-id**</span></span> | <span data-ttu-id="be14e-139">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="be14e-139">GUID</span></span> |    <span data-ttu-id="be14e-140">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-140">Y</span></span>     | <span data-ttu-id="be14e-141">IDENTIFIKÁTOR zákazníka s formátováním **ID tenanta** , který identifikuje zákazníka</span><span class="sxs-lookup"><span data-stu-id="be14e-141">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="be14e-142">**ID objednávky**</span><span class="sxs-lookup"><span data-stu-id="be14e-142">**order-id**</span></span>           | <span data-ttu-id="be14e-143">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="be14e-143">GUID</span></span> |    <span data-ttu-id="be14e-144">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-144">Y</span></span>     | <span data-ttu-id="be14e-145">Identifikátor objednávky</span><span class="sxs-lookup"><span data-stu-id="be14e-145">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="be14e-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="be14e-146">Request headers</span></span>

<span data-ttu-id="be14e-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="be14e-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="be14e-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="be14e-148">Request body</span></span>

<span data-ttu-id="be14e-149">V následujících tabulkách jsou popsány vlastnosti v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="be14e-149">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="be14e-150">Objednávka</span><span class="sxs-lookup"><span data-stu-id="be14e-150">Order</span></span>

| <span data-ttu-id="be14e-151">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="be14e-151">Property</span></span>           | <span data-ttu-id="be14e-152">Typ</span><span class="sxs-lookup"><span data-stu-id="be14e-152">Type</span></span>             | <span data-ttu-id="be14e-153">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="be14e-153">Required</span></span> | <span data-ttu-id="be14e-154">Popis</span><span class="sxs-lookup"><span data-stu-id="be14e-154">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="be14e-155">Id</span><span class="sxs-lookup"><span data-stu-id="be14e-155">Id</span></span>                 | <span data-ttu-id="be14e-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="be14e-156">string</span></span>           |    <span data-ttu-id="be14e-157">N</span><span class="sxs-lookup"><span data-stu-id="be14e-157">N</span></span>     | <span data-ttu-id="be14e-158">Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky</span><span class="sxs-lookup"><span data-stu-id="be14e-158">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="be14e-159">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="be14e-159">ReferenceCustomerId</span></span> | <span data-ttu-id="be14e-160">řetězec</span><span class="sxs-lookup"><span data-stu-id="be14e-160">string</span></span>           |    <span data-ttu-id="be14e-161">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-161">Y</span></span>     | <span data-ttu-id="be14e-162">Identifikátor zákazníka</span><span class="sxs-lookup"><span data-stu-id="be14e-162">The customer identifier</span></span>                                                    |
| <span data-ttu-id="be14e-163">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="be14e-163">BillingCycle</span></span>       | <span data-ttu-id="be14e-164">řetězec</span><span class="sxs-lookup"><span data-stu-id="be14e-164">string</span></span>           |    <span data-ttu-id="be14e-165">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-165">Y</span></span>     | <span data-ttu-id="be14e-166">Určuje četnost, s jakou se má partner fakturovat v této objednávce.</span><span class="sxs-lookup"><span data-stu-id="be14e-166">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="be14e-167">Podporované hodnoty jsou názvy členů nalezené v [BillingCycleType](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="be14e-167">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="be14e-168">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="be14e-168">LineItems</span></span>          | <span data-ttu-id="be14e-169">pole objektů</span><span class="sxs-lookup"><span data-stu-id="be14e-169">array of objects</span></span> |    <span data-ttu-id="be14e-170">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-170">Y</span></span>     | <span data-ttu-id="be14e-171">Pole prostředků [OrderLineItem](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="be14e-171">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="be14e-172">CreationDate</span><span class="sxs-lookup"><span data-stu-id="be14e-172">CreationDate</span></span>       | <span data-ttu-id="be14e-173">datetime</span><span class="sxs-lookup"><span data-stu-id="be14e-173">datetime</span></span>         |    <span data-ttu-id="be14e-174">N</span><span class="sxs-lookup"><span data-stu-id="be14e-174">N</span></span>     | <span data-ttu-id="be14e-175">Datum vytvoření objednávky ve formátu data a času</span><span class="sxs-lookup"><span data-stu-id="be14e-175">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="be14e-176">Atributy</span><span class="sxs-lookup"><span data-stu-id="be14e-176">Attributes</span></span>         | <span data-ttu-id="be14e-177">Objekt</span><span class="sxs-lookup"><span data-stu-id="be14e-177">Object</span></span>           |    <span data-ttu-id="be14e-178">N</span><span class="sxs-lookup"><span data-stu-id="be14e-178">N</span></span>     | <span data-ttu-id="be14e-179">Obsahuje ObjectType: "OrderLineItem"</span><span class="sxs-lookup"><span data-stu-id="be14e-179">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="be14e-180">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="be14e-180">OrderLineItem</span></span>

| <span data-ttu-id="be14e-181">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="be14e-181">Property</span></span>             | <span data-ttu-id="be14e-182">Typ</span><span class="sxs-lookup"><span data-stu-id="be14e-182">Type</span></span>   | <span data-ttu-id="be14e-183">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="be14e-183">Required</span></span> | <span data-ttu-id="be14e-184">Popis</span><span class="sxs-lookup"><span data-stu-id="be14e-184">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="be14e-185">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="be14e-185">LineItemNumber</span></span>       | <span data-ttu-id="be14e-186">číslo</span><span class="sxs-lookup"><span data-stu-id="be14e-186">number</span></span> |    <span data-ttu-id="be14e-187">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-187">Y</span></span>     | <span data-ttu-id="be14e-188">Číslo položky řádku začínající na 0</span><span class="sxs-lookup"><span data-stu-id="be14e-188">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="be14e-189">Hodnotami OfferId</span><span class="sxs-lookup"><span data-stu-id="be14e-189">OfferId</span></span>              | <span data-ttu-id="be14e-190">řetězec</span><span class="sxs-lookup"><span data-stu-id="be14e-190">string</span></span> |    <span data-ttu-id="be14e-191">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-191">Y</span></span>     | <span data-ttu-id="be14e-192">ID nabídky</span><span class="sxs-lookup"><span data-stu-id="be14e-192">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="be14e-193">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="be14e-193">SubscriptionId</span></span>       | <span data-ttu-id="be14e-194">řetězec</span><span class="sxs-lookup"><span data-stu-id="be14e-194">string</span></span> |    <span data-ttu-id="be14e-195">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-195">Y</span></span>     | <span data-ttu-id="be14e-196">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="be14e-196">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="be14e-197">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="be14e-197">FriendlyName</span></span>         | <span data-ttu-id="be14e-198">řetězec</span><span class="sxs-lookup"><span data-stu-id="be14e-198">string</span></span> |    <span data-ttu-id="be14e-199">N</span><span class="sxs-lookup"><span data-stu-id="be14e-199">N</span></span>     | <span data-ttu-id="be14e-200">Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost</span><span class="sxs-lookup"><span data-stu-id="be14e-200">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="be14e-201">Množství</span><span class="sxs-lookup"><span data-stu-id="be14e-201">Quantity</span></span>             | <span data-ttu-id="be14e-202">číslo</span><span class="sxs-lookup"><span data-stu-id="be14e-202">number</span></span> |    <span data-ttu-id="be14e-203">Y</span><span class="sxs-lookup"><span data-stu-id="be14e-203">Y</span></span>     | <span data-ttu-id="be14e-204">Počet licencí nebo instancí</span><span class="sxs-lookup"><span data-stu-id="be14e-204">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="be14e-205">Id partneraZáznam</span><span class="sxs-lookup"><span data-stu-id="be14e-205">PartnerIdOnRecord</span></span>    | <span data-ttu-id="be14e-206">řetězec</span><span class="sxs-lookup"><span data-stu-id="be14e-206">string</span></span> |    <span data-ttu-id="be14e-207">N</span><span class="sxs-lookup"><span data-stu-id="be14e-207">N</span></span>     | <span data-ttu-id="be14e-208">ID MPN záznamu partnera</span><span class="sxs-lookup"><span data-stu-id="be14e-208">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="be14e-209">Atributy</span><span class="sxs-lookup"><span data-stu-id="be14e-209">Attributes</span></span>           | <span data-ttu-id="be14e-210">Objekt</span><span class="sxs-lookup"><span data-stu-id="be14e-210">Object</span></span> |    <span data-ttu-id="be14e-211">N</span><span class="sxs-lookup"><span data-stu-id="be14e-211">N</span></span>     | <span data-ttu-id="be14e-212">Obsahuje ObjectType: OrderLineItem.</span><span class="sxs-lookup"><span data-stu-id="be14e-212">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="be14e-213">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="be14e-213">Request example</span></span>

<span data-ttu-id="be14e-214">Aktualizace na roční fakturaci</span><span class="sxs-lookup"><span data-stu-id="be14e-214">Update to annual billing</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="be14e-215">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="be14e-215">REST response</span></span>

<span data-ttu-id="be14e-216">V případě úspěchu vrátí tato metoda v textu odpovědi aktualizované pořadí odběru.</span><span class="sxs-lookup"><span data-stu-id="be14e-216">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="be14e-217">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="be14e-217">Response success and error codes</span></span>

<span data-ttu-id="be14e-218">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="be14e-218">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="be14e-219">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="be14e-219">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="be14e-220">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="be14e-220">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="be14e-221">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="be14e-221">Response example</span></span>

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