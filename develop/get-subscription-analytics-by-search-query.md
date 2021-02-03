---
title: Získat analýzy předplatných pomocí vyhledávacího dotazu
description: Jak získat informace o analýze předplatného filtrované vyhledávacím dotazem.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766769"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="7a913-103">Získání analytických informací o předplatných filtrovaných podle vyhledávacího dotazu</span><span class="sxs-lookup"><span data-stu-id="7a913-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="7a913-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="7a913-104">**Applies To**</span></span>

- <span data-ttu-id="7a913-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="7a913-105">Partner Center</span></span>
- <span data-ttu-id="7a913-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="7a913-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7a913-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="7a913-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7a913-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7a913-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7a913-109">Jak získat informace o analýze předplatných pro zákazníky filtrované pomocí vyhledávacího dotazu.</span><span class="sxs-lookup"><span data-stu-id="7a913-109">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a913-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7a913-110">Prerequisites</span></span>

- <span data-ttu-id="7a913-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7a913-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7a913-112">Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.</span><span class="sxs-lookup"><span data-stu-id="7a913-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7a913-113">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="7a913-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7a913-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="7a913-114">Request syntax</span></span>

| <span data-ttu-id="7a913-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="7a913-115">Method</span></span> | <span data-ttu-id="7a913-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="7a913-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="7a913-117">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="7a913-117">**GET**</span></span> | <span data-ttu-id="7a913-118">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? Filter = {filter_string}</span><span class="sxs-lookup"><span data-stu-id="7a913-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="7a913-119">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="7a913-119">URI parameters</span></span>

<span data-ttu-id="7a913-120">Pomocí následujícího parametru cesty Identifikujte vaši organizaci a filtrujte hledání.</span><span class="sxs-lookup"><span data-stu-id="7a913-120">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="7a913-121">Název</span><span class="sxs-lookup"><span data-stu-id="7a913-121">Name</span></span> | <span data-ttu-id="7a913-122">Typ</span><span class="sxs-lookup"><span data-stu-id="7a913-122">Type</span></span> | <span data-ttu-id="7a913-123">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="7a913-123">Required</span></span> | <span data-ttu-id="7a913-124">Popis</span><span class="sxs-lookup"><span data-stu-id="7a913-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="7a913-125">filter_string</span><span class="sxs-lookup"><span data-stu-id="7a913-125">filter_string</span></span> | <span data-ttu-id="7a913-126">řetězec</span><span class="sxs-lookup"><span data-stu-id="7a913-126">string</span></span> | <span data-ttu-id="7a913-127">Yes</span><span class="sxs-lookup"><span data-stu-id="7a913-127">Yes</span></span> | <span data-ttu-id="7a913-128">Filtr, který se má použít pro analýzu předplatného</span><span class="sxs-lookup"><span data-stu-id="7a913-128">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="7a913-129">Viz část filtru a pole filtru pro syntaxi, pole a operátory pro použití v tomto parametru.</span><span class="sxs-lookup"><span data-stu-id="7a913-129">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="7a913-130">Syntaxe filtru</span><span class="sxs-lookup"><span data-stu-id="7a913-130">Filter syntax</span></span>

<span data-ttu-id="7a913-131">Parametr Filter musí být složen jako řada kombinací polí, hodnot a operátorů.</span><span class="sxs-lookup"><span data-stu-id="7a913-131">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="7a913-132">Více kombinací lze kombinovat pomocí **`and`** **`or`** operátorů or.</span><span class="sxs-lookup"><span data-stu-id="7a913-132">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="7a913-133">Nekódovaný příklad vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="7a913-133">An unencoded example looks like this:</span></span>

