---
title: Pokyny k omezování rozhraní API
description: Pro partnery, kteří volají rozhraní API partnerského centra, se dozvíte, která rozhraní API mají vliv na omezování a osvědčené postupy rozhraní Microsoft API, abyste zabránili omezení nebo lepšímu omezování procesů.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: ab1138e19e06111299ab43ea13a6f033274aaa5d
ms.sourcegitcommit: 3c3a21e73aaadf3023cf4c13b09809ceae5f027a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/14/2021
ms.locfileid: "107496140"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="de432-103">Pokyny k omezování rozhraní API pro partnery, kteří volají rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="de432-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="de432-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="de432-104">**Applies to**</span></span>

- <span data-ttu-id="de432-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="de432-105">Partner Center</span></span>

<span data-ttu-id="de432-106">Microsoft implementuje omezování rozhraní API, které umožňuje zajistit jednotnější výkon v časovém intervalu pro partnery, kteří volají rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="de432-106">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="de432-107">Omezování omezuje počet požadavků na službu v časovém intervalu, aby nedocházelo k nadměrnému využití prostředků.</span><span class="sxs-lookup"><span data-stu-id="de432-107">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="de432-108">I když je partnerské Centrum navrženo tak, aby zpracovával velký počet požadavků, pokud se k zahlcení počtu požadavků vychází z několika partnerů, omezování pomáhá udržet optimální výkon a spolehlivost pro všechny partnery.</span><span class="sxs-lookup"><span data-stu-id="de432-108">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="de432-109">Omezení omezování se liší v závislosti na scénáři.</span><span class="sxs-lookup"><span data-stu-id="de432-109">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="de432-110">Pokud například provádíte velký objem zápisů, je možnost omezování větší než v případě, že provádíte pouze čtení.</span><span class="sxs-lookup"><span data-stu-id="de432-110">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="de432-111">Co se stane, když dojde k omezování?</span><span class="sxs-lookup"><span data-stu-id="de432-111">What happens when throttling occurs?</span></span> 

<span data-ttu-id="de432-112">Po překročení prahové hodnoty omezuje Partnerská centra všechny další požadavky od tohoto klienta po určitou dobu.</span><span class="sxs-lookup"><span data-stu-id="de432-112">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="de432-113">Chování omezování závisí na typu a počtu požadavků.</span><span class="sxs-lookup"><span data-stu-id="de432-113">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="de432-114">Běžné scénáře omezování</span><span class="sxs-lookup"><span data-stu-id="de432-114">Common throttling scenarios</span></span> 

<span data-ttu-id="de432-115">Mezi nejběžnější příčiny omezení klientů patří:</span><span class="sxs-lookup"><span data-stu-id="de432-115">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="de432-116">**Velký počet žádostí o rozhraní API na ID tenanta partnera**: u některých rozhraní API partnerského centra se omezování určuje podle ID partnerského tenanta. příliš mnoho volání těchto rozhraní API na stejném ID partnerského tenanta bude mít za následek překročení prahové hodnoty omezování.</span><span class="sxs-lookup"><span data-stu-id="de432-116">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="de432-117">**Velký počet požadavků pro rozhraní API na ID tenanta partnera na ID tenanta zákazníka**: u jiných rozhraní API se omezování určuje podle ID partnerského tenanta/kombinace ID tenanta zákazníka; v těchto případech dojde k tomu, že provedení příliš velkého počtu volání proti stejnému ID tenanta zákazníka bude mít za následek omezení, zatímco volání jiných zákazníků budou úspěšná.</span><span class="sxs-lookup"><span data-stu-id="de432-117">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="de432-118">Osvědčené postupy pro zamezení omezování</span><span class="sxs-lookup"><span data-stu-id="de432-118">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="de432-119">Postupy programování, jako je průběžné cyklické dotazování prostředku pro kontrolu aktualizací a pravidelné prohledávání kolekcí prostředků pro kontrolu nových nebo odstraněných prostředků, mají větší vliv na omezování a sníží celkový výkon.</span><span class="sxs-lookup"><span data-stu-id="de432-119">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="de432-120">Souběžná volání rozhraní API mohou vést k vysokému počtu požadavků za jednotku času, což způsobí také omezení požadavků.</span><span class="sxs-lookup"><span data-stu-id="de432-120">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="de432-121">Místo toho byste měli využít sledování změn a oznámení změn.</span><span class="sxs-lookup"><span data-stu-id="de432-121">You should instead leverage change tracking and change notifications.</span></span> <span data-ttu-id="de432-122">Kromě toho byste měli být schopni využít protokoly aktivit k detekci změn. Další informace najdete v [protokolech aktivit partnerského centra](get-a-record-of-partner-center-activity-by-user.md) .</span><span class="sxs-lookup"><span data-stu-id="de432-122">Additionally, you should be able to leverage activity logs for detecting changes, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md) for more information.</span></span>  <span data-ttu-id="de432-123">Důrazně doporučujeme, aby partneři zvážili použití rozhraní API protokolu aktivit pro zajištění vyšší efektivity a zabránili omezování.</span><span class="sxs-lookup"><span data-stu-id="de432-123">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="de432-124">Viz také příklad použití protokolů aktivit níže.</span><span class="sxs-lookup"><span data-stu-id="de432-124">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="de432-125">Osvědčené postupy pro zpracování omezování</span><span class="sxs-lookup"><span data-stu-id="de432-125">Best practices to handle throttling</span></span>

