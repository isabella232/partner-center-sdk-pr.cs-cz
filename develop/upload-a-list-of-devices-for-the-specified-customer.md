---
title: Nahrání seznamu zařízení do stávající dávky pro konkrétního zákazníka
description: Jak nahrát seznam informací o zařízeních do existující dávky pro zadaného zákazníka. Tím se zařízení přidruží k již vytvořené dávce zařízení.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3fa9cff39113130c54cecfaef1f8ca28e0ac5adf
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530306"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a><span data-ttu-id="9e500-104">Nahrání seznamu zařízení do stávající dávky pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="9e500-104">Upload a list of devices to an existing batch for the specified customer</span></span>

<span data-ttu-id="9e500-105">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="9e500-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="9e500-106">Jak nahrát seznam informací o zařízeních do existující dávky pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9e500-106">How to upload a list of information about devices to an existing batch for the specified customer.</span></span> <span data-ttu-id="9e500-107">Tím se zařízení přidruží k již vytvořené dávce zařízení.</span><span class="sxs-lookup"><span data-stu-id="9e500-107">This associates the devices with a device batch already created.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e500-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9e500-108">Prerequisites</span></span>

- <span data-ttu-id="9e500-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9e500-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e500-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="9e500-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9e500-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9e500-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9e500-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="9e500-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9e500-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="9e500-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9e500-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="9e500-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9e500-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="9e500-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9e500-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9e500-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9e500-117">Identifikátor dávky zařízení</span><span class="sxs-lookup"><span data-stu-id="9e500-117">The device batch identifier.</span></span>

- <span data-ttu-id="9e500-118">Seznam prostředků zařízení, které poskytují informace o jednotlivých zařízeních.</span><span class="sxs-lookup"><span data-stu-id="9e500-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="9e500-119">C\#</span><span class="sxs-lookup"><span data-stu-id="9e500-119">C\#</span></span>

<span data-ttu-id="9e500-120">Pokud chcete nahrát seznam zařízení do existující dávky zařízení, nejdřív vytvořte instanci nového objektu [list/dotnet/API/System. Collections. Generic. list -1) typu [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) a naplňte seznam pomocí zařízení.</span><span class="sxs-lookup"><span data-stu-id="9e500-120">To upload a list of devices to an existing device batch, first, instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="9e500-121">Pro identifikaci každého zařízení se vyžadují minimálně následující kombinace naplněných vlastností:</span><span class="sxs-lookup"><span data-stu-id="9e500-121">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

- <span data-ttu-id="9e500-122">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="9e500-122">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>

