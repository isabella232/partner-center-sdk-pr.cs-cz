---
title: Vytvořit přenos
description: Jak vytvořit přenos předplatných pro zákazníka.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766694"
---
# <a name="create-a-transfer"></a><span data-ttu-id="0c5ee-103">Vytvořit přenos</span><span class="sxs-lookup"><span data-stu-id="0c5ee-103">Create a transfer</span></span>

<span data-ttu-id="0c5ee-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="0c5ee-104">**Applies to:**</span></span>

- <span data-ttu-id="0c5ee-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0c5ee-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c5ee-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0c5ee-106">Prerequisites</span></span>

- <span data-ttu-id="0c5ee-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0c5ee-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0c5ee-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0c5ee-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0c5ee-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0c5ee-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0c5ee-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0c5ee-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0c5ee-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="0c5ee-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0c5ee-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0c5ee-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="0c5ee-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0c5ee-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0c5ee-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0c5ee-116">Request syntax</span></span>

| <span data-ttu-id="0c5ee-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="0c5ee-117">Method</span></span>   | <span data-ttu-id="0c5ee-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0c5ee-118">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0c5ee-119">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="0c5ee-119">**POST**</span></span> | <span data-ttu-id="0c5ee-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0c5ee-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="0c5ee-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0c5ee-121">URI parameter</span></span>

<span data-ttu-id="0c5ee-122">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="0c5ee-123">Název</span><span class="sxs-lookup"><span data-stu-id="0c5ee-123">Name</span></span>            | <span data-ttu-id="0c5ee-124">Typ</span><span class="sxs-lookup"><span data-stu-id="0c5ee-124">Type</span></span>     | <span data-ttu-id="0c5ee-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0c5ee-125">Required</span></span> | <span data-ttu-id="0c5ee-126">Popis</span><span class="sxs-lookup"><span data-stu-id="0c5ee-126">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="0c5ee-127">**ID zákazníka**</span><span class="sxs-lookup"><span data-stu-id="0c5ee-127">**customer-id**</span></span> | <span data-ttu-id="0c5ee-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-128">string</span></span>   | <span data-ttu-id="0c5ee-129">Yes</span><span class="sxs-lookup"><span data-stu-id="0c5ee-129">Yes</span></span>      | <span data-ttu-id="0c5ee-130">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-130">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="0c5ee-131">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0c5ee-131">Request headers</span></span>

<span data-ttu-id="0c5ee-132">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0c5ee-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0c5ee-133">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0c5ee-133">Request body</span></span>

