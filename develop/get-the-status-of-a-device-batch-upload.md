---
title: Získání stavu nahrání dávek zařízení
description: Jak získat stav nahrávání dávky zařízení pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd8726af41fe4399797f39a0790cf962fde64acc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548477"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="fa132-103">Získání stavu nahrání dávek zařízení</span><span class="sxs-lookup"><span data-stu-id="fa132-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="fa132-104">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="fa132-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="fa132-105">Jak získat stav nahrávání dávky zařízení pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fa132-105">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa132-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fa132-106">Prerequisites</span></span>

- <span data-ttu-id="fa132-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fa132-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fa132-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="fa132-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fa132-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fa132-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fa132-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fa132-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fa132-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="fa132-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fa132-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="fa132-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fa132-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="fa132-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fa132-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fa132-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fa132-115">Identifikátor sledování dávky vrácený v hlavičce umístění při odeslání dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="fa132-115">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="fa132-116">další informace najdete v tématu [Upload seznamu zařízení pro zadaného zákazníka](upload-a-list-of-devices-for-the-specified-customer.md).</span><span class="sxs-lookup"><span data-stu-id="fa132-116">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="fa132-117">C\#</span><span class="sxs-lookup"><span data-stu-id="fa132-117">C\#</span></span>

<span data-ttu-id="fa132-118">Pokud chcete získat stav dávkového nahrání zařízení, nejdřív zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro konkrétního zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fa132-118">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="fa132-119">Pak zavolejte metodu [**BatchUploadStatus. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) s ID sledování dávky, aby se získalo rozhraní pro dávkové odesílání operací stavu.</span><span class="sxs-lookup"><span data-stu-id="fa132-119">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="fa132-120">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) načtěte stav.</span><span class="sxs-lookup"><span data-stu-id="fa132-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="fa132-121">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fa132-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fa132-122">**Project**: **třída** microsoft Partner SDK samples: GetBatchUploadStatus. cs</span><span class="sxs-lookup"><span data-stu-id="fa132-122">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fa132-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fa132-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fa132-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fa132-124">Request syntax</span></span>

| <span data-ttu-id="fa132-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="fa132-125">Method</span></span>  | <span data-ttu-id="fa132-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fa132-126">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fa132-127">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="fa132-127">**GET**</span></span> | <span data-ttu-id="fa132-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/batchJobStatus/{batchtracking-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fa132-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fa132-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fa132-129">URI parameter</span></span>

<span data-ttu-id="fa132-130">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="fa132-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="fa132-131">Název</span><span class="sxs-lookup"><span data-stu-id="fa132-131">Name</span></span>             | <span data-ttu-id="fa132-132">Typ</span><span class="sxs-lookup"><span data-stu-id="fa132-132">Type</span></span>   | <span data-ttu-id="fa132-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fa132-133">Required</span></span> | <span data-ttu-id="fa132-134">Popis</span><span class="sxs-lookup"><span data-stu-id="fa132-134">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fa132-135">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="fa132-135">customer-id</span></span>      | <span data-ttu-id="fa132-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="fa132-136">string</span></span> | <span data-ttu-id="fa132-137">Yes</span><span class="sxs-lookup"><span data-stu-id="fa132-137">Yes</span></span>      | <span data-ttu-id="fa132-138">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fa132-138">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="fa132-139">batchtracking-ID</span><span class="sxs-lookup"><span data-stu-id="fa132-139">batchtracking-id</span></span> | <span data-ttu-id="fa132-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="fa132-140">string</span></span> | <span data-ttu-id="fa132-141">Yes</span><span class="sxs-lookup"><span data-stu-id="fa132-141">Yes</span></span>      | <span data-ttu-id="fa132-142">Identifikátor GUID, který se používá k načtení stavu nahrávání dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="fa132-142">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="fa132-143">Toto ID se vrátí v hlavičce umístění po úspěšném odeslání dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="fa132-143">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fa132-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fa132-144">Request headers</span></span>

<span data-ttu-id="fa132-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fa132-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fa132-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fa132-146">Request body</span></span>

<span data-ttu-id="fa132-147">Žádná</span><span class="sxs-lookup"><span data-stu-id="fa132-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="fa132-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fa132-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="fa132-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fa132-149">REST response</span></span>

<span data-ttu-id="fa132-150">V případě úspěchu obsahuje odpověď prostředek [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) .</span><span class="sxs-lookup"><span data-stu-id="fa132-150">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fa132-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fa132-151">Response success and error codes</span></span>

<span data-ttu-id="fa132-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fa132-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fa132-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fa132-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fa132-154">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fa132-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fa132-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fa132-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```
