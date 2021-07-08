---
title: Získání analýz předplatného seskupených podle kalendářních dat nebo termínů
description: Jak získat analytické informace předplatného seskupené podle kalendářních dat nebo termínů
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8192a9863d53ec8697a7341cd38c69200614bd4a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548715"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="26e58-103">Získání analýz předplatného seskupených podle kalendářních dat nebo termínů</span><span class="sxs-lookup"><span data-stu-id="26e58-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="26e58-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="26e58-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="26e58-105">Jak získat analytické informace o předplatném pro zákazníky seskupené podle kalendářních dat nebo podmínek.</span><span class="sxs-lookup"><span data-stu-id="26e58-105">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26e58-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="26e58-106">Prerequisites</span></span>

- <span data-ttu-id="26e58-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="26e58-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="26e58-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů uživatele.</span><span class="sxs-lookup"><span data-stu-id="26e58-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="26e58-109">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="26e58-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="26e58-110">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="26e58-110">Request syntax</span></span>

| <span data-ttu-id="26e58-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="26e58-111">Method</span></span> | <span data-ttu-id="26e58-112">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="26e58-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="26e58-113">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="26e58-113">**GET**</span></span> | <span data-ttu-id="26e58-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="26e58-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="26e58-115">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="26e58-115">URI parameters</span></span>

<span data-ttu-id="26e58-116">Pomocí následujících požadovaných parametrů cesty identifikujte svou organizaci a seskupte výsledky.</span><span class="sxs-lookup"><span data-stu-id="26e58-116">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="26e58-117">Název</span><span class="sxs-lookup"><span data-stu-id="26e58-117">Name</span></span> | <span data-ttu-id="26e58-118">Typ</span><span class="sxs-lookup"><span data-stu-id="26e58-118">Type</span></span> | <span data-ttu-id="26e58-119">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="26e58-119">Required</span></span> | <span data-ttu-id="26e58-120">Popis</span><span class="sxs-lookup"><span data-stu-id="26e58-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="26e58-121">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="26e58-121">groupby_queries</span></span> | <span data-ttu-id="26e58-122">dvojice řetězců a dateTime</span><span class="sxs-lookup"><span data-stu-id="26e58-122">pairs of strings and dateTime</span></span> | <span data-ttu-id="26e58-123">Yes</span><span class="sxs-lookup"><span data-stu-id="26e58-123">Yes</span></span> | <span data-ttu-id="26e58-124">Termíny a kalendářní data pro filtrování výsledku.</span><span class="sxs-lookup"><span data-stu-id="26e58-124">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="26e58-125">Syntaxe GroupBy</span><span class="sxs-lookup"><span data-stu-id="26e58-125">GroupBy syntax</span></span>

