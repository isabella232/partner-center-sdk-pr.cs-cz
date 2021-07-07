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
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="e7e24-103">Aktualizace seznamu zařízení s využitím zásad</span><span class="sxs-lookup"><span data-stu-id="e7e24-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="e7e24-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)</span><span class="sxs-lookup"><span data-stu-id="e7e24-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e7e24-105">Postup aktualizace seznamu zařízení pomocí zásad konfigurace pro zadaného zákazníka</span><span class="sxs-lookup"><span data-stu-id="e7e24-105">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7e24-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e7e24-106">Prerequisites</span></span>

- <span data-ttu-id="e7e24-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e7e24-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e7e24-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="e7e24-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e7e24-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e7e24-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e7e24-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e7e24-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e7e24-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="e7e24-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e7e24-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="e7e24-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e7e24-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e7e24-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e7e24-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e7e24-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e7e24-115">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="e7e24-115">The policy identifier.</span></span>

- <span data-ttu-id="e7e24-116">Identifikátory zařízení, která se má aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="e7e24-116">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="e7e24-117">C\#</span><span class="sxs-lookup"><span data-stu-id="e7e24-117">C\#</span></span>

<span data-ttu-id="e7e24-118">Pokud chcete aktualizovat seznam zařízení pomocí zadaných zásad konfigurace, nejprve vytvořte instanci [List/dotnet/api/system.collections.generic.list-1) typu [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) a přidejte zásadu, která se má použít, jak je znázorněno v následujícím příkladu kódu.</span><span class="sxs-lookup"><span data-stu-id="e7e24-118">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="e7e24-119">Budete potřebovat identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="e7e24-119">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="e7e24-120">Pak vytvořte seznam Objektů [**zařízení,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) které se mají aktualizovat pomocí zásad a zadejte identifikátor zařízení a seznam obsahující zásadu, která se má použít, pro každé zařízení.</span><span class="sxs-lookup"><span data-stu-id="e7e24-120">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="e7e24-121">Dále vytvořte instanci objektu [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) a nastavte vlastnost [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) na seznam objektů zařízení.</span><span class="sxs-lookup"><span data-stu-id="e7e24-121">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="e7e24-122">Pokud chcete zpracovat požadavek na aktualizaci zásad zařízení, zavolejte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka a načtěte rozhraní pro operace zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e7e24-122">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="e7e24-123">Potom načtěte vlastnost [**DevicePolicy,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) abyste získali rozhraní pro operace shromažďování zařízení zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e7e24-123">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="e7e24-124">Nakonec zavolejte [**metodu Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) s objektem DevicePolicyUpdateRequest a aktualizujte zařízení pomocí zásad.</span><span class="sxs-lookup"><span data-stu-id="e7e24-124">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

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

<span data-ttu-id="e7e24-125">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e7e24-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e7e24-126">**Project**: SDK pro Partnerské centrum Samples **– třída:** UpdateDevicesPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="e7e24-126">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e7e24-127">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="e7e24-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e7e24-128">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="e7e24-128">Request syntax</span></span>

| <span data-ttu-id="e7e24-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="e7e24-129">Method</span></span>    | <span data-ttu-id="e7e24-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e7e24-130">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e7e24-131">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="e7e24-131">**PATCH**</span></span> | <span data-ttu-id="e7e24-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/DevicePolicyUpdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e7e24-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e7e24-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e7e24-133">URI parameter</span></span>

<span data-ttu-id="e7e24-134">Při vytváření požadavku použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="e7e24-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="e7e24-135">Název</span><span class="sxs-lookup"><span data-stu-id="e7e24-135">Name</span></span>        | <span data-ttu-id="e7e24-136">Typ</span><span class="sxs-lookup"><span data-stu-id="e7e24-136">Type</span></span>   | <span data-ttu-id="e7e24-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e7e24-137">Required</span></span> | <span data-ttu-id="e7e24-138">Popis</span><span class="sxs-lookup"><span data-stu-id="e7e24-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e7e24-139">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="e7e24-139">customer-id</span></span> | <span data-ttu-id="e7e24-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="e7e24-140">string</span></span> | <span data-ttu-id="e7e24-141">Yes</span><span class="sxs-lookup"><span data-stu-id="e7e24-141">Yes</span></span>      | <span data-ttu-id="e7e24-142">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e7e24-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e7e24-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e7e24-143">Request headers</span></span>

<span data-ttu-id="e7e24-144">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e7e24-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e7e24-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e7e24-145">Request body</span></span>

<span data-ttu-id="e7e24-146">Text požadavku musí obsahovat prostředek [DevicePolicyUpdateRequest.](device-deployment-resources.md#devicepolicyupdaterequest)</span><span class="sxs-lookup"><span data-stu-id="e7e24-146">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="e7e24-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e7e24-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e7e24-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e7e24-148">REST response</span></span>

<span data-ttu-id="e7e24-149">V případě úspěchu odpověď obsahuje **hlavičku Location** s identifikátorem URI, který lze použít k načtení stavu tohoto dávkového procesu.</span><span class="sxs-lookup"><span data-stu-id="e7e24-149">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="e7e24-150">Uložte si tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.</span><span class="sxs-lookup"><span data-stu-id="e7e24-150">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e7e24-151">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="e7e24-151">Response success and error codes</span></span>

<span data-ttu-id="e7e24-152">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e7e24-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e7e24-153">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="e7e24-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e7e24-154">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e7e24-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e7e24-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e7e24-155">Response example</span></span>

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
