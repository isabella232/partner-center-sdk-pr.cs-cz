---
title: Získání záznamu o aktivitě Partnerského centra
description: Jak načíst záznam o operacích provedených uživatelem partnera nebo aplikací v časovém období
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aec933d4b681d99080619505792bde56bdd25580
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873967"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="43f91-103">Získání záznamu o aktivitě Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="43f91-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="43f91-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="43f91-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="43f91-105">Tento článek popisuje, jak načíst záznam operací provedených partnerským uživatelem nebo aplikací v průběhu časového období.</span><span class="sxs-lookup"><span data-stu-id="43f91-105">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="43f91-106">Pomocí tohoto rozhraní API můžete načíst záznamy auditu za posledních 30 dnů od aktuálního data nebo pro rozsah dat určený zahrnutím počátečního a/nebo koncového data.</span><span class="sxs-lookup"><span data-stu-id="43f91-106">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="43f91-107">Upozorňujeme ale, že z důvodů výkonu je dostupnost dat protokolu aktivit omezená na předchozích 90 dnů.</span><span class="sxs-lookup"><span data-stu-id="43f91-107">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="43f91-108">Požadavky s počátečním datem delším než 90 dní před aktuálním datem obdrží výjimku chybný požadavek (kód chyby: 400) a příslušnou zprávu.</span><span class="sxs-lookup"><span data-stu-id="43f91-108">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43f91-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="43f91-109">Prerequisites</span></span>

- <span data-ttu-id="43f91-110">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="43f91-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="43f91-111">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="43f91-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="43f91-112">C\#</span><span class="sxs-lookup"><span data-stu-id="43f91-112">C\#</span></span>

<span data-ttu-id="43f91-113">Pokud chcete načíst záznam Partnerské centrum operací, nejprve vytvořte rozsah dat pro záznamy, které chcete načíst.</span><span class="sxs-lookup"><span data-stu-id="43f91-113">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="43f91-114">Následující příklad kódu používá pouze počáteční datum, ale můžete také zahrnout koncové datum.</span><span class="sxs-lookup"><span data-stu-id="43f91-114">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="43f91-115">Další informace najdete v tématu [**Metoda**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) dotazu.</span><span class="sxs-lookup"><span data-stu-id="43f91-115">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="43f91-116">Dále vytvořte proměnné, které potřebujete pro typ filtru, který chcete použít, a přiřaďte příslušné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="43f91-116">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="43f91-117">Pokud chcete například filtrovat podle podřetězce názvu společnosti, vytvořte proměnnou pro podřetězec.</span><span class="sxs-lookup"><span data-stu-id="43f91-117">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="43f91-118">Pokud chcete filtrovat podle ID zákazníka, vytvořte proměnnou pro jeho id.</span><span class="sxs-lookup"><span data-stu-id="43f91-118">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="43f91-119">V následujícím příkladu je k dispozici vzorový kód pro filtrování podle podřetězce názvu společnosti, ID zákazníka nebo typu prostředku.</span><span class="sxs-lookup"><span data-stu-id="43f91-119">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="43f91-120">Vyberte jednu a okomentování ostatních.</span><span class="sxs-lookup"><span data-stu-id="43f91-120">Choose one and comment out the others.</span></span> <span data-ttu-id="43f91-121">V každém případě nejprve vytvoříte instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) pomocí [**výchozího**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) konstruktoru pro vytvoření filtru.</span><span class="sxs-lookup"><span data-stu-id="43f91-121">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="43f91-122">Budete muset předat řetězec, který obsahuje pole k hledání, a odpovídající operátor, který se má použít, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="43f91-122">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="43f91-123">Musíte také zadat řetězec, podle který chcete filtrovat.</span><span class="sxs-lookup"><span data-stu-id="43f91-123">You also must provide the string to filter by.</span></span>

