---
title: Získání všech žádostí o službu pro zákazníka
description: Získá všechny žádosti o služby zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ffcbbb9cf14b1b2a5b3becab541d3042c3cad508
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760670"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="5168d-103">Získání všech žádostí o službu pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="5168d-103">Get all service requests for a customer</span></span>

<span data-ttu-id="5168d-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5168d-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5168d-105">Získá všechny žádosti o služby zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5168d-105">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="5168d-106">Na řídicím Partnerské centrum můžete tuto operaci provést tak, že nejprve [vyberete zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="5168d-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="5168d-107">Pak na levém **bočním** panelu vyberte Správa služeb.</span><span class="sxs-lookup"><span data-stu-id="5168d-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="5168d-108">Žádosti o služby zákazníka se zobrazují v části **Lístky podpory**.</span><span class="sxs-lookup"><span data-stu-id="5168d-108">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5168d-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5168d-109">Prerequisites</span></span>

- <span data-ttu-id="5168d-110">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5168d-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5168d-111">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="5168d-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5168d-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5168d-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5168d-113">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="5168d-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5168d-114">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="5168d-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5168d-115">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="5168d-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5168d-116">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5168d-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5168d-117">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5168d-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5168d-118">C\#</span><span class="sxs-lookup"><span data-stu-id="5168d-118">C\#</span></span>

<span data-ttu-id="5168d-119">Pokud chcete zobrazit seznam všech žádostí o služby zákazníka, použijte kolekci **IAggregatePartner.Customers** a zavolejte [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="5168d-119">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="5168d-120">Potom zavolejte [**vlastnost ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) a pak metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="5168d-120">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="5168d-121">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5168d-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5168d-122">**Project:** PartnerCenterSDK.FeaturesSamples **– třída:** CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="5168d-122">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5168d-123">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="5168d-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5168d-124">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="5168d-124">Request syntax</span></span>

| <span data-ttu-id="5168d-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="5168d-125">Method</span></span>  | <span data-ttu-id="5168d-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5168d-126">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5168d-127">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="5168d-127">**GET**</span></span> | <span data-ttu-id="5168d-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/servicerequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5168d-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5168d-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5168d-129">URI parameter</span></span>

<span data-ttu-id="5168d-130">Pomocí následujícího parametru dotazu získejte všechny žádosti o služby pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5168d-130">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="5168d-131">Název</span><span class="sxs-lookup"><span data-stu-id="5168d-131">Name</span></span>                   | <span data-ttu-id="5168d-132">Typ</span><span class="sxs-lookup"><span data-stu-id="5168d-132">Type</span></span>     | <span data-ttu-id="5168d-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="5168d-133">Required</span></span> | <span data-ttu-id="5168d-134">Popis</span><span class="sxs-lookup"><span data-stu-id="5168d-134">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="5168d-135">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="5168d-135">**customer-tenant-id**</span></span> | <span data-ttu-id="5168d-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="5168d-136">**guid**</span></span> | <span data-ttu-id="5168d-137">Y</span><span class="sxs-lookup"><span data-stu-id="5168d-137">Y</span></span>        | <span data-ttu-id="5168d-138">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="5168d-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5168d-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5168d-139">Request headers</span></span>

<span data-ttu-id="5168d-140">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5168d-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5168d-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="5168d-141">Request body</span></span>

<span data-ttu-id="5168d-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="5168d-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5168d-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="5168d-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="5168d-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5168d-144">REST response</span></span>

<span data-ttu-id="5168d-145">V případě úspěchu vrátí tato  metoda v textu odpovědi kolekci prostředků žádosti o služby.</span><span class="sxs-lookup"><span data-stu-id="5168d-145">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5168d-146">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="5168d-146">Response success and error codes</span></span>

<span data-ttu-id="5168d-147">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5168d-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5168d-148">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="5168d-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5168d-149">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5168d-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5168d-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="5168d-150">Response example</span></span>

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
