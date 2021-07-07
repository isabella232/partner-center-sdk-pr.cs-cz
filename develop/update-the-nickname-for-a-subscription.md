---
title: Aktualizace přezdívky pro předplatné
description: Aktualizuje popisný název nebo přezdívku pro předplatné zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 195a85fcf29b3e4c9fe0e578d4d8cb80ca068c40
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530000"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="59dbc-103">Aktualizace přezdívky pro předplatné</span><span class="sxs-lookup"><span data-stu-id="59dbc-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="59dbc-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="59dbc-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="59dbc-105">Aktualizuje popisný název nebo přezdívku pro předplatné [zákazníka.](subscription-resources.md)</span><span class="sxs-lookup"><span data-stu-id="59dbc-105">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="59dbc-106">Tento název se Partnerské centrum, který vám pomůže rozlišit předplatná v účtu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="59dbc-106">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="59dbc-107">Na řídicím Partnerské centrum můžete tuto operaci provést tak, že nejprve [vyberete zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="59dbc-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="59dbc-108">Pak vyberte předplatné, které chcete přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="59dbc-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="59dbc-109">Dokončete to tak, že v poli Název předplatného **změníte** název a pak vyberete **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="59dbc-109">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59dbc-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="59dbc-110">Prerequisites</span></span>

- <span data-ttu-id="59dbc-111">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="59dbc-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="59dbc-112">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="59dbc-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="59dbc-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59dbc-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="59dbc-114">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="59dbc-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="59dbc-115">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="59dbc-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="59dbc-116">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="59dbc-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="59dbc-117">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="59dbc-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="59dbc-118">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59dbc-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="59dbc-119">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="59dbc-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="59dbc-120">C\#</span><span class="sxs-lookup"><span data-stu-id="59dbc-120">C\#</span></span>

<span data-ttu-id="59dbc-121">Pokud chcete aktualizovat přezdívku předplatného zákazníka, nejprve [získejte](get-a-subscription-by-id.md)předplatné a pak změňte vlastnost [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) předplatného.</span><span class="sxs-lookup"><span data-stu-id="59dbc-121">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="59dbc-122">Po změně použijte kolekci [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="59dbc-122">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="59dbc-123">Potom zavolejte [**vlastnost Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a pak [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="59dbc-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="59dbc-124">Potom dokončete voláním [**metody Patch().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="59dbc-124">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="59dbc-125">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="59dbc-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="59dbc-126">**Project:** PartnerSDK.FeatureSamples – **třída:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="59dbc-126">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="59dbc-127">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="59dbc-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="59dbc-128">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="59dbc-128">Request syntax</span></span>

| <span data-ttu-id="59dbc-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="59dbc-129">Method</span></span>    | <span data-ttu-id="59dbc-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="59dbc-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="59dbc-131">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="59dbc-131">**PATCH**</span></span> | <span data-ttu-id="59dbc-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{id-pro-předplatné} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="59dbc-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="59dbc-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="59dbc-133">URI parameter</span></span>

<span data-ttu-id="59dbc-134">Tato tabulka uvádí požadovaný parametr dotazu pro aktualizaci přezdívky předplatného.</span><span class="sxs-lookup"><span data-stu-id="59dbc-134">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="59dbc-135">Název</span><span class="sxs-lookup"><span data-stu-id="59dbc-135">Name</span></span>                    | <span data-ttu-id="59dbc-136">Typ</span><span class="sxs-lookup"><span data-stu-id="59dbc-136">Type</span></span>     | <span data-ttu-id="59dbc-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="59dbc-137">Required</span></span> | <span data-ttu-id="59dbc-138">Popis</span><span class="sxs-lookup"><span data-stu-id="59dbc-138">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="59dbc-139">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="59dbc-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="59dbc-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="59dbc-140">**guid**</span></span> | <span data-ttu-id="59dbc-141">Y</span><span class="sxs-lookup"><span data-stu-id="59dbc-141">Y</span></span>        | <span data-ttu-id="59dbc-142">ID **tenanta zákazníka** (GUID).</span><span class="sxs-lookup"><span data-stu-id="59dbc-142">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="59dbc-143">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="59dbc-143">**id-for-subscription**</span></span> | <span data-ttu-id="59dbc-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="59dbc-144">**guid**</span></span> | <span data-ttu-id="59dbc-145">Y</span><span class="sxs-lookup"><span data-stu-id="59dbc-145">Y</span></span>        | <span data-ttu-id="59dbc-146">ID předplatného (GUID).</span><span class="sxs-lookup"><span data-stu-id="59dbc-146">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="59dbc-147">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="59dbc-147">Request headers</span></span>

<span data-ttu-id="59dbc-148">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="59dbc-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="59dbc-149">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="59dbc-149">Request body</span></span>

<span data-ttu-id="59dbc-150">V textu **požadavku** se vyžaduje úplný prostředek předplatného.</span><span class="sxs-lookup"><span data-stu-id="59dbc-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="59dbc-151">Ujistěte se, že byla aktualizována vlastnost **FriendlyName.**</span><span class="sxs-lookup"><span data-stu-id="59dbc-151">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="59dbc-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="59dbc-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="59dbc-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="59dbc-153">REST response</span></span>

<span data-ttu-id="59dbc-154">V případě úspěchu vrátí tato metoda [v](subscription-resources.md) textu odpovědi aktualizované vlastnosti prostředku předplatného.</span><span class="sxs-lookup"><span data-stu-id="59dbc-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="59dbc-155">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="59dbc-155">Response success and error codes</span></span>

<span data-ttu-id="59dbc-156">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="59dbc-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="59dbc-157">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="59dbc-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="59dbc-158">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="59dbc-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="59dbc-159">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="59dbc-159">Response example</span></span>

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
