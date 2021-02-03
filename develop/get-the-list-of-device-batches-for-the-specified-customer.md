---
title: Získání seznamu dávek zařízení pro konkrétního zákazníka
description: Jak načíst kolekci dávek zařízení pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea5797bbaff4d4eafd1e63428556ab784bcb0ee2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767021"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="fc36f-103">Získání seznamu dávek zařízení pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="fc36f-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="fc36f-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="fc36f-104">**Applies To**</span></span>

- <span data-ttu-id="fc36f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="fc36f-105">Partner Center</span></span>
- <span data-ttu-id="fc36f-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="fc36f-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="fc36f-107">Jak načíst kolekci dávek zařízení pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fc36f-107">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="fc36f-108">Každá dávka zařízení obsahuje souhrnné informace o stavu zařízení, která jsou zaregistrovaná v nasazení s nulovým dotykem.</span><span class="sxs-lookup"><span data-stu-id="fc36f-108">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc36f-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fc36f-109">Prerequisites</span></span>

- <span data-ttu-id="fc36f-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fc36f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fc36f-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="fc36f-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fc36f-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc36f-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fc36f-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fc36f-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fc36f-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="fc36f-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fc36f-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="fc36f-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fc36f-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="fc36f-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fc36f-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc36f-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="fc36f-118">C\#</span><span class="sxs-lookup"><span data-stu-id="fc36f-118">C\#</span></span>

<span data-ttu-id="fc36f-119">Chcete-li získat kolekci dávek zařízení pro zadaného zákazníka, nejprve zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní k operacím zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fc36f-119">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="fc36f-120">Pak načtěte hodnotu vlastnosti [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) , abyste získali rozhraní pro operace shromažďování dávky zařízení.</span><span class="sxs-lookup"><span data-stu-id="fc36f-120">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="fc36f-121">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) načtěte kolekci.</span><span class="sxs-lookup"><span data-stu-id="fc36f-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="fc36f-122">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fc36f-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fc36f-123">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetDevicesBatches.cs</span><span class="sxs-lookup"><span data-stu-id="fc36f-123">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fc36f-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fc36f-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc36f-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fc36f-125">Request syntax</span></span>

| <span data-ttu-id="fc36f-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="fc36f-126">Method</span></span>  | <span data-ttu-id="fc36f-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fc36f-127">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc36f-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="fc36f-128">**GET**</span></span> | <span data-ttu-id="fc36f-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fc36f-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fc36f-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fc36f-130">URI parameter</span></span>

<span data-ttu-id="fc36f-131">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="fc36f-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="fc36f-132">Název</span><span class="sxs-lookup"><span data-stu-id="fc36f-132">Name</span></span>        | <span data-ttu-id="fc36f-133">Typ</span><span class="sxs-lookup"><span data-stu-id="fc36f-133">Type</span></span>   | <span data-ttu-id="fc36f-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fc36f-134">Required</span></span> | <span data-ttu-id="fc36f-135">Popis</span><span class="sxs-lookup"><span data-stu-id="fc36f-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="fc36f-136">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="fc36f-136">customer-id</span></span> | <span data-ttu-id="fc36f-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="fc36f-137">string</span></span> | <span data-ttu-id="fc36f-138">Yes</span><span class="sxs-lookup"><span data-stu-id="fc36f-138">Yes</span></span>      | <span data-ttu-id="fc36f-139">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fc36f-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fc36f-140">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fc36f-140">Request headers</span></span>

<span data-ttu-id="fc36f-141">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fc36f-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fc36f-142">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fc36f-142">Request body</span></span>

<span data-ttu-id="fc36f-143">Žádné</span><span class="sxs-lookup"><span data-stu-id="fc36f-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="fc36f-144">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fc36f-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="fc36f-145">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fc36f-145">REST response</span></span>

<span data-ttu-id="fc36f-146">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [DeviceBatch](device-deployment-resources.md#devicebatch) .</span><span class="sxs-lookup"><span data-stu-id="fc36f-146">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc36f-147">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fc36f-147">Response success and error codes</span></span>

<span data-ttu-id="fc36f-148">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fc36f-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc36f-149">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fc36f-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc36f-150">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fc36f-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fc36f-151">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fc36f-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 339
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "Test batch",
            "status": "finished",
            "creationDate": "2017-07-25T01:51:00",
            "devicesCount": 5,
            "devicesLink": {
                "uri": "/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/Test batch/devices",
                "method": "GET",
                "headers": []
            },
            "attributes": {
                "objectType": "DeviceBatch"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
