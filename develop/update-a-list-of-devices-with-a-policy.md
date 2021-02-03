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
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="80bb1-103">Aktualizace seznamu zařízení s využitím zásad</span><span class="sxs-lookup"><span data-stu-id="80bb1-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="80bb1-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="80bb1-104">**Applies To**</span></span>

- <span data-ttu-id="80bb1-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="80bb1-105">Partner Center</span></span>
- <span data-ttu-id="80bb1-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="80bb1-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="80bb1-107">Jak aktualizovat seznam zařízení se zásadami konfigurace pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="80bb1-107">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80bb1-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="80bb1-108">Prerequisites</span></span>

- <span data-ttu-id="80bb1-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="80bb1-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80bb1-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="80bb1-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="80bb1-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80bb1-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="80bb1-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="80bb1-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="80bb1-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="80bb1-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="80bb1-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="80bb1-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="80bb1-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="80bb1-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="80bb1-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80bb1-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="80bb1-117">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="80bb1-117">The policy identifier.</span></span>

- <span data-ttu-id="80bb1-118">Identifikátory zařízení, která se mají aktualizovat</span><span class="sxs-lookup"><span data-stu-id="80bb1-118">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="80bb1-119">C\#</span><span class="sxs-lookup"><span data-stu-id="80bb1-119">C\#</span></span>

<span data-ttu-id="80bb1-120">Chcete-li aktualizovat seznam zařízení se zadanou zásadou konfigurace, nejprve vytvořte instanci [list/dotnet/API/System. Collections. Generic. list -1) typu [nenašla/dotnet/API/System. Collections. Generic. nenašla -2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) a přidejte zásadu, která se má použít, jak je znázorněno v následujícím příkladu kódu.</span><span class="sxs-lookup"><span data-stu-id="80bb1-120">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="80bb1-121">Budete potřebovat identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="80bb1-121">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="80bb1-122">Pak vytvořte seznam objektů [**zařízení**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) , které se mají aktualizovat pomocí zásad, zadáním identifikátoru zařízení a seznamu obsahujícího zásadu, která se má použít, pro každé zařízení.</span><span class="sxs-lookup"><span data-stu-id="80bb1-122">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="80bb1-123">Dále vytvořte instanci objektu [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) a nastavte vlastnost [**zařízení**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na seznam objektů zařízení.</span><span class="sxs-lookup"><span data-stu-id="80bb1-123">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="80bb1-124">Chcete-li zpracovat žádost o aktualizaci zásad zařízení, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka, aby bylo možné načíst rozhraní k operacím zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="80bb1-124">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="80bb1-125">Pak načtěte vlastnost [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) a získejte rozhraní pro operace shromažďování zařízení zákazníka.</span><span class="sxs-lookup"><span data-stu-id="80bb1-125">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="80bb1-126">Nakonec zavolejte metodu [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) s objektem DevicePolicyUpdateRequest a aktualizujte zařízení pomocí zásad.</span><span class="sxs-lookup"><span data-stu-id="80bb1-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

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

<span data-ttu-id="80bb1-127">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="80bb1-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80bb1-128">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdateDevicesPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="80bb1-128">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="80bb1-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="80bb1-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80bb1-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="80bb1-130">Request syntax</span></span>

| <span data-ttu-id="80bb1-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="80bb1-131">Method</span></span>    | <span data-ttu-id="80bb1-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="80bb1-132">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80bb1-133">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="80bb1-133">**PATCH**</span></span> | <span data-ttu-id="80bb1-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/DevicePolicyUpdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="80bb1-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="80bb1-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="80bb1-135">URI parameter</span></span>

<span data-ttu-id="80bb1-136">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="80bb1-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="80bb1-137">Název</span><span class="sxs-lookup"><span data-stu-id="80bb1-137">Name</span></span>        | <span data-ttu-id="80bb1-138">Typ</span><span class="sxs-lookup"><span data-stu-id="80bb1-138">Type</span></span>   | <span data-ttu-id="80bb1-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="80bb1-139">Required</span></span> | <span data-ttu-id="80bb1-140">Popis</span><span class="sxs-lookup"><span data-stu-id="80bb1-140">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="80bb1-141">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="80bb1-141">customer-id</span></span> | <span data-ttu-id="80bb1-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="80bb1-142">string</span></span> | <span data-ttu-id="80bb1-143">Yes</span><span class="sxs-lookup"><span data-stu-id="80bb1-143">Yes</span></span>      | <span data-ttu-id="80bb1-144">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="80bb1-144">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="80bb1-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="80bb1-145">Request headers</span></span>

<span data-ttu-id="80bb1-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="80bb1-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80bb1-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="80bb1-147">Request body</span></span>

<span data-ttu-id="80bb1-148">Tělo žádosti musí obsahovat prostředek [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) .</span><span class="sxs-lookup"><span data-stu-id="80bb1-148">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="80bb1-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="80bb1-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="80bb1-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="80bb1-150">REST response</span></span>

<span data-ttu-id="80bb1-151">V případě úspěchu odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který lze použít k načtení stavu tohoto dávkového procesu.</span><span class="sxs-lookup"><span data-stu-id="80bb1-151">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="80bb1-152">Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.</span><span class="sxs-lookup"><span data-stu-id="80bb1-152">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80bb1-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="80bb1-153">Response success and error codes</span></span>

<span data-ttu-id="80bb1-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="80bb1-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80bb1-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="80bb1-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80bb1-156">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="80bb1-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80bb1-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="80bb1-157">Response example</span></span>

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
