---
title: Získání předplatného podle ID
description: Získá prostředek předplatného, který odpovídá ID zákazníka a ID předplatného.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6690a6886eeb31a78cdb556280d4bdc2b4beb124
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766960"
---
# <a name="get-a-subscription-by-id"></a><span data-ttu-id="93445-103">Získání předplatného podle ID</span><span class="sxs-lookup"><span data-stu-id="93445-103">Get a subscription by ID</span></span>

<span data-ttu-id="93445-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="93445-104">**Applies To**</span></span>

- <span data-ttu-id="93445-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="93445-105">Partner Center</span></span>
- <span data-ttu-id="93445-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="93445-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="93445-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="93445-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="93445-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="93445-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="93445-109">Získá prostředek [předplatného](subscription-resources.md) , který odpovídá ID zákazníka a ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="93445-109">Gets a [Subscription](subscription-resources.md) resource that matches the customer ID and the subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93445-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="93445-110">Prerequisites</span></span>

- <span data-ttu-id="93445-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="93445-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="93445-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="93445-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="93445-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="93445-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="93445-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="93445-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="93445-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="93445-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="93445-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="93445-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="93445-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="93445-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="93445-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="93445-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="93445-119">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="93445-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="93445-120">C\#</span><span class="sxs-lookup"><span data-stu-id="93445-120">C\#</span></span>

<span data-ttu-id="93445-121">Chcete-li získat předplatné podle ID, Začněte získáním rozhraní pro operace předplatného voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, který identifikuje zákazníka, a [**předplatným metodu. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pro identifikaci předplatného.</span><span class="sxs-lookup"><span data-stu-id="93445-121">To get a subscription by ID, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription.</span></span> <span data-ttu-id="93445-122">Použijte toto [**rozhraní**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) k načtení podrobností o předplatném voláním [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="93445-122">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionID;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionID).Get();
```

<span data-ttu-id="93445-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="93445-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="93445-124">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="93445-124">**Project**: Partner Center SDK Samples **Class**: GetSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="93445-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="93445-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="93445-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="93445-126">Request syntax</span></span>

| <span data-ttu-id="93445-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="93445-127">Method</span></span>  | <span data-ttu-id="93445-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="93445-128">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="93445-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="93445-129">**GET**</span></span> | <span data-ttu-id="93445-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="93445-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="93445-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="93445-131">URI parameter</span></span>

<span data-ttu-id="93445-132">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání předplatného.</span><span class="sxs-lookup"><span data-stu-id="93445-132">This table lists the required query parameters to get the subscription.</span></span>

| <span data-ttu-id="93445-133">Název</span><span class="sxs-lookup"><span data-stu-id="93445-133">Name</span></span>                    | <span data-ttu-id="93445-134">Typ</span><span class="sxs-lookup"><span data-stu-id="93445-134">Type</span></span>     | <span data-ttu-id="93445-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="93445-135">Required</span></span> | <span data-ttu-id="93445-136">Popis</span><span class="sxs-lookup"><span data-stu-id="93445-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="93445-137">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="93445-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="93445-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="93445-138">**guid**</span></span> | <span data-ttu-id="93445-139">Y</span><span class="sxs-lookup"><span data-stu-id="93445-139">Y</span></span>        | <span data-ttu-id="93445-140">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="93445-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="93445-141">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="93445-141">**id-for-subscription**</span></span> | <span data-ttu-id="93445-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="93445-142">**guid**</span></span> | <span data-ttu-id="93445-143">Y</span><span class="sxs-lookup"><span data-stu-id="93445-143">Y</span></span>        | <span data-ttu-id="93445-144">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="93445-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="93445-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="93445-145">Request headers</span></span>

<span data-ttu-id="93445-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="93445-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="93445-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="93445-147">Request body</span></span>

<span data-ttu-id="93445-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="93445-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="93445-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="93445-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="93445-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="93445-150">REST response</span></span>

<span data-ttu-id="93445-151">V případě úspěchu tato metoda vrátí prostředek [odběru](subscription-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="93445-151">If successful, this method returns a [Subscription](subscription-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="93445-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="93445-152">Response success and error codes</span></span>

<span data-ttu-id="93445-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="93445-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="93445-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="93445-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="93445-155">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="93445-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-a-standard-subscription"></a><span data-ttu-id="93445-156">Příklad odpovědi pro standardní předplatné</span><span class="sxs-lookup"><span data-stu-id="93445-156">Response example for a standard subscription</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 833
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CV: 7v11Wa//5EuGEo+A.0
MS-ServerId: 202010406
Date: Fri, 27 Jan 2017 21:51:40 GMT

{
    "id": "A356AC8C-E310-44F4-BF85-C7F29044AF99",
    "entitlementId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
    "offerId": "MS-AZR-0145P",
    "offerName": "Microsoft Azure",
    "friendlyName": "Microsoft Azure",
    "quantity": 1,
    "unitType": "Usage-based",
    "creationDate": "2016-05-10T07:30:05.427Z",
    "effectiveStartDate": "2016-05-10T00:00:00Z",
    "commitmentEndDate": "9999-12-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": false,
    "billingType": "usage",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/MS-AZR-0145P?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "B23FDEDD-D6BD-415A-8B71-3624C81C9644",
    "attributes": {
        "etag": "eyJpZCI6ImEzNTZhYzhjLWUzMTAtNDRmNC1iZjg1LWM3ZjI5MDQ0YWY5OSIsInZlcnNpb24iOjJ9",
        "objectType": "Subscription"
    }
}
```

### <a name="response-example-for-an-add-on-subscription"></a><span data-ttu-id="93445-157">Příklad odpovědi pro předplatné doplňku</span><span class="sxs-lookup"><span data-stu-id="93445-157">Response example for an add-on subscription</span></span>

<span data-ttu-id="93445-158">Odpověď pro předplatné doplňku obsahuje ID nadřazeného předplatného v textu a v odkazech.</span><span class="sxs-lookup"><span data-stu-id="93445-158">The response for an add-on subscription includes the parent subscription ID in the body and in the links.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1132
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6eacec93-852d-4167-9d96-c57809bea7ed
MS-RequestId: 22bfd0fb-d1e6-4a8f-aa1a-124b7c820d80
MS-CV: cmde2DtbuUWi8JLq.0
MS-ServerId: 201022015
Date: Fri, 27 Jan 2017 00:12:53 GMT

{
    "id": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
    "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
    "offerName": "Exchange Online Archiving for Exchange Online",
    "friendlyName": "Some friendly name",
    "quantity": 2,
    "unitType": "Licenses",
    "parentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
    "creationDate": "2017-01-25T23:01:08.693Z",
    "effectiveStartDate": "2017-01-25T00:00:00Z",
    "commitmentEndDate": "2018-02-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": true,
    "billingType": "license",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60?country=US",
            "method": "GET",
            "headers": []
        },
        "parentSubscription": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "CF3B0E37-BE0B-4CDD-B584-D1A97D98A922",
    "attributes": {
        "etag": "eyJpZCI6Ijk2OGJhMWNmLWMxNDYtNGFkZi1hMzAwLTMwOGRjZjcxOGVlZSIsInZlcnNpb24iOjF9",
        "objectType": "Subscription"
    }
}
```