<span data-ttu-id="de432-126">Níže jsou uvedené osvědčené postupy pro omezení zpracování:</span><span class="sxs-lookup"><span data-stu-id="de432-126">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="de432-127">Snižte stupeň paralelismu.</span><span class="sxs-lookup"><span data-stu-id="de432-127">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="de432-128">Snižte frekvenci volání.</span><span class="sxs-lookup"><span data-stu-id="de432-128">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="de432-129">Vyhněte se okamžitým opakovaným pokusům, protože všechny požadavky se budou nacházet oproti omezením využití.</span><span class="sxs-lookup"><span data-stu-id="de432-129">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="de432-130">Při implementaci zpracování chyb k detekci omezování využijte kód chyby HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="de432-130">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="de432-131">Neúspěšná odpověď zahrnuje hlavičku Retry-After odpovědi.</span><span class="sxs-lookup"><span data-stu-id="de432-131">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="de432-132">Zálohování požadavků pomocí opakovaného zpoždění je nejrychlejší způsob, jak obnovit omezení.</span><span class="sxs-lookup"><span data-stu-id="de432-132">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="de432-133">Pokud chcete použít prodlevu po opakování, udělejte toto:</span><span class="sxs-lookup"><span data-stu-id="de432-133">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="de432-134">Počkejte, než bude stanovený počet sekund v hlavičce Retry-After.</span><span class="sxs-lookup"><span data-stu-id="de432-134">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="de432-135">Opakujte požadavek.</span><span class="sxs-lookup"><span data-stu-id="de432-135">Retry the request.</span></span>  

3. <span data-ttu-id="de432-136">Pokud se žádost znovu nepovede s kódem chyby 429, pořád se vám omezí.</span><span class="sxs-lookup"><span data-stu-id="de432-136">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="de432-137">Zkuste to znovu s exponenciálním omezení rychlosti, použijte doporučené zpoždění Retry-After a zkuste požadavek zopakovat, dokud to neproběhne úspěšně.</span><span class="sxs-lookup"><span data-stu-id="de432-137">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="de432-138">Pokud používáte sadu SDK, obdržíte výjimku se stavovým kódem 429, když se vaše žádost omezuje.</span><span class="sxs-lookup"><span data-stu-id="de432-138">If you are using SDK you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="de432-139">Ve výjimce použijte vlastnost RetryAfter a opakujte požadavek po uplynutí této doby.</span><span class="sxs-lookup"><span data-stu-id="de432-139">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="de432-140">Rozhraní API, která v současnosti ovlivňují omezování</span><span class="sxs-lookup"><span data-stu-id="de432-140">APIs currently impacted by throttling</span></span>

