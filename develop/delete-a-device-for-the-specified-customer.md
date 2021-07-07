---
title: Odstraní zařízení pro konkrétního zákazníka
description: Jak odstranit zařízení, které patří k zadanému zákazníkovi.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1e05ceb8615d6f84c1df101c542342f9a6eb04b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973073"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="f442e-103">Odstraní zařízení pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="f442e-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="f442e-104">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="f442e-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="f442e-105">Tento článek vysvětluje, jak odstranit zařízení, které patří k zadanému zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="f442e-105">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f442e-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f442e-106">Prerequisites</span></span>

- <span data-ttu-id="f442e-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f442e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f442e-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="f442e-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f442e-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f442e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f442e-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="f442e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f442e-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="f442e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f442e-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="f442e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f442e-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="f442e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f442e-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f442e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f442e-115">Identifikátor dávky zařízení</span><span class="sxs-lookup"><span data-stu-id="f442e-115">The device batch identifier.</span></span>

- <span data-ttu-id="f442e-116">Identifikátor zařízení</span><span class="sxs-lookup"><span data-stu-id="f442e-116">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="f442e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="f442e-117">C\#</span></span>

<span data-ttu-id="f442e-118">Postup odstranění zařízení pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="f442e-118">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="f442e-119">Voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka načtete rozhraní k operacím zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f442e-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="f442e-120">Pro získání rozhraní pro zadanou dávku volejte metodu [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) s identifikátorem dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="f442e-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="f442e-121">Voláním metody [**Devices. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) Získejte rozhraní na určeném zařízení.</span><span class="sxs-lookup"><span data-stu-id="f442e-121">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="f442e-122">Voláním metody [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) nebo [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) odstraníte zařízení z dávky.</span><span class="sxs-lookup"><span data-stu-id="f442e-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="f442e-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f442e-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f442e-124">**Project**: **třída** microsoft Partner SDK samples: DeleteDevice. cs</span><span class="sxs-lookup"><span data-stu-id="f442e-124">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f442e-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f442e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f442e-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f442e-126">Request syntax</span></span>

| <span data-ttu-id="f442e-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="f442e-127">Method</span></span>     | <span data-ttu-id="f442e-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f442e-128">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f442e-129">DELETE</span><span class="sxs-lookup"><span data-stu-id="f442e-129">DELETE</span></span>     | <span data-ttu-id="f442e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices/{Device-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f442e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="f442e-131">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="f442e-131">URI parameters</span></span>

<span data-ttu-id="f442e-132">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="f442e-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="f442e-133">Název</span><span class="sxs-lookup"><span data-stu-id="f442e-133">Name</span></span>           | <span data-ttu-id="f442e-134">Typ</span><span class="sxs-lookup"><span data-stu-id="f442e-134">Type</span></span>   | <span data-ttu-id="f442e-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f442e-135">Required</span></span> | <span data-ttu-id="f442e-136">Popis</span><span class="sxs-lookup"><span data-stu-id="f442e-136">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="f442e-137">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="f442e-137">customer-id</span></span>    | <span data-ttu-id="f442e-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="f442e-138">string</span></span> | <span data-ttu-id="f442e-139">Yes</span><span class="sxs-lookup"><span data-stu-id="f442e-139">Yes</span></span>      | <span data-ttu-id="f442e-140">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f442e-140">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="f442e-141">devicebatch-ID</span><span class="sxs-lookup"><span data-stu-id="f442e-141">devicebatch-id</span></span> | <span data-ttu-id="f442e-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="f442e-142">string</span></span> | <span data-ttu-id="f442e-143">Yes</span><span class="sxs-lookup"><span data-stu-id="f442e-143">Yes</span></span>      | <span data-ttu-id="f442e-144">Identifikátor dávky zařízení v dávce, která obsahuje zařízení.</span><span class="sxs-lookup"><span data-stu-id="f442e-144">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="f442e-145">ID zařízení</span><span class="sxs-lookup"><span data-stu-id="f442e-145">device-id</span></span>      | <span data-ttu-id="f442e-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="f442e-146">string</span></span> | <span data-ttu-id="f442e-147">Yes</span><span class="sxs-lookup"><span data-stu-id="f442e-147">Yes</span></span>      | <span data-ttu-id="f442e-148">Identifikátor zařízení</span><span class="sxs-lookup"><span data-stu-id="f442e-148">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="f442e-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f442e-149">Request headers</span></span>

<span data-ttu-id="f442e-150">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f442e-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f442e-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f442e-151">Request body</span></span>

<span data-ttu-id="f442e-152">Žádná</span><span class="sxs-lookup"><span data-stu-id="f442e-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f442e-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f442e-153">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f442e-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f442e-154">REST response</span></span>

<span data-ttu-id="f442e-155">V případě úspěchu vrátí odpověď **204 bez** stavového kódu obsahu.</span><span class="sxs-lookup"><span data-stu-id="f442e-155">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f442e-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f442e-156">Response success and error codes</span></span>

<span data-ttu-id="f442e-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f442e-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f442e-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f442e-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f442e-159">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f442e-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f442e-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f442e-160">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
