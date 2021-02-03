---
title: Získání stavu nahrání dávek zařízení
description: Jak získat stav nahrávání dávky zařízení pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fb887ba257d6fbe68f95ae4b59d701ac4c934860
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767016"
---
# <a name="get-the-status-of-a-device-batch-upload"></a>Získání stavu nahrání dávek zařízení

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo

Jak získat stav nahrávání dávky zařízení pro zadaného zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor sledování dávky vrácený v hlavičce umístění při odeslání dávky zařízení. Další informace najdete v tématu [nahrání seznamu zařízení pro zadaného zákazníka](upload-a-list-of-devices-for-the-specified-customer.md).

## <a name="c"></a>C\#

Pokud chcete získat stav dávkového nahrání zařízení, nejdřív zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro konkrétního zákazníka. Pak zavolejte metodu [**BatchUploadStatus. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) s ID sledování dávky, aby se získalo rozhraní pro dávkové odesílání operací stavu. Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) načtěte stav.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetBatchUploadStatus.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/batchJobStatus/{batchtracking-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření žádosti použít následující parametry cesty.

| Název             | Typ   | Vyžadováno | Popis                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID zákazníka      | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.                                                                                                                          |
| batchtracking-ID | řetězec | Yes      | Identifikátor GUID, který se používá k načtení stavu nahrávání dávky zařízení. Toto ID se vrátí v hlavičce umístění po úspěšném odeslání dávky zařízení. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

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

V případě úspěchu obsahuje odpověď prostředek [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
