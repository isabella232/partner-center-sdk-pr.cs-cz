---
title: Získání stavu nahrání dávek zařízení
description: Jak získat stav dávkového nahrávání zařízení pro konkrétního zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6c84e3e9f8717a0ecfb75c19291ca397c48e2435864d2c22d3dac893a1007f7f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996100"
---
# <a name="get-the-status-of-a-device-batch-upload"></a>Získání stavu nahrání dávek zařízení

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)

Jak získat stav dávkového nahrávání zařízení pro konkrétního zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor sledování dávky vrácený v hlavičce Location při odeslané dávce zařízení. Další informace najdete v [Upload seznamu zařízení pro zadaného zákazníka.](upload-a-list-of-devices-for-the-specified-customer.md)

## <a name="c"></a>C\#

Pokud chcete získat stav dávkového nahrávání zařízení, nejprve zavolejte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a načtěte rozhraní pro operace u zadaného zákazníka. Potom zavolejte [**metodu BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) s ID sledování dávky, abyste získali rozhraní pro operace stavu dávkového nahrávání. Nakonec zavolejte [**metodu Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) nebo [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) která načte stav.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** GetBatchUploadStatus.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/batchJobStatus/{batchtracking-id} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření požadavku použijte následující parametry cesty.

| Název             | Typ   | Vyžadováno | Popis                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id zákazníka      | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.                                                                                                                          |
| batchtracking-id | řetězec | Yes      | Identifikátor ve formátu GUID, který se používá k načtení stavu dávkového nahrávání zařízení. Toto ID se vrátí v hlavičce Location (Umístění), když se dávka zařízení úspěšně odeslala. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádná

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu odpověď obsahuje prostředek [BatchUploadDetails.](device-deployment-resources.md#batchuploaddetails)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```
