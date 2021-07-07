---
title: Nahrání seznamu zařízení pro vytvoření nové dávky pro konkrétního zákazníka
description: Jak nahrát seznam informací o zařízeních a vytvořit novou dávku pro zadaného zákazníka. Tím se vytvoří dávka zařízení pro registraci v nasazení s nulovým dotykem a přidružíme zařízení a dávku zařízení k zadanému zákazníkovi.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 285af12034562262c99b2aa3b139e948b0fdd462
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529728"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a>Nahrání seznamu zařízení pro vytvoření nové dávky pro konkrétního zákazníka

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo

Jak nahrát seznam informací o zařízeních a vytvořit novou dávku pro zadaného zákazníka. Tím se vytvoří dávka zařízení pro registraci v nasazení s nulovým dotykem a přidružíme zařízení a dávku zařízení k zadanému zákazníkovi.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele. Použijte [zabezpečený model aplikace](enable-secure-app-model.md) při použití ověřování aplikací a uživatelů s rozhraními API partnerského centra.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Seznam prostředků zařízení, které poskytují informace o jednotlivých zařízeních.

## <a name="c"></a>C\#

Postup nahrání seznamu zařízení pro vytvoření nové dávky zařízení:

1. Vytvořte instanci New [list/dotnet/API/System. Collections. Generic. list -1) typu [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) a naplňte seznam pomocí zařízení. Pro identifikaci každého zařízení se vyžadují minimálně následující kombinace naplněných vlastností:

   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).
   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).
   - [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).
   - Pouze [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .
   - Pouze [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .
   - [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**Model**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).

2. Vytvořte instanci objektu [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) a nastavte vlastnost [**ID dávky**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) na jedinečný název, který zvolíte, a vlastnost [**zařízení**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na seznam zařízení, která se mají nahrát.

3. Zpracujte žádost o vytvoření dávky zařízení voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka, který načte rozhraní pro konkrétního zákazníka.

4. Chcete-li vytvořit dávku, zavolejte metodu [**DeviceBatches. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) s žádostí o vytvoření dávky zařízení.

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: **třída** microsoft Partner SDK samples: CreateDeviceBatch. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Při vytváření žádosti použít následující parametry cesty.

| Název        | Typ   | Vyžadováno | Popis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tělo žádosti musí obsahovat prostředek [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) .

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

Pokud je úspěšná, odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který se dá použít k načtení stavu nahrávání zařízení. Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

#### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```
