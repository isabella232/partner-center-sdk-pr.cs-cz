---
title: Aktualizace seznamu zařízení s využitím zásad
description: Postup aktualizace seznamu zařízení pomocí zásad konfigurace pro zadaného zákazníka
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35b35873eb253b0929bfc01662b0beb9b31d0c6b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530068"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>Aktualizace seznamu zařízení s využitím zásad

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)

Postup aktualizace seznamu zařízení pomocí zásad konfigurace pro zadaného zákazníka

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor zásady.

- Identifikátory zařízení, která se má aktualizovat.

## <a name="c"></a>C\#

Pokud chcete aktualizovat seznam zařízení pomocí zadaných zásad konfigurace, nejprve vytvořte instanci [List/dotnet/api/system.collections.generic.list-1) typu [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) a přidejte zásadu, která se má použít, jak je znázorněno v následujícím příkladu kódu. Budete potřebovat identifikátor zásady.

Pak vytvořte seznam Objektů [**zařízení,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) které se mají aktualizovat pomocí zásad a zadejte identifikátor zařízení a seznam obsahující zásadu, která se má použít, pro každé zařízení. Dále vytvořte instanci objektu [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) a nastavte vlastnost [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na seznam objektů zařízení.

Pokud chcete zpracovat požadavek na aktualizaci zásad zařízení, zavolejte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka a načtěte rozhraní pro operace zadaného zákazníka. Potom načtěte vlastnost [**DevicePolicy,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) abyste získali rozhraní pro operace shromažďování zařízení zákazníka. Nakonec zavolejte [**metodu Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) s objektem DevicePolicyUpdateRequest a aktualizujte zařízení pomocí zásad.

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

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project**: SDK pro Partnerské centrum Samples **– třída:** UpdateDevicesPolicy.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda    | Identifikátor URI žádosti                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **Oprava** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/DevicePolicyUpdates HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření požadavku použijte následující parametry cesty.

| Název        | Typ   | Vyžadováno | Popis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| id zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Text požadavku musí obsahovat prostředek [DevicePolicyUpdateRequest.](device-deployment-resources.md#devicepolicyupdaterequest)

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

V případě úspěchu odpověď obsahuje **hlavičku Location** s identifikátorem URI, který lze použít k načtení stavu tohoto dávkového procesu. Uložte si tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
