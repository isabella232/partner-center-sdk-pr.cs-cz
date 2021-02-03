---
title: Získání záznamů o využití Azure zákazníkem
description: Rozhraní API využití Azure můžete použít k získání záznamů o využití předplatného Azure zákazníka za zadané časové období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcdeb51b04039fd05b923150c85119385c0537e0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766865"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="edf91-103">Získání záznamů o využití Azure zákazníkem</span><span class="sxs-lookup"><span data-stu-id="edf91-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="edf91-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="edf91-104">**Applies to:**</span></span>

- <span data-ttu-id="edf91-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="edf91-105">Partner Center</span></span>
- <span data-ttu-id="edf91-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="edf91-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="edf91-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="edf91-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="edf91-108">Záznamy o využití předplatného Azure zákazníka můžete získat v zadaném časovém období pomocí rozhraní API využití Azure.</span><span class="sxs-lookup"><span data-stu-id="edf91-108">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edf91-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="edf91-109">Prerequisites</span></span>

- <span data-ttu-id="edf91-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="edf91-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="edf91-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="edf91-111">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="edf91-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="edf91-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="edf91-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="edf91-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="edf91-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="edf91-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="edf91-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="edf91-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="edf91-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="edf91-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="edf91-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="edf91-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="edf91-118">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="edf91-118">A subscription identifier.</span></span>

<span data-ttu-id="edf91-119">Toto rozhraní API vrátí denní a hodinovou spotřebu nehodnoceného času pro libovolný časový rozsah.</span><span class="sxs-lookup"><span data-stu-id="edf91-119">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="edf91-120">*Toto rozhraní API se ale pro plány Azure nepodporuje*.</span><span class="sxs-lookup"><span data-stu-id="edf91-120">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="edf91-121">Pokud máte plán Azure, podívejte se na články [získat faktury za neúčtované řádky spotřeby](get-invoice-unbilled-consumption-lineitems.md) a místo toho [Získejte položky na řádcích spotřeby faktury](get-invoice-billed-consumption-lineitems.md) .</span><span class="sxs-lookup"><span data-stu-id="edf91-121">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="edf91-122">Tyto články popisují, jak získat hodnocenou spotřebu na denní úrovni pro každý měřič na jeden prostředek.</span><span class="sxs-lookup"><span data-stu-id="edf91-122">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="edf91-123">Tato spotřeba je rovnocenná datům denních zrn poskytovaných rozhraním API využití Azure.</span><span class="sxs-lookup"><span data-stu-id="edf91-123">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="edf91-124">K načtení fakturovaných dat o využití budete muset použít identifikátor faktury.</span><span class="sxs-lookup"><span data-stu-id="edf91-124">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="edf91-125">Nebo můžete použít aktuální a předchozí období k získání nefakturovaných odhadů využití.</span><span class="sxs-lookup"><span data-stu-id="edf91-125">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="edf91-126">*Pro prostředky předplatného Azure Plan se v současné době nepodporují data s hodinovou zrnitou a libovolné filtry rozsahu kalendářních dat*.</span><span class="sxs-lookup"><span data-stu-id="edf91-126">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="edf91-127">Rozhraní API využití Azure</span><span class="sxs-lookup"><span data-stu-id="edf91-127">Azure utilization API</span></span>

