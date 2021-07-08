---
title: Získání seznamu zákazníků filtrovaných podle vyhledávacího pole
description: Získá kolekci prostředků zákazníka, které odpovídají filtru. Volitelně můžete nastavit velikost stránky. Můžete filtrovat podle názvu společnosti, domény, nepřímého prodejce nebo nepřímého poskytovatele cloudových řešení (CSP).
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 663b8509d8704f9c443796d9fbcf72fb9c5b7fb2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874954"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="21e96-105">Získání seznamu zákazníků filtrovaných podle vyhledávacího pole</span><span class="sxs-lookup"><span data-stu-id="21e96-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="21e96-106">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="21e96-106">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="21e96-107">Získá kolekci prostředků [zákazníka,](customer-resources.md#customer) které odpovídají filtru.</span><span class="sxs-lookup"><span data-stu-id="21e96-107">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="21e96-108">Volitelně můžete nastavit velikost stránky.</span><span class="sxs-lookup"><span data-stu-id="21e96-108">You can optionally set a page size.</span></span> <span data-ttu-id="21e96-109">Můžete filtrovat podle názvu společnosti, domény, nepřímého prodejce nebo nepřímého poskytovatele cloudových řešení (CSP).</span><span class="sxs-lookup"><span data-stu-id="21e96-109">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21e96-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="21e96-110">Prerequisites</span></span>

- <span data-ttu-id="21e96-111">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="21e96-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="21e96-112">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="21e96-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="21e96-113">Uživatelem vytvořený filtr.</span><span class="sxs-lookup"><span data-stu-id="21e96-113">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="21e96-114">C\#</span><span class="sxs-lookup"><span data-stu-id="21e96-114">C\#</span></span>

<span data-ttu-id="21e96-115">Pokud chcete získat kolekci zákazníků, kteří odpovídají filtru, vytvořte nejprve instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) a vytvořte filtr.</span><span class="sxs-lookup"><span data-stu-id="21e96-115">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="21e96-116">Budete muset předat řetězec, který obsahuje [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), a určit typ operace filtru [**jako FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span><span class="sxs-lookup"><span data-stu-id="21e96-116">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="21e96-117">To je jediná operace filtru polí podporovaná koncovým bodem zákazníků.</span><span class="sxs-lookup"><span data-stu-id="21e96-117">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="21e96-118">Budete také muset zadat řetězec, podle který chcete filtrovat.</span><span class="sxs-lookup"><span data-stu-id="21e96-118">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="21e96-119">Dále vytvořte instanci objektu [**iQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) který se má předat dotazu voláním metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) a předáním filtru.</span><span class="sxs-lookup"><span data-stu-id="21e96-119">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="21e96-120">BuildSimplyQuery je pouze jedním z typů dotazů podporovaných [**třídou QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="21e96-120">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="21e96-121">Nakonec spusťte filtr a získejte výsledek tak, že nejprve pomocí [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) získáte rozhraní pro operace zákazníků partnera.</span><span class="sxs-lookup"><span data-stu-id="21e96-121">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="21e96-122">Potom zavolejte [**metodu Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="21e96-122">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

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

<span data-ttu-id="21e96-123">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="21e96-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="21e96-124">**Project:** SDK pro Partnerské centrum Samples **Class:** FilterCustomers.cs</span><span class="sxs-lookup"><span data-stu-id="21e96-124">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="21e96-125">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="21e96-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="21e96-126">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="21e96-126">Request syntax</span></span>

| <span data-ttu-id="21e96-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="21e96-127">Method</span></span>  | <span data-ttu-id="21e96-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="21e96-128">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="21e96-129">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="21e96-129">**GET**</span></span> | <span data-ttu-id="21e96-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="21e96-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="21e96-131">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="21e96-131">URI parameters</span></span>

<span data-ttu-id="21e96-132">Použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="21e96-132">Use the following query parameters.</span></span>

| <span data-ttu-id="21e96-133">Název</span><span class="sxs-lookup"><span data-stu-id="21e96-133">Name</span></span>   | <span data-ttu-id="21e96-134">Typ</span><span class="sxs-lookup"><span data-stu-id="21e96-134">Type</span></span>   | <span data-ttu-id="21e96-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="21e96-135">Required</span></span> | <span data-ttu-id="21e96-136">Popis</span><span class="sxs-lookup"><span data-stu-id="21e96-136">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="21e96-137">size</span><span class="sxs-lookup"><span data-stu-id="21e96-137">size</span></span>   | <span data-ttu-id="21e96-138">int</span><span class="sxs-lookup"><span data-stu-id="21e96-138">int</span></span>    | <span data-ttu-id="21e96-139">No</span><span class="sxs-lookup"><span data-stu-id="21e96-139">No</span></span>       | <span data-ttu-id="21e96-140">Počet výsledků, které se zobrazí najednou</span><span class="sxs-lookup"><span data-stu-id="21e96-140">The number of results to be displayed at one time.</span></span> <span data-ttu-id="21e96-141">Tento parametr je volitelný.</span><span class="sxs-lookup"><span data-stu-id="21e96-141">This parameter is optional.</span></span> |
| <span data-ttu-id="21e96-142">filter</span><span class="sxs-lookup"><span data-stu-id="21e96-142">filter</span></span> | <span data-ttu-id="21e96-143">filter</span><span class="sxs-lookup"><span data-stu-id="21e96-143">filter</span></span> | <span data-ttu-id="21e96-144">Yes</span><span class="sxs-lookup"><span data-stu-id="21e96-144">Yes</span></span>      | <span data-ttu-id="21e96-145">Filtr, který se má použít pro zákazníky.</span><span class="sxs-lookup"><span data-stu-id="21e96-145">The filter to apply to customers.</span></span> <span data-ttu-id="21e96-146">Musí to být zakódovaný řetězec.</span><span class="sxs-lookup"><span data-stu-id="21e96-146">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="21e96-147">Syntaxe filtru</span><span class="sxs-lookup"><span data-stu-id="21e96-147">Filter Syntax</span></span>

<span data-ttu-id="21e96-148">Parametr filtru musíte vytvořit jako řadu párů klíč-hodnota oddělených čárkami.</span><span class="sxs-lookup"><span data-stu-id="21e96-148">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="21e96-149">Každý klíč a hodnota musí být jednotlivě uvozené a oddělené dvojtečkou.</span><span class="sxs-lookup"><span data-stu-id="21e96-149">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="21e96-150">Celý filtr musí být kódovaný.</span><span class="sxs-lookup"><span data-stu-id="21e96-150">The entire filter must be encoded.</span></span>

<span data-ttu-id="21e96-151">Nekódovaný příklad vypadá jako tento:</span><span class="sxs-lookup"><span data-stu-id="21e96-151">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="21e96-152">Následující tabulka popisuje požadované páry klíč-hodnota:</span><span class="sxs-lookup"><span data-stu-id="21e96-152">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="21e96-153">Klíč</span><span class="sxs-lookup"><span data-stu-id="21e96-153">Key</span></span>      | <span data-ttu-id="21e96-154">Hodnota</span><span class="sxs-lookup"><span data-stu-id="21e96-154">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="21e96-155">Pole</span><span class="sxs-lookup"><span data-stu-id="21e96-155">Field</span></span>    | <span data-ttu-id="21e96-156">Pole, které chcete filtrovat.</span><span class="sxs-lookup"><span data-stu-id="21e96-156">The field to filter.</span></span> <span data-ttu-id="21e96-157">Platné hodnoty najdete v [**customerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span><span class="sxs-lookup"><span data-stu-id="21e96-157">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="21e96-158">Hodnota</span><span class="sxs-lookup"><span data-stu-id="21e96-158">Value</span></span>    | <span data-ttu-id="21e96-159">Hodnota, podle které se má filtrovat.</span><span class="sxs-lookup"><span data-stu-id="21e96-159">The value to filter by.</span></span> <span data-ttu-id="21e96-160">Případ hodnoty se ignoruje.</span><span class="sxs-lookup"><span data-stu-id="21e96-160">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="21e96-161">Operátor</span><span class="sxs-lookup"><span data-stu-id="21e96-161">Operator</span></span> | <span data-ttu-id="21e96-162">Operátor, který se má použít.</span><span class="sxs-lookup"><span data-stu-id="21e96-162">The operator to apply.</span></span> <span data-ttu-id="21e96-163">Jediná podporovaná hodnota pro tento zákaznický scénář je "začíná \_ na".</span><span class="sxs-lookup"><span data-stu-id="21e96-163">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="21e96-164">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="21e96-164">Request headers</span></span>

<span data-ttu-id="21e96-165">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="21e96-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="21e96-166">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="21e96-166">Request body</span></span>

<span data-ttu-id="21e96-167">Žádné</span><span class="sxs-lookup"><span data-stu-id="21e96-167">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="21e96-168">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="21e96-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="21e96-169">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="21e96-169">REST response</span></span>

<span data-ttu-id="21e96-170">V případě úspěchu vrátí tato [](customer-resources.md#customer) metoda v textu odpovědi kolekci odpovídajících prostředků zákazníka.</span><span class="sxs-lookup"><span data-stu-id="21e96-170">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="21e96-171">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="21e96-171">Response success and error codes</span></span>

<span data-ttu-id="21e96-172">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="21e96-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="21e96-173">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="21e96-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="21e96-174">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="21e96-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="21e96-175">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="21e96-175">Response example</span></span>

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
