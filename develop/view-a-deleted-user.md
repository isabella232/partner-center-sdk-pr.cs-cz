---
title: Zobrazení odstraněných uživatelů pro zákazníka
description: Načte seznam odstraněných prostředků CustomerUser pro zákazníka podle ID zákazníka. Volitelně můžete nastavit velikost stránky. Je nutné, abyste zadali filtr.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766929"
---
# <a name="view-deleted-users-for-a-customer"></a>Zobrazení odstraněných uživatelů pro zákazníka

**Platí pro**

- Partnerské centrum

Načte seznam odstraněných prostředků CustomerUser pro zákazníka podle ID zákazníka. Volitelně můžete nastavit velikost stránky. Je nutné, abyste zadali filtr.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="what-happens-when-you-delete-a-user-account"></a>Co se stane, když odstraníte uživatelský účet?

Stav uživatele je nastaven na "neaktivní" při odstranění uživatelského účtu. Zůstane to po dobu třiceti dnů, po jejímž uplynutí se uživatelský účet a jeho přidružená data vyprázdní a provedou neobnovitelné. Pokud chcete obnovit odstraněný uživatelský účet v rámci třiceti dnů, přečtěte si téma [Obnovení odstraněného uživatele pro zákazníka](restore-a-user-for-a-customer.md). Po odstranění a označení "neaktivní" již uživatelský účet nebude vrácen jako člen kolekce uživatelů (například pomocí příkazu [získat seznam všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md)). Chcete-li získat seznam odstraněných uživatelů, které ještě nebyly smazány, je nutné zadat dotaz na uživatelské účty, které byly nastaveny na neaktivní.

## <a name="c"></a>C\#

Chcete-li načíst seznam odstraněných uživatelů, vytvořte dotaz, který filtruje uživatele zákazníka, jejichž stav je nastaven na neaktivní. Nejprve vytvořte filtr vytvořením instance objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) s parametry, jak je znázorněno v následujícím fragmentu kódu. Pak vytvořte dotaz pomocí metody [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) . Pokud nechcete stránkované výsledky, můžete místo toho použít metodu [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) . V dalším kroku použijte k identifikaci zákazníka metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka. Nakonec zavolejte metodu [**dotazu**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) pro odeslání žádosti.

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

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? size = {size} &Filter = {Filter} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření žádosti použijte následující cestu a parametry dotazu.

| Název        | Typ   | Vyžadováno | Popis                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID zákazníka | guid   | Yes      | Hodnota je identifikátor zákazníka, který je ve formátu GUID, který identifikuje zákazníka.                                                                                                            |
| size        | int    | No       | Počet výsledků, které se mají zobrazit v jednom okamžiku. Tento parametr je volitelný.                                                                                                     |
| filter      | filter | Yes      | Dotaz, který filtruje hledání uživatelů Chcete-li načíst odstraněné uživatele, je nutné zahrnout a zakódovat následující řetězec: {"Field": "UserState", "value": "neaktivní", "operator": "Equals"}. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu tato metoda vrátí kolekci prostředků [CustomerUser](user-resources.md#customeruser) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