<span data-ttu-id="26e58-126">Parametr seskupit podle se musí skládat jako řada hodnot polí oddělených čárkami.</span><span class="sxs-lookup"><span data-stu-id="26e58-126">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="26e58-127">Nekódovaný příklad vypadá jako tento:</span><span class="sxs-lookup"><span data-stu-id="26e58-127">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="26e58-128">Následující tabulka obsahuje seznam podporovaných polí pro seskupení podle.</span><span class="sxs-lookup"><span data-stu-id="26e58-128">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="26e58-129">Pole</span><span class="sxs-lookup"><span data-stu-id="26e58-129">Field</span></span> | <span data-ttu-id="26e58-130">Typ</span><span class="sxs-lookup"><span data-stu-id="26e58-130">Type</span></span> | <span data-ttu-id="26e58-131">Description</span><span class="sxs-lookup"><span data-stu-id="26e58-131">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="26e58-132">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="26e58-132">customerTenantId</span></span> | <span data-ttu-id="26e58-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-133">string</span></span> | <span data-ttu-id="26e58-134">Řetězec ve formátu GUID, který identifikuje tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="26e58-134">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="26e58-135">customerName</span><span class="sxs-lookup"><span data-stu-id="26e58-135">customerName</span></span> | <span data-ttu-id="26e58-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-136">string</span></span> | <span data-ttu-id="26e58-137">Jméno zákazníka.</span><span class="sxs-lookup"><span data-stu-id="26e58-137">The name of the customer.</span></span> |
| <span data-ttu-id="26e58-138">customerMarket</span><span class="sxs-lookup"><span data-stu-id="26e58-138">customerMarket</span></span> | <span data-ttu-id="26e58-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-139">string</span></span> | <span data-ttu-id="26e58-140">Země nebo oblast, ve které zákazník obchoduje.</span><span class="sxs-lookup"><span data-stu-id="26e58-140">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="26e58-141">id</span><span class="sxs-lookup"><span data-stu-id="26e58-141">id</span></span> | <span data-ttu-id="26e58-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-142">string</span></span> | <span data-ttu-id="26e58-143">Řetězec formátovaný identifikátorem GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="26e58-143">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="26e58-144">status</span><span class="sxs-lookup"><span data-stu-id="26e58-144">status</span></span> | <span data-ttu-id="26e58-145">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-145">string</span></span> | <span data-ttu-id="26e58-146">Stav předplatného</span><span class="sxs-lookup"><span data-stu-id="26e58-146">The subscription status.</span></span> <span data-ttu-id="26e58-147">Podporované hodnoty: AKTIVNÍ, POZASTAVENO nebo ZRUŠENO ZŘÍZENÍ.</span><span class="sxs-lookup"><span data-stu-id="26e58-147">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="26e58-148">Productname</span><span class="sxs-lookup"><span data-stu-id="26e58-148">productName</span></span> | <span data-ttu-id="26e58-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-149">string</span></span> | <span data-ttu-id="26e58-150">Název produktu.</span><span class="sxs-lookup"><span data-stu-id="26e58-150">The name of the product.</span></span> |
| <span data-ttu-id="26e58-151">typ předplatného</span><span class="sxs-lookup"><span data-stu-id="26e58-151">subscriptionType</span></span> | <span data-ttu-id="26e58-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-152">string</span></span> | <span data-ttu-id="26e58-153">Typ předplatného.</span><span class="sxs-lookup"><span data-stu-id="26e58-153">The subscription type.</span></span> <span data-ttu-id="26e58-154">Poznámka: V tomto poli se rozlišují velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="26e58-154">Note: This field is case-sensitive.</span></span> <span data-ttu-id="26e58-155">Podporované hodnoty: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="26e58-155">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="26e58-156">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="26e58-156">autoRenewEnabled</span></span> | <span data-ttu-id="26e58-157">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="26e58-157">Boolean</span></span> | <span data-ttu-id="26e58-158">Hodnota, která určuje, jestli se předplatné obnovuje automaticky.</span><span class="sxs-lookup"><span data-stu-id="26e58-158">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="26e58-159">ID partnera</span><span class="sxs-lookup"><span data-stu-id="26e58-159">partnerId</span></span>  | <span data-ttu-id="26e58-160">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-160">string</span></span> | <span data-ttu-id="26e58-161">ID MPN.</span><span class="sxs-lookup"><span data-stu-id="26e58-161">The MPN ID.</span></span> <span data-ttu-id="26e58-162">Pro přímého prodejce bude tento parametr ID MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="26e58-162">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="26e58-163">Pro nepřímého prodejce bude tento parametr ID MPN nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="26e58-163">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="26e58-164">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="26e58-164">friendlyName</span></span> | <span data-ttu-id="26e58-165">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-165">string</span></span> | <span data-ttu-id="26e58-166">Název předplatného.</span><span class="sxs-lookup"><span data-stu-id="26e58-166">The name of the subscription.</span></span> |
| <span data-ttu-id="26e58-167">název partnera</span><span class="sxs-lookup"><span data-stu-id="26e58-167">partnerName</span></span> | <span data-ttu-id="26e58-168">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-168">string</span></span> | <span data-ttu-id="26e58-169">Název partnera, pro kterého bylo předplatné zakoupeno</span><span class="sxs-lookup"><span data-stu-id="26e58-169">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="26e58-170">Providername</span><span class="sxs-lookup"><span data-stu-id="26e58-170">providerName</span></span> | <span data-ttu-id="26e58-171">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-171">string</span></span> | <span data-ttu-id="26e58-172">Pokud je transakce předplatného zprostředkovatelem nepřímého prodejce, název poskytovatele je nepřímý poskytovatel, který předplatné zakoupil.</span><span class="sxs-lookup"><span data-stu-id="26e58-172">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="26e58-173">datum vytvoření</span><span class="sxs-lookup"><span data-stu-id="26e58-173">creationDate</span></span> | <span data-ttu-id="26e58-174">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-174">string in UTC date time format</span></span> | <span data-ttu-id="26e58-175">Datum vytvoření předplatného</span><span class="sxs-lookup"><span data-stu-id="26e58-175">The date the subscription was created.</span></span> |
| <span data-ttu-id="26e58-176">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="26e58-176">effectiveStartDate</span></span> | <span data-ttu-id="26e58-177">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-177">string in UTC date time format</span></span> | <span data-ttu-id="26e58-178">Datum zahájení odběru</span><span class="sxs-lookup"><span data-stu-id="26e58-178">The date the subscription starts.</span></span> |
| <span data-ttu-id="26e58-179">datum ukončení závazku</span><span class="sxs-lookup"><span data-stu-id="26e58-179">commitmentEndDate</span></span> | <span data-ttu-id="26e58-180">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-180">string in UTC date time format</span></span> | <span data-ttu-id="26e58-181">Datum, kdy odběr skončí.</span><span class="sxs-lookup"><span data-stu-id="26e58-181">The date the subscription ends.</span></span> |
| <span data-ttu-id="26e58-182">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="26e58-182">currentStateEndDate</span></span> | <span data-ttu-id="26e58-183">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-183">string in UTC date time format</span></span> | <span data-ttu-id="26e58-184">Datum, kdy se změní aktuální stav předplatného.</span><span class="sxs-lookup"><span data-stu-id="26e58-184">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="26e58-185">trialToPaidConversionDate</span><span class="sxs-lookup"><span data-stu-id="26e58-185">trialToPaidConversionDate</span></span> | <span data-ttu-id="26e58-186">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-186">string in UTC date time format</span></span> | <span data-ttu-id="26e58-187">Datum převodu předplatného ze zkušební verze na placenou verzi.</span><span class="sxs-lookup"><span data-stu-id="26e58-187">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="26e58-188">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="26e58-188">The default value is null.</span></span> |
| <span data-ttu-id="26e58-189">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="26e58-189">trialStartDate</span></span> | <span data-ttu-id="26e58-190">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-190">string in UTC date time format</span></span> | <span data-ttu-id="26e58-191">Datum zahájení zkušebního období předplatného</span><span class="sxs-lookup"><span data-stu-id="26e58-191">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="26e58-192">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="26e58-192">The default value is null.</span></span> |
| <span data-ttu-id="26e58-193">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="26e58-193">lastUsageDate</span></span> | <span data-ttu-id="26e58-194">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-194">string in UTC date time format</span></span> | <span data-ttu-id="26e58-195">Datum posledního použití předplatného</span><span class="sxs-lookup"><span data-stu-id="26e58-195">The date that the subscription was last used.</span></span> <span data-ttu-id="26e58-196">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="26e58-196">The default value is null.</span></span> |
| <span data-ttu-id="26e58-197">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="26e58-197">deprovisionedDate</span></span> | <span data-ttu-id="26e58-198">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-198">string in UTC date time format</span></span> | <span data-ttu-id="26e58-199">Datum, kdy bylo zrušeno zřízení předplatného.</span><span class="sxs-lookup"><span data-stu-id="26e58-199">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="26e58-200">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="26e58-200">The default value is null.</span></span> |
| <span data-ttu-id="26e58-201">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="26e58-201">lastRenewalDate</span></span> | <span data-ttu-id="26e58-202">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="26e58-202">string in UTC date time format</span></span> | <span data-ttu-id="26e58-203">Datum posledního prodloužení platnosti předplatného</span><span class="sxs-lookup"><span data-stu-id="26e58-203">The date that the subscription was last renewed.</span></span> <span data-ttu-id="26e58-204">Výchozí hodnotou je hodnota null.</span><span class="sxs-lookup"><span data-stu-id="26e58-204">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="26e58-205">Filtrování polí</span><span class="sxs-lookup"><span data-stu-id="26e58-205">Filter fields</span></span>

