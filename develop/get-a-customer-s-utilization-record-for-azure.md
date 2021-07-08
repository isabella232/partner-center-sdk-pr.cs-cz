---
title: Získání záznamů o využití Azure zákazníkem
description: Rozhraní API využití Azure můžete použít k získání záznamů o využití předplatného Azure zákazníka za zadané časové období.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7024bc65976a9b43a62b66c529d271519181ab23
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874920"
---
# <a name="get-a-customers-utilization-records-for-azure"></a><span data-ttu-id="d76e1-103">Získání záznamů o využití Azure zákazníkem</span><span class="sxs-lookup"><span data-stu-id="d76e1-103">Get a customer's utilization records for Azure</span></span>

<span data-ttu-id="d76e1-104">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d76e1-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d76e1-105">Záznamy o využití předplatného Azure zákazníka můžete získat v zadaném časovém období pomocí rozhraní API využití Azure.</span><span class="sxs-lookup"><span data-stu-id="d76e1-105">You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d76e1-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d76e1-106">Prerequisites</span></span>

- <span data-ttu-id="d76e1-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d76e1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d76e1-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="d76e1-108">This scenario supports authentication with both standalone app and App+User credentials.</span></span>

- <span data-ttu-id="d76e1-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d76e1-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d76e1-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="d76e1-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d76e1-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="d76e1-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d76e1-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="d76e1-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d76e1-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="d76e1-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d76e1-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d76e1-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d76e1-115">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="d76e1-115">A subscription identifier.</span></span>

<span data-ttu-id="d76e1-116">Toto rozhraní API vrátí denní a hodinovou spotřebu nehodnoceného času pro libovolný časový rozsah.</span><span class="sxs-lookup"><span data-stu-id="d76e1-116">This API returns daily and hourly unrated consumption for an arbitrary time span.</span></span> <span data-ttu-id="d76e1-117">*Toto rozhraní API se ale pro plány Azure nepodporuje*.</span><span class="sxs-lookup"><span data-stu-id="d76e1-117">However, *this API isn't supported for Azure plans*.</span></span> <span data-ttu-id="d76e1-118">Pokud máte plán Azure, podívejte se na články [získat faktury za neúčtované řádky spotřeby](get-invoice-unbilled-consumption-lineitems.md) a místo toho [Získejte položky na řádcích spotřeby faktury](get-invoice-billed-consumption-lineitems.md) .</span><span class="sxs-lookup"><span data-stu-id="d76e1-118">If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead.</span></span> <span data-ttu-id="d76e1-119">Tyto články popisují, jak získat hodnocenou spotřebu na denní úrovni pro každý měřič na jeden prostředek.</span><span class="sxs-lookup"><span data-stu-id="d76e1-119">These articles describe how to get rated consumption at a daily level per meter per resource.</span></span> <span data-ttu-id="d76e1-120">Tato spotřeba je rovnocenná datům denních zrn poskytovaných rozhraním API využití Azure.</span><span class="sxs-lookup"><span data-stu-id="d76e1-120">This rate consumption is equivalent to the daily grain data provided by the Azure utilization API.</span></span> <span data-ttu-id="d76e1-121">K načtení fakturovaných dat o využití budete muset použít identifikátor faktury.</span><span class="sxs-lookup"><span data-stu-id="d76e1-121">You'll need to use the invoice identifier to retrieve billed usage data.</span></span> <span data-ttu-id="d76e1-122">Nebo můžete použít aktuální a předchozí období k získání nefakturovaných odhadů využití.</span><span class="sxs-lookup"><span data-stu-id="d76e1-122">Or, you can use current and previous periods to get unbilled usage estimates.</span></span> <span data-ttu-id="d76e1-123">*Pro prostředky předplatného Azure Plan se v současné době nepodporují data s hodinovou zrnitou a libovolné filtry rozsahu kalendářních dat*.</span><span class="sxs-lookup"><span data-stu-id="d76e1-123">*Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.</span></span>

## <a name="azure-utilization-api"></a><span data-ttu-id="d76e1-124">Rozhraní API využití Azure</span><span class="sxs-lookup"><span data-stu-id="d76e1-124">Azure utilization API</span></span>

