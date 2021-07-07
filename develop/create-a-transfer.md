---
title: Vytvoření přenosu
description: Jak vytvořit převod předplatných pro zákazníka
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d459a0a96912ab27f312bc73af16af2d4fdb518c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973702"
---
# <a name="create-a-transfer"></a><span data-ttu-id="3768f-103">Vytvoření přenosu</span><span class="sxs-lookup"><span data-stu-id="3768f-103">Create a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3768f-104">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3768f-104">Prerequisites</span></span>

- <span data-ttu-id="3768f-105">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3768f-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3768f-106">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="3768f-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3768f-107">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3768f-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3768f-108">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="3768f-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3768f-109">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="3768f-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3768f-110">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="3768f-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3768f-111">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3768f-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3768f-112">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3768f-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="3768f-113">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="3768f-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3768f-114">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="3768f-114">Request syntax</span></span>

| <span data-ttu-id="3768f-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="3768f-115">Method</span></span>   | <span data-ttu-id="3768f-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3768f-116">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3768f-117">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="3768f-117">**POST**</span></span> | <span data-ttu-id="3768f-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/transfers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3768f-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="3768f-119">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="3768f-119">URI parameter</span></span>

<span data-ttu-id="3768f-120">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="3768f-120">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="3768f-121">Název</span><span class="sxs-lookup"><span data-stu-id="3768f-121">Name</span></span>            | <span data-ttu-id="3768f-122">Typ</span><span class="sxs-lookup"><span data-stu-id="3768f-122">Type</span></span>     | <span data-ttu-id="3768f-123">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3768f-123">Required</span></span> | <span data-ttu-id="3768f-124">Popis</span><span class="sxs-lookup"><span data-stu-id="3768f-124">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="3768f-125">**id zákazníka**</span><span class="sxs-lookup"><span data-stu-id="3768f-125">**customer-id**</span></span> | <span data-ttu-id="3768f-126">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-126">string</span></span>   | <span data-ttu-id="3768f-127">Yes</span><span class="sxs-lookup"><span data-stu-id="3768f-127">Yes</span></span>      | <span data-ttu-id="3768f-128">Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3768f-128">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="3768f-129">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="3768f-129">Request headers</span></span>

<span data-ttu-id="3768f-130">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3768f-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3768f-131">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="3768f-131">Request body</span></span>

