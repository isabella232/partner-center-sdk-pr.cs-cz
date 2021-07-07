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
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="e22dc-104">Nahrání seznamu zařízení pro vytvoření nové dávky pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="e22dc-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="e22dc-105">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="e22dc-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e22dc-106">Jak nahrát seznam informací o zařízeních a vytvořit novou dávku pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e22dc-106">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="e22dc-107">Tím se vytvoří dávka zařízení pro registraci v nasazení s nulovým dotykem a přidružíme zařízení a dávku zařízení k zadanému zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="e22dc-107">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e22dc-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e22dc-108">Prerequisites</span></span>

- <span data-ttu-id="e22dc-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e22dc-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e22dc-110">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="e22dc-110">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="e22dc-111">Použijte [zabezpečený model aplikace](enable-secure-app-model.md) při použití ověřování aplikací a uživatelů s rozhraními API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e22dc-111">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="e22dc-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e22dc-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e22dc-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e22dc-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e22dc-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e22dc-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e22dc-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e22dc-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e22dc-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e22dc-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e22dc-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e22dc-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e22dc-118">Seznam prostředků zařízení, které poskytují informace o jednotlivých zařízeních.</span><span class="sxs-lookup"><span data-stu-id="e22dc-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="e22dc-119">C\#</span><span class="sxs-lookup"><span data-stu-id="e22dc-119">C\#</span></span>

<span data-ttu-id="e22dc-120">Postup nahrání seznamu zařízení pro vytvoření nové dávky zařízení:</span><span class="sxs-lookup"><span data-stu-id="e22dc-120">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="e22dc-121">Vytvořte instanci New [list/dotnet/API/System. Collections. Generic. list -1) typu [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) a naplňte seznam pomocí zařízení.</span><span class="sxs-lookup"><span data-stu-id="e22dc-121">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="e22dc-122">Pro identifikaci každého zařízení se vyžadují minimálně následující kombinace naplněných vlastností:</span><span class="sxs-lookup"><span data-stu-id="e22dc-122">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="e22dc-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="e22dc-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="e22dc-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="e22dc-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="e22dc-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="e22dc-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="e22dc-126">Pouze [**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="e22dc-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="e22dc-127">Pouze [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="e22dc-127">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="e22dc-128">[**Sériové**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**Model**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="e22dc-128">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="e22dc-129">Vytvořte instanci objektu [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) a nastavte vlastnost [**ID dávky**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) na jedinečný název, který zvolíte, a vlastnost [**zařízení**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na seznam zařízení, která se mají nahrát.</span><span class="sxs-lookup"><span data-stu-id="e22dc-129">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="e22dc-130">Zpracujte žádost o vytvoření dávky zařízení voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka, který načte rozhraní pro konkrétního zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e22dc-130">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="e22dc-131">Chcete-li vytvořit dávku, zavolejte metodu [**DeviceBatches. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) s žádostí o vytvoření dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="e22dc-131">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

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

<span data-ttu-id="e22dc-132">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e22dc-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e22dc-133">**Project**: **třída** microsoft Partner SDK samples: CreateDeviceBatch. cs</span><span class="sxs-lookup"><span data-stu-id="e22dc-133">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e22dc-134">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e22dc-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e22dc-135">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e22dc-135">Request syntax</span></span>

| <span data-ttu-id="e22dc-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="e22dc-136">Method</span></span>   | <span data-ttu-id="e22dc-137">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e22dc-137">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="e22dc-138">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="e22dc-138">**POST**</span></span> | <span data-ttu-id="e22dc-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e22dc-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e22dc-140">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e22dc-140">URI parameter</span></span>

<span data-ttu-id="e22dc-141">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="e22dc-141">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="e22dc-142">Název</span><span class="sxs-lookup"><span data-stu-id="e22dc-142">Name</span></span>        | <span data-ttu-id="e22dc-143">Typ</span><span class="sxs-lookup"><span data-stu-id="e22dc-143">Type</span></span>   | <span data-ttu-id="e22dc-144">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e22dc-144">Required</span></span> | <span data-ttu-id="e22dc-145">Popis</span><span class="sxs-lookup"><span data-stu-id="e22dc-145">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e22dc-146">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="e22dc-146">customer-id</span></span> | <span data-ttu-id="e22dc-147">řetězec</span><span class="sxs-lookup"><span data-stu-id="e22dc-147">string</span></span> | <span data-ttu-id="e22dc-148">Yes</span><span class="sxs-lookup"><span data-stu-id="e22dc-148">Yes</span></span>      | <span data-ttu-id="e22dc-149">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e22dc-149">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e22dc-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e22dc-150">Request headers</span></span>

<span data-ttu-id="e22dc-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e22dc-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e22dc-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e22dc-152">Request body</span></span>

<span data-ttu-id="e22dc-153">Tělo žádosti musí obsahovat prostředek [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) .</span><span class="sxs-lookup"><span data-stu-id="e22dc-153">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="e22dc-154">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e22dc-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e22dc-155">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e22dc-155">REST response</span></span>

<span data-ttu-id="e22dc-156">Pokud je úspěšná, odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který se dá použít k načtení stavu nahrávání zařízení.</span><span class="sxs-lookup"><span data-stu-id="e22dc-156">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="e22dc-157">Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.</span><span class="sxs-lookup"><span data-stu-id="e22dc-157">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e22dc-158">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e22dc-158">Response success and error codes</span></span>

<span data-ttu-id="e22dc-159">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e22dc-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e22dc-160">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e22dc-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e22dc-161">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e22dc-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="e22dc-162">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e22dc-162">Response example</span></span>

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
