---
title: Získání zákazníků nepřímého prodejce
description: Jak získat seznam zákazníků nepřímého prodejce.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e4219f544a74bb3f34ec3aefe08cf18eed77fd42
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766980"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="94a93-103">Získání zákazníků nepřímého prodejce</span><span class="sxs-lookup"><span data-stu-id="94a93-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="94a93-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="94a93-104">**Applies To**</span></span>

- <span data-ttu-id="94a93-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="94a93-105">Partner Center</span></span>

<span data-ttu-id="94a93-106">Jak získat seznam zákazníků nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="94a93-106">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94a93-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="94a93-107">Prerequisites</span></span>

- <span data-ttu-id="94a93-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="94a93-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="94a93-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="94a93-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="94a93-110">Identifikátor tenanta nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="94a93-110">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="94a93-111">C\#</span><span class="sxs-lookup"><span data-stu-id="94a93-111">C\#</span></span>

<span data-ttu-id="94a93-112">Chcete-li získat kolekci zákazníků, kteří mají relaci se zadaným nepřímým prodejcem, nejprve vytvořte instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) pro vytvoření filtru.</span><span class="sxs-lookup"><span data-stu-id="94a93-112">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="94a93-113">Musíte předat člen výčtu [**CustomerSearchField. IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) převedený na řetězec a jako typ operace filtru označit [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) .</span><span class="sxs-lookup"><span data-stu-id="94a93-113">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="94a93-114">Budete taky muset zadat identifikátor tenanta nepřímého prodejce, podle kterého se má filtrovat.</span><span class="sxs-lookup"><span data-stu-id="94a93-114">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="94a93-115">Dále vytvořte instanci objektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , který se předá dotazu, voláním metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) a předáním filtru.</span><span class="sxs-lookup"><span data-stu-id="94a93-115">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="94a93-116">BuildSimplyQuery je pouze jeden z typů dotazu podporovaných třídou [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .</span><span class="sxs-lookup"><span data-stu-id="94a93-116">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="94a93-117">Pokud chcete spustit filtr a získat výsledek, nejdřív použijte [**IAggregatePartner. zákazníci**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby získali rozhraní pro zákaznické operace partnera.</span><span class="sxs-lookup"><span data-stu-id="94a93-117">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="94a93-118">Pak zavolejte [**dotaz**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo metodu [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .</span><span class="sxs-lookup"><span data-stu-id="94a93-118">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="94a93-119">Chcete-li vytvořit enumerátor pro procházení stránkovaných výsledků, Získejte rozhraní pro vytváření výčtu kolekce zákazníka od vlastnosti [**IAggregatePartner. enumerators. Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) a potom zavolejte metodu [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), jak je znázorněno v následujícím kódu, a předejte jí proměnnou, která obsahuje kolekci Customer.</span><span class="sxs-lookup"><span data-stu-id="94a93-119">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

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

<span data-ttu-id="94a93-120">**Ukázka**:**projekt** [aplikace testů konzoly](console-test-app.md): ukázkové **třídy** SDK pro partnerských Center: GetCustomersOfIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="94a93-120">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="94a93-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="94a93-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="94a93-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="94a93-122">Request syntax</span></span>

| <span data-ttu-id="94a93-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="94a93-123">Method</span></span>  | <span data-ttu-id="94a93-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="94a93-124">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="94a93-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="94a93-125">**GET**</span></span> | <span data-ttu-id="94a93-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size}? Filter = {Filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="94a93-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="94a93-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="94a93-127">URI parameter</span></span>

<span data-ttu-id="94a93-128">K vytvoření žádosti použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="94a93-128">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="94a93-129">Název</span><span class="sxs-lookup"><span data-stu-id="94a93-129">Name</span></span>   | <span data-ttu-id="94a93-130">Typ</span><span class="sxs-lookup"><span data-stu-id="94a93-130">Type</span></span>   | <span data-ttu-id="94a93-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="94a93-131">Required</span></span> | <span data-ttu-id="94a93-132">Popis</span><span class="sxs-lookup"><span data-stu-id="94a93-132">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="94a93-133">size</span><span class="sxs-lookup"><span data-stu-id="94a93-133">size</span></span>   | <span data-ttu-id="94a93-134">int</span><span class="sxs-lookup"><span data-stu-id="94a93-134">int</span></span>    | <span data-ttu-id="94a93-135">No</span><span class="sxs-lookup"><span data-stu-id="94a93-135">No</span></span>       | <span data-ttu-id="94a93-136">Počet výsledků, které se mají zobrazit v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="94a93-136">The number of results to be displayed at one time.</span></span> <span data-ttu-id="94a93-137">Tento parametr je volitelný.</span><span class="sxs-lookup"><span data-stu-id="94a93-137">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="94a93-138">filter</span><span class="sxs-lookup"><span data-stu-id="94a93-138">filter</span></span> | <span data-ttu-id="94a93-139">filter</span><span class="sxs-lookup"><span data-stu-id="94a93-139">filter</span></span> | <span data-ttu-id="94a93-140">Yes</span><span class="sxs-lookup"><span data-stu-id="94a93-140">Yes</span></span>      | <span data-ttu-id="94a93-141">Dotaz, který filtruje hledání</span><span class="sxs-lookup"><span data-stu-id="94a93-141">The query that filters the search.</span></span> <span data-ttu-id="94a93-142">Chcete-li načíst zákazníky pro zadaného nepřímého prodejce, je nutné vložit nepřímý identifikátor prodejce a zahrnout a zakódovat následující řetězec: {"Field": "IndirectReseller", "value": "{nepřímý prodejce identifikátorů}", "operator": "začíná řetězcem \_ "}.</span><span class="sxs-lookup"><span data-stu-id="94a93-142">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="94a93-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="94a93-143">Request headers</span></span>

<span data-ttu-id="94a93-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="94a93-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="94a93-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="94a93-145">Request body</span></span>

<span data-ttu-id="94a93-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="94a93-146">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="94a93-147">Příklad požadavku (kódovaný)</span><span class="sxs-lookup"><span data-stu-id="94a93-147">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="94a93-148">Příklad požadavku (dekódování)</span><span class="sxs-lookup"><span data-stu-id="94a93-148">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="94a93-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="94a93-149">REST response</span></span>

<span data-ttu-id="94a93-150">V případě úspěchu obsahuje tělo odpovědi informace o zákaznících prodejce.</span><span class="sxs-lookup"><span data-stu-id="94a93-150">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="94a93-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="94a93-151">Response success and error codes</span></span>

<span data-ttu-id="94a93-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="94a93-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="94a93-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="94a93-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="94a93-154">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="94a93-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="94a93-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="94a93-155">Response example</span></span>

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
