---
title: Aktualizace košíku
description: Jak aktualizovat objednávku pro zákazníka na vozíku
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766731"
---
# <a name="update-a-cart"></a><span data-ttu-id="028b4-103">Aktualizace košíku</span><span class="sxs-lookup"><span data-stu-id="028b4-103">Update a cart</span></span>

<span data-ttu-id="028b4-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="028b4-104">**Applies To**</span></span>

- <span data-ttu-id="028b4-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="028b4-105">Partner Center</span></span>

<span data-ttu-id="028b4-106">Jak aktualizovat objednávku pro zákazníka na vozíku</span><span class="sxs-lookup"><span data-stu-id="028b4-106">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="028b4-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="028b4-107">Prerequisites</span></span>

- <span data-ttu-id="028b4-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="028b4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="028b4-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="028b4-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="028b4-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="028b4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="028b4-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="028b4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="028b4-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="028b4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="028b4-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="028b4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="028b4-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="028b4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="028b4-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="028b4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="028b4-116">ID košíku pro existující košík.</span><span class="sxs-lookup"><span data-stu-id="028b4-116">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="028b4-117">C\#</span><span class="sxs-lookup"><span data-stu-id="028b4-117">C\#</span></span>

<span data-ttu-id="028b4-118">Chcete-li aktualizovat objednávku pro zákazníka, Získejte pomocí metody **Get ()** vozík pomocí funkce **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="028b4-118">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart ID's using the **ById()** function.</span></span> <span data-ttu-id="028b4-119">Proveďte potřebné změny košíku.</span><span class="sxs-lookup"><span data-stu-id="028b4-119">Make the necessary changes to the cart.</span></span> <span data-ttu-id="028b4-120">Nyní zavolejte metodu **Put** pomocí ID zákazníka a košíku pomocí metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="028b4-120">Now call the **Put** method by using customer and cart ID's using the **ById()** method.</span></span>

<span data-ttu-id="028b4-121">Nakonec zavolejte metodu **Put ()** nebo **PutAsync ()** pro vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="028b4-121">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="028b4-122">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="028b4-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="028b4-123">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="028b4-123">Request syntax</span></span>

