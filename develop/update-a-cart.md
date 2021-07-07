---
title: Aktualizace košíku
description: Jak aktualizovat objednávku zákazníka v košíku
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8954d4dad39f9b1a1b9a2f213e0231f01856fcd2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446679"
---
# <a name="update-a-cart"></a><span data-ttu-id="ced7e-103">Aktualizace košíku</span><span class="sxs-lookup"><span data-stu-id="ced7e-103">Update a cart</span></span>

<span data-ttu-id="ced7e-104">Jak aktualizovat objednávku zákazníka v košíku</span><span class="sxs-lookup"><span data-stu-id="ced7e-104">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ced7e-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ced7e-105">Prerequisites</span></span>

- <span data-ttu-id="ced7e-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ced7e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ced7e-107">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ced7e-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ced7e-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ced7e-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ced7e-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ced7e-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ced7e-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="ced7e-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ced7e-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="ced7e-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ced7e-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ced7e-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ced7e-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ced7e-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ced7e-114">ID košíku pro existující košík</span><span class="sxs-lookup"><span data-stu-id="ced7e-114">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="ced7e-115">C\#</span><span class="sxs-lookup"><span data-stu-id="ced7e-115">C\#</span></span>

<span data-ttu-id="ced7e-116">Pokud chcete aktualizovat objednávku zákazníka, získejte košík pomocí metody **Get()** předáním ID zákazníků a košíků pomocí funkce **ById().**</span><span class="sxs-lookup"><span data-stu-id="ced7e-116">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart IDs using the **ById()** function.</span></span> <span data-ttu-id="ced7e-117">Proveďte potřebné změny v košíku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-117">Make the necessary changes to the cart.</span></span> <span data-ttu-id="ced7e-118">Teď zavolejte **metodu Put** pomocí ID zákazníků a košíků pomocí metody **ById().**</span><span class="sxs-lookup"><span data-stu-id="ced7e-118">Now call the **Put** method by using customer and cart IDs using the **ById()** method.</span></span>

<span data-ttu-id="ced7e-119">Nakonec zavolejte **metodu Put()** nebo **PutAsync()** a vytvořte pořadí.</span><span class="sxs-lookup"><span data-stu-id="ced7e-119">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="ced7e-120">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="ced7e-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ced7e-121">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="ced7e-121">Request syntax</span></span>

| <span data-ttu-id="ced7e-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="ced7e-122">Method</span></span>  | <span data-ttu-id="ced7e-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ced7e-123">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ced7e-124">**PUT**</span><span class="sxs-lookup"><span data-stu-id="ced7e-124">**PUT**</span></span> | <span data-ttu-id="ced7e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/carts/{ID_košíku} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ced7e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="ced7e-126">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="ced7e-126">URI parameters</span></span>

<span data-ttu-id="ced7e-127">Pomocí následujících parametrů cesty identifikujte zákazníka a zadejte košík, který se má aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="ced7e-127">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="ced7e-128">Název</span><span class="sxs-lookup"><span data-stu-id="ced7e-128">Name</span></span>            | <span data-ttu-id="ced7e-129">Typ</span><span class="sxs-lookup"><span data-stu-id="ced7e-129">Type</span></span>     | <span data-ttu-id="ced7e-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ced7e-130">Required</span></span> | <span data-ttu-id="ced7e-131">Popis</span><span class="sxs-lookup"><span data-stu-id="ced7e-131">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="ced7e-132">**id zákazníka**</span><span class="sxs-lookup"><span data-stu-id="ced7e-132">**customer-id**</span></span> | <span data-ttu-id="ced7e-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-133">string</span></span>   | <span data-ttu-id="ced7e-134">Yes</span><span class="sxs-lookup"><span data-stu-id="ced7e-134">Yes</span></span>      | <span data-ttu-id="ced7e-135">Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ced7e-135">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="ced7e-136">**cart-id**</span><span class="sxs-lookup"><span data-stu-id="ced7e-136">**cart-id**</span></span>     | <span data-ttu-id="ced7e-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-137">string</span></span>   | <span data-ttu-id="ced7e-138">Yes</span><span class="sxs-lookup"><span data-stu-id="ced7e-138">Yes</span></span>      | <span data-ttu-id="ced7e-139">Identifikátor CART-ID formátovaný identifikátorem GUID, který identifikuje košík.</span><span class="sxs-lookup"><span data-stu-id="ced7e-139">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="ced7e-140">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ced7e-140">Request headers</span></span>

<span data-ttu-id="ced7e-141">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ced7e-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ced7e-142">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ced7e-142">Request body</span></span>

