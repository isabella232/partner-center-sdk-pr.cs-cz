---
title: Změna objemu předplatného
description: Zjistěte, jak Partnerské centrum api ke změně počtu licencí pro zákaznické předplatné. Můžete to provést také na řídicím Partnerské centrum panelu.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d57ece4dd19ef2852f39130916222c54a9ccc85a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974093"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="4290a-104">Změna počtu licencí v zákaznickém předplatném</span><span class="sxs-lookup"><span data-stu-id="4290a-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="4290a-105">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4290a-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4290a-106">Aktualizuje předplatné [a](subscription-resources.md) zvýší nebo sníží počet licencí.</span><span class="sxs-lookup"><span data-stu-id="4290a-106">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="4290a-107">Na řídicím Partnerské centrum můžete tuto operaci provést tak, že nejprve [vyberete zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="4290a-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="4290a-108">Pak vyberte předplatné, které chcete přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="4290a-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="4290a-109">Dokončete to tak, že změníte hodnotu v **poli Quantity (Množství)** a pak vyberete **Submit (Odeslat).**</span><span class="sxs-lookup"><span data-stu-id="4290a-109">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4290a-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4290a-110">Prerequisites</span></span>

- <span data-ttu-id="4290a-111">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4290a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4290a-112">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="4290a-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4290a-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4290a-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4290a-114">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4290a-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4290a-115">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="4290a-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4290a-116">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="4290a-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4290a-117">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="4290a-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4290a-118">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4290a-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4290a-119">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="4290a-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="4290a-120">C\#</span><span class="sxs-lookup"><span data-stu-id="4290a-120">C\#</span></span>

<span data-ttu-id="4290a-121">Pokud chcete změnit množství předplatného zákazníka, [](get-a-subscription-by-id.md)nejprve získejte předplatné a pak změňte vlastnost [**Quantity předplatného.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity)</span><span class="sxs-lookup"><span data-stu-id="4290a-121">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="4290a-122">Po změně použijte kolekci **IAggregatePartner.Customers** a zavolejte **metodu ById().**</span><span class="sxs-lookup"><span data-stu-id="4290a-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="4290a-123">Potom zavolejte [**vlastnost Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a pak [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="4290a-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="4290a-124">Potom dokončete voláním **metody Patch().**</span><span class="sxs-lookup"><span data-stu-id="4290a-124">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="4290a-125">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4290a-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4290a-126">**Project:** PartnerSDK.FeatureSample **– třída:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="4290a-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4290a-127">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="4290a-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4290a-128">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="4290a-128">Request syntax</span></span>

| <span data-ttu-id="4290a-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="4290a-129">Method</span></span>    | <span data-ttu-id="4290a-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="4290a-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4290a-131">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="4290a-131">**PATCH**</span></span> | <span data-ttu-id="4290a-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{id-pro-předplatné} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4290a-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4290a-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="4290a-133">URI parameter</span></span>

<span data-ttu-id="4290a-134">Tato tabulka uvádí požadovaný parametr dotazu pro změnu množství předplatného.</span><span class="sxs-lookup"><span data-stu-id="4290a-134">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="4290a-135">Název</span><span class="sxs-lookup"><span data-stu-id="4290a-135">Name</span></span>                    | <span data-ttu-id="4290a-136">Typ</span><span class="sxs-lookup"><span data-stu-id="4290a-136">Type</span></span>     | <span data-ttu-id="4290a-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="4290a-137">Required</span></span> | <span data-ttu-id="4290a-138">Popis</span><span class="sxs-lookup"><span data-stu-id="4290a-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="4290a-139">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="4290a-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="4290a-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="4290a-140">**guid**</span></span> | <span data-ttu-id="4290a-141">Y</span><span class="sxs-lookup"><span data-stu-id="4290a-141">Y</span></span>        | <span data-ttu-id="4290a-142">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="4290a-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="4290a-143">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="4290a-143">**id-for-subscription**</span></span> | <span data-ttu-id="4290a-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="4290a-144">**guid**</span></span> | <span data-ttu-id="4290a-145">Y</span><span class="sxs-lookup"><span data-stu-id="4290a-145">Y</span></span>        | <span data-ttu-id="4290a-146">Identifikátor GUID odpovídající předplatnému.</span><span class="sxs-lookup"><span data-stu-id="4290a-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4290a-147">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="4290a-147">Request headers</span></span>

<span data-ttu-id="4290a-148">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4290a-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4290a-149">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="4290a-149">Request body</span></span>

<span data-ttu-id="4290a-150">V textu **požadavku** se vyžaduje úplný prostředek předplatného.</span><span class="sxs-lookup"><span data-stu-id="4290a-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="4290a-151">Ujistěte **se, že byla** aktualizována vlastnost Quantity.</span><span class="sxs-lookup"><span data-stu-id="4290a-151">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="4290a-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="4290a-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4290a-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="4290a-153">REST response</span></span>

<span data-ttu-id="4290a-154">V případě úspěchu vrátí tato metoda stavový kód [](subscription-resources.md) **HTTP 200** a v textu odpovědi aktualizované vlastnosti prostředku předplatného.</span><span class="sxs-lookup"><span data-stu-id="4290a-154">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4290a-155">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="4290a-155">Response success and error codes</span></span>

<span data-ttu-id="4290a-156">Každá odpověď vrátí stavový kód HTTP, který indikuje úspěch nebo neúspěch, a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="4290a-156">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4290a-157">Ke čtení stavového kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="4290a-157">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="4290a-158">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4290a-158">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="4290a-159">Pokud operace opravy trvá déle, než je očekávaná doba, odešle Partnerské centrum stavový kód **HTTP 202** a hlavičku umístění, která odkazuje na umístění pro načtení odběru.</span><span class="sxs-lookup"><span data-stu-id="4290a-159">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="4290a-160">Odběr můžete pravidelně dotazovat, abyste mohli monitorovat změny stavu a množství.</span><span class="sxs-lookup"><span data-stu-id="4290a-160">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="4290a-161">Příklady odpovědí</span><span class="sxs-lookup"><span data-stu-id="4290a-161">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="4290a-162">Příklad odpovědi 1</span><span class="sxs-lookup"><span data-stu-id="4290a-162">Response example 1</span></span>

<span data-ttu-id="4290a-163">Úspěšný požadavek se **stavový kódem HTTP 200:**</span><span class="sxs-lookup"><span data-stu-id="4290a-163">Successful request with an **HTTP status 200** status code:</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="4290a-164">Příklad odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="4290a-164">Response example 2</span></span>

<span data-ttu-id="4290a-165">Úspěšný požadavek se **stavový kódem HTTP 202:**</span><span class="sxs-lookup"><span data-stu-id="4290a-165">Successful request with an **HTTP status 202** status code:</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```
