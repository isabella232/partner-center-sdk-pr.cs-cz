---
title: Získat analýzy předplatných pomocí vyhledávacího dotazu
description: Jak získat informace o analýze předplatného filtrované vyhledávacím dotazem.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8df777b9a88206f8b22579f0f445c54d80f7cd64
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548732"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="79f11-103">Získání analytických informací o předplatných filtrovaných podle vyhledávacího dotazu</span><span class="sxs-lookup"><span data-stu-id="79f11-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="79f11-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="79f11-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="79f11-105">Jak získat informace o analýze předplatných pro zákazníky filtrované pomocí vyhledávacího dotazu.</span><span class="sxs-lookup"><span data-stu-id="79f11-105">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79f11-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="79f11-106">Prerequisites</span></span>

- <span data-ttu-id="79f11-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="79f11-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="79f11-108">Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.</span><span class="sxs-lookup"><span data-stu-id="79f11-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="79f11-109">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="79f11-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="79f11-110">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="79f11-110">Request syntax</span></span>

| <span data-ttu-id="79f11-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="79f11-111">Method</span></span> | <span data-ttu-id="79f11-112">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="79f11-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="79f11-113">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="79f11-113">**GET**</span></span> | <span data-ttu-id="79f11-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? Filter = {filter_string}</span><span class="sxs-lookup"><span data-stu-id="79f11-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="79f11-115">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="79f11-115">URI parameters</span></span>

<span data-ttu-id="79f11-116">Pomocí následujícího parametru cesty Identifikujte vaši organizaci a filtrujte hledání.</span><span class="sxs-lookup"><span data-stu-id="79f11-116">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="79f11-117">Název</span><span class="sxs-lookup"><span data-stu-id="79f11-117">Name</span></span> | <span data-ttu-id="79f11-118">Typ</span><span class="sxs-lookup"><span data-stu-id="79f11-118">Type</span></span> | <span data-ttu-id="79f11-119">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="79f11-119">Required</span></span> | <span data-ttu-id="79f11-120">Popis</span><span class="sxs-lookup"><span data-stu-id="79f11-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="79f11-121">filter_string</span><span class="sxs-lookup"><span data-stu-id="79f11-121">filter_string</span></span> | <span data-ttu-id="79f11-122">řetězec</span><span class="sxs-lookup"><span data-stu-id="79f11-122">string</span></span> | <span data-ttu-id="79f11-123">Yes</span><span class="sxs-lookup"><span data-stu-id="79f11-123">Yes</span></span> | <span data-ttu-id="79f11-124">Filtr, který se má použít pro analýzu předplatného</span><span class="sxs-lookup"><span data-stu-id="79f11-124">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="79f11-125">Viz část filtru a pole filtru pro syntaxi, pole a operátory pro použití v tomto parametru.</span><span class="sxs-lookup"><span data-stu-id="79f11-125">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="79f11-126">Syntaxe filtru</span><span class="sxs-lookup"><span data-stu-id="79f11-126">Filter syntax</span></span>

<span data-ttu-id="79f11-127">Parametr Filter musí být složen jako řada kombinací polí, hodnot a operátorů.</span><span class="sxs-lookup"><span data-stu-id="79f11-127">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="79f11-128">Více kombinací lze kombinovat pomocí **`and`** **`or`** operátorů or.</span><span class="sxs-lookup"><span data-stu-id="79f11-128">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="79f11-129">Nekódovaný příklad vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="79f11-129">An unencoded example looks like this:</span></span>

