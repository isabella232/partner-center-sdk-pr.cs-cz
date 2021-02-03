---
title: Aktualizace přezdívky pro předplatné
description: Aktualizuje popisný název nebo přezdívku pro předplatné zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 57a9fec4b69d4a64128425ea58b4bb84d0d7dd54
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766966"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="050e6-103">Aktualizace přezdívky pro předplatné</span><span class="sxs-lookup"><span data-stu-id="050e6-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="050e6-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="050e6-104">**Applies To**</span></span>

- <span data-ttu-id="050e6-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="050e6-105">Partner Center</span></span>
- <span data-ttu-id="050e6-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="050e6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="050e6-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="050e6-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="050e6-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="050e6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="050e6-109">Aktualizuje popisný název nebo přezdívku pro [předplatné](subscription-resources.md)zákazníka.</span><span class="sxs-lookup"><span data-stu-id="050e6-109">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="050e6-110">Tento název se zobrazí v partnerském centru, které vám pomůžou odlišit předplatná v účtu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="050e6-110">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="050e6-111">Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="050e6-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="050e6-112">Pak vyberte příslušné předplatné, které chcete přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="050e6-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="050e6-113">Chcete-li dokončit, změňte název v poli **Přezdívka předplatného** a pak vyberte **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="050e6-113">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="050e6-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="050e6-114">Prerequisites</span></span>

- <span data-ttu-id="050e6-115">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="050e6-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="050e6-116">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="050e6-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="050e6-117">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="050e6-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="050e6-118">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="050e6-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="050e6-119">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="050e6-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="050e6-120">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="050e6-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="050e6-121">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="050e6-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="050e6-122">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="050e6-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="050e6-123">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="050e6-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="050e6-124">C\#</span><span class="sxs-lookup"><span data-stu-id="050e6-124">C\#</span></span>

<span data-ttu-id="050e6-125">Pokud chcete aktualizovat přezdívku předplatného zákazníka, nejdřív [získejte předplatné](get-a-subscription-by-id.md)a pak změňte vlastnost [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) předplatného.</span><span class="sxs-lookup"><span data-stu-id="050e6-125">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="050e6-126">Po provedení změny použijte svou kolekci [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="050e6-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="050e6-127">Poté zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a potom metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="050e6-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="050e6-128">Potom dokončete voláním metody [**patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) .</span><span class="sxs-lookup"><span data-stu-id="050e6-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="050e6-129">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="050e6-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="050e6-130">**Projekt**: PartnerSDK. FeatureSamples **Třída**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="050e6-130">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="050e6-131">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="050e6-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="050e6-132">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="050e6-132">Request syntax</span></span>

| <span data-ttu-id="050e6-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="050e6-133">Method</span></span>    | <span data-ttu-id="050e6-134">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="050e6-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="050e6-135">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="050e6-135">**PATCH**</span></span> | <span data-ttu-id="050e6-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="050e6-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="050e6-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="050e6-137">URI parameter</span></span>

<span data-ttu-id="050e6-138">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro aktualizaci přezdívky předplatného.</span><span class="sxs-lookup"><span data-stu-id="050e6-138">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="050e6-139">Název</span><span class="sxs-lookup"><span data-stu-id="050e6-139">Name</span></span>                    | <span data-ttu-id="050e6-140">Typ</span><span class="sxs-lookup"><span data-stu-id="050e6-140">Type</span></span>     | <span data-ttu-id="050e6-141">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="050e6-141">Required</span></span> | <span data-ttu-id="050e6-142">Popis</span><span class="sxs-lookup"><span data-stu-id="050e6-142">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="050e6-143">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="050e6-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="050e6-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="050e6-144">**guid**</span></span> | <span data-ttu-id="050e6-145">Y</span><span class="sxs-lookup"><span data-stu-id="050e6-145">Y</span></span>        | <span data-ttu-id="050e6-146">**Customer-tenant-ID** (identifikátor GUID).</span><span class="sxs-lookup"><span data-stu-id="050e6-146">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="050e6-147">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="050e6-147">**id-for-subscription**</span></span> | <span data-ttu-id="050e6-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="050e6-148">**guid**</span></span> | <span data-ttu-id="050e6-149">Y</span><span class="sxs-lookup"><span data-stu-id="050e6-149">Y</span></span>        | <span data-ttu-id="050e6-150">ID předplatného (identifikátor GUID).</span><span class="sxs-lookup"><span data-stu-id="050e6-150">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="050e6-151">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="050e6-151">Request headers</span></span>

<span data-ttu-id="050e6-152">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="050e6-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="050e6-153">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="050e6-153">Request body</span></span>

<span data-ttu-id="050e6-154">V těle žádosti se vyžaduje prostředek s úplným **předplatným** .</span><span class="sxs-lookup"><span data-stu-id="050e6-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="050e6-155">Zajistěte, aby byla vlastnost **FriendlyName** aktualizována.</span><span class="sxs-lookup"><span data-stu-id="050e6-155">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="050e6-156">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="050e6-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "<subscriptionID>",
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
    OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="050e6-157">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="050e6-157">REST response</span></span>

<span data-ttu-id="050e6-158">V případě úspěchu tato metoda vrátí aktualizované vlastnosti prostředku [předplatného](subscription-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="050e6-158">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="050e6-159">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="050e6-159">Response success and error codes</span></span>

<span data-ttu-id="050e6-160">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="050e6-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="050e6-161">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="050e6-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="050e6-162">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="050e6-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="050e6-163">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="050e6-163">Response example</span></span>

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
    "Id": "<subscriptionID>",
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