<span data-ttu-id="43f91-124">Dále pomocí vlastnosti [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) získejte rozhraní pro operace se záznamy auditu a voláním metody [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) nebo [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) spusťte filtr a získejte kolekci [**záznamů AuditRecord,**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) které představují první stránku výsledku.</span><span class="sxs-lookup"><span data-stu-id="43f91-124">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="43f91-125">Metodě předejte počáteční datum, volitelné koncové datum, které zde není použité, a objekt [**IQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) který představuje dotaz na entitu.</span><span class="sxs-lookup"><span data-stu-id="43f91-125">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="43f91-126">Objekt IQuery se vytvoří předáním výše vytvořeného filtru do metody [**BuildSimpleQuery objektu**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) [**QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="43f91-126">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="43f91-127">Jakmile máte počáteční stránku položek, pomocí metody [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) vytvořte enumerátor, který můžete použít k iteraci zbývajícími stránkami.</span><span class="sxs-lookup"><span data-stu-id="43f91-127">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (for example "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource.
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }

    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

<span data-ttu-id="43f91-128">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="43f91-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="43f91-129">**Project:** SDK pro Partnerské centrum **ukázky:** Auditování</span><span class="sxs-lookup"><span data-stu-id="43f91-129">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="43f91-130">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="43f91-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="43f91-131">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="43f91-131">Request syntax</span></span>

| <span data-ttu-id="43f91-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="43f91-132">Method</span></span>  | <span data-ttu-id="43f91-133">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="43f91-133">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="43f91-134">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="43f91-134">**GET**</span></span> | <span data-ttu-id="43f91-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="43f91-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="43f91-136">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="43f91-136">**GET**</span></span> | <span data-ttu-id="43f91-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="43f91-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="43f91-138">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="43f91-138">**GET**</span></span> | <span data-ttu-id="43f91-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="43f91-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="43f91-140">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="43f91-140">**GET**</span></span> | <span data-ttu-id="43f91-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="43f91-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="43f91-142">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="43f91-142">**GET**</span></span> | <span data-ttu-id="43f91-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="43f91-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="43f91-144">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="43f91-144">URI parameter</span></span>

<span data-ttu-id="43f91-145">Při vytváření požadavku použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="43f91-145">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="43f91-146">Název</span><span class="sxs-lookup"><span data-stu-id="43f91-146">Name</span></span>      | <span data-ttu-id="43f91-147">Typ</span><span class="sxs-lookup"><span data-stu-id="43f91-147">Type</span></span>   | <span data-ttu-id="43f91-148">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="43f91-148">Required</span></span> | <span data-ttu-id="43f91-149">Popis</span><span class="sxs-lookup"><span data-stu-id="43f91-149">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="43f91-150">Datum_spuštění</span><span class="sxs-lookup"><span data-stu-id="43f91-150">startDate</span></span> | <span data-ttu-id="43f91-151">date</span><span class="sxs-lookup"><span data-stu-id="43f91-151">date</span></span>   | <span data-ttu-id="43f91-152">No</span><span class="sxs-lookup"><span data-stu-id="43f91-152">No</span></span>       | <span data-ttu-id="43f91-153">Počáteční datum ve formátu rrrr-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="43f91-153">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="43f91-154">Pokud se žádná možnost zadá, sada výsledků dotazu se nastaví na 30 dní před datem žádosti.</span><span class="sxs-lookup"><span data-stu-id="43f91-154">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="43f91-155">Tento parametr je volitelný, pokud je zadán filtr.</span><span class="sxs-lookup"><span data-stu-id="43f91-155">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="43f91-156">Enddate</span><span class="sxs-lookup"><span data-stu-id="43f91-156">endDate</span></span>   | <span data-ttu-id="43f91-157">date</span><span class="sxs-lookup"><span data-stu-id="43f91-157">date</span></span>   | <span data-ttu-id="43f91-158">No</span><span class="sxs-lookup"><span data-stu-id="43f91-158">No</span></span>       | <span data-ttu-id="43f91-159">Koncové datum ve formátu rrrr-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="43f91-159">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="43f91-160">Tento parametr je volitelný, pokud je zadán filtr.</span><span class="sxs-lookup"><span data-stu-id="43f91-160">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="43f91-161">Pokud je koncové datum vynecháno nebo nastaveno na hodnotu null, požadavek vrátí maximální okno nebo jako koncové datum použije ještě dnes , podle toho, která hodnota je menší.</span><span class="sxs-lookup"><span data-stu-id="43f91-161">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="43f91-162">filter</span><span class="sxs-lookup"><span data-stu-id="43f91-162">filter</span></span>    | <span data-ttu-id="43f91-163">řetězec</span><span class="sxs-lookup"><span data-stu-id="43f91-163">string</span></span> | <span data-ttu-id="43f91-164">No</span><span class="sxs-lookup"><span data-stu-id="43f91-164">No</span></span>       | <span data-ttu-id="43f91-165">Filtr, který se má použít.</span><span class="sxs-lookup"><span data-stu-id="43f91-165">The filter to apply.</span></span> <span data-ttu-id="43f91-166">Tento parametr musí být zakódovaný řetězec.</span><span class="sxs-lookup"><span data-stu-id="43f91-166">This parameter must be an encoded string.</span></span> <span data-ttu-id="43f91-167">Tento parametr je volitelný, pokud je zadáno počáteční nebo koncové datum.</span><span class="sxs-lookup"><span data-stu-id="43f91-167">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="43f91-168">Syntaxe filtru</span><span class="sxs-lookup"><span data-stu-id="43f91-168">Filter syntax</span></span>
<span data-ttu-id="43f91-169">Parametr filtru musíte vytvořit jako řadu párů klíč-hodnota oddělených čárkami.</span><span class="sxs-lookup"><span data-stu-id="43f91-169">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="43f91-170">Každý klíč a hodnota musí být jednotlivě uvozené a oddělené dvojtečkou.</span><span class="sxs-lookup"><span data-stu-id="43f91-170">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="43f91-171">Celý filtr musí být kódovaný.</span><span class="sxs-lookup"><span data-stu-id="43f91-171">The entire filter must be encoded.</span></span>

<span data-ttu-id="43f91-172">Nekódovaný příklad vypadá jako tento:</span><span class="sxs-lookup"><span data-stu-id="43f91-172">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="43f91-173">Následující tabulka popisuje požadované páry klíč-hodnota:</span><span class="sxs-lookup"><span data-stu-id="43f91-173">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="43f91-174">Klíč</span><span class="sxs-lookup"><span data-stu-id="43f91-174">Key</span></span>                 | <span data-ttu-id="43f91-175">Hodnota</span><span class="sxs-lookup"><span data-stu-id="43f91-175">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="43f91-176">Pole</span><span class="sxs-lookup"><span data-stu-id="43f91-176">Field</span></span>               | <span data-ttu-id="43f91-177">Pole, které chcete filtrovat.</span><span class="sxs-lookup"><span data-stu-id="43f91-177">The field to filter.</span></span> <span data-ttu-id="43f91-178">Podporované hodnoty najdete v [syntaxi požadavku](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span><span class="sxs-lookup"><span data-stu-id="43f91-178">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="43f91-179">Hodnota</span><span class="sxs-lookup"><span data-stu-id="43f91-179">Value</span></span>               | <span data-ttu-id="43f91-180">Hodnota, podle které se má filtrovat.</span><span class="sxs-lookup"><span data-stu-id="43f91-180">The value to filter by.</span></span> <span data-ttu-id="43f91-181">Případ hodnoty se ignoruje.</span><span class="sxs-lookup"><span data-stu-id="43f91-181">The case of the value is ignored.</span></span> <span data-ttu-id="43f91-182">Podporují se následující parametry hodnot, jak je znázorněno v [syntaxi požadavku](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span><span class="sxs-lookup"><span data-stu-id="43f91-182">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="43f91-183">*searchSubstring* – nahraďte názvem společnosti.</span><span class="sxs-lookup"><span data-stu-id="43f91-183">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="43f91-184">Můžete zadat podřetězec, který odpovídá části názvu společnosti (například bude `bri` odpovídat `Fabrikam, Inc` ).</span><span class="sxs-lookup"><span data-stu-id="43f91-184">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="43f91-185">**Příklad:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="43f91-185">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="43f91-186">*customerId* – nahraďte řetězcem ve formátu GUID, který představuje identifikátor zákazníka.</span><span class="sxs-lookup"><span data-stu-id="43f91-186">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="43f91-187">**Příklad:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="43f91-187">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="43f91-188">*resourceType* – nahraďte typem prostředku, pro který se mají načíst záznamy auditu (například Předplatné).</span><span class="sxs-lookup"><span data-stu-id="43f91-188">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="43f91-189">Dostupné typy prostředků jsou definované v [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span><span class="sxs-lookup"><span data-stu-id="43f91-189">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="43f91-190">**Příklad:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="43f91-190">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="43f91-191">Operátor</span><span class="sxs-lookup"><span data-stu-id="43f91-191">Operator</span></span>          | <span data-ttu-id="43f91-192">Operátor, který se má použít.</span><span class="sxs-lookup"><span data-stu-id="43f91-192">The operator to apply.</span></span> <span data-ttu-id="43f91-193">Podporované operátory najdete v [syntaxi požadavku](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span><span class="sxs-lookup"><span data-stu-id="43f91-193">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="43f91-194">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="43f91-194">Request headers</span></span>

- <span data-ttu-id="43f91-195">Další informace najdete v tématu [Hlavičky REST](headers.md)centra součástí.</span><span class="sxs-lookup"><span data-stu-id="43f91-195">For more information, see [Parter Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="43f91-196">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="43f91-196">Request body</span></span>

<span data-ttu-id="43f91-197">Žádné</span><span class="sxs-lookup"><span data-stu-id="43f91-197">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="43f91-198">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="43f91-198">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="43f91-199">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="43f91-199">REST response</span></span>

<span data-ttu-id="43f91-200">V případě úspěchu tato metoda vrátí sadu aktivit, které splňují filtry.</span><span class="sxs-lookup"><span data-stu-id="43f91-200">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="43f91-201">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="43f91-201">Response success and error codes</span></span>

<span data-ttu-id="43f91-202">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="43f91-202">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="43f91-203">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="43f91-203">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="43f91-204">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="43f91-204">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="43f91-205">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="43f91-205">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```