---
title: Změna objemu předplatného
description: Naučte se používat rozhraní API partnerského centra ke změně počtu licencí pro předplatné zákazníka. Můžete to udělat taky na řídicím panelu partnerského centra.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9b781c50895aa3a14819bec43fcca1e931e3b30
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767108"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="96d80-104">Změna počtu licencí v rámci zákaznického předplatného</span><span class="sxs-lookup"><span data-stu-id="96d80-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="96d80-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="96d80-105">**Applies to:**</span></span>

- <span data-ttu-id="96d80-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="96d80-106">Partner Center</span></span>
- <span data-ttu-id="96d80-107">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="96d80-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="96d80-108">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="96d80-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="96d80-109">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="96d80-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="96d80-110">Aktualizuje [předplatné](subscription-resources.md) pro zvýšení nebo snížení počtu licencí.</span><span class="sxs-lookup"><span data-stu-id="96d80-110">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="96d80-111">Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="96d80-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="96d80-112">Pak vyberte příslušné předplatné, které chcete přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="96d80-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="96d80-113">Chcete-li dokončit, změňte hodnotu v poli **množství** a pak vyberte **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="96d80-113">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96d80-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="96d80-114">Prerequisites</span></span>

- <span data-ttu-id="96d80-115">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="96d80-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="96d80-116">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="96d80-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="96d80-117">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="96d80-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="96d80-118">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="96d80-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="96d80-119">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="96d80-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="96d80-120">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="96d80-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="96d80-121">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="96d80-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="96d80-122">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="96d80-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="96d80-123">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="96d80-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="96d80-124">C\#</span><span class="sxs-lookup"><span data-stu-id="96d80-124">C\#</span></span>

<span data-ttu-id="96d80-125">Pokud chcete změnit počet předplatných zákazníka, nejdřív [získejte předplatné](get-a-subscription-by-id.md)a pak změňte vlastnost [**množství**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) daného předplatného.</span><span class="sxs-lookup"><span data-stu-id="96d80-125">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="96d80-126">Po provedení změny použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="96d80-126">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="96d80-127">Poté zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a potom metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="96d80-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="96d80-128">Potom dokončete voláním metody **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="96d80-128">Then, finish by calling the **Patch()** method.</span></span>

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

<span data-ttu-id="96d80-129">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="96d80-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="96d80-130">**Projekt**: PartnerSDK. FeatureSample **Třída**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="96d80-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="96d80-131">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="96d80-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="96d80-132">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="96d80-132">Request syntax</span></span>

| <span data-ttu-id="96d80-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="96d80-133">Method</span></span>    | <span data-ttu-id="96d80-134">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="96d80-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="96d80-135">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="96d80-135">**PATCH**</span></span> | <span data-ttu-id="96d80-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="96d80-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="96d80-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="96d80-137">URI parameter</span></span>

<span data-ttu-id="96d80-138">Tato tabulka uvádí požadovaný parametr dotazu pro změnu množství předplatného.</span><span class="sxs-lookup"><span data-stu-id="96d80-138">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="96d80-139">Název</span><span class="sxs-lookup"><span data-stu-id="96d80-139">Name</span></span>                    | <span data-ttu-id="96d80-140">Typ</span><span class="sxs-lookup"><span data-stu-id="96d80-140">Type</span></span>     | <span data-ttu-id="96d80-141">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="96d80-141">Required</span></span> | <span data-ttu-id="96d80-142">Popis</span><span class="sxs-lookup"><span data-stu-id="96d80-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="96d80-143">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="96d80-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="96d80-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="96d80-144">**guid**</span></span> | <span data-ttu-id="96d80-145">Y</span><span class="sxs-lookup"><span data-stu-id="96d80-145">Y</span></span>        | <span data-ttu-id="96d80-146">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="96d80-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="96d80-147">**ID pro předplatné**</span><span class="sxs-lookup"><span data-stu-id="96d80-147">**id-for-subscription**</span></span> | <span data-ttu-id="96d80-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="96d80-148">**guid**</span></span> | <span data-ttu-id="96d80-149">Y</span><span class="sxs-lookup"><span data-stu-id="96d80-149">Y</span></span>        | <span data-ttu-id="96d80-150">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="96d80-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="96d80-151">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="96d80-151">Request headers</span></span>

<span data-ttu-id="96d80-152">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="96d80-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="96d80-153">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="96d80-153">Request body</span></span>

<span data-ttu-id="96d80-154">V těle žádosti se vyžaduje prostředek s úplným **předplatným** .</span><span class="sxs-lookup"><span data-stu-id="96d80-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="96d80-155">Ujistěte se, že se vlastnost **množství** aktualizovala.</span><span class="sxs-lookup"><span data-stu-id="96d80-155">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="96d80-156">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="96d80-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="96d80-157">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="96d80-157">REST response</span></span>

<span data-ttu-id="96d80-158">V případě úspěchu vrátí tato metoda stavový kód **protokolu HTTP 200** a aktualizované vlastnosti [prostředku předplatného](subscription-resources.md)  v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="96d80-158">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="96d80-159">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="96d80-159">Response success and error codes</span></span>

<span data-ttu-id="96d80-160">Každá odpověď vrátí stavový kód HTTP, který označuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="96d80-160">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="96d80-161">Pomocí nástroje pro trasování sítě si přečtěte stavový kód, typ chyby a další parametry.</span><span class="sxs-lookup"><span data-stu-id="96d80-161">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="96d80-162">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="96d80-162">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="96d80-163">Pokud operace opravy trvá déle, než je očekávaná doba, Partnerská centra pošle stavový kód **HTTP 202** a hlavičku umístění, která odkazuje na místo, kde se má předplatné načíst.</span><span class="sxs-lookup"><span data-stu-id="96d80-163">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="96d80-164">V pravidelném dotazování na předplatné můžete monitorovat stav a množství změn.</span><span class="sxs-lookup"><span data-stu-id="96d80-164">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="96d80-165">Příklady odpovědí</span><span class="sxs-lookup"><span data-stu-id="96d80-165">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="96d80-166">Příklad odpovědi 1</span><span class="sxs-lookup"><span data-stu-id="96d80-166">Response example 1</span></span>

<span data-ttu-id="96d80-167">Úspěšná žádost se stavovým kódem **HTTP 200** :</span><span class="sxs-lookup"><span data-stu-id="96d80-167">Successful request with an **HTTP status 200** status code:</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="96d80-168">Příklad odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="96d80-168">Response example 2</span></span>

<span data-ttu-id="96d80-169">Úspěšná žádost se stavovým kódem **HTTP 202** :</span><span class="sxs-lookup"><span data-stu-id="96d80-169">Successful request with an **HTTP status 202** status code:</span></span>

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