- <span data-ttu-id="7a913-134">Řetezce `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="7a913-134">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="7a913-135">Datového `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="7a913-135">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="7a913-136">Zobrazí `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="7a913-136">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="7a913-137">Filtrovat pole</span><span class="sxs-lookup"><span data-stu-id="7a913-137">Filter fields</span></span>

<span data-ttu-id="7a913-138">Parametr filtru požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="7a913-138">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="7a913-139">Každý příkaz obsahuje pole a hodnotu, která je spojena s **`eq`** **`ne`** operátory OR.</span><span class="sxs-lookup"><span data-stu-id="7a913-139">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="7a913-140">Některá pole také podporují **`contains`** operátory, **`gt`** ,, a **`lt`** **`ge`** **`le`** .</span><span class="sxs-lookup"><span data-stu-id="7a913-140">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="7a913-141">Příkazy lze kombinovat pomocí **`and`** **`or`** operátorů or.</span><span class="sxs-lookup"><span data-stu-id="7a913-141">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="7a913-142">Následují příklady řetězců filtru:</span><span class="sxs-lookup"><span data-stu-id="7a913-142">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="7a913-143">V následující tabulce je uveden seznam podporovaných polí a operátorů podpory pro parametr Filter.</span><span class="sxs-lookup"><span data-stu-id="7a913-143">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="7a913-144">Řetězcové hodnoty musí být obklopeny jednoduchými uvozovkami.</span><span class="sxs-lookup"><span data-stu-id="7a913-144">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="7a913-145">Parametr</span><span class="sxs-lookup"><span data-stu-id="7a913-145">Parameter</span></span> | <span data-ttu-id="7a913-146">Podporované operátory</span><span class="sxs-lookup"><span data-stu-id="7a913-146">Supported operators</span></span> | <span data-ttu-id="7a913-147">Description</span><span class="sxs-lookup"><span data-stu-id="7a913-147">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="7a913-148">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="7a913-148">autoRenewEnabled</span></span> | <span data-ttu-id="7a913-149">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7a913-149">`eq`, `ne`</span></span> | <span data-ttu-id="7a913-150">Hodnota, která označuje, jestli se předplatné obnovuje automaticky.</span><span class="sxs-lookup"><span data-stu-id="7a913-150">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="7a913-151">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="7a913-151">commitmentEndDate</span></span> | <span data-ttu-id="7a913-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="7a913-153">Datum ukončení předplatného</span><span class="sxs-lookup"><span data-stu-id="7a913-153">The date the subscription ends.</span></span> |
| <span data-ttu-id="7a913-154">creationDate</span><span class="sxs-lookup"><span data-stu-id="7a913-154">creationDate</span></span> | <span data-ttu-id="7a913-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="7a913-156">Datum vytvoření odběru.</span><span class="sxs-lookup"><span data-stu-id="7a913-156">The date the subscription was created.</span></span> |
| <span data-ttu-id="7a913-157">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="7a913-157">currentStateEndDate</span></span> | <span data-ttu-id="7a913-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7a913-159">Datum, kdy se změní aktuální stav předplatného.</span><span class="sxs-lookup"><span data-stu-id="7a913-159">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="7a913-160">customerMarket</span><span class="sxs-lookup"><span data-stu-id="7a913-160">customerMarket</span></span> | <span data-ttu-id="7a913-161">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7a913-161">`eq`, `ne`</span></span> | <span data-ttu-id="7a913-162">Země nebo oblast, ve které má zákazník obchodní oddělení</span><span class="sxs-lookup"><span data-stu-id="7a913-162">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="7a913-163">customerName</span><span class="sxs-lookup"><span data-stu-id="7a913-163">customerName</span></span> | `contains` | <span data-ttu-id="7a913-164">Jméno zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7a913-164">The name of the customer.</span></span> |
| <span data-ttu-id="7a913-165">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="7a913-165">customerTenantId</span></span> | <span data-ttu-id="7a913-166">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7a913-166">`eq`, `ne`</span></span> | <span data-ttu-id="7a913-167">Řetězec ve formátu GUID, který identifikuje tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7a913-167">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="7a913-168">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="7a913-168">deprovisionedDate</span></span> | <span data-ttu-id="7a913-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7a913-170">Datum zrušení zřízení předplatného.</span><span class="sxs-lookup"><span data-stu-id="7a913-170">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="7a913-171">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="7a913-171">The default value is null.</span></span> |
| <span data-ttu-id="7a913-172">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="7a913-172">effectiveStartDate</span></span> | <span data-ttu-id="7a913-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7a913-174">Datum, kdy se předplatné spustí.</span><span class="sxs-lookup"><span data-stu-id="7a913-174">The date the subscription starts.</span></span> |
| <span data-ttu-id="7a913-175">friendlyName</span><span class="sxs-lookup"><span data-stu-id="7a913-175">friendlyName</span></span> | `contains` | <span data-ttu-id="7a913-176">Název předplatného.</span><span class="sxs-lookup"><span data-stu-id="7a913-176">The name of the subscription.</span></span> |
| <span data-ttu-id="7a913-177">id</span><span class="sxs-lookup"><span data-stu-id="7a913-177">id</span></span> | <span data-ttu-id="7a913-178">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7a913-178">`eq`, `ne`</span></span> | <span data-ttu-id="7a913-179">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="7a913-179">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="7a913-180">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="7a913-180">lastRenewalDate</span></span> | <span data-ttu-id="7a913-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7a913-182">Datum poslední obnovy odběru</span><span class="sxs-lookup"><span data-stu-id="7a913-182">The date that the subscription was last renewed.</span></span> <span data-ttu-id="7a913-183">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="7a913-183">The default value is null.</span></span> |
| <span data-ttu-id="7a913-184">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="7a913-184">lastUsageDate</span></span> | <span data-ttu-id="7a913-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7a913-186">Datum posledního použití předplatného</span><span class="sxs-lookup"><span data-stu-id="7a913-186">The date that the subscription was last used.</span></span> <span data-ttu-id="7a913-187">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="7a913-187">The default value is null.</span></span> |
| <span data-ttu-id="7a913-188">partnerId</span><span class="sxs-lookup"><span data-stu-id="7a913-188">partnerId</span></span> | <span data-ttu-id="7a913-189">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7a913-189">`eq`, `ne`</span></span> | <span data-ttu-id="7a913-190">ID MPN</span><span class="sxs-lookup"><span data-stu-id="7a913-190">The MPN ID.</span></span> <span data-ttu-id="7a913-191">U přímého prodejce bude tato hodnota ID MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="7a913-191">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="7a913-192">Pro nepřímý prodejce bude tato hodnota ID MPN nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="7a913-192">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="7a913-193">partnerName</span><span class="sxs-lookup"><span data-stu-id="7a913-193">partnerName</span></span> | <span data-ttu-id="7a913-194">řetězec</span><span class="sxs-lookup"><span data-stu-id="7a913-194">string</span></span> | <span data-ttu-id="7a913-195">Název partnera, pro kterého se předplatné zakoupilo</span><span class="sxs-lookup"><span data-stu-id="7a913-195">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="7a913-196">NázevVýrobku</span><span class="sxs-lookup"><span data-stu-id="7a913-196">productName</span></span> | <span data-ttu-id="7a913-197">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7a913-197">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="7a913-198">Název produktu.</span><span class="sxs-lookup"><span data-stu-id="7a913-198">The name of the product.</span></span> |
| <span data-ttu-id="7a913-199">providerName</span><span class="sxs-lookup"><span data-stu-id="7a913-199">providerName</span></span> | <span data-ttu-id="7a913-200">řetězec</span><span class="sxs-lookup"><span data-stu-id="7a913-200">string</span></span> | <span data-ttu-id="7a913-201">Pokud je transakce předplatného určena pro nepřímý prodejce, jméno poskytovatele je nepřímým poskytovatelem, který si zakoupil předplatné.</span><span class="sxs-lookup"><span data-stu-id="7a913-201">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="7a913-202">status</span><span class="sxs-lookup"><span data-stu-id="7a913-202">status</span></span> | <span data-ttu-id="7a913-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7a913-203">`eq`, `ne`</span></span> | <span data-ttu-id="7a913-204">Stav předplatného.</span><span class="sxs-lookup"><span data-stu-id="7a913-204">The subscription status.</span></span> <span data-ttu-id="7a913-205">Podporovány jsou následující hodnoty: "aktivní", "pozastaveno" nebo "zrušení zřízení".</span><span class="sxs-lookup"><span data-stu-id="7a913-205">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="7a913-206">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="7a913-206">subscriptionType</span></span> | <span data-ttu-id="7a913-207">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="7a913-207">`eq`, `ne`</span></span> | <span data-ttu-id="7a913-208">Typ předplatného.</span><span class="sxs-lookup"><span data-stu-id="7a913-208">The subscription type.</span></span> <span data-ttu-id="7a913-209">**Poznámka**: Toto pole rozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="7a913-209">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="7a913-210">Podporované hodnoty jsou: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="7a913-210">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="7a913-211">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="7a913-211">trialStartDate</span></span> | <span data-ttu-id="7a913-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="7a913-213">Datum, kdy se začalo zkušební období předplatného.</span><span class="sxs-lookup"><span data-stu-id="7a913-213">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="7a913-214">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="7a913-214">The default value is null.</span></span> |
| <span data-ttu-id="7a913-215">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="7a913-215">trialToPaidConversionDate</span></span> | <span data-ttu-id="7a913-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="7a913-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="7a913-217">Datum, kdy se předplatné převede ze zkušební verze na placené.</span><span class="sxs-lookup"><span data-stu-id="7a913-217">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="7a913-218">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="7a913-218">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7a913-219">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="7a913-219">Request headers</span></span>

<span data-ttu-id="7a913-220">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7a913-220">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7a913-221">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="7a913-221">Request body</span></span>

<span data-ttu-id="7a913-222">Žádné</span><span class="sxs-lookup"><span data-stu-id="7a913-222">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7a913-223">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="7a913-223">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="7a913-224">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="7a913-224">REST response</span></span>

<span data-ttu-id="7a913-225">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [předplatného](partner-center-analytics-resources.md#subscription-resource) , které splňují kritéria filtru.</span><span class="sxs-lookup"><span data-stu-id="7a913-225">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7a913-226">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="7a913-226">Response success and error codes</span></span>

<span data-ttu-id="7a913-227">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="7a913-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7a913-228">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="7a913-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7a913-229">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7a913-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7a913-230">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="7a913-230">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123

{
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a><span data-ttu-id="7a913-231">Viz také</span><span class="sxs-lookup"><span data-stu-id="7a913-231">See also</span></span>

- [<span data-ttu-id="7a913-232">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="7a913-232">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
