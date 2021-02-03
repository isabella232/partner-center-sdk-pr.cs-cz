---
title: Získání stavu nahrání dávek zařízení
description: Jak získat stav nahrávání dávky zařízení pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fb887ba257d6fbe68f95ae4b59d701ac4c934860
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767016"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="9ca80-103">Získání stavu nahrání dávek zařízení</span><span class="sxs-lookup"><span data-stu-id="9ca80-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="9ca80-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="9ca80-104">**Applies To**</span></span>

- <span data-ttu-id="9ca80-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="9ca80-105">Partner Center</span></span>
- <span data-ttu-id="9ca80-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="9ca80-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="9ca80-107">Jak získat stav nahrávání dávky zařízení pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9ca80-107">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ca80-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9ca80-108">Prerequisites</span></span>

- <span data-ttu-id="9ca80-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9ca80-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9ca80-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="9ca80-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9ca80-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9ca80-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9ca80-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="9ca80-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9ca80-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="9ca80-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9ca80-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="9ca80-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9ca80-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="9ca80-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9ca80-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9ca80-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9ca80-117">Identifikátor sledování dávky vrácený v hlavičce umístění při odeslání dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="9ca80-117">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="9ca80-118">Další informace najdete v tématu [nahrání seznamu zařízení pro zadaného zákazníka](upload-a-list-of-devices-for-the-specified-customer.md).</span><span class="sxs-lookup"><span data-stu-id="9ca80-118">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="9ca80-119">C\#</span><span class="sxs-lookup"><span data-stu-id="9ca80-119">C\#</span></span>

<span data-ttu-id="9ca80-120">Pokud chcete získat stav dávkového nahrání zařízení, nejdřív zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro konkrétního zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9ca80-120">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="9ca80-121">Pak zavolejte metodu [**BatchUploadStatus. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) s ID sledování dávky, aby se získalo rozhraní pro dávkové odesílání operací stavu.</span><span class="sxs-lookup"><span data-stu-id="9ca80-121">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="9ca80-122">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) načtěte stav.</span><span class="sxs-lookup"><span data-stu-id="9ca80-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="9ca80-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9ca80-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9ca80-124">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetBatchUploadStatus.cs</span><span class="sxs-lookup"><span data-stu-id="9ca80-124">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9ca80-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="9ca80-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9ca80-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="9ca80-126">Request syntax</span></span>

| <span data-ttu-id="9ca80-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="9ca80-127">Method</span></span>  | <span data-ttu-id="9ca80-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9ca80-128">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9ca80-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="9ca80-129">**GET**</span></span> | <span data-ttu-id="9ca80-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/batchJobStatus/{batchtracking-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9ca80-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9ca80-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9ca80-131">URI parameter</span></span>

<span data-ttu-id="9ca80-132">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="9ca80-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="9ca80-133">Název</span><span class="sxs-lookup"><span data-stu-id="9ca80-133">Name</span></span>             | <span data-ttu-id="9ca80-134">Typ</span><span class="sxs-lookup"><span data-stu-id="9ca80-134">Type</span></span>   | <span data-ttu-id="9ca80-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9ca80-135">Required</span></span> | <span data-ttu-id="9ca80-136">Popis</span><span class="sxs-lookup"><span data-stu-id="9ca80-136">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9ca80-137">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="9ca80-137">customer-id</span></span>      | <span data-ttu-id="9ca80-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="9ca80-138">string</span></span> | <span data-ttu-id="9ca80-139">Yes</span><span class="sxs-lookup"><span data-stu-id="9ca80-139">Yes</span></span>      | <span data-ttu-id="9ca80-140">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9ca80-140">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="9ca80-141">batchtracking-ID</span><span class="sxs-lookup"><span data-stu-id="9ca80-141">batchtracking-id</span></span> | <span data-ttu-id="9ca80-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="9ca80-142">string</span></span> | <span data-ttu-id="9ca80-143">Yes</span><span class="sxs-lookup"><span data-stu-id="9ca80-143">Yes</span></span>      | <span data-ttu-id="9ca80-144">Identifikátor GUID, který se používá k načtení stavu nahrávání dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="9ca80-144">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="9ca80-145">Toto ID se vrátí v hlavičce umístění po úspěšném odeslání dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="9ca80-145">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9ca80-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9ca80-146">Request headers</span></span>

<span data-ttu-id="9ca80-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9ca80-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9ca80-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9ca80-148">Request body</span></span>

<span data-ttu-id="9ca80-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="9ca80-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="9ca80-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9ca80-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="9ca80-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9ca80-151">REST response</span></span>

<span data-ttu-id="9ca80-152">V případě úspěchu obsahuje odpověď prostředek [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) .</span><span class="sxs-lookup"><span data-stu-id="9ca80-152">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9ca80-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="9ca80-153">Response success and error codes</span></span>

<span data-ttu-id="9ca80-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9ca80-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9ca80-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="9ca80-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9ca80-156">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9ca80-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9ca80-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9ca80-157">Response example</span></span>

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