<span data-ttu-id="ced7e-143">Tato tabulka popisuje vlastnosti [Cart](cart-resources.md) (Košík) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-143">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="ced7e-144">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ced7e-144">Property</span></span>              | <span data-ttu-id="ced7e-145">Typ</span><span class="sxs-lookup"><span data-stu-id="ced7e-145">Type</span></span>             | <span data-ttu-id="ced7e-146">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ced7e-146">Required</span></span>        | <span data-ttu-id="ced7e-147">Popis</span><span class="sxs-lookup"><span data-stu-id="ced7e-147">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ced7e-148">id</span><span class="sxs-lookup"><span data-stu-id="ced7e-148">id</span></span>                    | <span data-ttu-id="ced7e-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-149">string</span></span>           | <span data-ttu-id="ced7e-150">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-150">No</span></span>              | <span data-ttu-id="ced7e-151">Identifikátor košíku, který se dodá po úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-151">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="ced7e-152">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ced7e-152">creationTimeStamp</span></span>     | <span data-ttu-id="ced7e-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="ced7e-153">DateTime</span></span>         | <span data-ttu-id="ced7e-154">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-154">No</span></span>              | <span data-ttu-id="ced7e-155">Datum vytvoření košíku ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="ced7e-155">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="ced7e-156">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-156">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="ced7e-157">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ced7e-157">lastModifiedTimeStamp</span></span> | <span data-ttu-id="ced7e-158">DateTime</span><span class="sxs-lookup"><span data-stu-id="ced7e-158">DateTime</span></span>         | <span data-ttu-id="ced7e-159">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-159">No</span></span>              | <span data-ttu-id="ced7e-160">Datum poslední aktualizace košíku ve formátu data a času</span><span class="sxs-lookup"><span data-stu-id="ced7e-160">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="ced7e-161">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-161">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="ced7e-162">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="ced7e-162">expirationTimeStamp</span></span>   | <span data-ttu-id="ced7e-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="ced7e-163">DateTime</span></span>         | <span data-ttu-id="ced7e-164">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-164">No</span></span>              | <span data-ttu-id="ced7e-165">Datum, kdy vyprší platnost košíku ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="ced7e-165">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="ced7e-166">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-166">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="ced7e-167">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="ced7e-167">lastModifiedUser</span></span>      | <span data-ttu-id="ced7e-168">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-168">string</span></span>           | <span data-ttu-id="ced7e-169">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-169">No</span></span>              | <span data-ttu-id="ced7e-170">Uživatel, který naposledy aktualizoval košík</span><span class="sxs-lookup"><span data-stu-id="ced7e-170">The user who last updated the cart.</span></span> <span data-ttu-id="ced7e-171">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-171">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="ced7e-172">položky řádku</span><span class="sxs-lookup"><span data-stu-id="ced7e-172">lineItems</span></span>             | <span data-ttu-id="ced7e-173">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="ced7e-173">Array of objects</span></span> | <span data-ttu-id="ced7e-174">Yes</span><span class="sxs-lookup"><span data-stu-id="ced7e-174">Yes</span></span>             | <span data-ttu-id="ced7e-175">Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)</span><span class="sxs-lookup"><span data-stu-id="ced7e-175">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="ced7e-176">Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-176">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="ced7e-177">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ced7e-177">Property</span></span>             | <span data-ttu-id="ced7e-178">Typ</span><span class="sxs-lookup"><span data-stu-id="ced7e-178">Type</span></span>                        | <span data-ttu-id="ced7e-179">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ced7e-179">Required</span></span>     | <span data-ttu-id="ced7e-180">Popis</span><span class="sxs-lookup"><span data-stu-id="ced7e-180">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ced7e-181">id</span><span class="sxs-lookup"><span data-stu-id="ced7e-181">id</span></span>                   | <span data-ttu-id="ced7e-182">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-182">string</span></span>                      | <span data-ttu-id="ced7e-183">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-183">No</span></span>           | <span data-ttu-id="ced7e-184">Jedinečný identifikátor řádkové položky košíku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-184">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="ced7e-185">Použije se při úspěšném vytvoření košíku.</span><span class="sxs-lookup"><span data-stu-id="ced7e-185">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="ced7e-186">id katalogu</span><span class="sxs-lookup"><span data-stu-id="ced7e-186">catalogId</span></span>            | <span data-ttu-id="ced7e-187">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-187">string</span></span>                      | <span data-ttu-id="ced7e-188">Yes</span><span class="sxs-lookup"><span data-stu-id="ced7e-188">Yes</span></span>          | <span data-ttu-id="ced7e-189">Identifikátor položky katalogu.</span><span class="sxs-lookup"><span data-stu-id="ced7e-189">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="ced7e-190">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="ced7e-190">friendlyName</span></span>         | <span data-ttu-id="ced7e-191">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-191">string</span></span>                      | <span data-ttu-id="ced7e-192">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-192">No</span></span>           | <span data-ttu-id="ced7e-193">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="ced7e-193">Optional.</span></span> <span data-ttu-id="ced7e-194">Popisný název položky definované partnerem, který pomáhá jednoznačně rozpoznat.</span><span class="sxs-lookup"><span data-stu-id="ced7e-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="ced7e-195">quantity</span><span class="sxs-lookup"><span data-stu-id="ced7e-195">quantity</span></span>             | <span data-ttu-id="ced7e-196">int</span><span class="sxs-lookup"><span data-stu-id="ced7e-196">int</span></span>                         | <span data-ttu-id="ced7e-197">Yes</span><span class="sxs-lookup"><span data-stu-id="ced7e-197">Yes</span></span>          | <span data-ttu-id="ced7e-198">Počet licencí nebo instancí</span><span class="sxs-lookup"><span data-stu-id="ced7e-198">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="ced7e-199">currencyCode</span><span class="sxs-lookup"><span data-stu-id="ced7e-199">currencyCode</span></span>         | <span data-ttu-id="ced7e-200">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-200">string</span></span>                      | <span data-ttu-id="ced7e-201">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-201">No</span></span>           | <span data-ttu-id="ced7e-202">Kód měny</span><span class="sxs-lookup"><span data-stu-id="ced7e-202">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="ced7e-203">billingCycle</span><span class="sxs-lookup"><span data-stu-id="ced7e-203">billingCycle</span></span>         | <span data-ttu-id="ced7e-204">Objekt</span><span class="sxs-lookup"><span data-stu-id="ced7e-204">Object</span></span>                      | <span data-ttu-id="ced7e-205">Yes</span><span class="sxs-lookup"><span data-stu-id="ced7e-205">Yes</span></span>          | <span data-ttu-id="ced7e-206">Typ fakturačního cyklu nastavený pro aktuální období</span><span class="sxs-lookup"><span data-stu-id="ced7e-206">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="ced7e-207">Účastníci</span><span class="sxs-lookup"><span data-stu-id="ced7e-207">participants</span></span>         | <span data-ttu-id="ced7e-208">Seznam párů řetězců objektů</span><span class="sxs-lookup"><span data-stu-id="ced7e-208">List of Object String pairs</span></span> | <span data-ttu-id="ced7e-209">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-209">No</span></span>           | <span data-ttu-id="ced7e-210">Kolekce účastníků nákupu.</span><span class="sxs-lookup"><span data-stu-id="ced7e-210">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="ced7e-211">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="ced7e-211">provisioningContext</span></span>  | <span data-ttu-id="ced7e-212">Slovníkový<řetězec, řetězec></span><span class="sxs-lookup"><span data-stu-id="ced7e-212">Dictionary<string, string></span></span>  | <span data-ttu-id="ced7e-213">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-213">No</span></span>           | <span data-ttu-id="ced7e-214">Kontext používaný ke zřízení nabídky.</span><span class="sxs-lookup"><span data-stu-id="ced7e-214">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="ced7e-215">orderGroup</span><span class="sxs-lookup"><span data-stu-id="ced7e-215">orderGroup</span></span>           | <span data-ttu-id="ced7e-216">řetězec</span><span class="sxs-lookup"><span data-stu-id="ced7e-216">string</span></span>                      | <span data-ttu-id="ced7e-217">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-217">No</span></span>           | <span data-ttu-id="ced7e-218">Skupina, která označuje, které položky lze umístit dohromady.</span><span class="sxs-lookup"><span data-stu-id="ced7e-218">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="ced7e-219">error</span><span class="sxs-lookup"><span data-stu-id="ced7e-219">error</span></span>                | <span data-ttu-id="ced7e-220">Objekt</span><span class="sxs-lookup"><span data-stu-id="ced7e-220">Object</span></span>                      | <span data-ttu-id="ced7e-221">No</span><span class="sxs-lookup"><span data-stu-id="ced7e-221">No</span></span>           | <span data-ttu-id="ced7e-222">Použije se po vytvoření košíku v případě chyby.</span><span class="sxs-lookup"><span data-stu-id="ced7e-222">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="ced7e-223">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ced7e-223">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ced7e-224">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ced7e-224">REST response</span></span>

<span data-ttu-id="ced7e-225">V případě úspěchu vrátí tato metoda v textu odpovědi naplněný prostředek [Cart.](cart-resources.md)</span><span class="sxs-lookup"><span data-stu-id="ced7e-225">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ced7e-226">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="ced7e-226">Response success and error codes</span></span>

<span data-ttu-id="ced7e-227">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ced7e-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ced7e-228">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="ced7e-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ced7e-229">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ced7e-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ced7e-230">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ced7e-230">Response example</span></span>

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