- <span data-ttu-id="79f11-130">Řetezce `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="79f11-130">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="79f11-131">Datového `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="79f11-131">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="79f11-132">Zobrazí `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="79f11-132">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="79f11-133">Filtrovat pole</span><span class="sxs-lookup"><span data-stu-id="79f11-133">Filter fields</span></span>

<span data-ttu-id="79f11-134">Parametr filtru požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="79f11-134">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="79f11-135">Každý příkaz obsahuje pole a hodnotu, která je spojena s **`eq`** **`ne`** operátory OR.</span><span class="sxs-lookup"><span data-stu-id="79f11-135">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="79f11-136">Některá pole také podporují **`contains`** operátory, **`gt`** ,, a **`lt`** **`ge`** **`le`** .</span><span class="sxs-lookup"><span data-stu-id="79f11-136">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="79f11-137">Příkazy lze kombinovat pomocí **`and`** **`or`** operátorů or.</span><span class="sxs-lookup"><span data-stu-id="79f11-137">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="79f11-138">Následují příklady řetězců filtru:</span><span class="sxs-lookup"><span data-stu-id="79f11-138">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="79f11-139">V následující tabulce je uveden seznam podporovaných polí a operátorů podpory pro parametr Filter.</span><span class="sxs-lookup"><span data-stu-id="79f11-139">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="79f11-140">Řetězcové hodnoty musí být obklopeny jednoduchými uvozovkami.</span><span class="sxs-lookup"><span data-stu-id="79f11-140">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="79f11-141">Parametr</span><span class="sxs-lookup"><span data-stu-id="79f11-141">Parameter</span></span> | <span data-ttu-id="79f11-142">Podporované operátory</span><span class="sxs-lookup"><span data-stu-id="79f11-142">Supported operators</span></span> | <span data-ttu-id="79f11-143">Description</span><span class="sxs-lookup"><span data-stu-id="79f11-143">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="79f11-144">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="79f11-144">autoRenewEnabled</span></span> | <span data-ttu-id="79f11-145">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="79f11-145">`eq`, `ne`</span></span> | <span data-ttu-id="79f11-146">Hodnota, která označuje, jestli se předplatné obnovuje automaticky.</span><span class="sxs-lookup"><span data-stu-id="79f11-146">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="79f11-147">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="79f11-147">commitmentEndDate</span></span> | <span data-ttu-id="79f11-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="79f11-149">Datum ukončení předplatného</span><span class="sxs-lookup"><span data-stu-id="79f11-149">The date the subscription ends.</span></span> |
| <span data-ttu-id="79f11-150">creationDate</span><span class="sxs-lookup"><span data-stu-id="79f11-150">creationDate</span></span> | <span data-ttu-id="79f11-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="79f11-152">Datum vytvoření odběru.</span><span class="sxs-lookup"><span data-stu-id="79f11-152">The date the subscription was created.</span></span> |
| <span data-ttu-id="79f11-153">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="79f11-153">currentStateEndDate</span></span> | <span data-ttu-id="79f11-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="79f11-155">Datum, kdy se změní aktuální stav předplatného.</span><span class="sxs-lookup"><span data-stu-id="79f11-155">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="79f11-156">customerMarket</span><span class="sxs-lookup"><span data-stu-id="79f11-156">customerMarket</span></span> | <span data-ttu-id="79f11-157">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="79f11-157">`eq`, `ne`</span></span> | <span data-ttu-id="79f11-158">Země nebo oblast, ve které má zákazník obchodní oddělení</span><span class="sxs-lookup"><span data-stu-id="79f11-158">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="79f11-159">customerName</span><span class="sxs-lookup"><span data-stu-id="79f11-159">customerName</span></span> | `contains` | <span data-ttu-id="79f11-160">Jméno zákazníka.</span><span class="sxs-lookup"><span data-stu-id="79f11-160">The name of the customer.</span></span> |
| <span data-ttu-id="79f11-161">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="79f11-161">customerTenantId</span></span> | <span data-ttu-id="79f11-162">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="79f11-162">`eq`, `ne`</span></span> | <span data-ttu-id="79f11-163">Řetězec ve formátu GUID, který identifikuje tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="79f11-163">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="79f11-164">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="79f11-164">deprovisionedDate</span></span> | <span data-ttu-id="79f11-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="79f11-166">Datum zrušení zřízení předplatného.</span><span class="sxs-lookup"><span data-stu-id="79f11-166">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="79f11-167">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="79f11-167">The default value is null.</span></span> |
| <span data-ttu-id="79f11-168">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="79f11-168">effectiveStartDate</span></span> | <span data-ttu-id="79f11-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="79f11-170">Datum, kdy se předplatné spustí.</span><span class="sxs-lookup"><span data-stu-id="79f11-170">The date the subscription starts.</span></span> |
| <span data-ttu-id="79f11-171">friendlyName</span><span class="sxs-lookup"><span data-stu-id="79f11-171">friendlyName</span></span> | `contains` | <span data-ttu-id="79f11-172">Název předplatného.</span><span class="sxs-lookup"><span data-stu-id="79f11-172">The name of the subscription.</span></span> |
| <span data-ttu-id="79f11-173">id</span><span class="sxs-lookup"><span data-stu-id="79f11-173">id</span></span> | <span data-ttu-id="79f11-174">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="79f11-174">`eq`, `ne`</span></span> | <span data-ttu-id="79f11-175">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="79f11-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="79f11-176">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="79f11-176">lastRenewalDate</span></span> | <span data-ttu-id="79f11-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="79f11-178">Datum poslední obnovy odběru</span><span class="sxs-lookup"><span data-stu-id="79f11-178">The date that the subscription was last renewed.</span></span> <span data-ttu-id="79f11-179">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="79f11-179">The default value is null.</span></span> |
| <span data-ttu-id="79f11-180">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="79f11-180">lastUsageDate</span></span> | <span data-ttu-id="79f11-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="79f11-182">Datum posledního použití předplatného</span><span class="sxs-lookup"><span data-stu-id="79f11-182">The date that the subscription was last used.</span></span> <span data-ttu-id="79f11-183">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="79f11-183">The default value is null.</span></span> |
| <span data-ttu-id="79f11-184">partnerId</span><span class="sxs-lookup"><span data-stu-id="79f11-184">partnerId</span></span> | <span data-ttu-id="79f11-185">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="79f11-185">`eq`, `ne`</span></span> | <span data-ttu-id="79f11-186">ID MPN</span><span class="sxs-lookup"><span data-stu-id="79f11-186">The MPN ID.</span></span> <span data-ttu-id="79f11-187">U přímého prodejce bude tato hodnota ID MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="79f11-187">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="79f11-188">Pro nepřímý prodejce bude tato hodnota ID MPN nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="79f11-188">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="79f11-189">partnerName</span><span class="sxs-lookup"><span data-stu-id="79f11-189">partnerName</span></span> | <span data-ttu-id="79f11-190">řetězec</span><span class="sxs-lookup"><span data-stu-id="79f11-190">string</span></span> | <span data-ttu-id="79f11-191">Název partnera, pro kterého se předplatné zakoupilo</span><span class="sxs-lookup"><span data-stu-id="79f11-191">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="79f11-192">NázevVýrobku</span><span class="sxs-lookup"><span data-stu-id="79f11-192">productName</span></span> | <span data-ttu-id="79f11-193">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="79f11-193">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="79f11-194">Název produktu.</span><span class="sxs-lookup"><span data-stu-id="79f11-194">The name of the product.</span></span> |
| <span data-ttu-id="79f11-195">providerName</span><span class="sxs-lookup"><span data-stu-id="79f11-195">providerName</span></span> | <span data-ttu-id="79f11-196">řetězec</span><span class="sxs-lookup"><span data-stu-id="79f11-196">string</span></span> | <span data-ttu-id="79f11-197">Pokud je transakce předplatného určena pro nepřímý prodejce, jméno poskytovatele je nepřímým poskytovatelem, který si zakoupil předplatné.</span><span class="sxs-lookup"><span data-stu-id="79f11-197">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="79f11-198">status</span><span class="sxs-lookup"><span data-stu-id="79f11-198">status</span></span> | <span data-ttu-id="79f11-199">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="79f11-199">`eq`, `ne`</span></span> | <span data-ttu-id="79f11-200">Stav předplatného.</span><span class="sxs-lookup"><span data-stu-id="79f11-200">The subscription status.</span></span> <span data-ttu-id="79f11-201">Podporovány jsou následující hodnoty: "aktivní", "pozastaveno" nebo "zrušení zřízení".</span><span class="sxs-lookup"><span data-stu-id="79f11-201">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="79f11-202">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="79f11-202">subscriptionType</span></span> | <span data-ttu-id="79f11-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="79f11-203">`eq`, `ne`</span></span> | <span data-ttu-id="79f11-204">Typ předplatného.</span><span class="sxs-lookup"><span data-stu-id="79f11-204">The subscription type.</span></span> <span data-ttu-id="79f11-205">**Poznámka**: Toto pole rozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="79f11-205">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="79f11-206">podporované hodnoty jsou: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="79f11-206">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="79f11-207">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="79f11-207">trialStartDate</span></span> | <span data-ttu-id="79f11-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="79f11-209">Datum, kdy se začalo zkušební období předplatného.</span><span class="sxs-lookup"><span data-stu-id="79f11-209">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="79f11-210">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="79f11-210">The default value is null.</span></span> |
| <span data-ttu-id="79f11-211">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="79f11-211">trialToPaidConversionDate</span></span> | <span data-ttu-id="79f11-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="79f11-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="79f11-213">Datum, kdy se předplatné převede ze zkušební verze na placené.</span><span class="sxs-lookup"><span data-stu-id="79f11-213">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="79f11-214">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="79f11-214">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="79f11-215">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="79f11-215">Request headers</span></span>

<span data-ttu-id="79f11-216">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="79f11-216">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="79f11-217">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="79f11-217">Request body</span></span>

<span data-ttu-id="79f11-218">Žádné</span><span class="sxs-lookup"><span data-stu-id="79f11-218">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="79f11-219">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="79f11-219">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="79f11-220">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="79f11-220">REST response</span></span>

<span data-ttu-id="79f11-221">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [předplatného](partner-center-analytics-resources.md#subscription-resource) , které splňují kritéria filtru.</span><span class="sxs-lookup"><span data-stu-id="79f11-221">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="79f11-222">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="79f11-222">Response success and error codes</span></span>

<span data-ttu-id="79f11-223">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="79f11-223">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="79f11-224">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="79f11-224">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="79f11-225">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="79f11-225">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="79f11-226">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="79f11-226">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="79f11-227">Viz také</span><span class="sxs-lookup"><span data-stu-id="79f11-227">See also</span></span>

- [<span data-ttu-id="79f11-228">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="79f11-228">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
