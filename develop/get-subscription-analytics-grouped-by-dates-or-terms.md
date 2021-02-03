---
title: Získání analýzy předplatných seskupených podle kalendářních dat nebo podmínek
description: Jak získat informace o analýze předplatného seskupené podle kalendářních dat nebo podmínek.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766768"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="dcd70-103">Získání analýzy předplatných seskupených podle kalendářních dat nebo podmínek</span><span class="sxs-lookup"><span data-stu-id="dcd70-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="dcd70-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="dcd70-104">**Applies To**</span></span>

- <span data-ttu-id="dcd70-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="dcd70-105">Partner Center</span></span>
- <span data-ttu-id="dcd70-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="dcd70-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="dcd70-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="dcd70-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="dcd70-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="dcd70-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="dcd70-109">Jak získat informace o analýze předplatných pro vaše zákazníky seskupené podle kalendářních dat nebo podmínek.</span><span class="sxs-lookup"><span data-stu-id="dcd70-109">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcd70-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="dcd70-110">Prerequisites</span></span>

- <span data-ttu-id="dcd70-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dcd70-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dcd70-112">Tento scénář podporuje ověřování pouze s přihlašovacími údaji uživatele.</span><span class="sxs-lookup"><span data-stu-id="dcd70-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="dcd70-113">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="dcd70-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dcd70-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="dcd70-114">Request syntax</span></span>

| <span data-ttu-id="dcd70-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="dcd70-115">Method</span></span> | <span data-ttu-id="dcd70-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="dcd70-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="dcd70-117">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="dcd70-117">**GET**</span></span> | <span data-ttu-id="dcd70-118">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Subscriptions? GroupBy = {groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="dcd70-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="dcd70-119">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="dcd70-119">URI parameters</span></span>

<span data-ttu-id="dcd70-120">K identifikaci vaší organizace a k seskupení výsledků použijte následující požadované parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="dcd70-120">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="dcd70-121">Název</span><span class="sxs-lookup"><span data-stu-id="dcd70-121">Name</span></span> | <span data-ttu-id="dcd70-122">Typ</span><span class="sxs-lookup"><span data-stu-id="dcd70-122">Type</span></span> | <span data-ttu-id="dcd70-123">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="dcd70-123">Required</span></span> | <span data-ttu-id="dcd70-124">Popis</span><span class="sxs-lookup"><span data-stu-id="dcd70-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="dcd70-125">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="dcd70-125">groupby_queries</span></span> | <span data-ttu-id="dcd70-126">páry řetězců a data a času</span><span class="sxs-lookup"><span data-stu-id="dcd70-126">pairs of strings and dateTime</span></span> | <span data-ttu-id="dcd70-127">Yes</span><span class="sxs-lookup"><span data-stu-id="dcd70-127">Yes</span></span> | <span data-ttu-id="dcd70-128">Termíny a data pro filtrování výsledku.</span><span class="sxs-lookup"><span data-stu-id="dcd70-128">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="dcd70-129">Syntaxe GroupBy</span><span class="sxs-lookup"><span data-stu-id="dcd70-129">GroupBy syntax</span></span>

