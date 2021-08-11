---
title: Odstraní zařízení pro konkrétního zákazníka
description: Jak odstranit zařízení, které patří k zadanému zákazníkovi.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f44c94ff35ecdb709b44ba6eebc17ae37e513313d464a28378ce22ceb0097ee3
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995063"
---
# <a name="delete-a-device-for-the-specified-customer"></a>Odstraní zařízení pro konkrétního zákazníka

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo

Tento článek vysvětluje, jak odstranit zařízení, které patří k zadanému zákazníkovi.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor dávky zařízení

- Identifikátor zařízení

## <a name="c"></a>C\#

Postup odstranění zařízení pro zadaného zákazníka:

1. Voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka načtete rozhraní k operacím zákazníka.

2. Pro získání rozhraní pro zadanou dávku volejte metodu [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) s identifikátorem dávky zařízení.

3. Voláním metody [**Devices. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) Získejte rozhraní na určeném zařízení.

4. Voláním metody [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) nebo [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) odstraníte zařízení z dávky.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: **třída** microsoft Partner SDK samples: DeleteDevice. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda     | Identifikátor URI žádosti                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices/{Device-ID} HTTP/1.1  |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Při vytváření žádosti použít následující parametry cesty.

| Název           | Typ   | Vyžadováno | Popis                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| ID zákazníka    | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.              |
| devicebatch-ID | řetězec | Yes      | Identifikátor dávky zařízení v dávce, která obsahuje zařízení. |
| ID zařízení      | řetězec | Yes      | Identifikátor zařízení                                             |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádná

### <a name="request-example"></a>Příklad požadavku

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí odpověď **204 bez** stavového kódu obsahu.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
