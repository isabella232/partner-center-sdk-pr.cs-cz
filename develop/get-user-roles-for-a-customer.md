---
title: Získání uživatelských rolí pro zákazníka
description: Získá seznam všech rolí/oprávnění připojených k uživatelskému účtu. Mezi varianty patří získání seznamu všech oprávnění pro zákazníka a získání seznamu uživatelů, kteří mají danou roli.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b139ee69ae5148896b1a438b061907e022175f318956667cebb91ead15b863f6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989334"
---
# <a name="get-user-roles-for-a-customer"></a>Získání uživatelských rolí pro zákazníka

Získá seznam všech rolí/oprávnění připojených k uživatelskému účtu. Mezi varianty patří získání seznamu všech oprávnění pro zákazníka a získání seznamu uživatelů, kteří mají danou roli.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Pokud chcete načíst všechny role adresáře pro určitého zákazníka, napřed si načtěte zadané ID zákazníka. Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** . Poté zavolejte vlastnost **DirectoryRoles** , za kterou následuje metoda **Get ()** nebo **GetAsync ()**.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: **třída** microsoft Partner SDK samples: GetCustomerDirectoryRoles. cs

Pokud chcete načíst seznam zákaznických uživatelů, kteří mají danou roli, nejdřív načtěte zadané ID zákazníka a ID role adresáře. Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** . Pak zavolejte vlastnost **DirectoryRoles** , potom metodu **ById ()** , pak vlastnost **UserMembers** , za kterou následuje metoda **Get ()** nebo **GetAsync ()** .

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: PartnerSDK. FeatureSamples **třída**: GetCustomerDirectoryRoleUserMembers. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID}/directoryroles HTTP/1.1 |
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles HTTP/1.1                 |
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers    |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci správného zákazníka použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.                                                      |
| **ID uživatele**            | **guid** | N        | Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.                                                                                                                            |
| **ID role**            | **guid** | N        | Hodnota je **ID formátované role** identifikátoru GUID, která patří do typu role. Tato ID můžete získat dotazem na všechny role adresáře pro zákazníka v rámci všech uživatelských účtů. (Druhý scénář výše). |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí seznam rolí přidružených k danému uživatelskému účtu.

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
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
