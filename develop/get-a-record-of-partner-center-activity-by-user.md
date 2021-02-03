---
title: Získání záznamu o aktivitě Partnerského centra
description: Jak načíst záznam o operacích, jak ho provede partnerský uživatel nebo aplikace, v časovém intervalu.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f37eae8bb96c1c1e7008e8c566b085e25d8807d
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766928"
---
# <a name="get-a-record-of-partner-center-activity"></a><span data-ttu-id="a8845-103">Získání záznamu o aktivitě Partnerského centra</span><span class="sxs-lookup"><span data-stu-id="a8845-103">Get a record of Partner Center activity</span></span>

<span data-ttu-id="a8845-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="a8845-104">**Applies To**</span></span>

- <span data-ttu-id="a8845-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="a8845-105">Partner Center</span></span>
- <span data-ttu-id="a8845-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="a8845-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a8845-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a8845-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a8845-108">Tento článek popisuje, jak načíst záznam o operacích, které provedl partnerský uživatel nebo aplikace v časovém intervalu.</span><span class="sxs-lookup"><span data-stu-id="a8845-108">This article describes how to retrieve a record of operations that was performed by a partner user or application over a period of time.</span></span>

<span data-ttu-id="a8845-109">Pomocí tohoto rozhraní API můžete načíst záznamy auditu za posledních 30 dní od aktuálního data nebo pro rozsah dat zadaný zahrnutím počátečního data a/nebo koncového data.</span><span class="sxs-lookup"><span data-stu-id="a8845-109">Use this API to retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="a8845-110">Upozorňujeme ale, že z důvodů výkonu je dostupnost dat protokolu aktivit omezená na předchozí 90 dní.</span><span class="sxs-lookup"><span data-stu-id="a8845-110">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="a8845-111">Žádosti s počátečním datem větším než 90 dní před aktuálním datem obdrží výjimku špatné žádosti (kód chyby: 400) a příslušnou zprávu.</span><span class="sxs-lookup"><span data-stu-id="a8845-111">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8845-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a8845-112">Prerequisites</span></span>

- <span data-ttu-id="a8845-113">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a8845-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a8845-114">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="a8845-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a8845-115">C\#</span><span class="sxs-lookup"><span data-stu-id="a8845-115">C\#</span></span>

<span data-ttu-id="a8845-116">Pokud chcete načíst záznam o operacích partnerského centra, nejdřív navažte rozsah kalendářních dat pro záznamy, které chcete načíst.</span><span class="sxs-lookup"><span data-stu-id="a8845-116">To retrieve a record of Partner Center operations, first establish the date range for the records you want to retrieve.</span></span> <span data-ttu-id="a8845-117">Následující příklad kódu používá pouze počáteční datum, ale můžete také zahrnout koncové datum.</span><span class="sxs-lookup"><span data-stu-id="a8845-117">The following code example only uses a start date, but you can also include an end date.</span></span> <span data-ttu-id="a8845-118">Další informace najdete v tématu metoda [**dotazu**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) .</span><span class="sxs-lookup"><span data-stu-id="a8845-118">For more information, see the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) method.</span></span> <span data-ttu-id="a8845-119">Dále vytvořte potřebné proměnné pro typ filtru, který chcete použít, a přiřaďte příslušné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a8845-119">Next, create the variables you need for the type of filter you want to apply, and assign the appropriate values.</span></span> <span data-ttu-id="a8845-120">Chcete-li například filtrovat podle podřetězce názvu společnosti, vytvořte proměnnou pro uložení podřetězce.</span><span class="sxs-lookup"><span data-stu-id="a8845-120">For example, to filter by company name substring, create a variable to hold the substring.</span></span> <span data-ttu-id="a8845-121">Pokud chcete filtrovat podle ID zákazníka, vytvořte proměnnou pro uchování ID.</span><span class="sxs-lookup"><span data-stu-id="a8845-121">To filter by customer ID, create a variable to hold the ID.</span></span>

<span data-ttu-id="a8845-122">V následujícím příkladu je k dispozici vzorový kód, který bude filtrovat podle podřetězce názvu společnosti, ID zákazníka nebo typu prostředku.</span><span class="sxs-lookup"><span data-stu-id="a8845-122">In the following example, sample code is provided to filter by a company name substring, customer ID, or resource type.</span></span> <span data-ttu-id="a8845-123">Vyberte jednu z nich a přidejte komentář k ostatním.</span><span class="sxs-lookup"><span data-stu-id="a8845-123">Choose one and comment out the others.</span></span> <span data-ttu-id="a8845-124">V každém případě je nejprve vytvořena instance objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) s použitím jeho výchozího [**konstruktoru**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) pro vytvoření filtru.</span><span class="sxs-lookup"><span data-stu-id="a8845-124">In each case, you first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object using its default [**constructor**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) to create the filter.</span></span> <span data-ttu-id="a8845-125">Budete muset předat řetězec, který obsahuje pole, které chcete vyhledat, a příslušný operátor, jak je znázorněno.</span><span class="sxs-lookup"><span data-stu-id="a8845-125">You'll need to pass a string that contains the field to search, and the appropriate operator to apply, as shown.</span></span> <span data-ttu-id="a8845-126">Je také nutné zadat řetězec, podle kterého se má filtrovat.</span><span class="sxs-lookup"><span data-stu-id="a8845-126">You also must provide the string to filter by.</span></span>

