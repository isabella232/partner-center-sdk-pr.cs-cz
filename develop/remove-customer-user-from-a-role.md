---
title: Odebrání uživatele zákazníka z role
description: Jak odebrat uživatele z role adresáře v rámci účtu zákazníka
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253e86f3733bbf2b9c593c5ca3f3e2fccce7c2c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766967"
---
# <a name="remove-a-customer-user-from-a-role"></a>Odebrání uživatele zákazníka z role

**Platí pro**

- Partnerské centrum

Jak odebrat uživatele z role adresáře v rámci účtu zákazníka

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Chcete-li odebrat uživatele z role adresáře, vyberte zákazníka s uživatelem, který chcete upravit pomocí volání metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) , a od této role zadejte roli pomocí metody [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) s ID role adresáře. Pak přejděte k metodě [**UserMembers. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) a Identifikujte uživatele, který chcete odebrat, a metodu [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) pro odebrání uživatele z role.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: RemoveCustomerUserMemberFromDirectoryRole.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda     | Identifikátor URI žádosti                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **DSTRANIT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers/{User-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci správného zákazníka, role a uživatele použijte následující parametry identifikátoru URI.

| Název                   | Typ     | Vyžadováno | Popis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka (zákazníka** ), který identifikuje zákazníka. |
| **ID role**            | **guid** | Y        | Hodnota je identifikátor GUID s formátovaným **ID** , který identifikuje roli.                |
| **ID uživatele**            | **guid** | Y        | Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který identifikuje jeden uživatelský účet.   |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

Pokud se uživatel z role úspěšně odebere, tělo odpovědi je prázdné.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