<span data-ttu-id="dcd70-130">Parametr Group by se musí skládat jako řada hodnot polí oddělených čárkou.</span><span class="sxs-lookup"><span data-stu-id="dcd70-130">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="dcd70-131">Nekódovaný příklad vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="dcd70-131">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="dcd70-132">V následující tabulce je uveden seznam podporovaných polí pro Group by.</span><span class="sxs-lookup"><span data-stu-id="dcd70-132">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="dcd70-133">Pole</span><span class="sxs-lookup"><span data-stu-id="dcd70-133">Field</span></span> | <span data-ttu-id="dcd70-134">Typ</span><span class="sxs-lookup"><span data-stu-id="dcd70-134">Type</span></span> | <span data-ttu-id="dcd70-135">Description</span><span class="sxs-lookup"><span data-stu-id="dcd70-135">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="dcd70-136">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="dcd70-136">customerTenantId</span></span> | <span data-ttu-id="dcd70-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-137">string</span></span> | <span data-ttu-id="dcd70-138">Řetězec ve formátu GUID, který identifikuje tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="dcd70-138">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="dcd70-139">customerName</span><span class="sxs-lookup"><span data-stu-id="dcd70-139">customerName</span></span> | <span data-ttu-id="dcd70-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-140">string</span></span> | <span data-ttu-id="dcd70-141">Jméno zákazníka.</span><span class="sxs-lookup"><span data-stu-id="dcd70-141">The name of the customer.</span></span> |
| <span data-ttu-id="dcd70-142">customerMarket</span><span class="sxs-lookup"><span data-stu-id="dcd70-142">customerMarket</span></span> | <span data-ttu-id="dcd70-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-143">string</span></span> | <span data-ttu-id="dcd70-144">Země nebo oblast, ve které má zákazník obchodní oddělení</span><span class="sxs-lookup"><span data-stu-id="dcd70-144">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="dcd70-145">id</span><span class="sxs-lookup"><span data-stu-id="dcd70-145">id</span></span> | <span data-ttu-id="dcd70-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-146">string</span></span> | <span data-ttu-id="dcd70-147">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="dcd70-147">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="dcd70-148">status</span><span class="sxs-lookup"><span data-stu-id="dcd70-148">status</span></span> | <span data-ttu-id="dcd70-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-149">string</span></span> | <span data-ttu-id="dcd70-150">Stav předplatného.</span><span class="sxs-lookup"><span data-stu-id="dcd70-150">The subscription status.</span></span> <span data-ttu-id="dcd70-151">Podporovány jsou následující hodnoty: "aktivní", "pozastaveno" nebo "zrušení zřízení".</span><span class="sxs-lookup"><span data-stu-id="dcd70-151">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="dcd70-152">NázevVýrobku</span><span class="sxs-lookup"><span data-stu-id="dcd70-152">productName</span></span> | <span data-ttu-id="dcd70-153">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-153">string</span></span> | <span data-ttu-id="dcd70-154">Název produktu.</span><span class="sxs-lookup"><span data-stu-id="dcd70-154">The name of the product.</span></span> |
| <span data-ttu-id="dcd70-155">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="dcd70-155">subscriptionType</span></span> | <span data-ttu-id="dcd70-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-156">string</span></span> | <span data-ttu-id="dcd70-157">Typ předplatného.</span><span class="sxs-lookup"><span data-stu-id="dcd70-157">The subscription type.</span></span> <span data-ttu-id="dcd70-158">Poznámka: Toto pole rozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="dcd70-158">Note: This field is case sensitive.</span></span> <span data-ttu-id="dcd70-159">Podporované hodnoty jsou: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="dcd70-159">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="dcd70-160">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="dcd70-160">autoRenewEnabled</span></span> | <span data-ttu-id="dcd70-161">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="dcd70-161">Boolean</span></span> | <span data-ttu-id="dcd70-162">Hodnota, která označuje, jestli se předplatné obnovuje automaticky.</span><span class="sxs-lookup"><span data-stu-id="dcd70-162">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="dcd70-163">partnerId</span><span class="sxs-lookup"><span data-stu-id="dcd70-163">partnerId</span></span>  | <span data-ttu-id="dcd70-164">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-164">string</span></span> | <span data-ttu-id="dcd70-165">ID MPN</span><span class="sxs-lookup"><span data-stu-id="dcd70-165">The MPN ID.</span></span> <span data-ttu-id="dcd70-166">U přímého prodejce bude tento parametr ID MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="dcd70-166">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="dcd70-167">Pro nepřímý prodejce tento parametr bude ID MPN nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="dcd70-167">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="dcd70-168">friendlyName</span><span class="sxs-lookup"><span data-stu-id="dcd70-168">friendlyName</span></span> | <span data-ttu-id="dcd70-169">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-169">string</span></span> | <span data-ttu-id="dcd70-170">Název předplatného.</span><span class="sxs-lookup"><span data-stu-id="dcd70-170">The name of the subscription.</span></span> |
| <span data-ttu-id="dcd70-171">partnerName</span><span class="sxs-lookup"><span data-stu-id="dcd70-171">partnerName</span></span> | <span data-ttu-id="dcd70-172">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-172">string</span></span> | <span data-ttu-id="dcd70-173">Název partnera, pro kterého se předplatné zakoupilo</span><span class="sxs-lookup"><span data-stu-id="dcd70-173">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="dcd70-174">providerName</span><span class="sxs-lookup"><span data-stu-id="dcd70-174">providerName</span></span> | <span data-ttu-id="dcd70-175">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-175">string</span></span> | <span data-ttu-id="dcd70-176">Pokud je transakce předplatného určena pro nepřímý prodejce, jméno poskytovatele je nepřímým poskytovatelem, který si zakoupil předplatné.</span><span class="sxs-lookup"><span data-stu-id="dcd70-176">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="dcd70-177">creationDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-177">creationDate</span></span> | <span data-ttu-id="dcd70-178">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-178">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-179">Datum vytvoření odběru.</span><span class="sxs-lookup"><span data-stu-id="dcd70-179">The date the subscription was created.</span></span> |
| <span data-ttu-id="dcd70-180">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-180">effectiveStartDate</span></span> | <span data-ttu-id="dcd70-181">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-181">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-182">Datum, kdy se předplatné spustí.</span><span class="sxs-lookup"><span data-stu-id="dcd70-182">The date the subscription starts.</span></span> |
| <span data-ttu-id="dcd70-183">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-183">commitmentEndDate</span></span> | <span data-ttu-id="dcd70-184">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-184">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-185">Datum ukončení předplatného</span><span class="sxs-lookup"><span data-stu-id="dcd70-185">The date the subscription ends.</span></span> |
| <span data-ttu-id="dcd70-186">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-186">currentStateEndDate</span></span> | <span data-ttu-id="dcd70-187">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-187">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-188">Datum, kdy se změní aktuální stav předplatného.</span><span class="sxs-lookup"><span data-stu-id="dcd70-188">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="dcd70-189">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-189">trialToPaidConversionDate</span></span> | <span data-ttu-id="dcd70-190">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-190">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-191">Datum, kdy se předplatné převede ze zkušební verze na placené.</span><span class="sxs-lookup"><span data-stu-id="dcd70-191">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="dcd70-192">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="dcd70-192">The default value is null.</span></span> |
| <span data-ttu-id="dcd70-193">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-193">trialStartDate</span></span> | <span data-ttu-id="dcd70-194">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-194">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-195">Datum, kdy se začalo zkušební období předplatného.</span><span class="sxs-lookup"><span data-stu-id="dcd70-195">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="dcd70-196">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="dcd70-196">The default value is null.</span></span> |
| <span data-ttu-id="dcd70-197">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-197">lastUsageDate</span></span> | <span data-ttu-id="dcd70-198">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-198">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-199">Datum posledního použití předplatného</span><span class="sxs-lookup"><span data-stu-id="dcd70-199">The date that the subscription was last used.</span></span> <span data-ttu-id="dcd70-200">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="dcd70-200">The default value is null.</span></span> |
| <span data-ttu-id="dcd70-201">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-201">deprovisionedDate</span></span> | <span data-ttu-id="dcd70-202">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-202">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-203">Datum zrušení zřízení předplatného.</span><span class="sxs-lookup"><span data-stu-id="dcd70-203">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="dcd70-204">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="dcd70-204">The default value is null.</span></span> |
| <span data-ttu-id="dcd70-205">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="dcd70-205">lastRenewalDate</span></span> | <span data-ttu-id="dcd70-206">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="dcd70-206">string in UTC date time format</span></span> | <span data-ttu-id="dcd70-207">Datum poslední obnovy odběru</span><span class="sxs-lookup"><span data-stu-id="dcd70-207">The date that the subscription was last renewed.</span></span> <span data-ttu-id="dcd70-208">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="dcd70-208">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="dcd70-209">Filtrovat pole</span><span class="sxs-lookup"><span data-stu-id="dcd70-209">Filter fields</span></span>

