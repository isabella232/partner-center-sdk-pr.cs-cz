---
title: Nahrání seznamu zařízení do stávající dávky pro konkrétního zákazníka
description: Jak nahrát seznam informací o zařízeních do existující dávky pro zadaného zákazníka. Tím se zařízení přidruží k již vytvořené dávce zařízení.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d01ac1a42c50416487167070be9d104562300baf
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766999"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>Nahrání seznamu zařízení do stávající dávky pro konkrétního zákazníka

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo

Jak nahrát seznam informací o zařízeních do existující dávky pro zadaného zákazníka. Tím se zařízení přidruží k již vytvořené dávce zařízení.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor dávky zařízení

- Seznam prostředků zařízení, které poskytují informace o jednotlivých zařízeních.

## <a name="c"></a>C\#

Pokud chcete nahrát seznam zařízení do existující dávky zařízení, nejdřív vytvořte instanci nového objektu [list/dotnet/API/System. Collections. Generic. list -1) typu [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) a naplňte seznam pomocí zařízení. Pro identifikaci každého zařízení se vyžadují minimálně následující kombinace naplněných vlastností:

- [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).

- [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).

- [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).

- Pouze [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .

- Pouze [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .

- [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**Model**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).

Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka, aby bylo možné načíst rozhraní k operacím zadaného zákazníka. V dalším kroku zavolejte metodu [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) s identifikátorem dávky zařízení, aby se získalo rozhraní pro operaci pro zadanou dávku. Nakonec zavolejte metodu [**Devices. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) pomocí seznamu zařízení, aby se zařízení přidala do dávky zařízení.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateDevices.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření žádosti použijte následující cestu a parametry dotazu.

| Název           | Typ   | Vyžadováno | Popis                                           |
|----------------|--------|----------|-------------------------------------------------------|
| ID zákazníka    | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |
| devicebatch-ID | řetězec | Yes      | Identifikátor řetězce identifikující dávku zařízení. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tělo žádosti musí obsahovat pole objektů [zařízení](device-deployment-resources.md#device) . Jsou přijaty následující kombinace polí pro identifikaci zařízení:

- hardwareHash + productKey.
- hardwareHash + sériové.
- hardwareHash + productKey + sériové.
- pouze hardwareHash.
- pouze productKey.
- Sériové + oemManufacturerName + model.

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a>Odpověď REST

Pokud je úspěšná, odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který se dá použít k načtení stavu nahrávání zařízení. Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