<span data-ttu-id="d76e1-125">Toto rozhraní API využití Azure poskytuje přístup k záznamům o využití za časové období, které představuje, kdy bylo využití oznámeno v systému fakturace.</span><span class="sxs-lookup"><span data-stu-id="d76e1-125">This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system.</span></span> <span data-ttu-id="d76e1-126">Poskytuje přístup ke stejným datům využití, která se používají k vytvoření a výpočtu souboru pro odsouhlasení.</span><span class="sxs-lookup"><span data-stu-id="d76e1-126">It provides access to the same utilization data that is used to create and calculate the reconciliation file.</span></span> <span data-ttu-id="d76e1-127">Nemá ale znalosti o logice souborů odsouhlasení systému fakturace.</span><span class="sxs-lookup"><span data-stu-id="d76e1-127">However, it does not have knowledge of billing system reconciliation file logic.</span></span> <span data-ttu-id="d76e1-128">Neočekává se, že souhrn výsledků souborů sloučení nebude odpovídat výsledku načtenému z tohoto rozhraní API přesně za stejné časové období.</span><span class="sxs-lookup"><span data-stu-id="d76e1-128">You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.</span></span>

<span data-ttu-id="d76e1-129">Například fakturační systém má stejná data o využití a pro určení toho, co se účtuje v souboru pro odsouhlasení, aplikují pravidla pro pozdě.</span><span class="sxs-lookup"><span data-stu-id="d76e1-129">For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file.</span></span> <span data-ttu-id="d76e1-130">Po uzavření fakturačního období bude veškeré využití až do konce dne, kdy se v souboru pro odsouhlasení zařadí fakturační období.</span><span class="sxs-lookup"><span data-stu-id="d76e1-130">When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file.</span></span> <span data-ttu-id="d76e1-131">Jakékoli pozdní využití v rámci fakturačního období, které se nahlásí během 24 hodin od konce fakturačního období, se účtuje v dalším souboru pro odsouhlasení.</span><span class="sxs-lookup"><span data-stu-id="d76e1-131">Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file.</span></span> <span data-ttu-id="d76e1-132">Pravidla pro pozdě, jak se partner účtuje, najdete v tématu [získání dat o spotřebě pro předplatné Azure](/previous-versions/azure/reference/mt219001(v=azure.100)).</span><span class="sxs-lookup"><span data-stu-id="d76e1-132">For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](/previous-versions/azure/reference/mt219001(v=azure.100)).</span></span>

<span data-ttu-id="d76e1-133">Tato REST API jsou stránkovaná.</span><span class="sxs-lookup"><span data-stu-id="d76e1-133">This REST API is paged.</span></span> <span data-ttu-id="d76e1-134">Pokud je datová část odpovědi větší než jedna stránka, je nutné použít následující odkaz k získání další stránky záznamů o využití.</span><span class="sxs-lookup"><span data-stu-id="d76e1-134">If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.</span></span>

### <a name="scenario-partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a><span data-ttu-id="d76e1-135">Scénář: partner A převedl na partnera B vlastnictví fakturace předplatného Azure starší verze (145P).</span><span class="sxs-lookup"><span data-stu-id="d76e1-135">Scenario: Partner A has transferred billing ownership of Azure Legacy Subscription (145P) to Partner B</span></span>

<span data-ttu-id="d76e1-136">Pokud partner přenese vlastnictví fakturace předplatného Azure staršího na jiného partnera, když nový partner rozhraní API pro přenesené předplatné zavolá, musí použít ID předplatného Commerce (které se zobrazí v účtu partnerského centra) místo ID nároku Azure.</span><span class="sxs-lookup"><span data-stu-id="d76e1-136">If a partner transfers billing ownership of an Azure legacy subscription to another partner, when new the new partner calls Utilization API for transferred subscription they have to use Commerce Subscription ID (which shows up in their Partner Center account) rather than the Azure Entitlement ID.</span></span> <span data-ttu-id="d76e1-137">ID nároku Azure se zobrazuje pro partnera B jenom v případě, že se jedná o správce jménem (ADMINISTRATE) na Azure Portal zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d76e1-137">Azure Entitlement ID appears for Partner B only when they are Admin on behalf of (AOBO) to Customer's Azure portal.</span></span> 

