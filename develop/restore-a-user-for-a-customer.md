---
title: Obnovení odstraněného uživatele pro zákazníka
description: Jak obnovit odstraněného uživatele podle ID zákazníka a ID uživatele
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23caf91c6b29b292c2638b4a1ad208c606c47492
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445710"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Obnovení odstraněného uživatele pro zákazníka

Jak obnovit odstraněného **uživatele podle** ID zákazníka a ID uživatele

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID uživatele. Pokud id uživatele nemáte, podívejte se na stránku [Zobrazení odstraněných uživatelů pro zákazníka.](view-a-deleted-user.md)

## <a name="when-can-you-restore-a-deleted-user-account"></a>Kdy můžete obnovit odstraněný uživatelský účet?

Stav uživatele je při odstranění uživatelského účtu nastavený na "neaktivní". Zůstane tak po dobu 30 dnů, po jejímž uplynutí se uživatelský účet a jeho přidružená data vyprázdní a nenapraví. Odstraněný uživatelský účet můžete obnovit pouze během tohoto 30denního období. Po odstranění a označení jako neaktivní už se uživatelský účet nebude vrátil jako člen kolekce uživatelů (například pomocí příkazu Získat seznam všech uživatelských účtů pro [zákazníka).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="c"></a>C\#

Pokud chcete obnovit uživatele, vytvořte novou instanci třídy [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) a nastavte hodnotu vlastnosti [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) na [**UserState.Active.**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)

Odstraněný uživatel obnovíte nastavením stavu uživatele na aktivní. Zbývající pole v uživatelském prostředku není možné znovu zapopilovat. Tyto hodnoty se automaticky obnoví z odstraněného neaktivního uživatelského prostředku. Dále pomocí metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka identifikujte zákazníka a metodu [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) k identifikaci uživatele.

Nakonec zavolejte [**metodu Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) a předejte instanci **CustomerUser,** která odešle požadavek na obnovení uživatele.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** CustomerUserRestore.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda    | Identifikátor URI žádosti                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **Oprava** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/users/{ID_uživatele} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Pomocí následujících parametrů dotazu zadejte ID zákazníka a ID uživatele.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který prodejci umožňuje filtrovat výsledky na daného zákazníka. |
| **ID uživatele**            | **guid** | Y        | Hodnota je ID uživatele ve **formátu** GUID, které patří jednomu uživatelskému účtu.                                         |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu požadavku.

| Název       | Typ   | Vyžadováno | Popis                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Stav      | řetězec | Y        | Stav uživatele Pokud chcete odstraněného uživatele obnovit, musí tento řetězec obsahovat hodnotu "active". |
| Atributy | object | N        | Obsahuje "ObjectType": "CustomerUser".                                 |

### <a name="request-example"></a>Příklad požadavku

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí odpověď obnovené informace o uživateli v textu odpovědi.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
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
```
