---
title: Aktualizace kontaktu podpory pro předplatné
description: Jak aktualizovat kontakt na podporu pro předplatné na jednu z hodnot partnera, který přidal prodejce.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8c6b658cfe6e14c75b0c06b177920ce3eb1b4ed
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766947"
---
# <a name="update-a-subscriptions-support-contact"></a>Aktualizace kontaktu podpory pro předplatné

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak aktualizovat kontakt na podporu pro předplatné na jednu z hodnot partnera, který přidal prodejce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor předplatného.

- Informace o novém kontaktu podpory: identifikátor tenanta, identifikátor Microsoft Partner Network a název. Kontakt na podporu musí být jednou z hodnot partnera, který přidal prodejce.

## <a name="c"></a>C\#

Chcete-li aktualizovat kontakt podpory předplatného, nejprve vytvořte instanci a naplňte objekt [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) novými hodnotami. Potom k identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka. Dále Získejte rozhraní pro operace předplatného voláním metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID předplatného. Pak pomocí vlastnosti [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) Získejte rozhraní pro podporu operací kontaktů. Nakonec zavolejte metodu [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) nebo [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) s naplněným objektem SupportContact, abyste aktualizovali kontakt na podporu.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdateSubscriptionSupportContact.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/supportcontact HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci zákazníka a předplatného použijte následující parametry cesty.

| Název            | Typ   | Vyžadováno | Popis                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| ID zákazníka     | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.           |
| ID předplatného | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zkušební předplatné. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Do textu žádosti musíte zahrnout naplněný prostředek [SupportContact](subscription-resources.md#supportcontact) . Kontakt na podporu musí být stávající prodejce s vztahem k partnerovi.

### <a name="request-example"></a>Příklad požadavku

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi prostředek [SupportContact](subscription-resources.md#supportcontact) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
