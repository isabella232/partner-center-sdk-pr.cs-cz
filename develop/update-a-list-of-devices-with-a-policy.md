---
title: Aktualizace seznamu zařízení s využitím zásad
description: Jak aktualizovat seznam zařízení se zásadami konfigurace pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04c2ef33116335db40bd2934dc7e33d57f015097
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767002"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>Aktualizace seznamu zařízení s využitím zásad

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo

Jak aktualizovat seznam zařízení se zásadami konfigurace pro zadaného zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor zásady.

- Identifikátory zařízení, která se mají aktualizovat

## <a name="c"></a>C\#

Chcete-li aktualizovat seznam zařízení se zadanou zásadou konfigurace, nejprve vytvořte instanci [list/dotnet/API/System. Collections. Generic. list -1) typu [nenašla/dotnet/API/System. Collections. Generic. nenašla -2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) a přidejte zásadu, která se má použít, jak je znázorněno v následujícím příkladu kódu. Budete potřebovat identifikátor zásady.

Pak vytvořte seznam objektů [**zařízení**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) , které se mají aktualizovat pomocí zásad, zadáním identifikátoru zařízení a seznamu obsahujícího zásadu, která se má použít, pro každé zařízení. Dále vytvořte instanci objektu [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) a nastavte vlastnost [**zařízení**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na seznam objektů zařízení.

Chcete-li zpracovat žádost o aktualizaci zásad zařízení, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka, aby bylo možné načíst rozhraní k operacím zadaného zákazníka. Pak načtěte vlastnost [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) a získejte rozhraní pro operace shromažďování zařízení zákazníka. Nakonec zavolejte metodu [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) s objektem DevicePolicyUpdateRequest a aktualizujte zařízení pomocí zásad.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;
string selectedDeviceId;

// Indicate the policy to apply to the list of devices.
List<KeyValuePair<PolicyCategory, string>>
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdateDevicesPolicy.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **POUŽITA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/DevicePolicyUpdates HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření žádosti použít následující parametry cesty.

| Název        | Typ   | Vyžadováno | Popis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tělo žádosti musí obsahovat prostředek [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) .

### <a name="request-example"></a>Příklad požadavku

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který lze použít k načtení stavu tohoto dávkového procesu. Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```