- <span data-ttu-id="9e500-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="9e500-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="9e500-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="9e500-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="9e500-125">Pouze [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="9e500-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>

- <span data-ttu-id="9e500-126">Pouze [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="9e500-126">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>

- <span data-ttu-id="9e500-127">[**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**Model**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="9e500-127">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

<span data-ttu-id="9e500-128">Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka, aby bylo možné načíst rozhraní k operacím zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9e500-128">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="9e500-129">V dalším kroku zavolejte metodu [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) s identifikátorem dávky zařízení, aby se získalo rozhraní pro operaci pro zadanou dávku.</span><span class="sxs-lookup"><span data-stu-id="9e500-129">Next, call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span> <span data-ttu-id="9e500-130">Nakonec zavolejte metodu [**Devices. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) pomocí seznamu zařízení, aby se zařízení přidala do dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="9e500-130">Finally, call the [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) method with the list of devices to add the devices to the device batch.</span></span>

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

<span data-ttu-id="9e500-131">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9e500-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9e500-132">**Project**: **třída** microsoft Partner SDK samples: CreateDevices. cs</span><span class="sxs-lookup"><span data-stu-id="9e500-132">**Project**: Partner Center SDK Samples **Class**: CreateDevices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9e500-133">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="9e500-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e500-134">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="9e500-134">Request syntax</span></span>

| <span data-ttu-id="9e500-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="9e500-135">Method</span></span>   | <span data-ttu-id="9e500-136">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9e500-136">Request URI</span></span>                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9e500-137">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="9e500-137">**POST**</span></span> | <span data-ttu-id="9e500-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9e500-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9e500-139">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9e500-139">URI parameter</span></span>

<span data-ttu-id="9e500-140">Při vytváření žádosti použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="9e500-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="9e500-141">Název</span><span class="sxs-lookup"><span data-stu-id="9e500-141">Name</span></span>           | <span data-ttu-id="9e500-142">Typ</span><span class="sxs-lookup"><span data-stu-id="9e500-142">Type</span></span>   | <span data-ttu-id="9e500-143">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9e500-143">Required</span></span> | <span data-ttu-id="9e500-144">Popis</span><span class="sxs-lookup"><span data-stu-id="9e500-144">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="9e500-145">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="9e500-145">customer-id</span></span>    | <span data-ttu-id="9e500-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="9e500-146">string</span></span> | <span data-ttu-id="9e500-147">Yes</span><span class="sxs-lookup"><span data-stu-id="9e500-147">Yes</span></span>      | <span data-ttu-id="9e500-148">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9e500-148">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="9e500-149">devicebatch-ID</span><span class="sxs-lookup"><span data-stu-id="9e500-149">devicebatch-id</span></span> | <span data-ttu-id="9e500-150">řetězec</span><span class="sxs-lookup"><span data-stu-id="9e500-150">string</span></span> | <span data-ttu-id="9e500-151">Yes</span><span class="sxs-lookup"><span data-stu-id="9e500-151">Yes</span></span>      | <span data-ttu-id="9e500-152">Identifikátor řetězce identifikující dávku zařízení.</span><span class="sxs-lookup"><span data-stu-id="9e500-152">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9e500-153">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9e500-153">Request headers</span></span>

<span data-ttu-id="9e500-154">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9e500-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9e500-155">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9e500-155">Request body</span></span>

<span data-ttu-id="9e500-156">Tělo žádosti musí obsahovat pole objektů [zařízení](device-deployment-resources.md#device) .</span><span class="sxs-lookup"><span data-stu-id="9e500-156">The request body must contain an array of [Device](device-deployment-resources.md#device) objects.</span></span> <span data-ttu-id="9e500-157">Jsou přijaty následující kombinace polí pro identifikaci zařízení:</span><span class="sxs-lookup"><span data-stu-id="9e500-157">The following combinations of fields for identifying a device are accepted:</span></span>

- <span data-ttu-id="9e500-158">hardwareHash + productKey.</span><span class="sxs-lookup"><span data-stu-id="9e500-158">hardwareHash + productKey.</span></span>
- <span data-ttu-id="9e500-159">hardwareHash + sériové.</span><span class="sxs-lookup"><span data-stu-id="9e500-159">hardwareHash + serialNumber.</span></span>
- <span data-ttu-id="9e500-160">hardwareHash + productKey + sériové.</span><span class="sxs-lookup"><span data-stu-id="9e500-160">hardwareHash + productKey + serialNumber.</span></span>
- <span data-ttu-id="9e500-161">pouze hardwareHash.</span><span class="sxs-lookup"><span data-stu-id="9e500-161">hardwareHash only.</span></span>
- <span data-ttu-id="9e500-162">pouze productKey.</span><span class="sxs-lookup"><span data-stu-id="9e500-162">productKey only.</span></span>
- <span data-ttu-id="9e500-163">Sériové + oemManufacturerName + model.</span><span class="sxs-lookup"><span data-stu-id="9e500-163">serialNumber + oemManufacturerName + modelName.</span></span>

### <a name="request-example"></a><span data-ttu-id="9e500-164">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9e500-164">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9e500-165">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9e500-165">REST response</span></span>

<span data-ttu-id="9e500-166">Pokud je úspěšná, odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který se dá použít k načtení stavu nahrávání zařízení.</span><span class="sxs-lookup"><span data-stu-id="9e500-166">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="9e500-167">Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.</span><span class="sxs-lookup"><span data-stu-id="9e500-167">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e500-168">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="9e500-168">Response success and error codes</span></span>

<span data-ttu-id="9e500-169">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9e500-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9e500-170">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="9e500-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e500-171">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9e500-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9e500-172">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9e500-172">Response example</span></span>

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
