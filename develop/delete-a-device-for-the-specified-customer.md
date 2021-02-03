---
title: Odstraní zařízení pro konkrétního zákazníka
description: Jak odstranit zařízení, které patří k zadanému zákazníkovi.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69b5440f2cf07d3cb4ecd5addf429acd64530257
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766880"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="e8dfa-103">Odstraní zařízení pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="e8dfa-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="e8dfa-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="e8dfa-104">**Applies to:**</span></span>

- <span data-ttu-id="e8dfa-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e8dfa-105">Partner Center</span></span>
- <span data-ttu-id="e8dfa-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="e8dfa-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e8dfa-107">Tento článek vysvětluje, jak odstranit zařízení, které patří k zadanému zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-107">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8dfa-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e8dfa-108">Prerequisites</span></span>

- <span data-ttu-id="e8dfa-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e8dfa-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e8dfa-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e8dfa-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e8dfa-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e8dfa-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e8dfa-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e8dfa-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e8dfa-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e8dfa-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e8dfa-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e8dfa-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e8dfa-117">Identifikátor dávky zařízení</span><span class="sxs-lookup"><span data-stu-id="e8dfa-117">The device batch identifier.</span></span>

- <span data-ttu-id="e8dfa-118">Identifikátor zařízení</span><span class="sxs-lookup"><span data-stu-id="e8dfa-118">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="e8dfa-119">C\#</span><span class="sxs-lookup"><span data-stu-id="e8dfa-119">C\#</span></span>

<span data-ttu-id="e8dfa-120">Postup odstranění zařízení pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="e8dfa-120">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="e8dfa-121">Voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka načtete rozhraní k operacím zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="e8dfa-122">Pro získání rozhraní pro zadanou dávku volejte metodu [**DeviceBatches. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) s identifikátorem dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="e8dfa-123">Voláním metody [**Devices. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) Získejte rozhraní na určeném zařízení.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-123">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="e8dfa-124">Voláním metody [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) nebo [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) odstraníte zařízení z dávky.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-124">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="e8dfa-125">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e8dfa-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e8dfa-126">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: DeleteDevice.cs</span><span class="sxs-lookup"><span data-stu-id="e8dfa-126">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e8dfa-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e8dfa-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e8dfa-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e8dfa-128">Request syntax</span></span>

| <span data-ttu-id="e8dfa-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="e8dfa-129">Method</span></span>     | <span data-ttu-id="e8dfa-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e8dfa-130">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e8dfa-131">DELETE</span><span class="sxs-lookup"><span data-stu-id="e8dfa-131">DELETE</span></span>     | <span data-ttu-id="e8dfa-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices/{Device-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e8dfa-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="e8dfa-133">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="e8dfa-133">URI parameters</span></span>

<span data-ttu-id="e8dfa-134">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="e8dfa-135">Název</span><span class="sxs-lookup"><span data-stu-id="e8dfa-135">Name</span></span>           | <span data-ttu-id="e8dfa-136">Typ</span><span class="sxs-lookup"><span data-stu-id="e8dfa-136">Type</span></span>   | <span data-ttu-id="e8dfa-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e8dfa-137">Required</span></span> | <span data-ttu-id="e8dfa-138">Popis</span><span class="sxs-lookup"><span data-stu-id="e8dfa-138">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="e8dfa-139">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="e8dfa-139">customer-id</span></span>    | <span data-ttu-id="e8dfa-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="e8dfa-140">string</span></span> | <span data-ttu-id="e8dfa-141">Yes</span><span class="sxs-lookup"><span data-stu-id="e8dfa-141">Yes</span></span>      | <span data-ttu-id="e8dfa-142">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-142">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="e8dfa-143">devicebatch-ID</span><span class="sxs-lookup"><span data-stu-id="e8dfa-143">devicebatch-id</span></span> | <span data-ttu-id="e8dfa-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="e8dfa-144">string</span></span> | <span data-ttu-id="e8dfa-145">Yes</span><span class="sxs-lookup"><span data-stu-id="e8dfa-145">Yes</span></span>      | <span data-ttu-id="e8dfa-146">Identifikátor dávky zařízení v dávce, která obsahuje zařízení.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-146">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="e8dfa-147">ID zařízení</span><span class="sxs-lookup"><span data-stu-id="e8dfa-147">device-id</span></span>      | <span data-ttu-id="e8dfa-148">řetězec</span><span class="sxs-lookup"><span data-stu-id="e8dfa-148">string</span></span> | <span data-ttu-id="e8dfa-149">Yes</span><span class="sxs-lookup"><span data-stu-id="e8dfa-149">Yes</span></span>      | <span data-ttu-id="e8dfa-150">Identifikátor zařízení</span><span class="sxs-lookup"><span data-stu-id="e8dfa-150">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="e8dfa-151">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e8dfa-151">Request headers</span></span>

<span data-ttu-id="e8dfa-152">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e8dfa-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e8dfa-153">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e8dfa-153">Request body</span></span>

<span data-ttu-id="e8dfa-154">Žádné</span><span class="sxs-lookup"><span data-stu-id="e8dfa-154">None</span></span>

### <a name="request-example"></a><span data-ttu-id="e8dfa-155">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e8dfa-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e8dfa-156">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e8dfa-156">REST response</span></span>

<span data-ttu-id="e8dfa-157">V případě úspěchu vrátí odpověď **204 bez** stavového kódu obsahu.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-157">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e8dfa-158">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e8dfa-158">Response success and error codes</span></span>

<span data-ttu-id="e8dfa-159">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e8dfa-160">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e8dfa-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e8dfa-161">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e8dfa-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e8dfa-162">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e8dfa-162">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
