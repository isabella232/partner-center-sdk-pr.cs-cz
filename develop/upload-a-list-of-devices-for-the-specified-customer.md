---
title: Nahrání seznamu zařízení do stávající dávky pro konkrétního zákazníka
description: Postup nahrání seznamu informací o zařízeních do existující dávky pro zadaného zákazníka Tím se zařízení přidruží k již vytvořené dávce zařízení.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d83812f32312d5742fd69c43456cb3ba64dca56bc0c81fe6eedb14d2c010a7fc
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995471"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>Nahrání seznamu zařízení do stávající dávky pro konkrétního zákazníka

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)

Postup nahrání seznamu informací o zařízeních do existující dávky pro zadaného zákazníka Tím se zařízení přidruží k již vytvořené dávce zařízení.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor dávky zařízení.

- Seznam prostředků zařízení, které poskytují informace o jednotlivých zařízeních.

## <a name="c"></a>C\#

Pokud chcete nahrát seznam zařízení do existující dávky zařízení, nejprve vytvořte instanci nového typu [List/dotnet/api/system.collections.generic.list-1) typu Zařízení a naplňte seznam zařízeními. [](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) Pro identifikaci jednotlivých zařízení se vyžaduje minimálně následující kombinace naplněných vlastností:

- [**Hardwarováhash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).

- [**Hardwarováhash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).

- [**Hardwarováhash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Klíč produktu**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).

- [**Pouze HardwareHash.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)

- [**Jenom ProductKey.**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)

- [**Sériové číslo**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).

Potom zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka a načtěte rozhraní pro operace v zadaném zákazníkovi. Dále zavolejte [**metodu DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) s identifikátorem dávky zařízení, abyste získali rozhraní pro operace pro zadanou dávku. Nakonec zavolejte [**metodu Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) se seznamem zařízení a přidejte zařízení do dávky zařízení.

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

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** CreateDevices.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/deviceBatches/{ID_nácrtu_zařízení}/http/1.1 zařízení |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření požadavku použijte následující cestu a parametry dotazu.

| Název           | Typ   | Vyžadováno | Popis                                           |
|----------------|--------|----------|-------------------------------------------------------|
| id zákazníka    | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |
| devicebatch-id | řetězec | Yes      | Identifikátor řetězce, který identifikuje dávku zařízení. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Text požadavku musí obsahovat pole [objektů](device-deployment-resources.md#device) Zařízení. Akceptují se následující kombinace polí pro identifikaci zařízení:

- hardwareHash + productKey.
- hardwareHash + serialNumber.
- hardwareHash + productKey + serialNumber.
- Pouze hardwareHash.
- Jenom productKey.
- serialNumber + oemManufacturerName + modelName.

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

V případě úspěchu odpověď obsahuje **hlavičku Location** s identifikátorem URI, který je možné použít k načtení stavu nahrávání zařízení. Uložte si tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
