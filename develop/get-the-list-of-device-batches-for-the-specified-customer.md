---
title: Získání seznamu dávek zařízení pro konkrétního zákazníka
description: Jak načíst kolekci dávek zařízení pro zadaného zákazníka
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d020bbfa1faef0be423d2fef2d8982465dfa21f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548410"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="b1a11-103">Získání seznamu dávek zařízení pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="b1a11-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="b1a11-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)</span><span class="sxs-lookup"><span data-stu-id="b1a11-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="b1a11-105">Jak načíst kolekci dávek zařízení pro zadaného zákazníka</span><span class="sxs-lookup"><span data-stu-id="b1a11-105">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="b1a11-106">Každá dávka zařízení obsahuje souhrnné informace o stavu zařízení, která byla zaregistrovaná v bezobsahovém nasazení.</span><span class="sxs-lookup"><span data-stu-id="b1a11-106">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1a11-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b1a11-107">Prerequisites</span></span>

- <span data-ttu-id="b1a11-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b1a11-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b1a11-109">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b1a11-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b1a11-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b1a11-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b1a11-111">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b1a11-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b1a11-112">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="b1a11-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b1a11-113">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="b1a11-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b1a11-114">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b1a11-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b1a11-115">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b1a11-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b1a11-116">C\#</span><span class="sxs-lookup"><span data-stu-id="b1a11-116">C\#</span></span>

<span data-ttu-id="b1a11-117">Pokud chcete získat kolekci dávek zařízení pro zadaného zákazníka, nejprve zavolejte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a načtěte rozhraní pro operace se zadaným zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="b1a11-117">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="b1a11-118">Potom načtěte hodnotu vlastnosti [**DeviceBatches,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) abyste získali rozhraní pro operace dávkového shromažďování zařízení.</span><span class="sxs-lookup"><span data-stu-id="b1a11-118">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="b1a11-119">Nakonec zavolejte [**metodu Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) pro načtení kolekce.</span><span class="sxs-lookup"><span data-stu-id="b1a11-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="b1a11-120">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1a11-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b1a11-121">**Project:** SDK pro Partnerské centrum Samples **Class:** GetDevicesBatches.cs</span><span class="sxs-lookup"><span data-stu-id="b1a11-121">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b1a11-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="b1a11-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b1a11-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="b1a11-123">Request syntax</span></span>

| <span data-ttu-id="b1a11-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="b1a11-124">Method</span></span>  | <span data-ttu-id="b1a11-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b1a11-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="b1a11-126">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="b1a11-126">**GET**</span></span> | <span data-ttu-id="b1a11-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/deviceBatches HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b1a11-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b1a11-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b1a11-128">URI parameter</span></span>

<span data-ttu-id="b1a11-129">Při vytváření požadavku použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="b1a11-129">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="b1a11-130">Název</span><span class="sxs-lookup"><span data-stu-id="b1a11-130">Name</span></span>        | <span data-ttu-id="b1a11-131">Typ</span><span class="sxs-lookup"><span data-stu-id="b1a11-131">Type</span></span>   | <span data-ttu-id="b1a11-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b1a11-132">Required</span></span> | <span data-ttu-id="b1a11-133">Popis</span><span class="sxs-lookup"><span data-stu-id="b1a11-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="b1a11-134">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="b1a11-134">customer-id</span></span> | <span data-ttu-id="b1a11-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="b1a11-135">string</span></span> | <span data-ttu-id="b1a11-136">Yes</span><span class="sxs-lookup"><span data-stu-id="b1a11-136">Yes</span></span>      | <span data-ttu-id="b1a11-137">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b1a11-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b1a11-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b1a11-138">Request headers</span></span>

<span data-ttu-id="b1a11-139">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b1a11-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b1a11-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b1a11-140">Request body</span></span>

<span data-ttu-id="b1a11-141">Žádná</span><span class="sxs-lookup"><span data-stu-id="b1a11-141">None</span></span>

### <a name="request-example"></a><span data-ttu-id="b1a11-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b1a11-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="b1a11-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b1a11-143">REST response</span></span>

<span data-ttu-id="b1a11-144">V případě úspěchu bude tělo odpovědi obsahovat kolekci [prostředků DeviceBatch.](device-deployment-resources.md#devicebatch)</span><span class="sxs-lookup"><span data-stu-id="b1a11-144">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b1a11-145">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="b1a11-145">Response success and error codes</span></span>

<span data-ttu-id="b1a11-146">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b1a11-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b1a11-147">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="b1a11-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b1a11-148">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b1a11-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b1a11-149">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b1a11-149">Response example</span></span>

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
