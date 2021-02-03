---
title: Získání licencí přiřazených uživateli podle skupiny licencí
description: Jak získat seznam licencí přiřazených uživateli pro zadané skupiny licencí.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 28c10e3e2acb30e4110213344959a87d4ddfcffb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766974"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a>Získání licencí přiřazených uživateli podle skupiny licencí

**Platí pro**

- Partnerské centrum

Jak získat seznam licencí přiřazených uživateli pro zadané skupiny licencí.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor uživatele

- Seznam jednoho nebo více identifikátorů skupin licencí.

## <a name="c"></a>C\#

Chcete-li zjistit, které licence jsou přiřazeny uživateli ze zadaných skupin licencí, Začněte vytvořením instance [list/dotnet/API/System. Collections. Generic. list -1) typu [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)a poté přidejte do seznamu skupiny licencí. Potom k identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka. Dále zavolejte metodu User [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID uživatele k identifikaci uživatele. Pak z vlastnosti [**licence**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) Získejte rozhraní pro uživatelské operace s uživatelskými licencemi. Nakonec předejte seznam skupin licencí do metody [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) , aby se načetla kolekce licencí přiřazených uživateli.

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Group1 HTTP/1.1                        |
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = skupina2 HTTP/1.1                        |
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Group1&LicenseGroupIds = skupina2 HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci zákazníka, uživatele a skupin licencí použijte následující cestu a parametry dotazu.

| Název            | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID zákazníka     | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.                                                                                                                                                                                                                 |
| user-id         | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje uživatele.                                                                                                                                                                                                                     |
| licenseGroupIds | řetězec | No       | Hodnota výčtu, která označuje skupinu licencí přiřazených licencí. Platné hodnoty: group1, Skupina2 Group1 – Tato skupina obsahuje všechny produkty, jejichž licence se dají spravovat v Azure Active Directory (AAD). Skupina2 – Tato skupina má pouze licence na produkty Minecraftu. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci [licenčních](license-resources.md#license) prostředků.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-licenses-found"></a>Příklad odpovědi (nenašly se žádné vyhovující licence)

Pokud pro zadané skupiny licencí nenajdete žádné vyhovující licence, odpověď obsahuje prázdnou kolekci s elementem totalCount, jehož hodnota je 0.

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
