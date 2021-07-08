---
title: Získání seznamu doplňků pro předplatné
description: Jak získat kolekci doplňků, které si zákazník rozhodl přidat do svého předplatného.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: c627f595333a295048b02ec4326dcdc279d07b51
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874631"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="f0cd2-103">Získání seznamu doplňků pro předplatné</span><span class="sxs-lookup"><span data-stu-id="f0cd2-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="f0cd2-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f0cd2-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f0cd2-105">Tento článek popisuje, jak získat kolekci doplňků, které si zákazník rozhodl přidat do svého prostředku **[předplatného](subscription-resources.md)** .</span><span class="sxs-lookup"><span data-stu-id="f0cd2-105">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0cd2-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f0cd2-106">Prerequisites</span></span>

- <span data-ttu-id="f0cd2-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f0cd2-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f0cd2-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f0cd2-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f0cd2-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f0cd2-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f0cd2-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f0cd2-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f0cd2-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="f0cd2-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f0cd2-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f0cd2-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f0cd2-115">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-115">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="f0cd2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="f0cd2-116">C\#</span></span>

<span data-ttu-id="f0cd2-117">Získání seznamu doplňků pro předplatné zákazníka:</span><span class="sxs-lookup"><span data-stu-id="f0cd2-117">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="f0cd2-118">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="f0cd2-118">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="f0cd2-119">Zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , za kterou následuje metoda [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="f0cd2-119">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="f0cd2-120">Zavolejte vlastnost [**addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) a za ní [**použijte Get ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span><span class="sxs-lookup"><span data-stu-id="f0cd2-120">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="f0cd2-121">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="f0cd2-121">For an example, see the following:</span></span>

- <span data-ttu-id="f0cd2-122">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f0cd2-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f0cd2-123">Project: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="f0cd2-123">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="f0cd2-124">Třída: **SubscriptionAddons. cs**</span><span class="sxs-lookup"><span data-stu-id="f0cd2-124">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f0cd2-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f0cd2-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f0cd2-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f0cd2-126">Request syntax</span></span>

| <span data-ttu-id="f0cd2-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="f0cd2-127">Method</span></span>  | <span data-ttu-id="f0cd2-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f0cd2-128">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f0cd2-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="f0cd2-129">**GET**</span></span> | <span data-ttu-id="f0cd2-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription}/addons HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f0cd2-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="f0cd2-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f0cd2-131">URI parameter</span></span>

<span data-ttu-id="f0cd2-132">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání seznamu doplňků pro odběr.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-132">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="f0cd2-133">Název</span><span class="sxs-lookup"><span data-stu-id="f0cd2-133">Name</span></span>                    | <span data-ttu-id="f0cd2-134">Typ</span><span class="sxs-lookup"><span data-stu-id="f0cd2-134">Type</span></span>     | <span data-ttu-id="f0cd2-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f0cd2-135">Required</span></span> | <span data-ttu-id="f0cd2-136">Popis</span><span class="sxs-lookup"><span data-stu-id="f0cd2-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="f0cd2-137">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="f0cd2-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="f0cd2-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="f0cd2-138">**guid**</span></span> | <span data-ttu-id="f0cd2-139">Y</span><span class="sxs-lookup"><span data-stu-id="f0cd2-139">Y</span></span>        | <span data-ttu-id="f0cd2-140">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="f0cd2-141">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="f0cd2-141">**id-for-subscription**</span></span> | <span data-ttu-id="f0cd2-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="f0cd2-142">**guid**</span></span> | <span data-ttu-id="f0cd2-143">Y</span><span class="sxs-lookup"><span data-stu-id="f0cd2-143">Y</span></span>        | <span data-ttu-id="f0cd2-144">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f0cd2-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f0cd2-145">Request headers</span></span>

<span data-ttu-id="f0cd2-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f0cd2-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f0cd2-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f0cd2-147">Request body</span></span>

<span data-ttu-id="f0cd2-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="f0cd2-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f0cd2-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f0cd2-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="f0cd2-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f0cd2-150">REST response</span></span>

<span data-ttu-id="f0cd2-151">V případě úspěchu tato metoda vrátí kolekci prostředků v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-151">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f0cd2-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f0cd2-152">Response success and error codes</span></span>

<span data-ttu-id="f0cd2-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f0cd2-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f0cd2-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f0cd2-155">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f0cd2-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f0cd2-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f0cd2-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 25 Nov 2015 05:50:45 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "42226ed6-070a-4e0f-b80c-4cdfB3e97aa7",
        "friendlyName": "Myofferpurchase",
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
