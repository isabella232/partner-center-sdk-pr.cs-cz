---
title: Získání předplatných zákazníka
description: Jak získat kolekci předplatných zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a037e4a81fccbff0a02b0bdf6d93478ee15fd50f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766990"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="55801-103">Získání předplatných zákazníka</span><span class="sxs-lookup"><span data-stu-id="55801-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="55801-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="55801-104">**Applies To**</span></span>

- <span data-ttu-id="55801-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="55801-105">Partner Center</span></span>
- <span data-ttu-id="55801-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="55801-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="55801-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="55801-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="55801-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="55801-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="55801-109">Jak získat kolekci předplatných zákazníka.</span><span class="sxs-lookup"><span data-stu-id="55801-109">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55801-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="55801-110">Prerequisites</span></span>

- <span data-ttu-id="55801-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="55801-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="55801-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="55801-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="55801-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="55801-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="55801-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="55801-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="55801-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="55801-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="55801-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="55801-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="55801-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="55801-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="55801-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="55801-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="55801-119">C\#</span><span class="sxs-lookup"><span data-stu-id="55801-119">C\#</span></span>

<span data-ttu-id="55801-120">Pokud chcete získat seznam všech předplatných zákazníka, nejprve použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="55801-120">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="55801-121">Pak pomocí vlastnosti [**Subscriptions (předplatná**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) ) načtěte rozhraní pro operace shromažďování předplatných.</span><span class="sxs-lookup"><span data-stu-id="55801-121">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="55801-122">Nakonec voláním metod [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) načtěte kolekci předplatných zákazníka.</span><span class="sxs-lookup"><span data-stu-id="55801-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="55801-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="55801-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="55801-124">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetSubscriptions.cs</span><span class="sxs-lookup"><span data-stu-id="55801-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="55801-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="55801-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="55801-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="55801-126">Request syntax</span></span>

| <span data-ttu-id="55801-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="55801-127">Method</span></span>  | <span data-ttu-id="55801-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="55801-128">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="55801-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="55801-129">**GET**</span></span> | <span data-ttu-id="55801-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="55801-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="55801-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="55801-131">URI parameter</span></span>

<span data-ttu-id="55801-132">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech předplatných.</span><span class="sxs-lookup"><span data-stu-id="55801-132">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="55801-133">Název</span><span class="sxs-lookup"><span data-stu-id="55801-133">Name</span></span>               | <span data-ttu-id="55801-134">Typ</span><span class="sxs-lookup"><span data-stu-id="55801-134">Type</span></span>   | <span data-ttu-id="55801-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="55801-135">Required</span></span> | <span data-ttu-id="55801-136">Popis</span><span class="sxs-lookup"><span data-stu-id="55801-136">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="55801-137">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="55801-137">customer-tenant-id</span></span> | <span data-ttu-id="55801-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="55801-138">string</span></span> | <span data-ttu-id="55801-139">Yes</span><span class="sxs-lookup"><span data-stu-id="55801-139">Yes</span></span>      | <span data-ttu-id="55801-140">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="55801-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="55801-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="55801-141">Request headers</span></span>

<span data-ttu-id="55801-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="55801-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="55801-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="55801-143">Request body</span></span>

<span data-ttu-id="55801-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="55801-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="55801-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="55801-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="55801-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="55801-146">REST response</span></span>

<span data-ttu-id="55801-147">V případě úspěchu tato metoda vrátí kolekci prostředků [předplatného](subscription-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="55801-147">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="55801-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="55801-148">Response success and error codes</span></span>

<span data-ttu-id="55801-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="55801-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="55801-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="55801-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="55801-151">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="55801-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="55801-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="55801-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
Date: Wed, 25 Nov 2015 05:43:06 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "nickname",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
