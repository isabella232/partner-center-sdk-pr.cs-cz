---
title: Získání seznamu zařízení pro konkrétní dávku a zákazníka
description: Jak načíst kolekci zařízení a podrobností o zařízení v zadané dávce zařízení pro zákazníka.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 36fe3b97612adfd26c1b498f31b90f743bf774cb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766934"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="d184d-103">Získání seznamu zařízení pro konkrétní dávku a zákazníka</span><span class="sxs-lookup"><span data-stu-id="d184d-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="d184d-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="d184d-104">**Applies to:**</span></span>

- <span data-ttu-id="d184d-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d184d-105">Partner Center</span></span>
- <span data-ttu-id="d184d-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="d184d-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="d184d-107">Tento článek popisuje, jak načíst kolekci zařízení v zadané dávce zařízení pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d184d-107">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="d184d-108">Každý prostředek zařízení obsahuje podrobnosti o zařízení.</span><span class="sxs-lookup"><span data-stu-id="d184d-108">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d184d-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d184d-109">Prerequisites</span></span>

- <span data-ttu-id="d184d-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d184d-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d184d-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="d184d-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d184d-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d184d-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d184d-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="d184d-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d184d-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="d184d-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d184d-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="d184d-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d184d-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="d184d-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d184d-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d184d-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d184d-118">Identifikátor dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="d184d-118">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="d184d-119">C\#</span><span class="sxs-lookup"><span data-stu-id="d184d-119">C\#</span></span>

<span data-ttu-id="d184d-120">Načtení kolekce zařízení v zadané dávce zařízení pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="d184d-120">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="d184d-121">Zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro operace zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d184d-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="d184d-122">Voláním metody [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) Získejte rozhraní pro operaci shromažďování dávky zařízení pro zadanou dávku.</span><span class="sxs-lookup"><span data-stu-id="d184d-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="d184d-123">Načtěte vlastnost [**zařízení**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) , abyste získali rozhraní pro operace shromažďování zařízení pro dávku.</span><span class="sxs-lookup"><span data-stu-id="d184d-123">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="d184d-124">Pro načtení kolekce zařízení zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="d184d-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="d184d-125">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="d184d-125">For an example, see the following:</span></span>

- <span data-ttu-id="d184d-126">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d184d-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d184d-127">Projekt: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="d184d-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="d184d-128">Třída: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="d184d-128">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d184d-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d184d-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d184d-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d184d-130">Request syntax</span></span>

| <span data-ttu-id="d184d-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="d184d-131">Method</span></span>  | <span data-ttu-id="d184d-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d184d-132">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d184d-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="d184d-133">**GET**</span></span> | <span data-ttu-id="d184d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d184d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="d184d-135">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="d184d-135">URI parameters</span></span>

<span data-ttu-id="d184d-136">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="d184d-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="d184d-137">Název</span><span class="sxs-lookup"><span data-stu-id="d184d-137">Name</span></span>           | <span data-ttu-id="d184d-138">Typ</span><span class="sxs-lookup"><span data-stu-id="d184d-138">Type</span></span>   | <span data-ttu-id="d184d-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d184d-139">Required</span></span> | <span data-ttu-id="d184d-140">Popis</span><span class="sxs-lookup"><span data-stu-id="d184d-140">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="d184d-141">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="d184d-141">customer-id</span></span>    | <span data-ttu-id="d184d-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="d184d-142">string</span></span> | <span data-ttu-id="d184d-143">Yes</span><span class="sxs-lookup"><span data-stu-id="d184d-143">Yes</span></span>      | <span data-ttu-id="d184d-144">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d184d-144">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="d184d-145">devicebatch-ID</span><span class="sxs-lookup"><span data-stu-id="d184d-145">devicebatch-id</span></span> | <span data-ttu-id="d184d-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="d184d-146">string</span></span> | <span data-ttu-id="d184d-147">Yes</span><span class="sxs-lookup"><span data-stu-id="d184d-147">Yes</span></span>      | <span data-ttu-id="d184d-148">Identifikátor řetězce identifikující dávku zařízení.</span><span class="sxs-lookup"><span data-stu-id="d184d-148">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d184d-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d184d-149">Request headers</span></span>

<span data-ttu-id="d184d-150">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d184d-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d184d-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d184d-151">Request body</span></span>

<span data-ttu-id="d184d-152">Žádné</span><span class="sxs-lookup"><span data-stu-id="d184d-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="d184d-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d184d-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d184d-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d184d-154">REST response</span></span>

<span data-ttu-id="d184d-155">V případě úspěchu obsahuje tělo odpovědi stránkované kolekci prostředků [zařízení](device-deployment-resources.md#device) .</span><span class="sxs-lookup"><span data-stu-id="d184d-155">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="d184d-156">Kolekce obsahuje zařízení 100 na stránce.</span><span class="sxs-lookup"><span data-stu-id="d184d-156">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="d184d-157">Pokud chcete načíst další stránku 100 zařízení, token continuationtoken v textu odpovědi musí být součástí následné žádosti jako hlavička MS-ContinuationToken.</span><span class="sxs-lookup"><span data-stu-id="d184d-157">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d184d-158">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d184d-158">Response success and error codes</span></span>

<span data-ttu-id="d184d-159">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d184d-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d184d-160">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d184d-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d184d-161">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d184d-161">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d184d-162">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d184d-162">Response example</span></span>

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