<span data-ttu-id="0c5ee-134">Tato tabulka popisuje vlastnosti [TransferEntity](transfer-entity-resources.md) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-134">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="0c5ee-135">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="0c5ee-135">Property</span></span>              | <span data-ttu-id="0c5ee-136">Typ</span><span class="sxs-lookup"><span data-stu-id="0c5ee-136">Type</span></span>          | <span data-ttu-id="0c5ee-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0c5ee-137">Required</span></span>  | <span data-ttu-id="0c5ee-138">Popis</span><span class="sxs-lookup"><span data-stu-id="0c5ee-138">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="0c5ee-139">id</span><span class="sxs-lookup"><span data-stu-id="0c5ee-139">id</span></span>                    | <span data-ttu-id="0c5ee-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-140">string</span></span>        | <span data-ttu-id="0c5ee-141">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-141">No</span></span>    | <span data-ttu-id="0c5ee-142">TransferEntity identifikátor, který je poskytnut po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-142">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="0c5ee-143">createdTime</span><span class="sxs-lookup"><span data-stu-id="0c5ee-143">createdTime</span></span>           | <span data-ttu-id="0c5ee-144">DateTime</span><span class="sxs-lookup"><span data-stu-id="0c5ee-144">DateTime</span></span>      | <span data-ttu-id="0c5ee-145">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-145">No</span></span>    | <span data-ttu-id="0c5ee-146">Datum, kdy byl transferEntity vytvořen, ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-146">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="0c5ee-147">Použito po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-147">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="0c5ee-148">Časposledníúpravy</span><span class="sxs-lookup"><span data-stu-id="0c5ee-148">lastModifiedTime</span></span>      | <span data-ttu-id="0c5ee-149">DateTime</span><span class="sxs-lookup"><span data-stu-id="0c5ee-149">DateTime</span></span>      | <span data-ttu-id="0c5ee-150">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-150">No</span></span>    | <span data-ttu-id="0c5ee-151">Datum poslední aktualizace transferEntity ve formátu data a času.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-151">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="0c5ee-152">Použito po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-152">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="0c5ee-153">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="0c5ee-153">lastModifiedUser</span></span>      | <span data-ttu-id="0c5ee-154">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-154">string</span></span>        | <span data-ttu-id="0c5ee-155">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-155">No</span></span>    | <span data-ttu-id="0c5ee-156">Uživatel, který transferEntity naposledy aktualizoval.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-156">The user who last updated the transferEntity.</span></span> <span data-ttu-id="0c5ee-157">Použito po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-157">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="0c5ee-158">customerName</span><span class="sxs-lookup"><span data-stu-id="0c5ee-158">customerName</span></span>          | <span data-ttu-id="0c5ee-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-159">string</span></span>        | <span data-ttu-id="0c5ee-160">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-160">No</span></span>    | <span data-ttu-id="0c5ee-161">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-161">Optional.</span></span> <span data-ttu-id="0c5ee-162">Jméno zákazníka, jehož odběry se přenáší.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-162">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="0c5ee-163">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="0c5ee-163">customerTenantId</span></span>      | <span data-ttu-id="0c5ee-164">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-164">string</span></span>        | <span data-ttu-id="0c5ee-165">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-165">No</span></span>    | <span data-ttu-id="0c5ee-166">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-166">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="0c5ee-167">Použito po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-167">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="0c5ee-168">partnertenantid</span><span class="sxs-lookup"><span data-stu-id="0c5ee-168">partnertenantid</span></span>       | <span data-ttu-id="0c5ee-169">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-169">string</span></span>        | <span data-ttu-id="0c5ee-170">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-170">No</span></span>    | <span data-ttu-id="0c5ee-171">ID partnera naformátovaného identifikátorem GUID, který identifikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-171">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="0c5ee-172">sourcePartnerName</span><span class="sxs-lookup"><span data-stu-id="0c5ee-172">sourcePartnerName</span></span>     | <span data-ttu-id="0c5ee-173">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-173">string</span></span>        | <span data-ttu-id="0c5ee-174">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-174">No</span></span>    | <span data-ttu-id="0c5ee-175">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-175">Optional.</span></span> <span data-ttu-id="0c5ee-176">Název organizace partnera, který iniciuje přenos.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-176">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="0c5ee-177">sourcePartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="0c5ee-177">sourcePartnerTenantId</span></span> | <span data-ttu-id="0c5ee-178">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-178">string</span></span>        | <span data-ttu-id="0c5ee-179">Yes</span><span class="sxs-lookup"><span data-stu-id="0c5ee-179">Yes</span></span>   | <span data-ttu-id="0c5ee-180">ID partnera naformátovaného identifikátorem GUID, který identifikuje partnera iniciující přenos.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-180">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="0c5ee-181">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="0c5ee-181">targetPartnerName</span></span>     | <span data-ttu-id="0c5ee-182">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-182">string</span></span>        | <span data-ttu-id="0c5ee-183">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-183">No</span></span>    | <span data-ttu-id="0c5ee-184">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-184">Optional.</span></span> <span data-ttu-id="0c5ee-185">Název organizace partnera, na kterou je přenos zaměřen.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-185">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="0c5ee-186">targetPartnerTenantId</span><span class="sxs-lookup"><span data-stu-id="0c5ee-186">targetPartnerTenantId</span></span> | <span data-ttu-id="0c5ee-187">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-187">string</span></span>        | <span data-ttu-id="0c5ee-188">Yes</span><span class="sxs-lookup"><span data-stu-id="0c5ee-188">Yes</span></span>   | <span data-ttu-id="0c5ee-189">ID partnera formátovaného identifikátorem GUID, který identifikuje partnera, kterému je směrován cíl přenosu.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-189">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="0c5ee-190">Položky řádku</span><span class="sxs-lookup"><span data-stu-id="0c5ee-190">lineItems</span></span>             | <span data-ttu-id="0c5ee-191">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="0c5ee-191">Array of objects</span></span> | <span data-ttu-id="0c5ee-192">Yes</span><span class="sxs-lookup"><span data-stu-id="0c5ee-192">Yes</span></span>| <span data-ttu-id="0c5ee-193">Pole prostředků [TransferLineItem](transfer-entity-resources.md#transferlineitem)</span><span class="sxs-lookup"><span data-stu-id="0c5ee-193">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="0c5ee-194">status</span><span class="sxs-lookup"><span data-stu-id="0c5ee-194">status</span></span>                | <span data-ttu-id="0c5ee-195">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-195">string</span></span>        | <span data-ttu-id="0c5ee-196">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-196">No</span></span>    | <span data-ttu-id="0c5ee-197">Stav transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-197">The status of the transferEntity.</span></span> <span data-ttu-id="0c5ee-198">Možné hodnoty jsou "aktivní" (lze je odstranit/odeslat) a "dokončeno" (již bylo dokončeno).</span><span class="sxs-lookup"><span data-stu-id="0c5ee-198">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="0c5ee-199">Použito po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-199">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="0c5ee-200">Tato tabulka popisuje vlastnosti [TransferLineItem](transfer-entity-resources.md#transferlineitem) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-200">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="0c5ee-201">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="0c5ee-201">Property</span></span>       |            <span data-ttu-id="0c5ee-202">Typ</span><span class="sxs-lookup"><span data-stu-id="0c5ee-202">Type</span></span>             | <span data-ttu-id="0c5ee-203">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0c5ee-203">Required</span></span> | <span data-ttu-id="0c5ee-204">Popis</span><span class="sxs-lookup"><span data-stu-id="0c5ee-204">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0c5ee-205">id</span><span class="sxs-lookup"><span data-stu-id="0c5ee-205">id</span></span>                   | <span data-ttu-id="0c5ee-206">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-206">string</span></span>                     | <span data-ttu-id="0c5ee-207">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-207">No</span></span>       | <span data-ttu-id="0c5ee-208">Jedinečný identifikátor pro položku na lince přenosu.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-208">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="0c5ee-209">Použito po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-209">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="0c5ee-210">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0c5ee-210">subscriptionId</span></span>       | <span data-ttu-id="0c5ee-211">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-211">string</span></span>                     | <span data-ttu-id="0c5ee-212">Yes</span><span class="sxs-lookup"><span data-stu-id="0c5ee-212">Yes</span></span>      | <span data-ttu-id="0c5ee-213">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-213">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="0c5ee-214">quantity</span><span class="sxs-lookup"><span data-stu-id="0c5ee-214">quantity</span></span>             | <span data-ttu-id="0c5ee-215">int</span><span class="sxs-lookup"><span data-stu-id="0c5ee-215">int</span></span>                        | <span data-ttu-id="0c5ee-216">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-216">No</span></span>       | <span data-ttu-id="0c5ee-217">Počet licencí nebo instancí.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-217">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="0c5ee-218">billingCycle</span><span class="sxs-lookup"><span data-stu-id="0c5ee-218">billingCycle</span></span>         | <span data-ttu-id="0c5ee-219">Objekt</span><span class="sxs-lookup"><span data-stu-id="0c5ee-219">Object</span></span>                     | <span data-ttu-id="0c5ee-220">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-220">No</span></span>       | <span data-ttu-id="0c5ee-221">Typ fakturačního cyklu nastaveného pro aktuální období.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-221">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="0c5ee-222">friendlyName</span><span class="sxs-lookup"><span data-stu-id="0c5ee-222">friendlyName</span></span>         | <span data-ttu-id="0c5ee-223">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-223">string</span></span>                     | <span data-ttu-id="0c5ee-224">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-224">No</span></span>       | <span data-ttu-id="0c5ee-225">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-225">Optional.</span></span> <span data-ttu-id="0c5ee-226">Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-226">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="0c5ee-227">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="0c5ee-227">partnerIdOnRecord</span></span>    | <span data-ttu-id="0c5ee-228">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-228">string</span></span>                     | <span data-ttu-id="0c5ee-229">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-229">No</span></span>       | <span data-ttu-id="0c5ee-230">PartnerId na záznamu (MPNID) při nákupu, který se stane při přijetí přenosu.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-230">PartnerId on Record (MPNID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="0c5ee-231">Hodnotami OfferId</span><span class="sxs-lookup"><span data-stu-id="0c5ee-231">offerId</span></span>              | <span data-ttu-id="0c5ee-232">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-232">string</span></span>                     | <span data-ttu-id="0c5ee-233">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-233">No</span></span>       | <span data-ttu-id="0c5ee-234">Identifikátor nabídky</span><span class="sxs-lookup"><span data-stu-id="0c5ee-234">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="0c5ee-235">addonItems</span><span class="sxs-lookup"><span data-stu-id="0c5ee-235">addonItems</span></span>           | <span data-ttu-id="0c5ee-236">Seznam objektů **TransferLineItem**</span><span class="sxs-lookup"><span data-stu-id="0c5ee-236">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="0c5ee-237">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-237">No</span></span> | <span data-ttu-id="0c5ee-238">Kolekce položek řádku transferEntity pro doplňky, které se přenesou spolu se základním předplatným, které se přenáší.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-238">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="0c5ee-239">Použito po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-239">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="0c5ee-240">transferError</span><span class="sxs-lookup"><span data-stu-id="0c5ee-240">transferError</span></span>        | <span data-ttu-id="0c5ee-241">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-241">string</span></span>                     | <span data-ttu-id="0c5ee-242">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-242">No</span></span>       | <span data-ttu-id="0c5ee-243">Používá se po přijetí transferEntity v případě chyby.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-243">Applied after transferEntity is accepted in case of an error.</span></span>                                        |
| <span data-ttu-id="0c5ee-244">status</span><span class="sxs-lookup"><span data-stu-id="0c5ee-244">status</span></span>               | <span data-ttu-id="0c5ee-245">řetězec</span><span class="sxs-lookup"><span data-stu-id="0c5ee-245">string</span></span>                     | <span data-ttu-id="0c5ee-246">No</span><span class="sxs-lookup"><span data-stu-id="0c5ee-246">No</span></span>       | <span data-ttu-id="0c5ee-247">Stav LineItem v transferEntity.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-247">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="0c5ee-248">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0c5ee-248">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0c5ee-249">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0c5ee-249">REST response</span></span>

<span data-ttu-id="0c5ee-250">V případě úspěchu tato metoda vrátí naplněný prostředek [TransferEnity](transfer-entity-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-250">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0c5ee-251">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0c5ee-251">Response success and error codes</span></span>

<span data-ttu-id="0c5ee-252">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-252">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0c5ee-253">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0c5ee-253">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0c5ee-254">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0c5ee-254">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0c5ee-255">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0c5ee-255">Response example</span></span>

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