<span data-ttu-id="de432-141">V dlouhodobém běhu budou všechna samostatná rozhraní API partnerského centra, která volají koncový bod "api.partnercenter.microsoft.com/", omezená.</span><span class="sxs-lookup"><span data-stu-id="de432-141">In the long run, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="de432-142">V současné době se omezení omezování uplatní jenom na rozhraních API uvedených níže.</span><span class="sxs-lookup"><span data-stu-id="de432-142">Currently, the throttling limits are only enforced on the APIs listed below.</span></span> <span data-ttu-id="de432-143">Partnerské centrum bude shromažďovat telemetrii na každé z rozhraní API a bude dynamicky upravovat limity omezování.</span><span class="sxs-lookup"><span data-stu-id="de432-143">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="de432-144">V následující tabulce jsou uvedena rozhraní API, kde je omezování aktuálně vynutilo.</span><span class="sxs-lookup"><span data-stu-id="de432-144">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="de432-145">**Operace**</span><span class="sxs-lookup"><span data-stu-id="de432-145">**Operation**</span></span>| <span data-ttu-id="de432-146">**Dokumentace k Partnerskému centru**</span><span class="sxs-lookup"><span data-stu-id="de432-146">**Partner Center documentation**</span></span>|
|------------------------|----------------------------|
|<span data-ttu-id="de432-147">{baseURL}/v1/Customers/{customer_id}/Orders</span><span class="sxs-lookup"><span data-stu-id="de432-147">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="de432-148">vytvoření objednávky</span><span class="sxs-lookup"><span data-stu-id="de432-148">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="de432-149">{baseURL}/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription}/upgrades</span><span class="sxs-lookup"><span data-stu-id="de432-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="de432-150">převod předplatného</span><span class="sxs-lookup"><span data-stu-id="de432-150">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="de432-151">{baseURL}/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID}</span><span class="sxs-lookup"><span data-stu-id="de432-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="de432-152">zakoupení doplňku k předplatnému</span><span class="sxs-lookup"><span data-stu-id="de432-152">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="de432-153">{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}</span><span class="sxs-lookup"><span data-stu-id="de432-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="de432-154">Vytvoření košíku</span><span class="sxs-lookup"><span data-stu-id="de432-154">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="de432-155">{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}/Checkout</span><span class="sxs-lookup"><span data-stu-id="de432-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="de432-156">rezervace košíku</span><span class="sxs-lookup"><span data-stu-id="de432-156">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="de432-157">{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}</span><span class="sxs-lookup"><span data-stu-id="de432-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="de432-158">aktualizace košíku</span><span class="sxs-lookup"><span data-stu-id="de432-158">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="de432-159">{baseURL}/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrations</span><span class="sxs-lookup"><span data-stu-id="de432-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="de432-160">registrace předplatného</span><span class="sxs-lookup"><span data-stu-id="de432-160">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="de432-161">{baseURL}/v1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="de432-161">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="de432-162">vytvořit entitu upgradu produktu</span><span class="sxs-lookup"><span data-stu-id="de432-162">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="de432-163">{baseURL}/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions</span><span class="sxs-lookup"><span data-stu-id="de432-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="de432-164">převod zkušebního předplatného na placené</span><span class="sxs-lookup"><span data-stu-id="de432-164">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="de432-165">{baseURL}/v1/Customers/{Customer-tenant-ID}</span><span class="sxs-lookup"><span data-stu-id="de432-165">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="de432-166">získat zákazníka podle ID</span><span class="sxs-lookup"><span data-stu-id="de432-166">get a customer by id</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="de432-167">{baseURL}/v1/productUpgrades/eligibility</span><span class="sxs-lookup"><span data-stu-id="de432-167">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="de432-168">získat nárok na upgrade produktu</span><span class="sxs-lookup"><span data-stu-id="de432-168">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="de432-169">{baseURL}/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription}</span><span class="sxs-lookup"><span data-stu-id="de432-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="de432-170">Spravovat předplatné</span><span class="sxs-lookup"><span data-stu-id="de432-170">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="de432-171">{baseURL}/v1/Customers/{customer_id}/Subscriptions</span><span class="sxs-lookup"><span data-stu-id="de432-171">{baseURL}/v1/customers/{customer_id}/subscriptions</span></span> |[<span data-ttu-id="de432-172">Get-All-of-Customer</span><span class="sxs-lookup"><span data-stu-id="de432-172">get-all-of-a-customer-s-subscriptions</span></span>](get-all-of-a-customer-s-subscriptions.md)|
|<span data-ttu-id="de432-173">{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="de432-173">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="de432-174">Získání předplatného podle ID</span><span class="sxs-lookup"><span data-stu-id="de432-174">Get a subscription by ID</span></span>](get-a-subscription-by-id.md)|
|<span data-ttu-id="de432-175">{baseURL}/v1/Customers/{customer_id}/Orders</span><span class="sxs-lookup"><span data-stu-id="de432-175">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="de432-176">Získat všechny zákaznické objednávky</span><span class="sxs-lookup"><span data-stu-id="de432-176">Get all customer orders</span></span>](get-all-of-a-customer-s-orders.md)|
|<span data-ttu-id="de432-177">{baseURL}/v1/Customers/{customer_id}/Orders/{order_id}</span><span class="sxs-lookup"><span data-stu-id="de432-177">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span></span>|[<span data-ttu-id="de432-178">Získání objednávky podle ID</span><span class="sxs-lookup"><span data-stu-id="de432-178">Get an order by ID</span></span>](get-an-order-by-id.md)|
|<span data-ttu-id="de432-179">{baseURL}/v1/Customers/{customer_id}/Orders/{order_id}/provisioningstatus</span><span class="sxs-lookup"><span data-stu-id="de432-179">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span></span>|[<span data-ttu-id="de432-180">Získání stavu zřizování předplatných</span><span class="sxs-lookup"><span data-stu-id="de432-180">Get subscription provisioning status</span></span>](get-subscription-provisioning-status.md)|
|<span data-ttu-id="de432-181">{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="de432-181">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="de432-182">Správa objednávek a Správa předplatného</span><span class="sxs-lookup"><span data-stu-id="de432-182">Manage orders and manage a subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="de432-183">{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}/addons</span><span class="sxs-lookup"><span data-stu-id="de432-183">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span></span>|[<span data-ttu-id="de432-184">Získání seznamu doplňků pro předplatné</span><span class="sxs-lookup"><span data-stu-id="de432-184">Get a list of add-ons for a subscription</span></span>](get-a-list-of-add-ons-for-a-subscription.md)|
|<span data-ttu-id="de432-185">{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}/azureEntitlements</span><span class="sxs-lookup"><span data-stu-id="de432-185">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span></span>|[<span data-ttu-id="de432-186">Získat seznam nároků na Azure pro předplatné</span><span class="sxs-lookup"><span data-stu-id="de432-186">Get a list of Azure entitlements for a subscription</span></span>](get-a-list-of-azure-entitlements-for-subscription.md)|
|<span data-ttu-id="de432-187">{baseURL}/v1/Customers/{customer_id}/Subscriptions/{subscription_id}/registrationstatus</span><span class="sxs-lookup"><span data-stu-id="de432-187">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span></span>|[<span data-ttu-id="de432-188">Získání stavu registrace předplatných</span><span class="sxs-lookup"><span data-stu-id="de432-188">Get subscription registration status</span></span>](get-subscription-registration-status.md)|
|<span data-ttu-id="de432-189">{baseURL}/v1/Customers/{Customer-tenant-ID}/Transfers</span><span class="sxs-lookup"><span data-stu-id="de432-189">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span></span>|[<span data-ttu-id="de432-190">Získat všechny přenosy zákazníka</span><span class="sxs-lookup"><span data-stu-id="de432-190">Get all of a customer's transfers</span></span>](get-all-of-a-customer-s-transfers.md)|
|<span data-ttu-id="de432-191">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span><span class="sxs-lookup"><span data-stu-id="de432-191">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span></span>|[<span data-ttu-id="de432-192">Získání stavu upgradu produktů</span><span class="sxs-lookup"><span data-stu-id="de432-192">Get product upgrade status</span></span>](get-product-upgrade-status.md)|
|<span data-ttu-id="de432-193">{baseURL}/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions</span><span class="sxs-lookup"><span data-stu-id="de432-193">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span>|[<span data-ttu-id="de432-194">Získání seznamu nabídek převod zkušebních verzí</span><span class="sxs-lookup"><span data-stu-id="de432-194">Get a list of trial conversion offers</span></span>](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a><span data-ttu-id="de432-195">Odpověď kódu chyby:</span><span class="sxs-lookup"><span data-stu-id="de432-195">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="de432-196">Příklad protokolu aktivit</span><span class="sxs-lookup"><span data-stu-id="de432-196">Example of activity log</span></span>

<span data-ttu-id="de432-197">Osvědčeným postupem při analýze každodenních změn doporučujeme zadat dotaz na záznam auditu pro určitý den.</span><span class="sxs-lookup"><span data-stu-id="de432-197">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="de432-198">V odpovědi se zobrazí výsledek se změnami konkrétního typu operace.</span><span class="sxs-lookup"><span data-stu-id="de432-198">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="de432-199">Můžete filtrovat podle toho, o jakou operaci máte starosti.</span><span class="sxs-lookup"><span data-stu-id="de432-199">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="de432-200">Pokud vás například zajímá nově vytvořeného zákazníka, můžete se podívat na typem operace OperationType = "add_customer".</span><span class="sxs-lookup"><span data-stu-id="de432-200"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="de432-201">Seznam typem operace OperationType/prostředků najdete níže v dokumentaci k rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="de432-201">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="de432-202">Auditování prostředků</span><span class="sxs-lookup"><span data-stu-id="de432-202">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="de432-203">Získání záznamu aktivity partnerského centra podle uživatele</span><span class="sxs-lookup"><span data-stu-id="de432-203">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="de432-204">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="de432-204">Response example</span></span>

<span data-ttu-id="de432-205">**Požadavek**:</span><span class="sxs-lookup"><span data-stu-id="de432-205">**Request**:</span></span>  
```http
Http Get call:  https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Authorization: Bearer <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-US 

Host: api.partnercenter.microsoft.com 

Connection: Keep-Alive 
```

<span data-ttu-id="de432-206">**Odpověď**:</span><span class="sxs-lookup"><span data-stu-id="de432-206">**Response**:</span></span>    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

