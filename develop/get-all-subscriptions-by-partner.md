---
title: Získání předplatných zákazníka podle ID MPN partnera
description: Jak získat seznam předplatných poskytnutých daným partnerem konkrétnímu zákazníkovi.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 857caa667245503f111b27379a5c8f93aa1fb0b0
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760653"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="95dae-103">Získání předplatných zákazníka podle ID MPN partnera</span><span class="sxs-lookup"><span data-stu-id="95dae-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="95dae-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="95dae-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="95dae-105">Jak získat seznam předplatných poskytovaných daným partnerem Microsoft Partner Network (MPN) pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="95dae-105">How to get a list of subscriptions provided by a given Microsoft Partner Network (MPN) partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95dae-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="95dae-106">Prerequisites</span></span>

- <span data-ttu-id="95dae-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="95dae-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95dae-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="95dae-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="95dae-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95dae-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="95dae-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="95dae-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="95dae-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="95dae-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="95dae-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="95dae-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="95dae-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="95dae-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="95dae-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95dae-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="95dae-115">Identifikátor MPN partnera.</span><span class="sxs-lookup"><span data-stu-id="95dae-115">A partner MPN identifier.</span></span>

## <a name="c"></a><span data-ttu-id="95dae-116">C\#</span><span class="sxs-lookup"><span data-stu-id="95dae-116">C\#</span></span>

<span data-ttu-id="95dae-117">Chcete-li získat seznam předplatných poskytovaných daným partnerem pro určitého zákazníka, nejprve použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="95dae-117">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="95dae-118">Pak z vlastnosti [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) Získejte rozhraní pro operace shromažďování předplatných zákazníků a zavolejte metodu [**BYPARTNER**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) s ID MPN, abyste identifikovali partnera a načetli rozhraní pro partnerských operacích předplatného.</span><span class="sxs-lookup"><span data-stu-id="95dae-118">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="95dae-119">Nakonec zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) pro získání kolekce.</span><span class="sxs-lookup"><span data-stu-id="95dae-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="95dae-120">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="95dae-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="95dae-121">**Project**: **třída** microsoft Partner SDK samples: GetSubscriptionsByMpnid. cs</span><span class="sxs-lookup"><span data-stu-id="95dae-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="95dae-122">Java</span><span class="sxs-lookup"><span data-stu-id="95dae-122">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="95dae-123">Chcete-li získat seznam předplatných poskytovaných daným partnerem pro určitého zákazníka, nejprve použijte funkci **IAggregatePartner. GetCustomers. byId** s ID zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="95dae-123">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="95dae-124">Pak z funkce **Getsubscriptions** Získejte rozhraní pro operace shromažďování předplatných zákazníků a zavolejte funkci **BYPARTNER** s ID MPN k identifikaci partnera a načtení rozhraní pro partnerský odběr operace.</span><span class="sxs-lookup"><span data-stu-id="95dae-124">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="95dae-125">Nakonec zavolejte funkci **Get** pro získání kolekce.</span><span class="sxs-lookup"><span data-stu-id="95dae-125">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="95dae-126">PowerShell</span><span class="sxs-lookup"><span data-stu-id="95dae-126">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="95dae-127">Pokud chcete získat seznam předplatných poskytovaných daným partnerem konkrétnímu zákazníkovi, spusťte příkaz [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) .</span><span class="sxs-lookup"><span data-stu-id="95dae-127">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="95dae-128">Zadejte ID zákazníka pro identifikaci zákazníka pomocí parametru **CustomerID** a naplňte parametr **MpnId** číslem MPN k identifikaci partnera.</span><span class="sxs-lookup"><span data-stu-id="95dae-128">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="95dae-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="95dae-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95dae-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="95dae-130">Request syntax</span></span>

| <span data-ttu-id="95dae-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="95dae-131">Method</span></span>  | <span data-ttu-id="95dae-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="95dae-132">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95dae-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="95dae-133">**GET**</span></span> | <span data-ttu-id="95dae-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions? MPN \_ ID = {MPN-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="95dae-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="95dae-135">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="95dae-135">URI parameters</span></span>

<span data-ttu-id="95dae-136">K identifikaci zákazníka a partnera použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="95dae-136">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="95dae-137">Název</span><span class="sxs-lookup"><span data-stu-id="95dae-137">Name</span></span>        | <span data-ttu-id="95dae-138">Typ</span><span class="sxs-lookup"><span data-stu-id="95dae-138">Type</span></span>   | <span data-ttu-id="95dae-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="95dae-139">Required</span></span> | <span data-ttu-id="95dae-140">Popis</span><span class="sxs-lookup"><span data-stu-id="95dae-140">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="95dae-141">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="95dae-141">customer-id</span></span> | <span data-ttu-id="95dae-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="95dae-142">string</span></span> | <span data-ttu-id="95dae-143">Yes</span><span class="sxs-lookup"><span data-stu-id="95dae-143">Yes</span></span>      | <span data-ttu-id="95dae-144">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="95dae-144">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="95dae-145">MPN – ID</span><span class="sxs-lookup"><span data-stu-id="95dae-145">mpn-id</span></span>      | <span data-ttu-id="95dae-146">int</span><span class="sxs-lookup"><span data-stu-id="95dae-146">int</span></span>    | <span data-ttu-id="95dae-147">Yes</span><span class="sxs-lookup"><span data-stu-id="95dae-147">Yes</span></span>      | <span data-ttu-id="95dae-148">ID Microsoft Partner Network, které identifikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="95dae-148">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="95dae-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="95dae-149">Request headers</span></span>

<span data-ttu-id="95dae-150">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="95dae-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95dae-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="95dae-151">Request body</span></span>

<span data-ttu-id="95dae-152">Žádné</span><span class="sxs-lookup"><span data-stu-id="95dae-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="95dae-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="95dae-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="95dae-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="95dae-154">REST response</span></span>

<span data-ttu-id="95dae-155">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [předplatného](subscription-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="95dae-155">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95dae-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="95dae-156">Response success and error codes</span></span>

<span data-ttu-id="95dae-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="95dae-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95dae-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="95dae-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="95dae-159">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="95dae-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="95dae-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="95dae-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a><span data-ttu-id="95dae-161">Viz také</span><span class="sxs-lookup"><span data-stu-id="95dae-161">See also</span></span>

- [<span data-ttu-id="95dae-162">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="95dae-162">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
