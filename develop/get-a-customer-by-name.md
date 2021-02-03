---
title: Získání seznamu zákazníků filtrovaných podle vyhledávacího pole
description: Získá kolekci zákaznických prostředků, které odpovídají filtru. Volitelně můžete nastavit velikost stránky. Můžete filtrovat podle názvu společnosti, domény, nepřímého prodejce nebo poskytovatele nepřímých cloudových řešení (CSP).
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: aad9524dbe2c9edbbd7c1d50da7a448f6872fcb9
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766876"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="752f6-105">Získání seznamu zákazníků filtrovaných podle vyhledávacího pole</span><span class="sxs-lookup"><span data-stu-id="752f6-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="752f6-106">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="752f6-106">**Applies To**</span></span>

- <span data-ttu-id="752f6-107">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="752f6-107">Partner Center</span></span>
- <span data-ttu-id="752f6-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="752f6-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="752f6-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="752f6-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="752f6-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="752f6-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="752f6-111">Získá kolekci [zákaznických](customer-resources.md#customer) prostředků, které odpovídají filtru.</span><span class="sxs-lookup"><span data-stu-id="752f6-111">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="752f6-112">Volitelně můžete nastavit velikost stránky.</span><span class="sxs-lookup"><span data-stu-id="752f6-112">You can optionally set a page size.</span></span> <span data-ttu-id="752f6-113">Můžete filtrovat podle názvu společnosti, domény, nepřímého prodejce nebo poskytovatele nepřímých cloudových řešení (CSP).</span><span class="sxs-lookup"><span data-stu-id="752f6-113">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="752f6-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="752f6-114">Prerequisites</span></span>

- <span data-ttu-id="752f6-115">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="752f6-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="752f6-116">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="752f6-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="752f6-117">Filtr vytvořený uživatelem.</span><span class="sxs-lookup"><span data-stu-id="752f6-117">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="752f6-118">C\#</span><span class="sxs-lookup"><span data-stu-id="752f6-118">C\#</span></span>

<span data-ttu-id="752f6-119">Pro získání kolekce zákazníků, které odpovídají filtru, nejprve vytvořte instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) , abyste vytvořili filtr.</span><span class="sxs-lookup"><span data-stu-id="752f6-119">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="752f6-120">Budete muset předat řetězec, který obsahuje [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), a označit typ operace filtru jako [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span><span class="sxs-lookup"><span data-stu-id="752f6-120">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="752f6-121">To je jediná operace filtru pole podporovaná koncovým bodem zákazníků.</span><span class="sxs-lookup"><span data-stu-id="752f6-121">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="752f6-122">Také budete muset zadat řetězec, podle kterého se má filtrovat.</span><span class="sxs-lookup"><span data-stu-id="752f6-122">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="752f6-123">Dále vytvořte instanci objektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , který se předá dotazu, voláním metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) a předáním filtru.</span><span class="sxs-lookup"><span data-stu-id="752f6-123">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="752f6-124">BuildSimplyQuery je pouze jeden z typů dotazu podporovaných třídou [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .</span><span class="sxs-lookup"><span data-stu-id="752f6-124">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="752f6-125">Nakonec, pokud chcete spustit filtr a získat výsledek, nejdřív použijte [**IAggregatePartner. zákazníci**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby získali rozhraní pro zákaznické operace partnera.</span><span class="sxs-lookup"><span data-stu-id="752f6-125">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="752f6-126">Pak zavolejte [**dotaz**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo metodu [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .</span><span class="sxs-lookup"><span data-stu-id="752f6-126">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

<span data-ttu-id="752f6-127">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="752f6-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="752f6-128">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: FilterCustomers.cs</span><span class="sxs-lookup"><span data-stu-id="752f6-128">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="752f6-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="752f6-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="752f6-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="752f6-130">Request syntax</span></span>

| <span data-ttu-id="752f6-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="752f6-131">Method</span></span>  | <span data-ttu-id="752f6-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="752f6-132">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="752f6-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="752f6-133">**GET**</span></span> | <span data-ttu-id="752f6-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size} &Filter = {Filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="752f6-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="752f6-135">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="752f6-135">URI parameters</span></span>

<span data-ttu-id="752f6-136">Použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="752f6-136">Use the following query parameters.</span></span>

| <span data-ttu-id="752f6-137">Název</span><span class="sxs-lookup"><span data-stu-id="752f6-137">Name</span></span>   | <span data-ttu-id="752f6-138">Typ</span><span class="sxs-lookup"><span data-stu-id="752f6-138">Type</span></span>   | <span data-ttu-id="752f6-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="752f6-139">Required</span></span> | <span data-ttu-id="752f6-140">Popis</span><span class="sxs-lookup"><span data-stu-id="752f6-140">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="752f6-141">size</span><span class="sxs-lookup"><span data-stu-id="752f6-141">size</span></span>   | <span data-ttu-id="752f6-142">int</span><span class="sxs-lookup"><span data-stu-id="752f6-142">int</span></span>    | <span data-ttu-id="752f6-143">No</span><span class="sxs-lookup"><span data-stu-id="752f6-143">No</span></span>       | <span data-ttu-id="752f6-144">Počet výsledků, které se mají zobrazit v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="752f6-144">The number of results to be displayed at one time.</span></span> <span data-ttu-id="752f6-145">Tento parametr je volitelný.</span><span class="sxs-lookup"><span data-stu-id="752f6-145">This parameter is optional.</span></span> |
| <span data-ttu-id="752f6-146">filter</span><span class="sxs-lookup"><span data-stu-id="752f6-146">filter</span></span> | <span data-ttu-id="752f6-147">filter</span><span class="sxs-lookup"><span data-stu-id="752f6-147">filter</span></span> | <span data-ttu-id="752f6-148">Yes</span><span class="sxs-lookup"><span data-stu-id="752f6-148">Yes</span></span>      | <span data-ttu-id="752f6-149">Filtr, který se má použít pro zákazníky</span><span class="sxs-lookup"><span data-stu-id="752f6-149">The filter to apply to customers.</span></span> <span data-ttu-id="752f6-150">Musí se jednat o kódovaný řetězec.</span><span class="sxs-lookup"><span data-stu-id="752f6-150">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="752f6-151">Syntaxe filtru</span><span class="sxs-lookup"><span data-stu-id="752f6-151">Filter Syntax</span></span>

<span data-ttu-id="752f6-152">Parametr Filter je nutné vytvořit jako řadu párů klíč-hodnota oddělené čárkami.</span><span class="sxs-lookup"><span data-stu-id="752f6-152">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="752f6-153">Každý klíč a hodnota musí být jednotlivě kotované a oddělené dvojtečkou.</span><span class="sxs-lookup"><span data-stu-id="752f6-153">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="752f6-154">Celý filtr musí být kódovaný.</span><span class="sxs-lookup"><span data-stu-id="752f6-154">The entire filter must be encoded.</span></span>

<span data-ttu-id="752f6-155">Nekódovaný příklad vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="752f6-155">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="752f6-156">Následující tabulka popisuje požadované páry klíč-hodnota:</span><span class="sxs-lookup"><span data-stu-id="752f6-156">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="752f6-157">Klíč</span><span class="sxs-lookup"><span data-stu-id="752f6-157">Key</span></span>      | <span data-ttu-id="752f6-158">Hodnota</span><span class="sxs-lookup"><span data-stu-id="752f6-158">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="752f6-159">Pole</span><span class="sxs-lookup"><span data-stu-id="752f6-159">Field</span></span>    | <span data-ttu-id="752f6-160">Pole, které se má filtrovat</span><span class="sxs-lookup"><span data-stu-id="752f6-160">The field to filter.</span></span> <span data-ttu-id="752f6-161">Platné hodnoty najdete v [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span><span class="sxs-lookup"><span data-stu-id="752f6-161">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="752f6-162">Hodnota</span><span class="sxs-lookup"><span data-stu-id="752f6-162">Value</span></span>    | <span data-ttu-id="752f6-163">Hodnota, podle které se má filtrovat</span><span class="sxs-lookup"><span data-stu-id="752f6-163">The value to filter by.</span></span> <span data-ttu-id="752f6-164">Případ hodnoty je ignorován.</span><span class="sxs-lookup"><span data-stu-id="752f6-164">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="752f6-165">Operátor</span><span class="sxs-lookup"><span data-stu-id="752f6-165">Operator</span></span> | <span data-ttu-id="752f6-166">Operátor, který se má použít</span><span class="sxs-lookup"><span data-stu-id="752f6-166">The operator to apply.</span></span> <span data-ttu-id="752f6-167">Jediná podporovaná hodnota pro tento scénář zákazníka je "začíná na \_ ".</span><span class="sxs-lookup"><span data-stu-id="752f6-167">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="752f6-168">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="752f6-168">Request headers</span></span>

<span data-ttu-id="752f6-169">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="752f6-169">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="752f6-170">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="752f6-170">Request body</span></span>

<span data-ttu-id="752f6-171">Žádné</span><span class="sxs-lookup"><span data-stu-id="752f6-171">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="752f6-172">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="752f6-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="752f6-173">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="752f6-173">REST response</span></span>

<span data-ttu-id="752f6-174">V případě úspěchu tato metoda vrátí kolekci vyhovujících [zákaznických](customer-resources.md#customer) prostředků v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="752f6-174">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="752f6-175">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="752f6-175">Response success and error codes</span></span>

<span data-ttu-id="752f6-176">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="752f6-176">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="752f6-177">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="752f6-177">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="752f6-178">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="752f6-178">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="752f6-179">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="752f6-179">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
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
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
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
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
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
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
