---
title: Zobrazení odstraněných uživatelů pro zákazníka
description: Získá seznam odstraněných prostředků CustomerUser pro zákazníka podle ID zákazníka. Volitelně můžete nastavit velikost stránky. Musíte zadat filtr.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f7e94d5e360075378e1895e586690597baaf66237f0b93bb526baee0c5d84ae
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989810"
---
# <a name="view-deleted-users-for-a-customer"></a>Zobrazení odstraněných uživatelů pro zákazníka

Získá seznam odstraněných prostředků CustomerUser pro zákazníka podle ID zákazníka. Volitelně můžete nastavit velikost stránky. Musíte zadat filtr.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="what-happens-when-you-delete-a-user-account"></a>Co se stane, když odstraníte uživatelský účet?

Stav uživatele je při odstranění uživatelského účtu nastavený na "neaktivní". Zůstane tak po dobu 30 dnů, po jejímž uplynutí se uživatelský účet a jeho přidružená data vyprázdní a nenapraví. Pokud chcete odstraněný uživatelský účet obnovit v rámci 30denního okna, podívejte se na stránku Obnovení odstraněných uživatelů [pro zákazníka.](restore-a-user-for-a-customer.md) Po odstranění a označení "neaktivní" už se uživatelský účet nebude vrátil jako člen kolekce uživatelů (například pomocí příkazu Získat seznam všech uživatelských účtů pro [zákazníka).](get-a-list-of-all-user-accounts-for-a-customer.md) Pokud chcete získat seznam odstraněných uživatelů, kteří ještě nejsou vyprázdnění, musíte zadat dotaz na uživatelské účty, které byly nastaveny na neaktivní.

## <a name="c"></a>C\#

Pokud chcete načíst seznam odstraněných uživatelů, vytvořte dotaz, který vyfiltruje uživatele zákazníka, jejichž stav je neaktivní. Nejprve vytvořte filtr vytvořením instance objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) s parametry, jak je znázorněno v následujícím fragmentu kódu. Pak vytvořte dotaz pomocí metody [**BuildIndexedQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) Pokud nechcete stránkované výsledky, můžete místo toho použít metodu [**BuildSimpleQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) Dále k identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka. Nakonec zavolejte [**metodu Query,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) která odešle požadavek.

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{id_zákazníka}/users?size={velikost}&filter={filter} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření požadavku použijte následující cestu a parametry dotazu.

| Název        | Typ   | Vyžadováno | Popis                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id zákazníka | guid   | Yes      | Hodnota je ID zákazníka ve formátu GUID, které identifikuje zákazníka.                                                                                                            |
| size        | int    | No       | Počet výsledků, které se zobrazí najednou Tento parametr je volitelný.                                                                                                     |
| filter      | filter | Yes      | Dotaz, který filtruje vyhledávání uživatelů. Pokud chcete načíst odstraněné uživatele, musíte zahrnout a zakódovat následující řetězec: {"Field":"UserState","Value":"Inactive","Operator":"equals"}. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v textu odpovědi kolekci prostředků [CustomerUser.](user-resources.md#customeruser)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
