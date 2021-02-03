---
title: Získání všech žádostí o službu pro zákazníka
description: Získá všechny žádosti o služby zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f473c7a7d43b1a3929d983fb23dae92fdafbc0f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767050"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="5d5af-103">Získání všech žádostí o službu pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="5d5af-103">Get all service requests for a customer</span></span>

<span data-ttu-id="5d5af-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="5d5af-104">**Applies To**</span></span>

- <span data-ttu-id="5d5af-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="5d5af-105">Partner Center</span></span>
- <span data-ttu-id="5d5af-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="5d5af-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5d5af-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5d5af-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5d5af-108">Získá všechny žádosti o služby zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5d5af-108">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="5d5af-109">Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="5d5af-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="5d5af-110">Pak na levém bočním panelu vyberte **Správa služeb** .</span><span class="sxs-lookup"><span data-stu-id="5d5af-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="5d5af-111">Žádosti o služby zákazníka se zobrazí v části **lístky podpory**.</span><span class="sxs-lookup"><span data-stu-id="5d5af-111">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d5af-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5d5af-112">Prerequisites</span></span>

- <span data-ttu-id="5d5af-113">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5d5af-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5d5af-114">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="5d5af-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5d5af-115">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5d5af-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5d5af-116">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="5d5af-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5d5af-117">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="5d5af-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5d5af-118">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="5d5af-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5d5af-119">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="5d5af-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5d5af-120">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5d5af-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5d5af-121">C\#</span><span class="sxs-lookup"><span data-stu-id="5d5af-121">C\#</span></span>

<span data-ttu-id="5d5af-122">Pokud chcete zobrazit seznam všech žádostí o služby zákazníka, použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="5d5af-122">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="5d5af-123">Potom zavolejte vlastnost [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) a za ní volejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="5d5af-123">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="5d5af-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5d5af-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5d5af-125">**Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="5d5af-125">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5d5af-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="5d5af-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5d5af-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="5d5af-127">Request syntax</span></span>

| <span data-ttu-id="5d5af-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="5d5af-128">Method</span></span>  | <span data-ttu-id="5d5af-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5d5af-129">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5d5af-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="5d5af-130">**GET**</span></span> | <span data-ttu-id="5d5af-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/servicerequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5d5af-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5d5af-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5d5af-132">URI parameter</span></span>

<span data-ttu-id="5d5af-133">K získání všech žádostí o služby pro zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="5d5af-133">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="5d5af-134">Název</span><span class="sxs-lookup"><span data-stu-id="5d5af-134">Name</span></span>                   | <span data-ttu-id="5d5af-135">Typ</span><span class="sxs-lookup"><span data-stu-id="5d5af-135">Type</span></span>     | <span data-ttu-id="5d5af-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="5d5af-136">Required</span></span> | <span data-ttu-id="5d5af-137">Popis</span><span class="sxs-lookup"><span data-stu-id="5d5af-137">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="5d5af-138">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="5d5af-138">**customer-tenant-id**</span></span> | <span data-ttu-id="5d5af-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="5d5af-139">**guid**</span></span> | <span data-ttu-id="5d5af-140">Y</span><span class="sxs-lookup"><span data-stu-id="5d5af-140">Y</span></span>        | <span data-ttu-id="5d5af-141">Identifikátor GUID odpovídající zákazníkovi...</span><span class="sxs-lookup"><span data-stu-id="5d5af-141">A GUID corresponding to the customer..</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5d5af-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5d5af-142">Request headers</span></span>

<span data-ttu-id="5d5af-143">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5d5af-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5d5af-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="5d5af-144">Request body</span></span>

<span data-ttu-id="5d5af-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="5d5af-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5d5af-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="5d5af-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="5d5af-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5d5af-147">REST response</span></span>

<span data-ttu-id="5d5af-148">V případě úspěchu tato metoda vrátí kolekci prostředků **žádosti o službu** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="5d5af-148">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5d5af-149">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="5d5af-149">Response success and error codes</span></span>

<span data-ttu-id="5d5af-150">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5d5af-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5d5af-151">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="5d5af-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5d5af-152">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5d5af-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5d5af-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="5d5af-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 742
Content-Type: application/json
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
Date: Tue, 24 Nov 2015 07:19:21 GMT

{
    "totalCount": 1,
    "items": [{
        "title": "Test",
        "severity": 0,
        "id": "615112491169010",
        "status": 1,
        "primaryContact": {
            "lastName": "LastName",
            "firstName": "FirstName"
        },
        "createdDate": "2015-11-24T01:07:00.863",
        "lastModifiedDate": "2015-11-24T01:17:10.61",
        "lastClosedDate": "0001-01-01T00:00:00",
        "attributes": {
            "objectType": "ServiceRequest"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