<span data-ttu-id="a8845-127">Dále pomocí vlastnosti [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) Získejte rozhraní pro audit operací záznamů a zavolejte [**dotaz**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) nebo metodu [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) pro spuštění filtru a získejte kolekci [**AuditRecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) , která představuje první stránku výsledku.</span><span class="sxs-lookup"><span data-stu-id="a8845-127">Next, use the [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) property to get an interface to audit record operations, and call the [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) method to execute the filter and get the collection of [**AuditRecord's**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) that represent the first page of the result.</span></span> <span data-ttu-id="a8845-128">Předat metodu počáteční datum, volitelné koncové datum nepoužitelné v tomto příkladu a objekt [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , který představuje dotaz na entitu.</span><span class="sxs-lookup"><span data-stu-id="a8845-128">Pass the method the start date, an optional end date not used in the example here, and an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object that represents a query on an entity.</span></span> <span data-ttu-id="a8845-129">Objekt IQuery se vytvoří předáním filtru vytvořeného výše do [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metody [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .</span><span class="sxs-lookup"><span data-stu-id="a8845-129">The IQuery object is created by passing the filter created above to the [**QueryFactory's**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method.</span></span>

<span data-ttu-id="a8845-130">Jakmile máte počáteční stránku položek, použijte metodu [**Enumerator. AuditRecords. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) k vytvoření enumerátoru, který můžete použít k iteraci na zbývajících stránkách.</span><span class="sxs-lookup"><span data-stu-id="a8845-130">Once you have the initial page of items, use the [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) method to create an enumerator that you can use to iterate through the remaining pages.</span></span>

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

<span data-ttu-id="a8845-131">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a8845-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a8845-132">**Projekt**: sada SDK pro partnerských Center – **Složka** s ukázkami: auditování</span><span class="sxs-lookup"><span data-stu-id="a8845-132">**Project**: Partner Center SDK Samples **Folder**: Auditing</span></span>

## <a name="rest-request"></a><span data-ttu-id="a8845-133">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="a8845-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a8845-134">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="a8845-134">Request syntax</span></span>

| <span data-ttu-id="a8845-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="a8845-135">Method</span></span>  | <span data-ttu-id="a8845-136">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a8845-136">Request URI</span></span>                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a8845-137">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="a8845-137">**GET**</span></span> | <span data-ttu-id="a8845-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {STARTDATE} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a8845-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1</span></span>                                                                                                     |
| <span data-ttu-id="a8845-139">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="a8845-139">**GET**</span></span> | <span data-ttu-id="a8845-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {startDate} &EndDate = {ENDDATE} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a8845-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1</span></span>                                                                                   |
| <span data-ttu-id="a8845-141">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="a8845-141">**GET**</span></span> | <span data-ttu-id="a8845-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {startDate} &EndDate = {endDate} &Filter = {"Field": "CompanyName"; "value": "{searchSubstring}"; "operator": "substring"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a8845-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1</span></span> |
| <span data-ttu-id="a8845-143">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="a8845-143">**GET**</span></span> | <span data-ttu-id="a8845-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {startDate} &EndDate = {endDate} &Filter = {"Field": "CustomerID"; "value": "{CustomerID}"; "operator": "Equals"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a8845-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1</span></span>          |
| <span data-ttu-id="a8845-145">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="a8845-145">**GET**</span></span> | <span data-ttu-id="a8845-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {startDate} &EndDate = {endDate} &Filter = {"Field": "ResourceType"; "value": "{ResourceType}", "operator": "Equals"} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a8845-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="a8845-147">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a8845-147">URI parameter</span></span>

<span data-ttu-id="a8845-148">Při vytváření žádosti použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="a8845-148">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="a8845-149">Název</span><span class="sxs-lookup"><span data-stu-id="a8845-149">Name</span></span>      | <span data-ttu-id="a8845-150">Typ</span><span class="sxs-lookup"><span data-stu-id="a8845-150">Type</span></span>   | <span data-ttu-id="a8845-151">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a8845-151">Required</span></span> | <span data-ttu-id="a8845-152">Popis</span><span class="sxs-lookup"><span data-stu-id="a8845-152">Description</span></span>                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a8845-153">startDate</span><span class="sxs-lookup"><span data-stu-id="a8845-153">startDate</span></span> | <span data-ttu-id="a8845-154">date</span><span class="sxs-lookup"><span data-stu-id="a8845-154">date</span></span>   | <span data-ttu-id="a8845-155">No</span><span class="sxs-lookup"><span data-stu-id="a8845-155">No</span></span>       | <span data-ttu-id="a8845-156">Počáteční datum ve formátu rrrr-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="a8845-156">The start date in yyyy-mm-dd format.</span></span> <span data-ttu-id="a8845-157">Pokud není k dispozici žádný, bude sada výsledků Standard nastavena na 30 dní před datem požadavku.</span><span class="sxs-lookup"><span data-stu-id="a8845-157">If none is provided, the result set will default to 30 days prior to the request date.</span></span> <span data-ttu-id="a8845-158">Tento parametr je nepovinný, pokud je zadán filtr.</span><span class="sxs-lookup"><span data-stu-id="a8845-158">This parameter is optional when a filter is supplied.</span></span>                                          |
| <span data-ttu-id="a8845-159">endDate</span><span class="sxs-lookup"><span data-stu-id="a8845-159">endDate</span></span>   | <span data-ttu-id="a8845-160">date</span><span class="sxs-lookup"><span data-stu-id="a8845-160">date</span></span>   | <span data-ttu-id="a8845-161">No</span><span class="sxs-lookup"><span data-stu-id="a8845-161">No</span></span>       | <span data-ttu-id="a8845-162">Koncové datum ve formátu rrrr-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="a8845-162">The end date in yyyy-mm-dd format.</span></span> <span data-ttu-id="a8845-163">Tento parametr je nepovinný, pokud je zadán filtr.</span><span class="sxs-lookup"><span data-stu-id="a8845-163">This parameter is optional when a filter is supplied.</span></span> <span data-ttu-id="a8845-164">Když je koncové datum vynecháno nebo je nastaveno na hodnotu null, vrátí požadavek maximální okno nebo použije dnešní den jako koncové datum, podle toho, co je menší.</span><span class="sxs-lookup"><span data-stu-id="a8845-164">When the end date is omitted or set to null, the request returns the max window or uses today as the end date, whichever is less.</span></span> |
| <span data-ttu-id="a8845-165">filter</span><span class="sxs-lookup"><span data-stu-id="a8845-165">filter</span></span>    | <span data-ttu-id="a8845-166">řetězec</span><span class="sxs-lookup"><span data-stu-id="a8845-166">string</span></span> | <span data-ttu-id="a8845-167">No</span><span class="sxs-lookup"><span data-stu-id="a8845-167">No</span></span>       | <span data-ttu-id="a8845-168">Filtr, který se má použít</span><span class="sxs-lookup"><span data-stu-id="a8845-168">The filter to apply.</span></span> <span data-ttu-id="a8845-169">Tento parametr musí být kódovaný řetězec.</span><span class="sxs-lookup"><span data-stu-id="a8845-169">This parameter must be an encoded string.</span></span> <span data-ttu-id="a8845-170">Tento parametr je nepovinný, pokud jsou dodány počáteční datum nebo koncové datum.</span><span class="sxs-lookup"><span data-stu-id="a8845-170">This parameter is optional when the start date or end date are supplied.</span></span>                                                                                              |

### <a name="filter-syntax"></a><span data-ttu-id="a8845-171">Syntaxe filtru</span><span class="sxs-lookup"><span data-stu-id="a8845-171">Filter syntax</span></span>
<span data-ttu-id="a8845-172">Parametr Filter je nutné vytvořit jako řadu párů klíč-hodnota oddělené čárkami.</span><span class="sxs-lookup"><span data-stu-id="a8845-172">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="a8845-173">Každý klíč a hodnota musí být jednotlivě kotované a oddělené dvojtečkou.</span><span class="sxs-lookup"><span data-stu-id="a8845-173">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="a8845-174">Celý filtr musí být kódovaný.</span><span class="sxs-lookup"><span data-stu-id="a8845-174">The entire filter must be encoded.</span></span>

<span data-ttu-id="a8845-175">Nekódovaný příklad vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="a8845-175">An unencoded example looks like this:</span></span>

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

<span data-ttu-id="a8845-176">Následující tabulka popisuje požadované páry klíč-hodnota:</span><span class="sxs-lookup"><span data-stu-id="a8845-176">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="a8845-177">Klíč</span><span class="sxs-lookup"><span data-stu-id="a8845-177">Key</span></span>                 | <span data-ttu-id="a8845-178">Hodnota</span><span class="sxs-lookup"><span data-stu-id="a8845-178">Value</span></span>                             |
|:--------------------|:----------------------------------|
| <span data-ttu-id="a8845-179">Pole</span><span class="sxs-lookup"><span data-stu-id="a8845-179">Field</span></span>               | <span data-ttu-id="a8845-180">Pole, které se má filtrovat</span><span class="sxs-lookup"><span data-stu-id="a8845-180">The field to filter.</span></span> <span data-ttu-id="a8845-181">Podporované hodnoty najdete v [syntaxi žádosti](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span><span class="sxs-lookup"><span data-stu-id="a8845-181">The supported values can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>                                         |
| <span data-ttu-id="a8845-182">Hodnota</span><span class="sxs-lookup"><span data-stu-id="a8845-182">Value</span></span>               | <span data-ttu-id="a8845-183">Hodnota, podle které se má filtrovat</span><span class="sxs-lookup"><span data-stu-id="a8845-183">The value to filter by.</span></span> <span data-ttu-id="a8845-184">Případ hodnoty je ignorován.</span><span class="sxs-lookup"><span data-stu-id="a8845-184">The case of the value is ignored.</span></span> <span data-ttu-id="a8845-185">Následující parametry hodnot jsou podporovány, jak je znázorněno v [syntaxi žádosti](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span><span class="sxs-lookup"><span data-stu-id="a8845-185">The following value parameters are supported as shown in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request):</span></span><br/><br/>                                                                <span data-ttu-id="a8845-186">*searchSubstring* – nahraďte názvem společnosti.</span><span class="sxs-lookup"><span data-stu-id="a8845-186">*searchSubstring* - Replace with the name of the company.</span></span> <span data-ttu-id="a8845-187">Můžete zadat podřetězec, který bude odpovídat části názvu společnosti (například, `bri` bude odpovídat `Fabrikam, Inc` ).</span><span class="sxs-lookup"><span data-stu-id="a8845-187">You can enter a substring to match part of the company name (for example, `bri` will match `Fabrikam, Inc`).</span></span><br/><span data-ttu-id="a8845-188">**Příklad:**`"Value":"bri"`</span><span class="sxs-lookup"><span data-stu-id="a8845-188">**Example:** `"Value":"bri"`</span></span><br/><br/>                                                                <span data-ttu-id="a8845-189">*customerId* -nahraďte řetězcem FORMÁTOVANÉho identifikátorem GUID, který představuje identifikátor zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a8845-189">*customerId* - Replace with a GUID formatted string that represents the customer identifier.</span></span><br/><span data-ttu-id="a8845-190">**Příklad:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span><span class="sxs-lookup"><span data-stu-id="a8845-190">**Example:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`</span></span><br/><br/>                                                                                        <span data-ttu-id="a8845-191">*ResourceType* – nahraďte typem prostředku, pro který chcete načíst záznamy auditu (například předplatné).</span><span class="sxs-lookup"><span data-stu-id="a8845-191">*resourceType* - Replace with the type of resource for which to retrieve audit records (for example, Subscription).</span></span> <span data-ttu-id="a8845-192">Typy prostředků, které jsou k dispozici, jsou definovány v typu [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span><span class="sxs-lookup"><span data-stu-id="a8845-192">The available resource types are defined in [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).</span></span><br/><span data-ttu-id="a8845-193">**Příklad:**`"Value":"Subscription"`</span><span class="sxs-lookup"><span data-stu-id="a8845-193">**Example:** `"Value":"Subscription"`</span></span>                                 |
| <span data-ttu-id="a8845-194">Operátor</span><span class="sxs-lookup"><span data-stu-id="a8845-194">Operator</span></span>          | <span data-ttu-id="a8845-195">Operátor, který se má použít</span><span class="sxs-lookup"><span data-stu-id="a8845-195">The operator to apply.</span></span> <span data-ttu-id="a8845-196">Podporované operátory lze nalézt v [syntaxi žádosti](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span><span class="sxs-lookup"><span data-stu-id="a8845-196">The supported operators can be found in [Request syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="a8845-197">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a8845-197">Request headers</span></span>

- <span data-ttu-id="a8845-198">Další informace najdete v [části Center – záhlaví REST](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="a8845-198">See [Parter Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="a8845-199">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a8845-199">Request body</span></span>

<span data-ttu-id="a8845-200">Žádné</span><span class="sxs-lookup"><span data-stu-id="a8845-200">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a8845-201">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a8845-201">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a8845-202">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a8845-202">REST response</span></span>

<span data-ttu-id="a8845-203">V případě úspěchu tato metoda vrátí sadu aktivit, které odpovídají filtrům.</span><span class="sxs-lookup"><span data-stu-id="a8845-203">If successful, this method returns a set of activities that meet the filters.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a8845-204">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="a8845-204">Response success and error codes</span></span>

<span data-ttu-id="a8845-205">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a8845-205">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a8845-206">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="a8845-206">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a8845-207">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a8845-207">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a8845-208">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a8845-208">Response example</span></span>

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