<span data-ttu-id="edf91-128">Toto rozhraní API využití Azure poskytuje přístup k záznamům o využití za časové období, které představuje, kdy bylo využití oznámeno v systému fakturace.</span><span class="sxs-lookup"><span data-stu-id="edf91-128">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="edf91-129">Poskytuje přístup ke stejným datům využití, která se používají k vytvoření a výpočtu souboru pro odsouhlasení.</span><span class="sxs-lookup"><span data-stu-id="edf91-129">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="edf91-130">Nemá ale znalosti o logice souborů odsouhlasení systému fakturace.</span><span class="sxs-lookup"><span data-stu-id="edf91-130">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="edf91-131">Neočekává se, že souhrn výsledků souborů sloučení nebude odpovídat výsledku načtenému z tohoto rozhraní API přesně za stejné časové období.</span><span class="sxs-lookup"><span data-stu-id="edf91-131">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="edf91-132">Například fakturační systém má stejná data o využití a pro určení toho, co se účtuje v souboru pro odsouhlasení, aplikují pravidla pro pozdě.</span><span class="sxs-lookup"><span data-stu-id="edf91-132">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="edf91-133">Po uzavření fakturačního období bude veškeré využití až do konce dne, kdy se v souboru pro odsouhlasení zařadí fakturační období.</span><span class="sxs-lookup"><span data-stu-id="edf91-133">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="edf91-134">Jakékoli pozdní využití v rámci fakturačního období, které se nahlásí během 24 hodin od konce fakturačního období, se účtuje v dalším souboru pro odsouhlasení.</span><span class="sxs-lookup"><span data-stu-id="edf91-134">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="edf91-135">Pravidla pro pozdě, jak se partner účtuje, najdete v tématu [získání dat o spotřebě pro předplatné Azure](/previous-versions/azure/reference/mt219001(v=azure.100)).</span><span class="sxs-lookup"><span data-stu-id="edf91-135">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="edf91-136">Tato REST API jsou stránkovaná.</span><span class="sxs-lookup"><span data-stu-id="edf91-136">This REST API is paged.</span></span> <span data-ttu-id="edf91-137">Pokud je datová část odpovědi větší než jedna stránka, je nutné použít následující odkaz k získání další stránky záznamů o využití.</span><span class="sxs-lookup"><span data-stu-id="edf91-137">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

## <a name="c"></a><span data-ttu-id="edf91-138">C\#</span><span class="sxs-lookup"><span data-stu-id="edf91-138">C\#</span></span>

<span data-ttu-id="edf91-139">Získání záznamů o využití Azure:</span><span class="sxs-lookup"><span data-stu-id="edf91-139">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="edf91-140">Získejte ID zákazníka a ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="edf91-140">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="edf91-141">Voláním metody [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) vrátíte [**resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) , která obsahuje záznamy o využití.</span><span class="sxs-lookup"><span data-stu-id="edf91-141">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="edf91-142">Získejte enumerátor záznamů využití Azure pro procházení stránek využití.</span><span class="sxs-lookup"><span data-stu-id="edf91-142">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="edf91-143">Tento krok je povinný, protože kolekce prostředků je stránkovaná.</span><span class="sxs-lookup"><span data-stu-id="edf91-143">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="edf91-144">**Ukázka**: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="edf91-144">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="edf91-145">**Projekt**: ukázky sady SDK pro partnerských Center</span><span class="sxs-lookup"><span data-stu-id="edf91-145">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="edf91-146">**Třída**: GetAzureSubscriptionUtilization.cs</span><span class="sxs-lookup"><span data-stu-id="edf91-146">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a><span data-ttu-id="edf91-147">Java</span><span class="sxs-lookup"><span data-stu-id="edf91-147">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="edf91-148">Pokud chcete získat záznamy o využití Azure, musíte nejdřív potřebovat identifikátor zákazníka a identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="edf91-148">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="edf91-149">Potom zavolejte funkci **IAzureUtilizationCollection. Query** , která vrátí **zdrojovou** , která obsahuje záznamy o využití.</span><span class="sxs-lookup"><span data-stu-id="edf91-149">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="edf91-150">Vzhledem k tomu, že je kolekce prostředků stránkovaná, musíte získat enumerátor záznamů využití Azure pro procházení stránek využití.</span><span class="sxs-lookup"><span data-stu-id="edf91-150">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="edf91-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="edf91-151">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="edf91-152">Pokud chcete získat záznamy o využití Azure, musíte nejdřív potřebovat identifikátor zákazníka a identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="edf91-152">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="edf91-153">Pak zavolejte [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span><span class="sxs-lookup"><span data-stu-id="edf91-153">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="edf91-154">Tento příkaz vrátí všechny záznamy, které jsou k dispozici po určenou dobu.</span><span class="sxs-lookup"><span data-stu-id="edf91-154">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="edf91-155">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="edf91-155">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="edf91-156">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="edf91-156">Request syntax</span></span>