<span data-ttu-id="3768f-132">Tato tabulka popisuje vlastnosti [TransferEntity](transfer-entity-resources.md) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="3768f-132">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="3768f-133">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="3768f-133">Property</span></span>              | <span data-ttu-id="3768f-134">Typ</span><span class="sxs-lookup"><span data-stu-id="3768f-134">Type</span></span>          | <span data-ttu-id="3768f-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3768f-135">Required</span></span>  | <span data-ttu-id="3768f-136">Popis</span><span class="sxs-lookup"><span data-stu-id="3768f-136">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="3768f-137">id</span><span class="sxs-lookup"><span data-stu-id="3768f-137">id</span></span>                    | <span data-ttu-id="3768f-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-138">string</span></span>        | <span data-ttu-id="3768f-139">No</span><span class="sxs-lookup"><span data-stu-id="3768f-139">No</span></span>    | <span data-ttu-id="3768f-140">Identifikátor transferEntity zadaný po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-140">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="3768f-141">čas vytvoření</span><span class="sxs-lookup"><span data-stu-id="3768f-141">createdTime</span></span>           | <span data-ttu-id="3768f-142">DateTime</span><span class="sxs-lookup"><span data-stu-id="3768f-142">DateTime</span></span>      | <span data-ttu-id="3768f-143">No</span><span class="sxs-lookup"><span data-stu-id="3768f-143">No</span></span>    | <span data-ttu-id="3768f-144">Datum vytvoření transferEntity ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="3768f-144">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="3768f-145">Použije se při úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-145">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="3768f-146">lastModifiedTime</span><span class="sxs-lookup"><span data-stu-id="3768f-146">lastModifiedTime</span></span>      | <span data-ttu-id="3768f-147">DateTime</span><span class="sxs-lookup"><span data-stu-id="3768f-147">DateTime</span></span>      | <span data-ttu-id="3768f-148">No</span><span class="sxs-lookup"><span data-stu-id="3768f-148">No</span></span>    | <span data-ttu-id="3768f-149">Datum poslední aktualizace transferEntity ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="3768f-149">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="3768f-150">Použije se při úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-150">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="3768f-151">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="3768f-151">lastModifiedUser</span></span>      | <span data-ttu-id="3768f-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-152">string</span></span>        | <span data-ttu-id="3768f-153">No</span><span class="sxs-lookup"><span data-stu-id="3768f-153">No</span></span>    | <span data-ttu-id="3768f-154">Uživatel, který naposledy aktualizoval transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-154">The user who last updated the transferEntity.</span></span> <span data-ttu-id="3768f-155">Použije se při úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-155">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="3768f-156">customerName</span><span class="sxs-lookup"><span data-stu-id="3768f-156">customerName</span></span>          | <span data-ttu-id="3768f-157">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-157">string</span></span>        | <span data-ttu-id="3768f-158">No</span><span class="sxs-lookup"><span data-stu-id="3768f-158">No</span></span>    | <span data-ttu-id="3768f-159">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="3768f-159">Optional.</span></span> <span data-ttu-id="3768f-160">Jméno zákazníka, jehož předplatná se převádějí.</span><span class="sxs-lookup"><span data-stu-id="3768f-160">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="3768f-161">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="3768f-161">customerTenantId</span></span>      | <span data-ttu-id="3768f-162">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-162">string</span></span>        | <span data-ttu-id="3768f-163">No</span><span class="sxs-lookup"><span data-stu-id="3768f-163">No</span></span>    | <span data-ttu-id="3768f-164">Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3768f-164">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="3768f-165">Použije se při úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-165">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="3768f-166">partnertenantid</span><span class="sxs-lookup"><span data-stu-id="3768f-166">partnertenantid</span></span>       | <span data-ttu-id="3768f-167">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-167">string</span></span>        | <span data-ttu-id="3768f-168">No</span><span class="sxs-lookup"><span data-stu-id="3768f-168">No</span></span>    | <span data-ttu-id="3768f-169">Identifikátor GUID naformátovaný jako partner-ID, který identifikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="3768f-169">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="3768f-170">sourcePartnerName</span><span class="sxs-lookup"><span data-stu-id="3768f-170">sourcePartnerName</span></span>     | <span data-ttu-id="3768f-171">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-171">string</span></span>        | <span data-ttu-id="3768f-172">No</span><span class="sxs-lookup"><span data-stu-id="3768f-172">No</span></span>    | <span data-ttu-id="3768f-173">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="3768f-173">Optional.</span></span> <span data-ttu-id="3768f-174">Název organizace partnera, která iniciuje převod.</span><span class="sxs-lookup"><span data-stu-id="3768f-174">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="3768f-175">sourcePartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="3768f-175">sourcePartnerTenantId</span></span> | <span data-ttu-id="3768f-176">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-176">string</span></span>        | <span data-ttu-id="3768f-177">Yes</span><span class="sxs-lookup"><span data-stu-id="3768f-177">Yes</span></span>   | <span data-ttu-id="3768f-178">Identifikátor GUID naformátovaný jako partner-ID, který identifikuje partnera, který zahájí převod.</span><span class="sxs-lookup"><span data-stu-id="3768f-178">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="3768f-179">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="3768f-179">targetPartnerName</span></span>     | <span data-ttu-id="3768f-180">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-180">string</span></span>        | <span data-ttu-id="3768f-181">No</span><span class="sxs-lookup"><span data-stu-id="3768f-181">No</span></span>    | <span data-ttu-id="3768f-182">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="3768f-182">Optional.</span></span> <span data-ttu-id="3768f-183">Název organizace partnera, na kterou se převod cílí.</span><span class="sxs-lookup"><span data-stu-id="3768f-183">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="3768f-184">targetPartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="3768f-184">targetPartnerTenantId</span></span> | <span data-ttu-id="3768f-185">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-185">string</span></span>        | <span data-ttu-id="3768f-186">Yes</span><span class="sxs-lookup"><span data-stu-id="3768f-186">Yes</span></span>   | <span data-ttu-id="3768f-187">Identifikátor GUID naformátovaný jako partner-ID, který identifikuje partnera, na kterého se přenos cílí.</span><span class="sxs-lookup"><span data-stu-id="3768f-187">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="3768f-188">položky řádku</span><span class="sxs-lookup"><span data-stu-id="3768f-188">lineItems</span></span>             | <span data-ttu-id="3768f-189">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="3768f-189">Array of objects</span></span> | <span data-ttu-id="3768f-190">Yes</span><span class="sxs-lookup"><span data-stu-id="3768f-190">Yes</span></span>| <span data-ttu-id="3768f-191">Pole prostředků [TransferLineItem.](transfer-entity-resources.md#transferlineitem)</span><span class="sxs-lookup"><span data-stu-id="3768f-191">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="3768f-192">status</span><span class="sxs-lookup"><span data-stu-id="3768f-192">status</span></span>                | <span data-ttu-id="3768f-193">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-193">string</span></span>        | <span data-ttu-id="3768f-194">No</span><span class="sxs-lookup"><span data-stu-id="3768f-194">No</span></span>    | <span data-ttu-id="3768f-195">Stav transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-195">The status of the transferEntity.</span></span> <span data-ttu-id="3768f-196">Možné hodnoty jsou Aktivní (je možné je odstranit nebo odeslat) a Dokončeno (už je hotové).</span><span class="sxs-lookup"><span data-stu-id="3768f-196">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="3768f-197">Použije se při úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-197">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="3768f-198">Tato tabulka popisuje vlastnosti [TransferLineItem](transfer-entity-resources.md#transferlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="3768f-198">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="3768f-199">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="3768f-199">Property</span></span>       |            <span data-ttu-id="3768f-200">Typ</span><span class="sxs-lookup"><span data-stu-id="3768f-200">Type</span></span>             | <span data-ttu-id="3768f-201">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3768f-201">Required</span></span> | <span data-ttu-id="3768f-202">Popis</span><span class="sxs-lookup"><span data-stu-id="3768f-202">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3768f-203">id</span><span class="sxs-lookup"><span data-stu-id="3768f-203">id</span></span>                   | <span data-ttu-id="3768f-204">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-204">string</span></span>                     | <span data-ttu-id="3768f-205">No</span><span class="sxs-lookup"><span data-stu-id="3768f-205">No</span></span>       | <span data-ttu-id="3768f-206">Jedinečný identifikátor položky řádku přenosu.</span><span class="sxs-lookup"><span data-stu-id="3768f-206">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="3768f-207">Použije se při úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-207">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="3768f-208">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="3768f-208">subscriptionId</span></span>       | <span data-ttu-id="3768f-209">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-209">string</span></span>                     | <span data-ttu-id="3768f-210">Yes</span><span class="sxs-lookup"><span data-stu-id="3768f-210">Yes</span></span>      | <span data-ttu-id="3768f-211">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="3768f-211">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="3768f-212">quantity</span><span class="sxs-lookup"><span data-stu-id="3768f-212">quantity</span></span>             | <span data-ttu-id="3768f-213">int</span><span class="sxs-lookup"><span data-stu-id="3768f-213">int</span></span>                        | <span data-ttu-id="3768f-214">No</span><span class="sxs-lookup"><span data-stu-id="3768f-214">No</span></span>       | <span data-ttu-id="3768f-215">Počet licencí nebo instancí</span><span class="sxs-lookup"><span data-stu-id="3768f-215">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="3768f-216">billingCycle</span><span class="sxs-lookup"><span data-stu-id="3768f-216">billingCycle</span></span>         | <span data-ttu-id="3768f-217">Objekt</span><span class="sxs-lookup"><span data-stu-id="3768f-217">Object</span></span>                     | <span data-ttu-id="3768f-218">No</span><span class="sxs-lookup"><span data-stu-id="3768f-218">No</span></span>       | <span data-ttu-id="3768f-219">Typ fakturačního cyklu nastavený pro aktuální období</span><span class="sxs-lookup"><span data-stu-id="3768f-219">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="3768f-220">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="3768f-220">friendlyName</span></span>         | <span data-ttu-id="3768f-221">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-221">string</span></span>                     | <span data-ttu-id="3768f-222">No</span><span class="sxs-lookup"><span data-stu-id="3768f-222">No</span></span>       | <span data-ttu-id="3768f-223">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="3768f-223">Optional.</span></span> <span data-ttu-id="3768f-224">Popisný název položky definované partnerem, který pomáhá jednoznačně rozpoznat.</span><span class="sxs-lookup"><span data-stu-id="3768f-224">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="3768f-225">id partneraZáznam</span><span class="sxs-lookup"><span data-stu-id="3768f-225">partnerIdOnRecord</span></span>    | <span data-ttu-id="3768f-226">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-226">string</span></span>                     | <span data-ttu-id="3768f-227">No</span><span class="sxs-lookup"><span data-stu-id="3768f-227">No</span></span>       | <span data-ttu-id="3768f-228">ID partnera v záznamu (ID MPN) při nákupu, ke které dojde při přijetí převodu.</span><span class="sxs-lookup"><span data-stu-id="3768f-228">PartnerId on Record (MPN ID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="3768f-229">ID nabídky</span><span class="sxs-lookup"><span data-stu-id="3768f-229">offerId</span></span>              | <span data-ttu-id="3768f-230">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-230">string</span></span>                     | <span data-ttu-id="3768f-231">No</span><span class="sxs-lookup"><span data-stu-id="3768f-231">No</span></span>       | <span data-ttu-id="3768f-232">Identifikátor nabídky.</span><span class="sxs-lookup"><span data-stu-id="3768f-232">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="3768f-233">addonItems</span><span class="sxs-lookup"><span data-stu-id="3768f-233">addonItems</span></span>           | <span data-ttu-id="3768f-234">Seznam objektů **TransferLineItem**</span><span class="sxs-lookup"><span data-stu-id="3768f-234">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="3768f-235">No</span><span class="sxs-lookup"><span data-stu-id="3768f-235">No</span></span> | <span data-ttu-id="3768f-236">Kolekce řádových položek transferEntity pro doplňky, které se přenesou spolu se základním předplatným, které se převádí.</span><span class="sxs-lookup"><span data-stu-id="3768f-236">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="3768f-237">Použije se při úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-237">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="3768f-238">chyba přenosu</span><span class="sxs-lookup"><span data-stu-id="3768f-238">transferError</span></span>        | <span data-ttu-id="3768f-239">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-239">string</span></span>                     | <span data-ttu-id="3768f-240">No</span><span class="sxs-lookup"><span data-stu-id="3768f-240">No</span></span>       | <span data-ttu-id="3768f-241">Použije se po přijetí transferEntity, pokud dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="3768f-241">Applied after transferEntity is accepted if there is an error.</span></span>                                        |
| <span data-ttu-id="3768f-242">status</span><span class="sxs-lookup"><span data-stu-id="3768f-242">status</span></span>               | <span data-ttu-id="3768f-243">řetězec</span><span class="sxs-lookup"><span data-stu-id="3768f-243">string</span></span>                     | <span data-ttu-id="3768f-244">No</span><span class="sxs-lookup"><span data-stu-id="3768f-244">No</span></span>       | <span data-ttu-id="3768f-245">Stav položky řádku v transferEntity.</span><span class="sxs-lookup"><span data-stu-id="3768f-245">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="3768f-246">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="3768f-246">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="3768f-247">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3768f-247">REST response</span></span>

<span data-ttu-id="3768f-248">V případě úspěchu tato metoda vrátí vyplněný prostředek [TransferEnity](transfer-entity-resources.md) v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="3768f-248">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3768f-249">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="3768f-249">Response success and error codes</span></span>

<span data-ttu-id="3768f-250">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="3768f-250">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3768f-251">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="3768f-251">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3768f-252">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3768f-252">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3768f-253">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="3768f-253">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
