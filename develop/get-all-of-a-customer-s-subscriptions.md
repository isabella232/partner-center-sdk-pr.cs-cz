---
title: Získání předplatných zákazníka
description: Jak získat kolekci předplatných zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 01ac9e5169258d0ac263d5bbe8cff567c76f98ed
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760619"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="afddd-103">Získání předplatných zákazníka</span><span class="sxs-lookup"><span data-stu-id="afddd-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="afddd-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="afddd-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="afddd-105">Jak získat kolekci předplatných zákazníka.</span><span class="sxs-lookup"><span data-stu-id="afddd-105">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afddd-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="afddd-106">Prerequisites</span></span>

- <span data-ttu-id="afddd-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="afddd-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="afddd-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="afddd-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="afddd-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="afddd-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="afddd-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="afddd-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="afddd-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="afddd-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="afddd-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="afddd-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="afddd-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="afddd-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="afddd-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="afddd-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="afddd-115">C\#</span><span class="sxs-lookup"><span data-stu-id="afddd-115">C\#</span></span>

<span data-ttu-id="afddd-116">Pokud chcete získat seznam všech předplatných zákazníka, nejprve použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="afddd-116">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="afddd-117">Pak pomocí vlastnosti [**Subscriptions (předplatná**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) ) načtěte rozhraní pro operace shromažďování předplatných.</span><span class="sxs-lookup"><span data-stu-id="afddd-117">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="afddd-118">Nakonec voláním metod [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) načtěte kolekci předplatných zákazníka.</span><span class="sxs-lookup"><span data-stu-id="afddd-118">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="afddd-119">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="afddd-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="afddd-120">**Project**: sada SDK pro partnerských Center: **třídy** ukázek: getsubscriptions. cs</span><span class="sxs-lookup"><span data-stu-id="afddd-120">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="afddd-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="afddd-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="afddd-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="afddd-122">Request syntax</span></span>

| <span data-ttu-id="afddd-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="afddd-123">Method</span></span>  | <span data-ttu-id="afddd-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="afddd-124">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="afddd-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="afddd-125">**GET**</span></span> | <span data-ttu-id="afddd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="afddd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="afddd-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="afddd-127">URI parameter</span></span>

<span data-ttu-id="afddd-128">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech předplatných.</span><span class="sxs-lookup"><span data-stu-id="afddd-128">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="afddd-129">Název</span><span class="sxs-lookup"><span data-stu-id="afddd-129">Name</span></span>               | <span data-ttu-id="afddd-130">Typ</span><span class="sxs-lookup"><span data-stu-id="afddd-130">Type</span></span>   | <span data-ttu-id="afddd-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="afddd-131">Required</span></span> | <span data-ttu-id="afddd-132">Popis</span><span class="sxs-lookup"><span data-stu-id="afddd-132">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="afddd-133">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="afddd-133">customer-tenant-id</span></span> | <span data-ttu-id="afddd-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="afddd-134">string</span></span> | <span data-ttu-id="afddd-135">Yes</span><span class="sxs-lookup"><span data-stu-id="afddd-135">Yes</span></span>      | <span data-ttu-id="afddd-136">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="afddd-136">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="afddd-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="afddd-137">Request headers</span></span>

<span data-ttu-id="afddd-138">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="afddd-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="afddd-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="afddd-139">Request body</span></span>

<span data-ttu-id="afddd-140">Žádné</span><span class="sxs-lookup"><span data-stu-id="afddd-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="afddd-141">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="afddd-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="afddd-142">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="afddd-142">REST response</span></span>

<span data-ttu-id="afddd-143">V případě úspěchu tato metoda vrátí kolekci prostředků [předplatného](subscription-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="afddd-143">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="afddd-144">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="afddd-144">Response success and error codes</span></span>

<span data-ttu-id="afddd-145">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="afddd-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="afddd-146">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="afddd-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="afddd-147">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="afddd-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="afddd-148">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="afddd-148">Response example</span></span>

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
