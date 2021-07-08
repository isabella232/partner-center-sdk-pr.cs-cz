---
title: Získání seznamu dostupných licencí podle skupiny licencí
description: Jak získat seznam licencí pro zadané skupiny licencí dostupné uživatelům zadaného zákazníka.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: de59dfccf723c8f2411d9dadc51beb88688d5b02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874512"
---
# <a name="get-a-list-of-available-licenses-by-license-group"></a>Získání seznamu dostupných licencí podle skupiny licencí

Jak získat seznam licencí pro zadané skupiny licencí dostupné uživatelům zadaného zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Seznam jednoho nebo více identifikátorů skupin licencí.

## <a name="c"></a>C\#

Pokud chcete získat seznam dostupných licencí pro zadané skupiny licencí, začněte vytvořením instance [seznamu](/dotnet/api/system.collections.generic.list-1) typu [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)a pak skupiny licencí přidejte do seznamu. Dále k identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka. Pak získejte hodnotu vlastnosti [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) a načtěte rozhraní pro operace kolekce SKU odebíraných zákazníkem. Nakonec předejte seznam skupin licencí metodě [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) nebo [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) která načte seznam předplacených skladových položek s podrobnostmi o dostupných licenčních jednotkách.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get subscribed SKUs available for group1, the license group for Azure Active Directory (AAD).
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1};
var customerUserAadSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get subscribed SKUs available for group2, the license group for Minecraft product licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group2};
var customerUserSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get both AAD and Minecraft subscribed SKUs.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1, LicenseGroupId.Group2};
var customerUserBothAadAndSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{id_zákazníka}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1                        |
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1                        |
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Pomocí následující cesty a parametrů dotazu identifikujte zákazníka a skupiny licencí.

| Název            | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id zákazníka     | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.                                                                                                                                                                                                                 |
| licenseGroupIds | řetězec | No       | Hodnota výčtu, která označuje skupinu licencí přiřazených licencí. Platné hodnoty: Group1, Group2 Group1 – tato skupina obsahuje všechny produkty, jejichž licenci je možné spravovat v Azure Active Directory (AAD). Skupina2 – Tato skupina má pouze Minecraft licence k produktu. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu bude tělo odpovědi obsahovat kolekci prostředků [SubscribedSku.](license-resources.md#subscribedsku)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 4328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: S6Pd5XQAx0Ss/zQi.0
MS-ServerId: 030011719
Date: Sat, 10 Jun 2017 00:19:44 GMT

{
    "totalCount": 04,
    "items": [{
            "availableUnits": 15,
            "activeUnits": 15,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 15,
            "warningUnits": 0,
            "productSku": {
                "id": "078d2b04-f1bd-4111-bbd4-b4b1b354cef4",
                "name": "Azure Active Directory Premium P1",
                "skuPartNumber": "AAD_PREMIUM",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Exchange Foundation",
                    "serviceName": "EXCHANGE_S_FOUNDATION",
                    "id": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "capabilityStatus": "Enabled",
                    "targetType": "Tenant"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 1,
            "activeUnits": 1,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "54b84594-9c77-4499-8d65-5e0d5f410e78",
                "name": "Dynamics AX Task",
                "skuPartNumber": "AX_TASK_USER",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 23,
            "activeUnits": 72,
            "consumedUnits": 49,
            "suspendedUnits": 0,
            "totalUnits": 72,
            "warningUnits": 0,
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "targetType": "User",
                "licenseGroupId": "group2"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 71,
            "activeUnits": 112,
            "consumedUnits": 41,
            "suspendedUnits": 0,
            "totalUnits": 112,
            "warningUnits": 0,
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-skus-found"></a>Příklad odpovědi (nenašly se žádné odpovídající skladové položky)

Pokud pro zadané skupiny licencí nelze najít žádné odpovídající předplacené skladové položky, odpověď obsahuje prázdnou kolekci s elementem totalCount, jehož hodnota je 0.

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
