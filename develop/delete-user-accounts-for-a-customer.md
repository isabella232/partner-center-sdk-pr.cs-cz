---
title: Odstranění uživatelských účtů pro zákazníka
description: Postup odstranění existujícího uživatelského účtu pro zákazníka
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 64e9175a2a4545022175b326a2d765ecd6a1106242b8926fe19e32c7e2ab6ec2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994876"
---
# <a name="delete-a-user-account-for-a-customer"></a>Odstranění uživatelských účtů pro zákazníka

Tento článek vysvětluje, jak odstranit existující uživatelský účet zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID uživatele. Pokud id uživatele nemáte, podívejte se na část Získání seznamu [všech uživatelských účtů pro zákazníka.](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="deleting-a-user-account"></a>Odstranění uživatelského účtu

Když odstraníte uživatelský účet, stav uživatele bude po dobu 30 dnů **neaktivní.** Po 30 dnech se uživatelský účet a jeho přidružená data vyprázdní a nenapraví.

Odstraněný [uživatelský účet zákazníka můžete obnovit, pokud](restore-a-user-for-a-customer.md) se neaktivní účet nachází v 30denním okně. Když ale obnovíte odstraněný účet, který je označený jako neaktivní, nebude už tento účet vrácen jako člen kolekce uživatelů (například když získáte seznam všech uživatelských účtů pro [zákazníka).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="c"></a>C\#

Odstranění existujícího uživatelského účtu zákazníka:

1. K identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.

2. Voláním [**metody Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) identifikujte uživatele.

3. Voláním [**metody Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) odstraňte uživatele a nastavte stav uživatele na neaktivní.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** DeleteCustomerUser.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda     | Identifikátor URI žádosti                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/users/{ID_uživatele} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka a uživatele použijte následující parametry dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| customer-tenant-id     | Identifikátor GUID     | Y        | Hodnota je ID tenanta zákazníka ve formátu GUID, které prodejci umožňuje filtrovat výsledky pro daného zákazníka.  |
| user-id                | Identifikátor GUID     | Y        | Hodnota je ID uživatele ve **formátu** GUID, které patří k jednomu uživatelskému účtu.                                          |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí stavový kód **204 Žádný** obsah.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
