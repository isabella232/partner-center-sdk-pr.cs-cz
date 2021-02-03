---
title: Aktualizace uživatelských účtů pro zákazníka
description: Aktualizujte podrobnosti v existujícím uživatelském účtu pro zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 52a43341bf2c3ba64d8c232af01f3fbae6765d82
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766812"
---
# <a name="update-user-accounts-for-a-customer"></a>Aktualizace uživatelských účtů pro zákazníka

**Platí pro**

- Partnerské centrum

Aktualizujte podrobnosti v existujícím uživatelském účtu pro zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Chcete-li aktualizovat podrobnosti pro zadaného uživatele zákazníka, napřed si načtěte zadané ID zákazníka a uživatele, které chcete aktualizovat. Pak v novém objektu **CustomerUser** vytvořte aktualizovanou verzi uživatele. Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** . Pak zavolejte vlastnost **Users** , metodu **ById ()** následovanou metodou **patch ()** .

``` csharp
// string selectedCustomerId;
// customerUser specifiedUser;
// IAggregatePartner partnerOperations;

// Updated information
var userToUpdate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "testPw@!122B" },
    DisplayName = "DisplayNameChange",
    FirstName = "FirstNameChange",
    LastName = "LastNameChange",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

// Update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: PartnerSDK. FeatureSamples **Třída**: CustomerUserUpdate.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| **POUŽITA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci správného zákazníka použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci. |
| **ID uživatele**            | **guid** | Y        | Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.                                                                       |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

### <a name="request-example"></a>Příklad požadavku

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "new country/region code",

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda uživatelský účet s aktualizovanými informacemi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "new country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "emailidchange@abcdefgh1234.ccsctp.net",
  "firstName": "FirstNameChange",
  "lastName": "LastNameChange",
  "displayName": "DisplayNameChange",
  "userDomainType": "none",
  "state": "active",
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/4b10bf41-ab11-40e3-8c53-cd67849b50de",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
