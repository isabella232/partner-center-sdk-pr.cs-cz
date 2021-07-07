---
title: Získání zákazníků nepřímého prodejce
description: Jak získat seznam zákazníků nepřímého prodejce
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e05248b16b803529258de806c25b117f3104ad2a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446322"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="afac7-103">Získání zákazníků nepřímého prodejce</span><span class="sxs-lookup"><span data-stu-id="afac7-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="afac7-104">Jak získat seznam zákazníků nepřímého prodejce</span><span class="sxs-lookup"><span data-stu-id="afac7-104">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afac7-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="afac7-105">Prerequisites</span></span>

- <span data-ttu-id="afac7-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="afac7-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="afac7-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="afac7-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="afac7-108">Identifikátor tenanta nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="afac7-108">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="afac7-109">C\#</span><span class="sxs-lookup"><span data-stu-id="afac7-109">C\#</span></span>

<span data-ttu-id="afac7-110">Pokud chcete získat kolekci zákazníků, kteří mají vztah se zadaným nepřímým prodejcem, vytvořte nejprve instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) a vytvořte filtr.</span><span class="sxs-lookup"><span data-stu-id="afac7-110">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="afac7-111">Budete muset předat člena výčtu [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) převedeného na řetězec a označit [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) jako typ operace filtru.</span><span class="sxs-lookup"><span data-stu-id="afac7-111">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="afac7-112">Budete také muset zadat identifikátor tenanta nepřímého prodejce, podle kterých chcete filtrovat.</span><span class="sxs-lookup"><span data-stu-id="afac7-112">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="afac7-113">Dále vytvořte instanci objektu [**iQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) který se má předat dotazu voláním metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) a předáním filtru.</span><span class="sxs-lookup"><span data-stu-id="afac7-113">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="afac7-114">BuildSimplyQuery je pouze jedním z typů dotazů podporovaných [**třídou QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="afac7-114">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="afac7-115">Pokud chcete spustit filtr a získat výsledek, nejprve pomocí [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) získejte rozhraní pro operace zákazníka partnera.</span><span class="sxs-lookup"><span data-stu-id="afac7-115">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="afac7-116">Potom zavolejte [**metodu Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="afac7-116">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="afac7-117">Pokud chcete vytvořit enumerátor pro procházení stránkovaných výsledků, získejte rozhraní factory enumerátoru kolekce zákazníků z vlastnosti [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) a potom zavolejte metodu [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), jak je znázorněno v následujícím kódu, a předejte proměnnou, která obsahuje kolekci zákazníků.</span><span class="sxs-lookup"><span data-stu-id="afac7-117">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

<span data-ttu-id="afac7-118">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md)**Project:** SDK pro Partnerské centrum Samples **Class**: GetCustomersOfIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="afac7-118">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="afac7-119">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="afac7-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="afac7-120">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="afac7-120">Request syntax</span></span>

| <span data-ttu-id="afac7-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="afac7-121">Method</span></span>  | <span data-ttu-id="afac7-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="afac7-122">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="afac7-123">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="afac7-123">**GET**</span></span> | <span data-ttu-id="afac7-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="afac7-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="afac7-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="afac7-125">URI parameter</span></span>

<span data-ttu-id="afac7-126">K vytvoření požadavku použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="afac7-126">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="afac7-127">Název</span><span class="sxs-lookup"><span data-stu-id="afac7-127">Name</span></span>   | <span data-ttu-id="afac7-128">Typ</span><span class="sxs-lookup"><span data-stu-id="afac7-128">Type</span></span>   | <span data-ttu-id="afac7-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="afac7-129">Required</span></span> | <span data-ttu-id="afac7-130">Popis</span><span class="sxs-lookup"><span data-stu-id="afac7-130">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="afac7-131">size</span><span class="sxs-lookup"><span data-stu-id="afac7-131">size</span></span>   | <span data-ttu-id="afac7-132">int</span><span class="sxs-lookup"><span data-stu-id="afac7-132">int</span></span>    | <span data-ttu-id="afac7-133">No</span><span class="sxs-lookup"><span data-stu-id="afac7-133">No</span></span>       | <span data-ttu-id="afac7-134">Počet výsledků, které se zobrazí najednou</span><span class="sxs-lookup"><span data-stu-id="afac7-134">The number of results to be displayed at one time.</span></span> <span data-ttu-id="afac7-135">Tento parametr je volitelný.</span><span class="sxs-lookup"><span data-stu-id="afac7-135">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="afac7-136">filter</span><span class="sxs-lookup"><span data-stu-id="afac7-136">filter</span></span> | <span data-ttu-id="afac7-137">filter</span><span class="sxs-lookup"><span data-stu-id="afac7-137">filter</span></span> | <span data-ttu-id="afac7-138">Yes</span><span class="sxs-lookup"><span data-stu-id="afac7-138">Yes</span></span>      | <span data-ttu-id="afac7-139">Dotaz, který filtruje hledání.</span><span class="sxs-lookup"><span data-stu-id="afac7-139">The query that filters the search.</span></span> <span data-ttu-id="afac7-140">Pokud chcete načíst zákazníky pro zadaného nepřímého prodejce, musíte vložit identifikátor nepřímého prodejce a zakódovat a zakódovat následující řetězec: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts \_ with"}.</span><span class="sxs-lookup"><span data-stu-id="afac7-140">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="afac7-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="afac7-141">Request headers</span></span>

<span data-ttu-id="afac7-142">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="afac7-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="afac7-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="afac7-143">Request body</span></span>

<span data-ttu-id="afac7-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="afac7-144">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="afac7-145">Příklad požadavku (zakódovaný)</span><span class="sxs-lookup"><span data-stu-id="afac7-145">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="afac7-146">Příklad požadavku (dekódované)</span><span class="sxs-lookup"><span data-stu-id="afac7-146">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="afac7-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="afac7-147">REST response</span></span>

<span data-ttu-id="afac7-148">V případě úspěchu bude text odpovědi obsahovat informace o zákaznících prodejce.</span><span class="sxs-lookup"><span data-stu-id="afac7-148">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="afac7-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="afac7-149">Response success and error codes</span></span>

<span data-ttu-id="afac7-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="afac7-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="afac7-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="afac7-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="afac7-152">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="afac7-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="afac7-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="afac7-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
