---
title: Získání seznamu nabídek převod zkušebních verzí
description: Jak načíst seznam nabídek zkušebního převodu.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e1eadecde9efa0b59fc7790bd474889bb32821dc
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766931"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="60163-103">Získání seznamu nabídek převod zkušebních verzí</span><span class="sxs-lookup"><span data-stu-id="60163-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="60163-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="60163-104">**Applies To**</span></span>

- <span data-ttu-id="60163-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="60163-105">Partner Center</span></span>

<span data-ttu-id="60163-106">Jak načíst seznam nabídek zkušebního převodu.</span><span class="sxs-lookup"><span data-stu-id="60163-106">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60163-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="60163-107">Prerequisites</span></span>

- <span data-ttu-id="60163-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="60163-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="60163-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="60163-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="60163-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="60163-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="60163-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="60163-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="60163-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="60163-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="60163-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="60163-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="60163-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="60163-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="60163-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="60163-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="60163-116">ID předplatného pro aktivní zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="60163-116">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="60163-117">C\#</span><span class="sxs-lookup"><span data-stu-id="60163-117">C\#</span></span>

<span data-ttu-id="60163-118">Pokud chcete získat seznam dostupných převodů zkušební verze, začněte tím, že k identifikaci zákazníka použijete metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="60163-118">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="60163-119">Potom Získejte rozhraní pro operace předplatného voláním metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID zkušebního předplatného.</span><span class="sxs-lookup"><span data-stu-id="60163-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="60163-120">Dále pomocí vlastnosti [**převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) Získejte rozhraní k dostupným operacím pro převody a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) pro načtení kolekce dostupných nabídek [**převodu**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) .</span><span class="sxs-lookup"><span data-stu-id="60163-120">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="60163-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="60163-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="60163-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="60163-122">Request syntax</span></span>

| <span data-ttu-id="60163-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="60163-123">Method</span></span>  | <span data-ttu-id="60163-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="60163-124">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="60163-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="60163-125">**GET**</span></span> | <span data-ttu-id="60163-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="60163-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="60163-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="60163-127">URI parameter</span></span>

<span data-ttu-id="60163-128">K identifikaci zákazníka a zkušebního předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="60163-128">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="60163-129">Název</span><span class="sxs-lookup"><span data-stu-id="60163-129">Name</span></span>            | <span data-ttu-id="60163-130">Typ</span><span class="sxs-lookup"><span data-stu-id="60163-130">Type</span></span>   | <span data-ttu-id="60163-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="60163-131">Required</span></span> | <span data-ttu-id="60163-132">Popis</span><span class="sxs-lookup"><span data-stu-id="60163-132">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="60163-133">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="60163-133">customer-id</span></span>     | <span data-ttu-id="60163-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="60163-134">string</span></span> | <span data-ttu-id="60163-135">Yes</span><span class="sxs-lookup"><span data-stu-id="60163-135">Yes</span></span>      | <span data-ttu-id="60163-136">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="60163-136">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="60163-137">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="60163-137">subscription-id</span></span> | <span data-ttu-id="60163-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="60163-138">string</span></span> | <span data-ttu-id="60163-139">Yes</span><span class="sxs-lookup"><span data-stu-id="60163-139">Yes</span></span>      | <span data-ttu-id="60163-140">Řetězec ve formátu GUID, který identifikuje zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="60163-140">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="60163-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="60163-141">Request headers</span></span>

<span data-ttu-id="60163-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="60163-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="60163-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="60163-143">Request body</span></span>

<span data-ttu-id="60163-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="60163-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="60163-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="60163-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="60163-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="60163-146">REST response</span></span>

<span data-ttu-id="60163-147">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [převodu](conversions-resources.md#conversionresult) .</span><span class="sxs-lookup"><span data-stu-id="60163-147">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="60163-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="60163-148">Response success and error codes</span></span>

<span data-ttu-id="60163-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="60163-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="60163-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="60163-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="60163-151">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="60163-151">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="60163-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="60163-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 305
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CV: feJByqU1X0ObaTQr.0
MS-ServerId: 030011719
Date: Thu, 15 Jun 2017 23:10:01 GMT

 {
    "totalCount": 1,
    "items": [{
            "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
            "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
            "orderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
            "quantity": 25,
            "billingCycle": "monthly",
            "attributes": {
                "objectType": "Conversion"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
