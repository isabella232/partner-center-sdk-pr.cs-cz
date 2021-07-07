---
title: Získání seznamu nabídek převod zkušebních verzí
description: Jak načíst seznam nabídek zkušebního převodu.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 981910560faf7b7957b28e643c09a003826b9cff
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873917"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="50a91-103">Získání seznamu nabídek převod zkušebních verzí</span><span class="sxs-lookup"><span data-stu-id="50a91-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="50a91-104">Jak načíst seznam nabídek zkušebního převodu.</span><span class="sxs-lookup"><span data-stu-id="50a91-104">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50a91-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="50a91-105">Prerequisites</span></span>

- <span data-ttu-id="50a91-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="50a91-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="50a91-107">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="50a91-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="50a91-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="50a91-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="50a91-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="50a91-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="50a91-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="50a91-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="50a91-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="50a91-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="50a91-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="50a91-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="50a91-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="50a91-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="50a91-114">ID předplatného pro aktivní zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="50a91-114">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="50a91-115">C\#</span><span class="sxs-lookup"><span data-stu-id="50a91-115">C\#</span></span>

<span data-ttu-id="50a91-116">Pokud chcete získat seznam dostupných převodů zkušební verze, začněte tím, že k identifikaci zákazníka použijete metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="50a91-116">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="50a91-117">Potom Získejte rozhraní pro operace předplatného voláním metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID zkušebního předplatného.</span><span class="sxs-lookup"><span data-stu-id="50a91-117">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="50a91-118">Dále pomocí vlastnosti [**převody**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) Získejte rozhraní k dostupným operacím pro převody a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) pro načtení kolekce dostupných nabídek [**převodu**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) .</span><span class="sxs-lookup"><span data-stu-id="50a91-118">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="50a91-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="50a91-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="50a91-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="50a91-120">Request syntax</span></span>

| <span data-ttu-id="50a91-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="50a91-121">Method</span></span>  | <span data-ttu-id="50a91-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="50a91-122">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="50a91-123">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="50a91-123">**GET**</span></span> | <span data-ttu-id="50a91-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="50a91-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="50a91-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="50a91-125">URI parameter</span></span>

<span data-ttu-id="50a91-126">K identifikaci zákazníka a zkušebního předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="50a91-126">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="50a91-127">Název</span><span class="sxs-lookup"><span data-stu-id="50a91-127">Name</span></span>            | <span data-ttu-id="50a91-128">Typ</span><span class="sxs-lookup"><span data-stu-id="50a91-128">Type</span></span>   | <span data-ttu-id="50a91-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="50a91-129">Required</span></span> | <span data-ttu-id="50a91-130">Popis</span><span class="sxs-lookup"><span data-stu-id="50a91-130">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="50a91-131">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="50a91-131">customer-id</span></span>     | <span data-ttu-id="50a91-132">řetězec</span><span class="sxs-lookup"><span data-stu-id="50a91-132">string</span></span> | <span data-ttu-id="50a91-133">Yes</span><span class="sxs-lookup"><span data-stu-id="50a91-133">Yes</span></span>      | <span data-ttu-id="50a91-134">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="50a91-134">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="50a91-135">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="50a91-135">subscription-id</span></span> | <span data-ttu-id="50a91-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="50a91-136">string</span></span> | <span data-ttu-id="50a91-137">Yes</span><span class="sxs-lookup"><span data-stu-id="50a91-137">Yes</span></span>      | <span data-ttu-id="50a91-138">Řetězec ve formátu GUID, který identifikuje zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="50a91-138">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="50a91-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="50a91-139">Request headers</span></span>

<span data-ttu-id="50a91-140">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="50a91-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="50a91-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="50a91-141">Request body</span></span>

<span data-ttu-id="50a91-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="50a91-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="50a91-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="50a91-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="50a91-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="50a91-144">REST response</span></span>

<span data-ttu-id="50a91-145">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [převodu](conversions-resources.md#conversionresult) .</span><span class="sxs-lookup"><span data-stu-id="50a91-145">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="50a91-146">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="50a91-146">Response success and error codes</span></span>

<span data-ttu-id="50a91-147">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="50a91-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="50a91-148">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="50a91-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="50a91-149">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="50a91-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="50a91-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="50a91-150">Response example</span></span>

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
