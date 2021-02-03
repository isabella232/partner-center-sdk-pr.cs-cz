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
# <a name="get-customers-of-an-indirect-reseller"></a>Získání zákazníků nepřímého prodejce

**Platí pro**

- Partnerské centrum

Jak získat seznam zákazníků nepřímého prodejce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- Identifikátor tenanta nepřímého prodejce.

## <a name="c"></a>C\#

Chcete-li získat kolekci zákazníků, kteří mají relaci se zadaným nepřímým prodejcem, nejprve vytvořte instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) pro vytvoření filtru. Musíte předat člen výčtu [**CustomerSearchField. IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) převedený na řetězec a jako typ operace filtru označit [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) . Budete taky muset zadat identifikátor tenanta nepřímého prodejce, podle kterého se má filtrovat.

Dále vytvořte instanci objektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , který se předá dotazu, voláním metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) a předáním filtru. BuildSimplyQuery je pouze jeden z typů dotazu podporovaných třídou [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .

Pokud chcete spustit filtr a získat výsledek, nejdřív použijte [**IAggregatePartner. zákazníci**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby získali rozhraní pro zákaznické operace partnera. Pak zavolejte [**dotaz**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo metodu [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .

Chcete-li vytvořit enumerátor pro procházení stránkovaných výsledků, Získejte rozhraní pro vytváření výčtu kolekce zákazníka od vlastnosti [**IAggregatePartner. enumerators. Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) a potom zavolejte metodu [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), jak je znázorněno v následujícím kódu, a předejte jí proměnnou, která obsahuje kolekci Customer.

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

**Ukázka**:**projekt** [aplikace testů konzoly](console-test-app.md): ukázkové **třídy** SDK pro partnerských Center: GetCustomersOfIndirectReseller.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size}? Filter = {Filter} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K vytvoření žádosti použijte následující parametry dotazu.

| Název   | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| size   | int    | No       | Počet výsledků, které se mají zobrazit v jednom okamžiku. Tento parametr je volitelný.                                                                                                                                                                                                                |
| filter | filter | Yes      | Dotaz, který filtruje hledání Chcete-li načíst zákazníky pro zadaného nepřímého prodejce, je nutné vložit nepřímý identifikátor prodejce a zahrnout a zakódovat následující řetězec: {"Field": "IndirectReseller", "value": "{nepřímý prodejce identifikátorů}", "operator": "začíná řetězcem \_ "}. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example-encoded"></a>Příklad požadavku (kódovaný)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a>Příklad požadavku (dekódování)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi informace o zákaznících prodejce.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

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
