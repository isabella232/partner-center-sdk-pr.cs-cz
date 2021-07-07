---
title: Opětovná aktivace pozastaveného předplatného
description: Znovu aktivuje předplatné, které bylo dříve pozastavené kvůli nezaplacení. Na Partnerské centrum řídicím panelu můžete tuto operaci provést tak, že nejprve vyberete zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2b6e3574119f9c645cc3f730047d2a23484ad8a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547702"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="14082-104">Opětovná aktivace pozastaveného předplatného</span><span class="sxs-lookup"><span data-stu-id="14082-104">Reactivate a suspended subscription</span></span>

<span data-ttu-id="14082-105">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="14082-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="14082-106">Znovu aktivuje [předplatné, které](subscription-resources.md) bylo dříve pozastavené kvůli nezaplacení.</span><span class="sxs-lookup"><span data-stu-id="14082-106">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="14082-107">Na řídicím Partnerské centrum můžete tuto operaci provést tak, že nejprve [vyberete zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="14082-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="14082-108">Pak vyberte předplatné, které chcete přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="14082-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="14082-109">Dokončete to tak, **že zvolíte tlačítko Active (Aktivní)** a pak vyberete **Submit (Odeslat).**</span><span class="sxs-lookup"><span data-stu-id="14082-109">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14082-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="14082-110">Prerequisites</span></span>

- <span data-ttu-id="14082-111">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="14082-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="14082-112">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="14082-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="14082-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14082-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="14082-114">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="14082-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="14082-115">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="14082-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="14082-116">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="14082-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="14082-117">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="14082-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="14082-118">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14082-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="14082-119">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="14082-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="14082-120">C\#</span><span class="sxs-lookup"><span data-stu-id="14082-120">C\#</span></span>

<span data-ttu-id="14082-121">Pokud chcete znovu aktivovat předplatné zákazníka, [nejprve získejte](get-a-subscription-by-id.md)předplatné a pak změňte vlastnost [**Stav**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) předplatného.</span><span class="sxs-lookup"><span data-stu-id="14082-121">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="14082-122">Informace o **stavových kódech** najdete v [výčet/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="14082-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="14082-123">Po změně použijte kolekci [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="14082-123">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="14082-124">Potom zavolejte [**vlastnost Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a pak [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="14082-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="14082-125">Potom dokončete voláním [**metody Patch().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="14082-125">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

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

<span data-ttu-id="14082-126">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="14082-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="14082-127">**Project:** FeatureSamplesApplication.</span><span class="sxs-lookup"><span data-stu-id="14082-127">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="14082-128">**Třída:** UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="14082-128">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="14082-129">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="14082-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="14082-130">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="14082-130">Request syntax</span></span>

| <span data-ttu-id="14082-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="14082-131">Method</span></span>    | <span data-ttu-id="14082-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="14082-132">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14082-133">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="14082-133">**PATCH**</span></span> | <span data-ttu-id="14082-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{id-pro-předplatné} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="14082-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="14082-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="14082-135">URI parameter</span></span>

<span data-ttu-id="14082-136">Tato tabulka uvádí požadovaný parametr dotazu pro opětovnou aktivaci předplatného.</span><span class="sxs-lookup"><span data-stu-id="14082-136">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="14082-137">Název</span><span class="sxs-lookup"><span data-stu-id="14082-137">Name</span></span>                    | <span data-ttu-id="14082-138">Typ</span><span class="sxs-lookup"><span data-stu-id="14082-138">Type</span></span>     | <span data-ttu-id="14082-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="14082-139">Required</span></span> | <span data-ttu-id="14082-140">Popis</span><span class="sxs-lookup"><span data-stu-id="14082-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="14082-141">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="14082-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="14082-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="14082-142">**guid**</span></span> | <span data-ttu-id="14082-143">Y</span><span class="sxs-lookup"><span data-stu-id="14082-143">Y</span></span>        | <span data-ttu-id="14082-144">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="14082-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="14082-145">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="14082-145">**id-for-subscription**</span></span> | <span data-ttu-id="14082-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="14082-146">**guid**</span></span> | <span data-ttu-id="14082-147">Y</span><span class="sxs-lookup"><span data-stu-id="14082-147">Y</span></span>        | <span data-ttu-id="14082-148">Identifikátor GUID odpovídající předplatnému.</span><span class="sxs-lookup"><span data-stu-id="14082-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="14082-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="14082-149">Request headers</span></span>

<span data-ttu-id="14082-150">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="14082-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="14082-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="14082-151">Request body</span></span>

<span data-ttu-id="14082-152">V textu **požadavku** se vyžaduje úplný prostředek předplatného.</span><span class="sxs-lookup"><span data-stu-id="14082-152">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="14082-153">Ujistěte **se, že byla** aktualizována vlastnost Status.</span><span class="sxs-lookup"><span data-stu-id="14082-153">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="14082-154">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="14082-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="14082-155">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="14082-155">REST response</span></span>

<span data-ttu-id="14082-156">V případě úspěchu vrátí tato metoda [v](subscription-resources.md) textu odpovědi aktualizované vlastnosti prostředku předplatného.</span><span class="sxs-lookup"><span data-stu-id="14082-156">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="14082-157">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="14082-157">Response success and error codes</span></span>

<span data-ttu-id="14082-158">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="14082-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="14082-159">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="14082-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="14082-160">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="14082-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="14082-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="14082-161">Response example</span></span>

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
