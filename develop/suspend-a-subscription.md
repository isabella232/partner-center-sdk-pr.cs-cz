---
title: Pozastavení předplatného
description: Pozastaví prostředek předplatného, který se shoduje s ID zákazníka a předplatného, kvůli podvodům nebo nedoplatkům. Na řídicím panelu partnerského centra se tato operace dá provést při prvním výběru zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dae7c3422a403c48a2b10424c4ae5dbdbc498ea
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547338"
---
# <a name="suspend-a-subscription"></a><span data-ttu-id="fc413-104">Pozastavení předplatného</span><span class="sxs-lookup"><span data-stu-id="fc413-104">Suspend a subscription</span></span>

<span data-ttu-id="fc413-105">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fc413-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fc413-106">Pozastaví prostředek [předplatného](subscription-resources.md) , který se shoduje s ID zákazníka a předplatného, kvůli podvodům nebo nedoplatkům.</span><span class="sxs-lookup"><span data-stu-id="fc413-106">Suspends a [Subscription](subscription-resources.md) resource that matches the customer and subscription ID due to fraud or non-payment.</span></span>

<span data-ttu-id="fc413-107">Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="fc413-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="fc413-108">Pak vyberte příslušné předplatné, které chcete přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="fc413-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="fc413-109">Chcete-li dokončit, klikněte na tlačítko **pozastaveno** a pak vyberte **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="fc413-109">To finish, choose the **Suspended** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc413-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fc413-110">Prerequisites</span></span>

- <span data-ttu-id="fc413-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fc413-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fc413-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="fc413-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fc413-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc413-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fc413-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fc413-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fc413-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="fc413-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fc413-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="fc413-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fc413-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="fc413-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fc413-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc413-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fc413-119">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="fc413-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="fc413-120">C\#</span><span class="sxs-lookup"><span data-stu-id="fc413-120">C\#</span></span>

<span data-ttu-id="fc413-121">Pokud chcete pozastavit předplatné zákazníka, nejdřív [získejte předplatné](get-a-subscription-by-id.md)a pak změňte vlastnost [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) odběru.</span><span class="sxs-lookup"><span data-stu-id="fc413-121">To suspend a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="fc413-122">Informace o **stavových** kódech naleznete v [SubscriptionStatus Enumeration/dotnet/API/Microsoft. Store. partnercenter. Models. Subscriptions. SubscriptionStatus).</span><span class="sxs-lookup"><span data-stu-id="fc413-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="fc413-123">Po provedení změny použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="fc413-123">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="fc413-124">Poté zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a potom metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="fc413-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="fc413-125">Potom dokončete voláním metody **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="fc413-125">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Suspended
   });
```

<span data-ttu-id="fc413-126">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fc413-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fc413-127">**Project**: PartnerSDK. FeatureSample **třída**: UpdateSubscription. cs</span><span class="sxs-lookup"><span data-stu-id="fc413-127">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fc413-128">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fc413-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc413-129">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fc413-129">Request syntax</span></span>

| <span data-ttu-id="fc413-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="fc413-130">Method</span></span>    | <span data-ttu-id="fc413-131">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fc413-131">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc413-132">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="fc413-132">**PATCH**</span></span> | <span data-ttu-id="fc413-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fc413-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fc413-134">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fc413-134">URI parameter</span></span>

<span data-ttu-id="fc413-135">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro pozastavení předplatného.</span><span class="sxs-lookup"><span data-stu-id="fc413-135">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="fc413-136">Název</span><span class="sxs-lookup"><span data-stu-id="fc413-136">Name</span></span>                    | <span data-ttu-id="fc413-137">Typ</span><span class="sxs-lookup"><span data-stu-id="fc413-137">Type</span></span>     | <span data-ttu-id="fc413-138">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fc413-138">Required</span></span> | <span data-ttu-id="fc413-139">Popis</span><span class="sxs-lookup"><span data-stu-id="fc413-139">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="fc413-140">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="fc413-140">**customer-tenant-id**</span></span>  | <span data-ttu-id="fc413-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="fc413-141">**guid**</span></span> | <span data-ttu-id="fc413-142">Y</span><span class="sxs-lookup"><span data-stu-id="fc413-142">Y</span></span>        | <span data-ttu-id="fc413-143">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="fc413-143">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="fc413-144">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="fc413-144">**id-for-subscription**</span></span> | <span data-ttu-id="fc413-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="fc413-145">**guid**</span></span> | <span data-ttu-id="fc413-146">Y</span><span class="sxs-lookup"><span data-stu-id="fc413-146">Y</span></span>        | <span data-ttu-id="fc413-147">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="fc413-147">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fc413-148">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fc413-148">Request headers</span></span>

<span data-ttu-id="fc413-149">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fc413-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fc413-150">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fc413-150">Request body</span></span>

<span data-ttu-id="fc413-151">V těle žádosti se vyžaduje prostředek s úplným **předplatným** .</span><span class="sxs-lookup"><span data-stu-id="fc413-151">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="fc413-152">Ujistěte se, že se vlastnost **status** aktualizovala.</span><span class="sxs-lookup"><span data-stu-id="fc413-152">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="fc413-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fc413-153">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="fc413-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fc413-154">REST response</span></span>

<span data-ttu-id="fc413-155">V případě úspěchu tato metoda vrátí aktualizované vlastnosti prostředku [předplatného](subscription-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="fc413-155">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc413-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fc413-156">Response success and error codes</span></span>

<span data-ttu-id="fc413-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fc413-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc413-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fc413-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc413-159">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fc413-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fc413-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fc413-160">Response example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
