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
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Získání seznamu zákazníků filtrovaných podle vyhledávacího pole

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Získá kolekci prostředků [zákazníka,](customer-resources.md#customer) které odpovídají filtru. Volitelně můžete nastavit velikost stránky. Můžete filtrovat podle názvu společnosti, domény, nepřímého prodejce nebo nepřímého poskytovatele cloudových řešení (CSP).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- Uživatelem vytvořený filtr.

## <a name="c"></a>C\#

Pokud chcete získat kolekci zákazníků, kteří odpovídají filtru, vytvořte nejprve instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) a vytvořte filtr. Budete muset předat řetězec, který obsahuje [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), a určit typ operace filtru [**jako FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation). To je jediná operace filtru polí podporovaná koncovým bodem zákazníků. Budete také muset zadat řetězec, podle který chcete filtrovat.

Dále vytvořte instanci objektu [**iQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) který se má předat dotazu voláním metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) a předáním filtru. BuildSimplyQuery je pouze jedním z typů dotazů podporovaných [**třídou QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)

Nakonec spusťte filtr a získejte výsledek tak, že nejprve pomocí [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) získáte rozhraní pro operace zákazníků partnera. Potom zavolejte [**metodu Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)

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

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** FilterCustomers.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

Použijte následující parametry dotazu.

| Název   | Typ   | Vyžadováno | Popis                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | int    | No       | Počet výsledků, které se zobrazí najednou Tento parametr je volitelný. |
| filter | filter | Yes      | Filtr, který se má použít pro zákazníky. Musí to být zakódovaný řetězec.              |

### <a name="filter-syntax"></a>Syntaxe filtru

Parametr filtru musíte vytvořit jako řadu párů klíč-hodnota oddělených čárkami. Každý klíč a hodnota musí být jednotlivě uvozené a oddělené dvojtečkou. Celý filtr musí být kódovaný.

Nekódovaný příklad vypadá jako tento:

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

Následující tabulka popisuje požadované páry klíč-hodnota:

| Klíč      | Hodnota                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Pole    | Pole, které chcete filtrovat. Platné hodnoty najdete v [**customerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield). |
| Hodnota    | Hodnota, podle které se má filtrovat. Případ hodnoty se ignoruje.                                                                |
| Operátor | Operátor, který se má použít. Jediná podporovaná hodnota pro tento zákaznický scénář je "začíná \_ na".                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

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

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato [](customer-resources.md#customer) metoda v textu odpovědi kolekci odpovídajících prostředků zákazníka.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

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
