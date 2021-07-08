---
title: Získání stavu zřizování předplatných
description: Jak získat stav zřizování předplatného pro předplatné zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8797fa494cd77f11a1179d6406ca021f0d7788c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548698"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="16a7d-103">Získání stavu zřizování předplatných</span><span class="sxs-lookup"><span data-stu-id="16a7d-103">Get subscription provisioning status</span></span>

<span data-ttu-id="16a7d-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="16a7d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="16a7d-105">Jak získat stav zřizování předplatného pro předplatné zákazníka.</span><span class="sxs-lookup"><span data-stu-id="16a7d-105">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16a7d-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="16a7d-106">Prerequisites</span></span>

- <span data-ttu-id="16a7d-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="16a7d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="16a7d-108">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="16a7d-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="16a7d-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="16a7d-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="16a7d-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="16a7d-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="16a7d-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="16a7d-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="16a7d-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="16a7d-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="16a7d-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="16a7d-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="16a7d-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="16a7d-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="16a7d-115">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="16a7d-115">A subscription identifier.</span></span>

- <span data-ttu-id="16a7d-116">K provedení této operace se vyžaduje delegované oprávnění správce k předplatnému.</span><span class="sxs-lookup"><span data-stu-id="16a7d-116">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="16a7d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="16a7d-117">C\#</span></span>

<span data-ttu-id="16a7d-118">Pokud chcete získat stav zřizování předplatného, začněte tím, že k identifikaci zákazníka použijete metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="16a7d-118">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="16a7d-119">Pak můžete získat rozhraní k operacím předplatného voláním metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="16a7d-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="16a7d-120">Dále pomocí vlastnosti [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) Získejte rozhraní pro operace stavu zřizování aktuálního předplatného a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) pro načtení objektu [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) .</span><span class="sxs-lookup"><span data-stu-id="16a7d-120">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="16a7d-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="16a7d-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="16a7d-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="16a7d-122">Request syntax</span></span>

| <span data-ttu-id="16a7d-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="16a7d-123">Method</span></span>  | <span data-ttu-id="16a7d-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="16a7d-124">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="16a7d-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="16a7d-125">**GET**</span></span> | <span data-ttu-id="16a7d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/provisioningstatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="16a7d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="16a7d-127">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="16a7d-127">URI parameters</span></span>

<span data-ttu-id="16a7d-128">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="16a7d-128">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="16a7d-129">Název</span><span class="sxs-lookup"><span data-stu-id="16a7d-129">Name</span></span>            | <span data-ttu-id="16a7d-130">Typ</span><span class="sxs-lookup"><span data-stu-id="16a7d-130">Type</span></span>   | <span data-ttu-id="16a7d-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="16a7d-131">Required</span></span> | <span data-ttu-id="16a7d-132">Popis</span><span class="sxs-lookup"><span data-stu-id="16a7d-132">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="16a7d-133">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="16a7d-133">customer-id</span></span>     | <span data-ttu-id="16a7d-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="16a7d-134">string</span></span> | <span data-ttu-id="16a7d-135">Yes</span><span class="sxs-lookup"><span data-stu-id="16a7d-135">Yes</span></span>      | <span data-ttu-id="16a7d-136">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="16a7d-136">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="16a7d-137">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="16a7d-137">subscription-id</span></span> | <span data-ttu-id="16a7d-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="16a7d-138">string</span></span> | <span data-ttu-id="16a7d-139">Yes</span><span class="sxs-lookup"><span data-stu-id="16a7d-139">Yes</span></span>      | <span data-ttu-id="16a7d-140">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="16a7d-140">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="16a7d-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="16a7d-141">Request headers</span></span>

<span data-ttu-id="16a7d-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="16a7d-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="16a7d-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="16a7d-143">Request body</span></span>

<span data-ttu-id="16a7d-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="16a7d-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="16a7d-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="16a7d-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="16a7d-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="16a7d-146">REST response</span></span>

<span data-ttu-id="16a7d-147">V případě úspěchu obsahuje tělo odpovědi prostředek [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) .</span><span class="sxs-lookup"><span data-stu-id="16a7d-147">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="16a7d-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="16a7d-148">Response success and error codes</span></span>

<span data-ttu-id="16a7d-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="16a7d-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="16a7d-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="16a7d-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="16a7d-151">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="16a7d-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="16a7d-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="16a7d-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a><span data-ttu-id="16a7d-153">Poznámky</span><span class="sxs-lookup"><span data-stu-id="16a7d-153">Remarks</span></span>

- <span data-ttu-id="16a7d-154">Během přiřazení změny licence je pole stav v [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) nastaveno na "čeká".</span><span class="sxs-lookup"><span data-stu-id="16a7d-154">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="16a7d-155">Pole stav se aktualizuje každých 15 minut.</span><span class="sxs-lookup"><span data-stu-id="16a7d-155">The status field is updated every 15 minutes.</span></span>