| <span data-ttu-id="edf91-157">Metoda</span><span class="sxs-lookup"><span data-stu-id="edf91-157">Method</span></span> | <span data-ttu-id="edf91-158">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="edf91-158">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="edf91-159">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="edf91-159">**GET**</span></span> | <span data-ttu-id="edf91-160">*{baseURL}*/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/utilizations/Azure? \_ čas spuštění = {start-time} &koncový \_ čas = {čas ukončení} &členitost = {členitost} &zobrazit \_ Podrobnosti = {true}</span><span class="sxs-lookup"><span data-stu-id="edf91-160">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="edf91-161">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="edf91-161">URI parameters</span></span>

<span data-ttu-id="edf91-162">K získání záznamů o využití použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="edf91-162">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="edf91-163">Název</span><span class="sxs-lookup"><span data-stu-id="edf91-163">Name</span></span> | <span data-ttu-id="edf91-164">Typ</span><span class="sxs-lookup"><span data-stu-id="edf91-164">Type</span></span> | <span data-ttu-id="edf91-165">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="edf91-165">Required</span></span> | <span data-ttu-id="edf91-166">Popis</span><span class="sxs-lookup"><span data-stu-id="edf91-166">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="edf91-167">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="edf91-167">customer-tenant-id</span></span> | <span data-ttu-id="edf91-168">řetězec</span><span class="sxs-lookup"><span data-stu-id="edf91-168">string</span></span> | <span data-ttu-id="edf91-169">Yes</span><span class="sxs-lookup"><span data-stu-id="edf91-169">Yes</span></span> | <span data-ttu-id="edf91-170">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="edf91-170">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="edf91-171">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="edf91-171">subscription-id</span></span> | <span data-ttu-id="edf91-172">řetězec</span><span class="sxs-lookup"><span data-stu-id="edf91-172">string</span></span> | <span data-ttu-id="edf91-173">Yes</span><span class="sxs-lookup"><span data-stu-id="edf91-173">Yes</span></span> | <span data-ttu-id="edf91-174">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="edf91-174">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="edf91-175">start_time</span><span class="sxs-lookup"><span data-stu-id="edf91-175">start_time</span></span> | <span data-ttu-id="edf91-176">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="edf91-176">string in UTC date-time offset format</span></span> | <span data-ttu-id="edf91-177">Yes</span><span class="sxs-lookup"><span data-stu-id="edf91-177">Yes</span></span> | <span data-ttu-id="edf91-178">Začátek časového rozsahu, který představuje, kdy bylo využití oznámeno v systému fakturace.</span><span class="sxs-lookup"><span data-stu-id="edf91-178">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="edf91-179">end_time</span><span class="sxs-lookup"><span data-stu-id="edf91-179">end_time</span></span> | <span data-ttu-id="edf91-180">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="edf91-180">string in UTC date-time offset format</span></span> | <span data-ttu-id="edf91-181">Yes</span><span class="sxs-lookup"><span data-stu-id="edf91-181">Yes</span></span> | <span data-ttu-id="edf91-182">Konec časového rozsahu, který představuje, kdy bylo využití oznámeno v systému fakturace.</span><span class="sxs-lookup"><span data-stu-id="edf91-182">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="edf91-183">členitosti</span><span class="sxs-lookup"><span data-stu-id="edf91-183">granularity</span></span> | <span data-ttu-id="edf91-184">řetězec</span><span class="sxs-lookup"><span data-stu-id="edf91-184">string</span></span> | <span data-ttu-id="edf91-185">No</span><span class="sxs-lookup"><span data-stu-id="edf91-185">No</span></span> | <span data-ttu-id="edf91-186">Definuje členitost agregací využití.</span><span class="sxs-lookup"><span data-stu-id="edf91-186">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="edf91-187">Dostupné možnosti jsou: `daily` (výchozí) a `hourly` .</span><span class="sxs-lookup"><span data-stu-id="edf91-187">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="edf91-188">show_details</span><span class="sxs-lookup"><span data-stu-id="edf91-188">show_details</span></span> | <span data-ttu-id="edf91-189">boolean</span><span class="sxs-lookup"><span data-stu-id="edf91-189">boolean</span></span> | <span data-ttu-id="edf91-190">No</span><span class="sxs-lookup"><span data-stu-id="edf91-190">No</span></span> | <span data-ttu-id="edf91-191">Určuje, jestli se mají získat podrobnosti o využití na úrovni instance.</span><span class="sxs-lookup"><span data-stu-id="edf91-191">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="edf91-192">Výchozí formát je `true`.</span><span class="sxs-lookup"><span data-stu-id="edf91-192">The default is `true`.</span></span> |
| <span data-ttu-id="edf91-193">size</span><span class="sxs-lookup"><span data-stu-id="edf91-193">size</span></span> | <span data-ttu-id="edf91-194">číslo</span><span class="sxs-lookup"><span data-stu-id="edf91-194">number</span></span> | <span data-ttu-id="edf91-195">No</span><span class="sxs-lookup"><span data-stu-id="edf91-195">No</span></span> | <span data-ttu-id="edf91-196">Určuje počet agregací vrácených jedním voláním rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="edf91-196">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="edf91-197">Výchozí hodnota je 1 000.</span><span class="sxs-lookup"><span data-stu-id="edf91-197">The default is 1000.</span></span> <span data-ttu-id="edf91-198">Maximální hodnota je 1000.</span><span class="sxs-lookup"><span data-stu-id="edf91-198">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="edf91-199">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="edf91-199">Request headers</span></span>