<span data-ttu-id="26e58-206">Následující tabulka obsahuje volitelná pole filtru a jejich popisy:</span><span class="sxs-lookup"><span data-stu-id="26e58-206">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="26e58-207">Pole</span><span class="sxs-lookup"><span data-stu-id="26e58-207">Field</span></span> | <span data-ttu-id="26e58-208">Typ</span><span class="sxs-lookup"><span data-stu-id="26e58-208">Type</span></span> |  <span data-ttu-id="26e58-209">Description</span><span class="sxs-lookup"><span data-stu-id="26e58-209">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="26e58-210">top</span><span class="sxs-lookup"><span data-stu-id="26e58-210">top</span></span> | <span data-ttu-id="26e58-211">int</span><span class="sxs-lookup"><span data-stu-id="26e58-211">int</span></span> | <span data-ttu-id="26e58-212">Počet řádků dat, které se v požadavku vrátí.</span><span class="sxs-lookup"><span data-stu-id="26e58-212">The number of rows of data to return in the request.</span></span> <span data-ttu-id="26e58-213">Pokud hodnota není zadaná, maximální hodnota a výchozí hodnota jsou 10000.</span><span class="sxs-lookup"><span data-stu-id="26e58-213">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="26e58-214">Pokud dotaz obsahuje více řádků, obsahuje text odpovědi další odkaz, který můžete použít k vyžádání další stránky dat.</span><span class="sxs-lookup"><span data-stu-id="26e58-214">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="26e58-215">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="26e58-215">skip</span></span> | <span data-ttu-id="26e58-216">int</span><span class="sxs-lookup"><span data-stu-id="26e58-216">int</span></span> | <span data-ttu-id="26e58-217">Počet řádků, které se v dotazu přeskočí</span><span class="sxs-lookup"><span data-stu-id="26e58-217">The number of rows to skip in the query.</span></span> <span data-ttu-id="26e58-218">Tento parametr použijte k stránkování velkých datových sad.</span><span class="sxs-lookup"><span data-stu-id="26e58-218">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="26e58-219">Například top=10000 a skip=0 načte prvních 1 0000 řádků dat, top=10000 a skip=10000 načte dalších 1 0000 řádků dat.</span><span class="sxs-lookup"><span data-stu-id="26e58-219">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="26e58-220">filter</span><span class="sxs-lookup"><span data-stu-id="26e58-220">filter</span></span> | <span data-ttu-id="26e58-221">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-221">string</span></span> | <span data-ttu-id="26e58-222">Jeden nebo více příkazů, které filtruje řádky v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="26e58-222">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="26e58-223">Každý příkaz filtru obsahuje název pole z textu odpovědi a hodnotu přidruženou k operátoru , nebo pro **`eq`** **`ne`** určitá **`contains`** pole.</span><span class="sxs-lookup"><span data-stu-id="26e58-223">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="26e58-224">Příkazy lze kombinovat pomocí **`and`** nebo **`or`** .</span><span class="sxs-lookup"><span data-stu-id="26e58-224">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="26e58-225">Řetězcové hodnoty musí být v parametru filtru v jednoduchých uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="26e58-225">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="26e58-226">V následující části najdete seznam polí, která lze filtrovat, a operátory, které jsou u těchto polí podporovány.</span><span class="sxs-lookup"><span data-stu-id="26e58-226">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="26e58-227">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="26e58-227">aggregationLevel</span></span> | <span data-ttu-id="26e58-228">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-228">string</span></span> | <span data-ttu-id="26e58-229">Určuje časový rozsah, pro který se mají načíst agregovaná data.</span><span class="sxs-lookup"><span data-stu-id="26e58-229">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="26e58-230">Může to být jeden z následujících řetězců: **den,** **týden** nebo **měsíc**.</span><span class="sxs-lookup"><span data-stu-id="26e58-230">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="26e58-231">Pokud hodnota není zadaná, výchozí hodnota je **dateRange**.</span><span class="sxs-lookup"><span data-stu-id="26e58-231">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="26e58-232">**Poznámka:** Tento parametr se použije pouze v případě, že je pole data předáno jako součást parametru groupBy.</span><span class="sxs-lookup"><span data-stu-id="26e58-232">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="26e58-233">Groupby</span><span class="sxs-lookup"><span data-stu-id="26e58-233">groupBy</span></span> | <span data-ttu-id="26e58-234">řetězec</span><span class="sxs-lookup"><span data-stu-id="26e58-234">string</span></span> | <span data-ttu-id="26e58-235">Příkaz, který použije agregaci dat pouze na zadaná pole.</span><span class="sxs-lookup"><span data-stu-id="26e58-235">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="26e58-236">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="26e58-236">Request headers</span></span>

<span data-ttu-id="26e58-237">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="26e58-237">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="26e58-238">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="26e58-238">Request body</span></span>

<span data-ttu-id="26e58-239">Žádné</span><span class="sxs-lookup"><span data-stu-id="26e58-239">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="26e58-240">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="26e58-240">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="26e58-241">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="26e58-241">REST response</span></span>

<span data-ttu-id="26e58-242">V případě úspěchu bude text odpovědi obsahovat kolekci prostředků [předplatného](partner-center-analytics-resources.md#subscription-resource) seskupených podle zadaných termínů a kalendářních dat.</span><span class="sxs-lookup"><span data-stu-id="26e58-242">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="26e58-243">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="26e58-243">Response success and error codes</span></span>

<span data-ttu-id="26e58-244">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="26e58-244">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="26e58-245">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="26e58-245">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="26e58-246">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="26e58-246">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="26e58-247">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="26e58-247">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="26e58-248">Viz také</span><span class="sxs-lookup"><span data-stu-id="26e58-248">See also</span></span>

[<span data-ttu-id="26e58-249">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="26e58-249">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
