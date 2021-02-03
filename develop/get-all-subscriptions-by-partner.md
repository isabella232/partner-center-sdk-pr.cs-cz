---
title: Získání předplatných zákazníka podle ID MPN partnera
description: Jak získat seznam předplatných poskytnutých daným partnerem konkrétnímu zákazníkovi.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c95488b62449e1ab6bd2eeefea58d6686c291f4c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766988"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="76c82-103">Získání předplatných zákazníka podle ID MPN partnera</span><span class="sxs-lookup"><span data-stu-id="76c82-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="76c82-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="76c82-104">**Applies To**</span></span>

- <span data-ttu-id="76c82-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="76c82-105">Partner Center</span></span>
- <span data-ttu-id="76c82-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="76c82-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="76c82-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="76c82-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="76c82-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="76c82-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="76c82-109">Jak získat seznam předplatných poskytnutých daným partnerem konkrétnímu zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="76c82-109">How to get a list of subscriptions provided by a given partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76c82-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="76c82-110">Prerequisites</span></span>

- <span data-ttu-id="76c82-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="76c82-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="76c82-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="76c82-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="76c82-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="76c82-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="76c82-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="76c82-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="76c82-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="76c82-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="76c82-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="76c82-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="76c82-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="76c82-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="76c82-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="76c82-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="76c82-119">Identifikátor partnerského Microsoft Partner Network (MPN).</span><span class="sxs-lookup"><span data-stu-id="76c82-119">A partner Microsoft Partner Network (MPN) identifier.</span></span>

## <a name="c"></a><span data-ttu-id="76c82-120">C\#</span><span class="sxs-lookup"><span data-stu-id="76c82-120">C\#</span></span>

<span data-ttu-id="76c82-121">Chcete-li získat seznam předplatných poskytovaných daným partnerem pro určitého zákazníka, nejprve použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="76c82-121">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="76c82-122">Pak z vlastnosti [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) Získejte rozhraní pro operace shromažďování předplatných zákazníků a zavolejte metodu [**BYPARTNER**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) s ID MPN, abyste identifikovali partnera a načetli rozhraní pro partnerských operacích předplatného.</span><span class="sxs-lookup"><span data-stu-id="76c82-122">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="76c82-123">Nakonec zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) pro získání kolekce.</span><span class="sxs-lookup"><span data-stu-id="76c82-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="76c82-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="76c82-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="76c82-125">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetSubscriptionsByMpnid.cs</span><span class="sxs-lookup"><span data-stu-id="76c82-125">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="76c82-126">Java</span><span class="sxs-lookup"><span data-stu-id="76c82-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="76c82-127">Chcete-li získat seznam předplatných poskytovaných daným partnerem pro určitého zákazníka, nejprve použijte funkci **IAggregatePartner. GetCustomers. byId** s ID zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="76c82-127">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="76c82-128">Pak z funkce **Getsubscriptions** Získejte rozhraní pro operace shromažďování předplatných zákazníků a zavolejte funkci **BYPARTNER** s ID MPN k identifikaci partnera a načtení rozhraní pro partnerský odběr operace.</span><span class="sxs-lookup"><span data-stu-id="76c82-128">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="76c82-129">Nakonec zavolejte funkci **Get** pro získání kolekce.</span><span class="sxs-lookup"><span data-stu-id="76c82-129">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="76c82-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="76c82-130">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="76c82-131">Pokud chcete získat seznam předplatných poskytovaných daným partnerem konkrétnímu zákazníkovi, spusťte příkaz [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) .</span><span class="sxs-lookup"><span data-stu-id="76c82-131">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="76c82-132">Zadejte ID zákazníka pro identifikaci zákazníka pomocí parametru **CustomerID** a naplňte parametr **MpnId** číslem MPN k identifikaci partnera.</span><span class="sxs-lookup"><span data-stu-id="76c82-132">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="76c82-133">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="76c82-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="76c82-134">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="76c82-134">Request syntax</span></span>

| <span data-ttu-id="76c82-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="76c82-135">Method</span></span>  | <span data-ttu-id="76c82-136">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="76c82-136">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="76c82-137">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="76c82-137">**GET**</span></span> | <span data-ttu-id="76c82-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions? MPN \_ ID = {MPN-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="76c82-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="76c82-139">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="76c82-139">URI parameters</span></span>

<span data-ttu-id="76c82-140">K identifikaci zákazníka a partnera použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="76c82-140">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="76c82-141">Název</span><span class="sxs-lookup"><span data-stu-id="76c82-141">Name</span></span>        | <span data-ttu-id="76c82-142">Typ</span><span class="sxs-lookup"><span data-stu-id="76c82-142">Type</span></span>   | <span data-ttu-id="76c82-143">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="76c82-143">Required</span></span> | <span data-ttu-id="76c82-144">Popis</span><span class="sxs-lookup"><span data-stu-id="76c82-144">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="76c82-145">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="76c82-145">customer-id</span></span> | <span data-ttu-id="76c82-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="76c82-146">string</span></span> | <span data-ttu-id="76c82-147">Yes</span><span class="sxs-lookup"><span data-stu-id="76c82-147">Yes</span></span>      | <span data-ttu-id="76c82-148">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="76c82-148">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="76c82-149">MPN – ID</span><span class="sxs-lookup"><span data-stu-id="76c82-149">mpn-id</span></span>      | <span data-ttu-id="76c82-150">int</span><span class="sxs-lookup"><span data-stu-id="76c82-150">int</span></span>    | <span data-ttu-id="76c82-151">Yes</span><span class="sxs-lookup"><span data-stu-id="76c82-151">Yes</span></span>      | <span data-ttu-id="76c82-152">ID Microsoft Partner Network, které identifikuje partnera.</span><span class="sxs-lookup"><span data-stu-id="76c82-152">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="76c82-153">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="76c82-153">Request headers</span></span>

<span data-ttu-id="76c82-154">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="76c82-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="76c82-155">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="76c82-155">Request body</span></span>

<span data-ttu-id="76c82-156">Žádné</span><span class="sxs-lookup"><span data-stu-id="76c82-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="76c82-157">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="76c82-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="76c82-158">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="76c82-158">REST response</span></span>

<span data-ttu-id="76c82-159">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [předplatného](subscription-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="76c82-159">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="76c82-160">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="76c82-160">Response success and error codes</span></span>

<span data-ttu-id="76c82-161">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="76c82-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="76c82-162">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="76c82-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="76c82-163">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="76c82-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="76c82-164">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="76c82-164">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="76c82-165">Viz také</span><span class="sxs-lookup"><span data-stu-id="76c82-165">See also</span></span>

- [<span data-ttu-id="76c82-166">Analýzy Partnerského centra – prostředky</span><span class="sxs-lookup"><span data-stu-id="76c82-166">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
