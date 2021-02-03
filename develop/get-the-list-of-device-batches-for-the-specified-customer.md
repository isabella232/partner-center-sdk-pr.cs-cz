---
title: Získání seznamu dávek zařízení pro konkrétního zákazníka
description: Jak načíst kolekci dávek zařízení pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea5797bbaff4d4eafd1e63428556ab784bcb0ee2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767021"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a>Získání seznamu dávek zařízení pro konkrétního zákazníka

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo

Jak načíst kolekci dávek zařízení pro zadaného zákazníka.

Každá dávka zařízení obsahuje souhrnné informace o stavu zařízení, která jsou zaregistrovaná v nasazení s nulovým dotykem.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Chcete-li získat kolekci dávek zařízení pro zadaného zákazníka, nejprve zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní k operacím zadaného zákazníka. Pak načtěte hodnotu vlastnosti [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) , abyste získali rozhraní pro operace shromažďování dávky zařízení. Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) načtěte kolekci.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetDevicesBatches.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření žádosti použít následující parametry cesty.

| Název        | Typ   | Vyžadováno | Popis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [DeviceBatch](device-deployment-resources.md#devicebatch) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 339
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "Test batch",
            "status": "finished",
            "creationDate": "2017-07-25T01:51:00",
            "devicesCount": 5,
            "devicesLink": {
                "uri": "/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/Test batch/devices",
                "method": "GET",
                "headers": []
            },
            "attributes": {
                "objectType": "DeviceBatch"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
