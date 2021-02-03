---
title: Odstranění uživatelských účtů pro zákazníka
description: Jak odstranit existující uživatelský účet pro zákazníka.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766878"
---
# <a name="delete-a-user-account-for-a-customer"></a>Odstranění uživatelských účtů pro zákazníka

**Platí pro:**

- Partnerské centrum

Tento článek vysvětluje, jak odstranit existující uživatelský účet pro zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID uživatele Pokud nemáte ID uživatele, přečtěte si téma [získání seznamu všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md).

## <a name="deleting-a-user-account"></a>Odstranění uživatelského účtu

Po odstranění uživatelského účtu se stav uživatele nastaví na **neaktivní** po dobu třiceti dnů. Po 30 dnech se uživatelský účet a jeho přidružená data vyprázdní a provedou neobnovitelné.

[Odstraněný uživatelský účet můžete obnovit pro zákazníka](restore-a-user-for-a-customer.md) , pokud je neaktivní účet v rámci třiceti dnů. Když ale obnovíte účet, který se odstranil a je označený jako neaktivní, účet se už nevrátí jako člen kolekce uživatelů (například když [získáte seznam všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Odstranění existujícího uživatelského účtu zákazníka:

1. K identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.

2. Voláním metody User [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) Identifikujte uživatele.

3. Voláním metody [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) odstraňte uživatele a nastavte stav uživatele na neaktivní.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: DeleteCustomerUser.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda     | Identifikátor URI žádosti                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka a uživatele použijte následující parametry dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| Customer-tenant-ID     | Identifikátor GUID     | Y        | Hodnota je **zákazníkem** formátovaného identifikátoru GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka. |
| user-id                | Identifikátor GUID     | Y        | Hodnota je **uživatelské ID** formátované identifikátorem GUID, které patří jedinému uživatelskému účtu.                                          |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu tato metoda vrátí kód stavu **204 bez obsahu** .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
