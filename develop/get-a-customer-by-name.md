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
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Získání seznamu zákazníků filtrovaných podle vyhledávacího pole

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Získá kolekci [zákaznických](customer-resources.md#customer) prostředků, které odpovídají filtru. Volitelně můžete nastavit velikost stránky. Můžete filtrovat podle názvu společnosti, domény, nepřímého prodejce nebo poskytovatele nepřímých cloudových řešení (CSP).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- Filtr vytvořený uživatelem.

## <a name="c"></a>C\#

Pro získání kolekce zákazníků, které odpovídají filtru, nejprve vytvořte instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) , abyste vytvořili filtr. Budete muset předat řetězec, který obsahuje [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), a označit typ operace filtru jako [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation). To je jediná operace filtru pole podporovaná koncovým bodem zákazníků. Také budete muset zadat řetězec, podle kterého se má filtrovat.

Dále vytvořte instanci objektu [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) , který se předá dotazu, voláním metody [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) a předáním filtru. BuildSimplyQuery je pouze jeden z typů dotazu podporovaných třídou [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .

Nakonec, pokud chcete spustit filtr a získat výsledek, nejdřív použijte [**IAggregatePartner. zákazníci**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby získali rozhraní pro zákaznické operace partnera. Pak zavolejte [**dotaz**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo metodu [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .

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

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: FilterCustomers.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size} &Filter = {Filter} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

Použijte následující parametry dotazu.

| Název   | Typ   | Vyžadováno | Popis                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | int    | No       | Počet výsledků, které se mají zobrazit v jednom okamžiku. Tento parametr je volitelný. |
| filter | filter | Yes      | Filtr, který se má použít pro zákazníky Musí se jednat o kódovaný řetězec.              |

### <a name="filter-syntax"></a>Syntaxe filtru

Parametr Filter je nutné vytvořit jako řadu párů klíč-hodnota oddělené čárkami. Každý klíč a hodnota musí být jednotlivě kotované a oddělené dvojtečkou. Celý filtr musí být kódovaný.

Nekódovaný příklad vypadá takto:

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

Následující tabulka popisuje požadované páry klíč-hodnota:

| Klíč      | Hodnota                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Pole    | Pole, které se má filtrovat Platné hodnoty najdete v [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield). |
| Hodnota    | Hodnota, podle které se má filtrovat Případ hodnoty je ignorován.                                                                |
| Operátor | Operátor, který se má použít Jediná podporovaná hodnota pro tento scénář zákazníka je "začíná na \_ ".                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu tato metoda vrátí kolekci vyhovujících [zákaznických](customer-resources.md#customer) prostředků v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