<span data-ttu-id="dcd70-210">V následující tabulce jsou uvedena volitelná pole filtru a jejich popisy:</span><span class="sxs-lookup"><span data-stu-id="dcd70-210">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="dcd70-211">Pole</span><span class="sxs-lookup"><span data-stu-id="dcd70-211">Field</span></span> | <span data-ttu-id="dcd70-212">Typ</span><span class="sxs-lookup"><span data-stu-id="dcd70-212">Type</span></span> |  <span data-ttu-id="dcd70-213">Description</span><span class="sxs-lookup"><span data-stu-id="dcd70-213">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="dcd70-214">top</span><span class="sxs-lookup"><span data-stu-id="dcd70-214">top</span></span> | <span data-ttu-id="dcd70-215">int</span><span class="sxs-lookup"><span data-stu-id="dcd70-215">int</span></span> | <span data-ttu-id="dcd70-216">Počet řádků dat, který má být vrácen v požadavku.</span><span class="sxs-lookup"><span data-stu-id="dcd70-216">The number of rows of data to return in the request.</span></span> <span data-ttu-id="dcd70-217">Pokud hodnota není zadaná, maximální hodnota a výchozí hodnota jsou 10000.</span><span class="sxs-lookup"><span data-stu-id="dcd70-217">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="dcd70-218">Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="dcd70-218">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="dcd70-219">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="dcd70-219">skip</span></span> | <span data-ttu-id="dcd70-220">int</span><span class="sxs-lookup"><span data-stu-id="dcd70-220">int</span></span> | <span data-ttu-id="dcd70-221">Počet řádků, které mají být v dotazu přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="dcd70-221">The number of rows to skip in the query.</span></span> <span data-ttu-id="dcd70-222">Tento parametr použijte pro stránku s velkými datovými sadami.</span><span class="sxs-lookup"><span data-stu-id="dcd70-222">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="dcd70-223">Například Top = 10000 a Skip = 0 načte prvních 10000 řádků dat, Top = 10000 a Skip = 10000 načte další 10000 řádků dat.</span><span class="sxs-lookup"><span data-stu-id="dcd70-223">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="dcd70-224">filter</span><span class="sxs-lookup"><span data-stu-id="dcd70-224">filter</span></span> | <span data-ttu-id="dcd70-225">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-225">string</span></span> | <span data-ttu-id="dcd70-226">Jeden nebo více příkazů, které filtrují řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="dcd70-226">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="dcd70-227">Každý příkaz filtru obsahuje název pole z textu odpovědi a hodnotu, která je přidružena k **`eq`** , **`ne`** nebo pro určitá pole **`contains`** operátor.</span><span class="sxs-lookup"><span data-stu-id="dcd70-227">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="dcd70-228">Příkazy lze kombinovat pomocí operátoru **`and`** OR **`or`** .</span><span class="sxs-lookup"><span data-stu-id="dcd70-228">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="dcd70-229">Řetězcové hodnoty musí být obklopeny jednoduchými uvozovkami v parametru Filter.</span><span class="sxs-lookup"><span data-stu-id="dcd70-229">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="dcd70-230">Seznam polí, která lze filtrovat, a operátory, které jsou s těmito poli podporovány, naleznete v následující části.</span><span class="sxs-lookup"><span data-stu-id="dcd70-230">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="dcd70-231">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="dcd70-231">aggregationLevel</span></span> | <span data-ttu-id="dcd70-232">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-232">string</span></span> | <span data-ttu-id="dcd70-233">Určuje časový rozsah, pro který se mají načíst agregovaná data.</span><span class="sxs-lookup"><span data-stu-id="dcd70-233">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="dcd70-234">Může to být jeden z následujících řetězců: **den**, **týden** nebo **měsíc**.</span><span class="sxs-lookup"><span data-stu-id="dcd70-234">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="dcd70-235">Pokud hodnota není zadaná, výchozí hodnota je **DateRange**.</span><span class="sxs-lookup"><span data-stu-id="dcd70-235">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="dcd70-236">**Poznámka**: Tento parametr platí pouze v případě, že je pole data předáno jako součást parametru GroupBy.</span><span class="sxs-lookup"><span data-stu-id="dcd70-236">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="dcd70-237">groupBy</span><span class="sxs-lookup"><span data-stu-id="dcd70-237">groupBy</span></span> | <span data-ttu-id="dcd70-238">řetězec</span><span class="sxs-lookup"><span data-stu-id="dcd70-238">string</span></span> | <span data-ttu-id="dcd70-239">Příkaz, který aplikuje agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="dcd70-239">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dcd70-240">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="dcd70-240">Request headers</span></span>

<span data-ttu-id="dcd70-241">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dcd70-241">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dcd70-242">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="dcd70-242">Request body</span></span>

<span data-ttu-id="dcd70-243">Žádné</span><span class="sxs-lookup"><span data-stu-id="dcd70-243">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dcd70-244">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="dcd70-244">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="dcd70-245">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="dcd70-245">REST response</span></span>

<span data-ttu-id="dcd70-246">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [předplatného](partner-center-analytics-resources.md#subscription-resource) seskupených podle zadaných podmínek a dat.</span><span class="sxs-lookup"><span data-stu-id="dcd70-246">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dcd70-247">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="dcd70-247">Response success and error codes</span></span>

<span data-ttu-id="dcd70-248">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="dcd70-248">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dcd70-249">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="dcd70-249">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dcd70-250">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dcd70-250">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dcd70-251">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="dcd70-251">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a><span data-ttu-id="dcd70-252">Viz také</span><span class="sxs-lookup"><span data-stu-id="dcd70-252">See also</span></span>

[<span data-ttu-id="dcd70-253">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="dcd70-253">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
