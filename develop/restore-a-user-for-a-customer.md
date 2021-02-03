---
title: Obnovení odstraněného uživatele pro zákazníka
description: Jak obnovit odstraněné uživatele podle ID zákazníka a ID uživatele.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767017"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Obnovení odstraněného uživatele pro zákazníka

**Platí pro**

- Partnerské centrum

Jak obnovit odstraněné **uživatele** podle ID zákazníka a ID uživatele.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID uživatele Pokud nemáte ID uživatele, přečtěte si téma [zobrazení odstraněných uživatelů pro zákazníka](view-a-deleted-user.md).

## <a name="when-can-you-restore-a-deleted-user-account"></a>Kdy je možné obnovit odstraněný uživatelský účet?

Stav uživatele je nastaven na "neaktivní" při odstranění uživatelského účtu. Zůstane to po dobu třiceti dnů, po jejímž uplynutí se uživatelský účet a jeho přidružená data vyprázdní a provedou neobnovitelné. Odstraněný uživatelský účet můžete obnovit jenom během tohoto 30denní okna. Po odstranění a označení jako neaktivní se uživatelský účet už nevrátí jako člen kolekce uživatelů (například pomocí příkazu [získat seznam všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Chcete-li obnovit uživatele, vytvořte novou instanci třídy [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) a nastavte hodnotu vlastnosti [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) na [**userState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).

Odstraněné uživatele obnovíte tak, že nastavíte stav uživatele na aktivní. Zbývající pole v prostředku uživatele není nutné znovu naplňovat. Tyto hodnoty se automaticky obnoví z odstraněného neaktivního prostředku uživatele. Dále použijte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka a metodu [**Users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pro identifikaci uživatele.

Nakonec zavolejte metodu [**patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) a předejte instanci **CustomerUser** , aby odeslala požadavek na obnovení uživatele.

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

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: CustomerUserRestore.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **POUŽITA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Pomocí následujících parametrů dotazu zadejte ID zákazníka a ID uživatele.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky na daného zákazníka. |
| **ID uživatele**            | **guid** | Y        | Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.                                         |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu žádosti.

| Název       | Typ   | Vyžadováno | Popis                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| State      | řetězec | Y        | Stav uživatele Chcete-li obnovit odstraněného uživatele, musí tento řetězec obsahovat "aktivní". |
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

V případě úspěchu vrátí odpověď obnovené informace o uživateli v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