| <span data-ttu-id="028b4-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="028b4-124">Method</span></span>  | <span data-ttu-id="028b4-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="028b4-125">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="028b4-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="028b4-126">**PUT**</span></span> | <span data-ttu-id="028b4-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{Cart-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="028b4-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="028b4-128">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="028b4-128">URI parameters</span></span>

<span data-ttu-id="028b4-129">K identifikaci zákazníka použijte následující parametry cesty a určete, který vozík se má aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="028b4-129">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="028b4-130">Název</span><span class="sxs-lookup"><span data-stu-id="028b4-130">Name</span></span>            | <span data-ttu-id="028b4-131">Typ</span><span class="sxs-lookup"><span data-stu-id="028b4-131">Type</span></span>     | <span data-ttu-id="028b4-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="028b4-132">Required</span></span> | <span data-ttu-id="028b4-133">Popis</span><span class="sxs-lookup"><span data-stu-id="028b4-133">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="028b4-134">**ID zákazníka**</span><span class="sxs-lookup"><span data-stu-id="028b4-134">**customer-id**</span></span> | <span data-ttu-id="028b4-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-135">string</span></span>   | <span data-ttu-id="028b4-136">Yes</span><span class="sxs-lookup"><span data-stu-id="028b4-136">Yes</span></span>      | <span data-ttu-id="028b4-137">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="028b4-137">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="028b4-138">**košík – ID**</span><span class="sxs-lookup"><span data-stu-id="028b4-138">**cart-id**</span></span>     | <span data-ttu-id="028b4-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-139">string</span></span>   | <span data-ttu-id="028b4-140">Yes</span><span class="sxs-lookup"><span data-stu-id="028b4-140">Yes</span></span>      | <span data-ttu-id="028b4-141">Identifikátor košíku formátovaného identifikátorem GUID, který identifikuje vozík.</span><span class="sxs-lookup"><span data-stu-id="028b4-141">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="028b4-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="028b4-142">Request headers</span></span>

<span data-ttu-id="028b4-143">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="028b4-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="028b4-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="028b4-144">Request body</span></span>

<span data-ttu-id="028b4-145">Tato tabulka popisuje vlastnosti [košíku](cart-resources.md) v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="028b4-145">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="028b4-146">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="028b4-146">Property</span></span>              | <span data-ttu-id="028b4-147">Typ</span><span class="sxs-lookup"><span data-stu-id="028b4-147">Type</span></span>             | <span data-ttu-id="028b4-148">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="028b4-148">Required</span></span>        | <span data-ttu-id="028b4-149">Popis</span><span class="sxs-lookup"><span data-stu-id="028b4-149">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="028b4-150">id</span><span class="sxs-lookup"><span data-stu-id="028b4-150">id</span></span>                    | <span data-ttu-id="028b4-151">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-151">string</span></span>           | <span data-ttu-id="028b4-152">No</span><span class="sxs-lookup"><span data-stu-id="028b4-152">No</span></span>              | <span data-ttu-id="028b4-153">Identifikátor košíku, který se zadal po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="028b4-153">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="028b4-154">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="028b4-154">creationTimeStamp</span></span>     | <span data-ttu-id="028b4-155">DateTime</span><span class="sxs-lookup"><span data-stu-id="028b4-155">DateTime</span></span>         | <span data-ttu-id="028b4-156">No</span><span class="sxs-lookup"><span data-stu-id="028b4-156">No</span></span>              | <span data-ttu-id="028b4-157">Datum, kdy byl košík vytvořen, ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="028b4-157">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="028b4-158">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="028b4-158">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="028b4-159">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="028b4-159">lastModifiedTimeStamp</span></span> | <span data-ttu-id="028b4-160">DateTime</span><span class="sxs-lookup"><span data-stu-id="028b4-160">DateTime</span></span>         | <span data-ttu-id="028b4-161">No</span><span class="sxs-lookup"><span data-stu-id="028b4-161">No</span></span>              | <span data-ttu-id="028b4-162">Datum poslední aktualizace košíku ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="028b4-162">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="028b4-163">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="028b4-163">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="028b4-164">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="028b4-164">expirationTimeStamp</span></span>   | <span data-ttu-id="028b4-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="028b4-165">DateTime</span></span>         | <span data-ttu-id="028b4-166">No</span><span class="sxs-lookup"><span data-stu-id="028b4-166">No</span></span>              | <span data-ttu-id="028b4-167">Datum, kdy vyprší platnost košíku, ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="028b4-167">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="028b4-168">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="028b4-168">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="028b4-169">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="028b4-169">lastModifiedUser</span></span>      | <span data-ttu-id="028b4-170">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-170">string</span></span>           | <span data-ttu-id="028b4-171">No</span><span class="sxs-lookup"><span data-stu-id="028b4-171">No</span></span>              | <span data-ttu-id="028b4-172">Uživatel, který kartu naposledy aktualizoval.</span><span class="sxs-lookup"><span data-stu-id="028b4-172">The user who last updated the cart.</span></span> <span data-ttu-id="028b4-173">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="028b4-173">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="028b4-174">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="028b4-174">lineItems</span></span>             | <span data-ttu-id="028b4-175">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="028b4-175">Array of objects</span></span> | <span data-ttu-id="028b4-176">Yes</span><span class="sxs-lookup"><span data-stu-id="028b4-176">Yes</span></span>             | <span data-ttu-id="028b4-177">Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="028b4-177">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="028b4-178">Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="028b4-178">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="028b4-179">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="028b4-179">Property</span></span>             | <span data-ttu-id="028b4-180">Typ</span><span class="sxs-lookup"><span data-stu-id="028b4-180">Type</span></span>                        | <span data-ttu-id="028b4-181">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="028b4-181">Required</span></span>     | <span data-ttu-id="028b4-182">Popis</span><span class="sxs-lookup"><span data-stu-id="028b4-182">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="028b4-183">id</span><span class="sxs-lookup"><span data-stu-id="028b4-183">id</span></span>                   | <span data-ttu-id="028b4-184">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-184">string</span></span>                      | <span data-ttu-id="028b4-185">No</span><span class="sxs-lookup"><span data-stu-id="028b4-185">No</span></span>           | <span data-ttu-id="028b4-186">Jedinečný identifikátor položky řádku košíku</span><span class="sxs-lookup"><span data-stu-id="028b4-186">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="028b4-187">Použito po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="028b4-187">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="028b4-188">catalogId</span><span class="sxs-lookup"><span data-stu-id="028b4-188">catalogId</span></span>            | <span data-ttu-id="028b4-189">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-189">string</span></span>                      | <span data-ttu-id="028b4-190">Yes</span><span class="sxs-lookup"><span data-stu-id="028b4-190">Yes</span></span>          | <span data-ttu-id="028b4-191">Identifikátor položky katalogu</span><span class="sxs-lookup"><span data-stu-id="028b4-191">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="028b4-192">friendlyName</span><span class="sxs-lookup"><span data-stu-id="028b4-192">friendlyName</span></span>         | <span data-ttu-id="028b4-193">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-193">string</span></span>                      | <span data-ttu-id="028b4-194">No</span><span class="sxs-lookup"><span data-stu-id="028b4-194">No</span></span>           | <span data-ttu-id="028b4-195">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="028b4-195">Optional.</span></span> <span data-ttu-id="028b4-196">Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.</span><span class="sxs-lookup"><span data-stu-id="028b4-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="028b4-197">quantity</span><span class="sxs-lookup"><span data-stu-id="028b4-197">quantity</span></span>             | <span data-ttu-id="028b4-198">int</span><span class="sxs-lookup"><span data-stu-id="028b4-198">int</span></span>                         | <span data-ttu-id="028b4-199">Yes</span><span class="sxs-lookup"><span data-stu-id="028b4-199">Yes</span></span>          | <span data-ttu-id="028b4-200">Počet licencí nebo instancí.</span><span class="sxs-lookup"><span data-stu-id="028b4-200">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="028b4-201">currencyCode</span><span class="sxs-lookup"><span data-stu-id="028b4-201">currencyCode</span></span>         | <span data-ttu-id="028b4-202">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-202">string</span></span>                      | <span data-ttu-id="028b4-203">No</span><span class="sxs-lookup"><span data-stu-id="028b4-203">No</span></span>           | <span data-ttu-id="028b4-204">Kód měny.</span><span class="sxs-lookup"><span data-stu-id="028b4-204">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="028b4-205">billingCycle</span><span class="sxs-lookup"><span data-stu-id="028b4-205">billingCycle</span></span>         | <span data-ttu-id="028b4-206">Objekt</span><span class="sxs-lookup"><span data-stu-id="028b4-206">Object</span></span>                      | <span data-ttu-id="028b4-207">Yes</span><span class="sxs-lookup"><span data-stu-id="028b4-207">Yes</span></span>          | <span data-ttu-id="028b4-208">Typ fakturačního cyklu nastaveného pro aktuální období.</span><span class="sxs-lookup"><span data-stu-id="028b4-208">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="028b4-209">členům</span><span class="sxs-lookup"><span data-stu-id="028b4-209">participants</span></span>         | <span data-ttu-id="028b4-210">Seznam párů řetězců objektů</span><span class="sxs-lookup"><span data-stu-id="028b4-210">List of Object String pairs</span></span> | <span data-ttu-id="028b4-211">No</span><span class="sxs-lookup"><span data-stu-id="028b4-211">No</span></span>           | <span data-ttu-id="028b4-212">Kolekce účastníků na nákupu</span><span class="sxs-lookup"><span data-stu-id="028b4-212">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="028b4-213">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="028b4-213">provisioningContext</span></span>  | <span data-ttu-id="028b4-214">Řetězec<slovníku, řetězec></span><span class="sxs-lookup"><span data-stu-id="028b4-214">Dictionary<string, string></span></span>  | <span data-ttu-id="028b4-215">No</span><span class="sxs-lookup"><span data-stu-id="028b4-215">No</span></span>           | <span data-ttu-id="028b4-216">Kontext použitý ke zřízení nabídky.</span><span class="sxs-lookup"><span data-stu-id="028b4-216">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="028b4-217">pořadí</span><span class="sxs-lookup"><span data-stu-id="028b4-217">orderGroup</span></span>           | <span data-ttu-id="028b4-218">řetězec</span><span class="sxs-lookup"><span data-stu-id="028b4-218">string</span></span>                      | <span data-ttu-id="028b4-219">No</span><span class="sxs-lookup"><span data-stu-id="028b4-219">No</span></span>           | <span data-ttu-id="028b4-220">Skupina, která označuje, které položky lze umístit dohromady.</span><span class="sxs-lookup"><span data-stu-id="028b4-220">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="028b4-221">error</span><span class="sxs-lookup"><span data-stu-id="028b4-221">error</span></span>                | <span data-ttu-id="028b4-222">Objekt</span><span class="sxs-lookup"><span data-stu-id="028b4-222">Object</span></span>                      | <span data-ttu-id="028b4-223">No</span><span class="sxs-lookup"><span data-stu-id="028b4-223">No</span></span>           | <span data-ttu-id="028b4-224">Používá se po vytvoření košíku v případě chyby.</span><span class="sxs-lookup"><span data-stu-id="028b4-224">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="028b4-225">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="028b4-225">Request example</span></span>

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
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
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="028b4-226">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="028b4-226">REST response</span></span>

<span data-ttu-id="028b4-227">V případě úspěchu tato metoda vrátí prostředek vyplněné [vozíku](cart-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="028b4-227">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="028b4-228">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="028b4-228">Response success and error codes</span></span>

<span data-ttu-id="028b4-229">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="028b4-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="028b4-230">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="028b4-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="028b4-231">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="028b4-231">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="028b4-232">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="028b4-232">Response example</span></span>

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
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