<span data-ttu-id="edf91-200">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="edf91-200">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="edf91-201">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="edf91-201">Request body</span></span>

<span data-ttu-id="edf91-202">Žádné</span><span class="sxs-lookup"><span data-stu-id="edf91-202">None</span></span>

### <a name="request-example"></a><span data-ttu-id="edf91-203">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="edf91-203">Request example</span></span>

<span data-ttu-id="edf91-204">Následující příklad žádosti vytvoří výsledek podobný tomu, co se soubor pro odsouhlasení zobrazí po dobu 7/2-8/1.</span><span class="sxs-lookup"><span data-stu-id="edf91-204">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="edf91-205">Tyto výsledky se nemusí přesně shodovat (podrobnosti najdete v části [rozhraní API pro využití Azure](#azure-utilization-api) ).</span><span class="sxs-lookup"><span data-stu-id="edf91-205">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="edf91-206">Tento příklad žádosti vrátí data o využití uvedená v systému fakturace od 7/2 do 12:00 (UTC) a 8/2 ve 12:00 (UTC).</span><span class="sxs-lookup"><span data-stu-id="edf91-206">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="edf91-207">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="edf91-207">REST response</span></span>

<span data-ttu-id="edf91-208">V případě úspěchu tato metoda vrátí kolekci prostředků [záznamu využití Azure](azure-utilization-record-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="edf91-208">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="edf91-209">Pokud data o využití Azure ještě nejsou připravené v závislém systému, vrátí tato metoda stavový kód HTTP 204 s hlavičkou Retry-After.</span><span class="sxs-lookup"><span data-stu-id="edf91-209">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="edf91-210">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="edf91-210">Response success and error codes</span></span>

<span data-ttu-id="edf91-211">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="edf91-211">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="edf91-212">Pomocí nástroje pro trasování sítě si přečtěte stavový kód HTTP, [typ kódu chyby](error-codes.md)a další parametry.</span><span class="sxs-lookup"><span data-stu-id="edf91-212">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="edf91-213">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="edf91-213">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