<span data-ttu-id="d76e1-138">K úspěšnému volání rozhraní API pro přenesené předplatné vyžaduje, aby nový partner používal ID předplatného Commerce.</span><span class="sxs-lookup"><span data-stu-id="d76e1-138">To successfully call the Utilization API for the transferred subscription, the new partner needs to use the Commerce Subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="d76e1-139">C\#</span><span class="sxs-lookup"><span data-stu-id="d76e1-139">C\#</span></span>

<span data-ttu-id="d76e1-140">Získání záznamů o využití Azure:</span><span class="sxs-lookup"><span data-stu-id="d76e1-140">To obtain the Azure Utilization Records:</span></span>

1. <span data-ttu-id="d76e1-141">Získejte ID zákazníka a ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="d76e1-141">Get the customer ID and subscription ID.</span></span>

2. <span data-ttu-id="d76e1-142">Voláním metody [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) vrátíte [**resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) , která obsahuje záznamy o využití.</span><span class="sxs-lookup"><span data-stu-id="d76e1-142">Call the [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records.</span></span>

3. <span data-ttu-id="d76e1-143">Získejte enumerátor záznamů využití Azure pro procházení stránek využití.</span><span class="sxs-lookup"><span data-stu-id="d76e1-143">Obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span> <span data-ttu-id="d76e1-144">Tento krok je povinný, protože kolekce prostředků je stránkovaná.</span><span class="sxs-lookup"><span data-stu-id="d76e1-144">This step is required, because the resource collection is paged.</span></span>

- <span data-ttu-id="d76e1-145">**Ukázka**: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d76e1-145">**Sample**: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d76e1-146">**Project**: ukázky sady SDK pro partnerských Center</span><span class="sxs-lookup"><span data-stu-id="d76e1-146">**Project**: Partner Center SDK Samples</span></span>
- <span data-ttu-id="d76e1-147">**Třída**: GetAzureSubscriptionUtilization. cs</span><span class="sxs-lookup"><span data-stu-id="d76e1-147">**Class**: GetAzureSubscriptionUtilization.cs</span></span>

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

## <a name="java"></a><span data-ttu-id="d76e1-148">Java</span><span class="sxs-lookup"><span data-stu-id="d76e1-148">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="d76e1-149">Pokud chcete získat záznamy o využití Azure, musíte nejdřív potřebovat identifikátor zákazníka a identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="d76e1-149">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="d76e1-150">Potom zavolejte funkci **IAzureUtilizationCollection. Query** , která vrátí **zdrojovou** , která obsahuje záznamy o využití.</span><span class="sxs-lookup"><span data-stu-id="d76e1-150">You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records.</span></span> <span data-ttu-id="d76e1-151">Vzhledem k tomu, že je kolekce prostředků stránkovaná, musíte získat enumerátor záznamů využití Azure pro procházení stránek využití.</span><span class="sxs-lookup"><span data-stu-id="d76e1-151">Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="d76e1-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d76e1-152">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="d76e1-153">Pokud chcete získat záznamy o využití Azure, musíte nejdřív potřebovat identifikátor zákazníka a identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="d76e1-153">To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier.</span></span> <span data-ttu-id="d76e1-154">Pak zavolejte [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span><span class="sxs-lookup"><span data-stu-id="d76e1-154">You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md).</span></span> <span data-ttu-id="d76e1-155">Tento příkaz vrátí všechny záznamy, které jsou k dispozici po určenou dobu.</span><span class="sxs-lookup"><span data-stu-id="d76e1-155">This command will return all records available for the specified period of time.</span></span>

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a><span data-ttu-id="d76e1-156">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d76e1-156">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d76e1-157">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d76e1-157">Request syntax</span></span>

| <span data-ttu-id="d76e1-158">Metoda</span><span class="sxs-lookup"><span data-stu-id="d76e1-158">Method</span></span> | <span data-ttu-id="d76e1-159">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d76e1-159">Request URI</span></span> |
|------- | ----------- |
| <span data-ttu-id="d76e1-160">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="d76e1-160">**GET**</span></span> | <span data-ttu-id="d76e1-161">*{baseURL}*/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/utilizations/Azure? \_ čas spuštění = {start-time} &koncový \_ čas = {čas ukončení} &členitost = {členitost} &zobrazit \_ Podrobnosti = {true}</span><span class="sxs-lookup"><span data-stu-id="d76e1-161">*{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="d76e1-162">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="d76e1-162">URI parameters</span></span>

<span data-ttu-id="d76e1-163">K získání záznamů o využití použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="d76e1-163">Use the following path and query parameters to get the utilization records.</span></span>

| <span data-ttu-id="d76e1-164">Název</span><span class="sxs-lookup"><span data-stu-id="d76e1-164">Name</span></span> | <span data-ttu-id="d76e1-165">Typ</span><span class="sxs-lookup"><span data-stu-id="d76e1-165">Type</span></span> | <span data-ttu-id="d76e1-166">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d76e1-166">Required</span></span> | <span data-ttu-id="d76e1-167">Popis</span><span class="sxs-lookup"><span data-stu-id="d76e1-167">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="d76e1-168">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="d76e1-168">customer-tenant-id</span></span> | <span data-ttu-id="d76e1-169">řetězec</span><span class="sxs-lookup"><span data-stu-id="d76e1-169">string</span></span> | <span data-ttu-id="d76e1-170">Yes</span><span class="sxs-lookup"><span data-stu-id="d76e1-170">Yes</span></span> | <span data-ttu-id="d76e1-171">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d76e1-171">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="d76e1-172">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="d76e1-172">subscription-id</span></span> | <span data-ttu-id="d76e1-173">řetězec</span><span class="sxs-lookup"><span data-stu-id="d76e1-173">string</span></span> | <span data-ttu-id="d76e1-174">Yes</span><span class="sxs-lookup"><span data-stu-id="d76e1-174">Yes</span></span> | <span data-ttu-id="d76e1-175">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="d76e1-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="d76e1-176">start_time</span><span class="sxs-lookup"><span data-stu-id="d76e1-176">start_time</span></span> | <span data-ttu-id="d76e1-177">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="d76e1-177">string in UTC date-time offset format</span></span> | <span data-ttu-id="d76e1-178">Yes</span><span class="sxs-lookup"><span data-stu-id="d76e1-178">Yes</span></span> | <span data-ttu-id="d76e1-179">Začátek časového rozsahu, který představuje, kdy bylo využití oznámeno v systému fakturace.</span><span class="sxs-lookup"><span data-stu-id="d76e1-179">The start of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="d76e1-180">end_time</span><span class="sxs-lookup"><span data-stu-id="d76e1-180">end_time</span></span> | <span data-ttu-id="d76e1-181">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="d76e1-181">string in UTC date-time offset format</span></span> | <span data-ttu-id="d76e1-182">Yes</span><span class="sxs-lookup"><span data-stu-id="d76e1-182">Yes</span></span> | <span data-ttu-id="d76e1-183">Konec časového rozsahu, který představuje, kdy bylo využití oznámeno v systému fakturace.</span><span class="sxs-lookup"><span data-stu-id="d76e1-183">The end of the time range that represents when the utilization was reported in the billing system.</span></span> |
| <span data-ttu-id="d76e1-184">členitosti</span><span class="sxs-lookup"><span data-stu-id="d76e1-184">granularity</span></span> | <span data-ttu-id="d76e1-185">řetězec</span><span class="sxs-lookup"><span data-stu-id="d76e1-185">string</span></span> | <span data-ttu-id="d76e1-186">No</span><span class="sxs-lookup"><span data-stu-id="d76e1-186">No</span></span> | <span data-ttu-id="d76e1-187">Definuje členitost agregací využití.</span><span class="sxs-lookup"><span data-stu-id="d76e1-187">Defines the granularity of usage aggregations.</span></span> <span data-ttu-id="d76e1-188">Dostupné možnosti jsou: `daily` (výchozí) a `hourly` .</span><span class="sxs-lookup"><span data-stu-id="d76e1-188">Available options are: `daily` (default) and `hourly`.</span></span>
| <span data-ttu-id="d76e1-189">show_details</span><span class="sxs-lookup"><span data-stu-id="d76e1-189">show_details</span></span> | <span data-ttu-id="d76e1-190">boolean</span><span class="sxs-lookup"><span data-stu-id="d76e1-190">boolean</span></span> | <span data-ttu-id="d76e1-191">No</span><span class="sxs-lookup"><span data-stu-id="d76e1-191">No</span></span> | <span data-ttu-id="d76e1-192">Určuje, jestli se mají získat podrobnosti o využití na úrovni instance.</span><span class="sxs-lookup"><span data-stu-id="d76e1-192">Specifies whether to get the instance-level usage details.</span></span> <span data-ttu-id="d76e1-193">Výchozí formát je `true`.</span><span class="sxs-lookup"><span data-stu-id="d76e1-193">The default is `true`.</span></span> |
| <span data-ttu-id="d76e1-194">size</span><span class="sxs-lookup"><span data-stu-id="d76e1-194">size</span></span> | <span data-ttu-id="d76e1-195">číslo</span><span class="sxs-lookup"><span data-stu-id="d76e1-195">number</span></span> | <span data-ttu-id="d76e1-196">No</span><span class="sxs-lookup"><span data-stu-id="d76e1-196">No</span></span> | <span data-ttu-id="d76e1-197">Určuje počet agregací vrácených jedním voláním rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="d76e1-197">Specifies the number of aggregations returned by a single API call.</span></span> <span data-ttu-id="d76e1-198">Výchozí hodnota je 1 000.</span><span class="sxs-lookup"><span data-stu-id="d76e1-198">The default is 1000.</span></span> <span data-ttu-id="d76e1-199">Maximální hodnota je 1000.</span><span class="sxs-lookup"><span data-stu-id="d76e1-199">The max is 1000.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d76e1-200">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d76e1-200">Request headers</span></span>

<span data-ttu-id="d76e1-201">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d76e1-201">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d76e1-202">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d76e1-202">Request body</span></span>

<span data-ttu-id="d76e1-203">Žádná</span><span class="sxs-lookup"><span data-stu-id="d76e1-203">None</span></span>

### <a name="request-example"></a><span data-ttu-id="d76e1-204">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d76e1-204">Request example</span></span>

<span data-ttu-id="d76e1-205">Následující příklad žádosti vytvoří výsledek podobný tomu, co se soubor pro odsouhlasení zobrazí po dobu 7/2-8/1.</span><span class="sxs-lookup"><span data-stu-id="d76e1-205">The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1.</span></span> <span data-ttu-id="d76e1-206">Tyto výsledky se nemusí přesně shodovat (podrobnosti najdete v části [rozhraní API pro využití Azure](#azure-utilization-api) ).</span><span class="sxs-lookup"><span data-stu-id="d76e1-206">These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).</span></span>

<span data-ttu-id="d76e1-207">Tento příklad žádosti vrátí data o využití uvedená v systému fakturace od 7/2 do 12:00 (UTC) a 8/2 ve 12:00 (UTC).</span><span class="sxs-lookup"><span data-stu-id="d76e1-207">This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d76e1-208">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d76e1-208">REST response</span></span>

<span data-ttu-id="d76e1-209">V případě úspěchu tato metoda vrátí kolekci prostředků [záznamu využití Azure](azure-utilization-record-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="d76e1-209">If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body.</span></span> <span data-ttu-id="d76e1-210">Pokud data o využití Azure ještě nejsou připravené v závislém systému, vrátí tato metoda stavový kód HTTP 204 s hlavičkou Retry-After.</span><span class="sxs-lookup"><span data-stu-id="d76e1-210">If the Azure utilization data isn't yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d76e1-211">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d76e1-211">Response success and error codes</span></span>

<span data-ttu-id="d76e1-212">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d76e1-212">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d76e1-213">Pomocí nástroje pro trasování sítě si přečtěte stavový kód HTTP, [typ kódu chyby](error-codes.md)a další parametry.</span><span class="sxs-lookup"><span data-stu-id="d76e1-213">Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="d76e1-214">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d76e1-214">Response example</span></span>

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
