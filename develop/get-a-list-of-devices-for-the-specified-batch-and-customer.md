---
title: Získání seznamu zařízení pro konkrétní dávku a zákazníka
description: Jak načíst kolekci zařízení a podrobností o zařízení v zadané dávce zařízení pro zákazníka.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 28af1f568f755ba4c50cfac21529d6c677656c8e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874257"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="7c5eb-103">Získání seznamu zařízení pro konkrétní dávku a zákazníka</span><span class="sxs-lookup"><span data-stu-id="7c5eb-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="7c5eb-104">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="7c5eb-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="7c5eb-105">Tento článek popisuje, jak načíst kolekci zařízení v zadané dávce zařízení pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-105">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="7c5eb-106">Každý prostředek zařízení obsahuje podrobnosti o zařízení.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-106">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c5eb-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7c5eb-107">Prerequisites</span></span>

- <span data-ttu-id="7c5eb-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7c5eb-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7c5eb-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7c5eb-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7c5eb-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7c5eb-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7c5eb-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7c5eb-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7c5eb-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="7c5eb-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7c5eb-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7c5eb-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7c5eb-116">Identifikátor dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-116">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="7c5eb-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7c5eb-117">C\#</span></span>

<span data-ttu-id="7c5eb-118">Načtení kolekce zařízení v zadané dávce zařízení pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="7c5eb-118">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="7c5eb-119">Zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro operace zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="7c5eb-120">Voláním metody [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) Získejte rozhraní pro operaci shromažďování dávky zařízení pro zadanou dávku.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="7c5eb-121">Načtěte vlastnost [**zařízení**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) , abyste získali rozhraní pro operace shromažďování zařízení pro dávku.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-121">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="7c5eb-122">Pro načtení kolekce zařízení zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="7c5eb-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="7c5eb-123">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="7c5eb-123">For an example, see the following:</span></span>

- <span data-ttu-id="7c5eb-124">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7c5eb-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7c5eb-125">Project: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="7c5eb-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="7c5eb-126">Třída: **GetDevices. cs**</span><span class="sxs-lookup"><span data-stu-id="7c5eb-126">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7c5eb-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="7c5eb-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7c5eb-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="7c5eb-128">Request syntax</span></span>

| <span data-ttu-id="7c5eb-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="7c5eb-129">Method</span></span>  | <span data-ttu-id="7c5eb-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="7c5eb-130">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7c5eb-131">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="7c5eb-131">**GET**</span></span> | <span data-ttu-id="7c5eb-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7c5eb-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="7c5eb-133">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="7c5eb-133">URI parameters</span></span>

<span data-ttu-id="7c5eb-134">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="7c5eb-135">Název</span><span class="sxs-lookup"><span data-stu-id="7c5eb-135">Name</span></span>           | <span data-ttu-id="7c5eb-136">Typ</span><span class="sxs-lookup"><span data-stu-id="7c5eb-136">Type</span></span>   | <span data-ttu-id="7c5eb-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="7c5eb-137">Required</span></span> | <span data-ttu-id="7c5eb-138">Popis</span><span class="sxs-lookup"><span data-stu-id="7c5eb-138">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7c5eb-139">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="7c5eb-139">customer-id</span></span>    | <span data-ttu-id="7c5eb-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="7c5eb-140">string</span></span> | <span data-ttu-id="7c5eb-141">Yes</span><span class="sxs-lookup"><span data-stu-id="7c5eb-141">Yes</span></span>      | <span data-ttu-id="7c5eb-142">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-142">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="7c5eb-143">devicebatch-ID</span><span class="sxs-lookup"><span data-stu-id="7c5eb-143">devicebatch-id</span></span> | <span data-ttu-id="7c5eb-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="7c5eb-144">string</span></span> | <span data-ttu-id="7c5eb-145">Yes</span><span class="sxs-lookup"><span data-stu-id="7c5eb-145">Yes</span></span>      | <span data-ttu-id="7c5eb-146">Identifikátor řetězce identifikující dávku zařízení.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-146">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7c5eb-147">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="7c5eb-147">Request headers</span></span>

<span data-ttu-id="7c5eb-148">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7c5eb-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7c5eb-149">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="7c5eb-149">Request body</span></span>

<span data-ttu-id="7c5eb-150">Žádná</span><span class="sxs-lookup"><span data-stu-id="7c5eb-150">None</span></span>

### <a name="request-example"></a><span data-ttu-id="7c5eb-151">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="7c5eb-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7c5eb-152">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="7c5eb-152">REST response</span></span>

<span data-ttu-id="7c5eb-153">V případě úspěchu obsahuje tělo odpovědi stránkované kolekci prostředků [zařízení](device-deployment-resources.md#device) .</span><span class="sxs-lookup"><span data-stu-id="7c5eb-153">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="7c5eb-154">Kolekce obsahuje zařízení 100 na stránce.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-154">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="7c5eb-155">Pokud chcete načíst další stránku 100 zařízení, token continuationtoken v textu odpovědi musí být součástí následné žádosti jako hlavička MS-ContinuationToken.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-155">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7c5eb-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="7c5eb-156">Response success and error codes</span></span>

<span data-ttu-id="7c5eb-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7c5eb-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="7c5eb-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7c5eb-159">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7c5eb-159">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7c5eb-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="7c5eb-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
