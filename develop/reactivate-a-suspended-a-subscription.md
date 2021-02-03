---
title: Opětovná aktivace pozastaveného předplatného
description: Znovu aktivuje předplatné, které bylo dříve pozastaveno kvůli neplatbě. Na řídicím panelu partnerského centra se tato operace dá provést při prvním výběru zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17c63e9c6d4c9e111bfea28e97319696534fa122
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766956"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="f50ee-103">Opětovná aktivace pozastaveného předplatného</span><span class="sxs-lookup"><span data-stu-id="f50ee-103">Reactivate a suspended subscription</span></span>

<span data-ttu-id="f50ee-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="f50ee-104">**Applies To**</span></span>

- <span data-ttu-id="f50ee-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="f50ee-105">Partner Center</span></span>
- <span data-ttu-id="f50ee-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="f50ee-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f50ee-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="f50ee-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f50ee-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f50ee-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f50ee-109">Znovu aktivuje [předplatné](subscription-resources.md) , které bylo dříve pozastaveno kvůli neplatbě.</span><span class="sxs-lookup"><span data-stu-id="f50ee-109">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="f50ee-110">Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="f50ee-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="f50ee-111">Pak vyberte příslušné předplatné, které chcete přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="f50ee-111">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="f50ee-112">Chcete-li dokončit, klikněte na tlačítko **aktivní** a pak vyberte **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="f50ee-112">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f50ee-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f50ee-113">Prerequisites</span></span>

- <span data-ttu-id="f50ee-114">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f50ee-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f50ee-115">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="f50ee-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f50ee-116">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f50ee-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f50ee-117">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="f50ee-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f50ee-118">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="f50ee-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f50ee-119">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="f50ee-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f50ee-120">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="f50ee-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f50ee-121">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f50ee-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f50ee-122">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="f50ee-122">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="f50ee-123">C\#</span><span class="sxs-lookup"><span data-stu-id="f50ee-123">C\#</span></span>

<span data-ttu-id="f50ee-124">Pokud chcete znovu aktivovat předplatné zákazníka, nejdřív [získejte předplatné](get-a-subscription-by-id.md)a pak změňte vlastnost [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) odběru.</span><span class="sxs-lookup"><span data-stu-id="f50ee-124">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="f50ee-125">Informace o **stavových** kódech naleznete v [SubscriptionStatus Enumeration/dotnet/API/Microsoft. Store. partnercenter. Models. Subscriptions. SubscriptionStatus).</span><span class="sxs-lookup"><span data-stu-id="f50ee-125">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="f50ee-126">Po provedení změny použijte svou kolekci [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="f50ee-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="f50ee-127">Poté zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a potom metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="f50ee-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="f50ee-128">Potom dokončete voláním metody [**patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) .</span><span class="sxs-lookup"><span data-stu-id="f50ee-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

<span data-ttu-id="f50ee-129">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f50ee-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f50ee-130">**Projekt**: FeatureSamplesApplication.</span><span class="sxs-lookup"><span data-stu-id="f50ee-130">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="f50ee-131">**Třída**: UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="f50ee-131">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="f50ee-132">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f50ee-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f50ee-133">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f50ee-133">Request syntax</span></span>

| <span data-ttu-id="f50ee-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="f50ee-134">Method</span></span>    | <span data-ttu-id="f50ee-135">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f50ee-135">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f50ee-136">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="f50ee-136">**PATCH**</span></span> | <span data-ttu-id="f50ee-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f50ee-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f50ee-138">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f50ee-138">URI parameter</span></span>

<span data-ttu-id="f50ee-139">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro opětovnou aktivaci předplatného.</span><span class="sxs-lookup"><span data-stu-id="f50ee-139">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="f50ee-140">Název</span><span class="sxs-lookup"><span data-stu-id="f50ee-140">Name</span></span>                    | <span data-ttu-id="f50ee-141">Typ</span><span class="sxs-lookup"><span data-stu-id="f50ee-141">Type</span></span>     | <span data-ttu-id="f50ee-142">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f50ee-142">Required</span></span> | <span data-ttu-id="f50ee-143">Popis</span><span class="sxs-lookup"><span data-stu-id="f50ee-143">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="f50ee-144">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="f50ee-144">**customer-tenant-id**</span></span>  | <span data-ttu-id="f50ee-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="f50ee-145">**guid**</span></span> | <span data-ttu-id="f50ee-146">Y</span><span class="sxs-lookup"><span data-stu-id="f50ee-146">Y</span></span>        | <span data-ttu-id="f50ee-147">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="f50ee-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="f50ee-148">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="f50ee-148">**id-for-subscription**</span></span> | <span data-ttu-id="f50ee-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="f50ee-149">**guid**</span></span> | <span data-ttu-id="f50ee-150">Y</span><span class="sxs-lookup"><span data-stu-id="f50ee-150">Y</span></span>        | <span data-ttu-id="f50ee-151">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="f50ee-151">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f50ee-152">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f50ee-152">Request headers</span></span>

<span data-ttu-id="f50ee-153">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f50ee-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f50ee-154">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f50ee-154">Request body</span></span>

<span data-ttu-id="f50ee-155">V těle žádosti se vyžaduje prostředek s úplným **předplatným** .</span><span class="sxs-lookup"><span data-stu-id="f50ee-155">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="f50ee-156">Ujistěte se, že se vlastnost **status** aktualizovala.</span><span class="sxs-lookup"><span data-stu-id="f50ee-156">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="f50ee-157">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f50ee-157">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
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
    "Status": "active",
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

## <a name="rest-response"></a><span data-ttu-id="f50ee-158">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f50ee-158">REST response</span></span>

<span data-ttu-id="f50ee-159">V případě úspěchu tato metoda vrátí aktualizované vlastnosti prostředku [předplatného](subscription-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="f50ee-159">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f50ee-160">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f50ee-160">Response success and error codes</span></span>

<span data-ttu-id="f50ee-161">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f50ee-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f50ee-162">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f50ee-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f50ee-163">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f50ee-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f50ee-164">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f50ee-164">Response example</span></span>

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
    "Status": "active",
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
