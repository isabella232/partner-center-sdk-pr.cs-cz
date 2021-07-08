---
title: Získání spravovaných služeb pro zákazníka podle ID
description: Získá spravované služby pro zákazníka. Jinými slovy, získejte odkazy na všechna předplatná zákazníka, pro která máte delegovaná oprávnění správce. Tyto odkazy můžete použít k poskytování žádostí o podporu a souborovou službu u Microsoftu.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cf7e7b62113bd96b00fdc2301e4e7ac4f5d4243
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548443"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="d21a3-105">Získání spravovaných služeb pro zákazníka podle ID</span><span class="sxs-lookup"><span data-stu-id="d21a3-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="d21a3-106">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d21a3-106">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d21a3-107">Získá spravované služby pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d21a3-107">Gets the managed services for a customer.</span></span> <span data-ttu-id="d21a3-108">Jinými slovy, získejte odkazy na všechna předplatná zákazníka, pro která máte delegovaná oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="d21a3-108">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="d21a3-109">Tyto odkazy můžete použít k poskytování žádostí o podporu a souborovou službu u Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="d21a3-109">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d21a3-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d21a3-110">Prerequisites</span></span>

- <span data-ttu-id="d21a3-111">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d21a3-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d21a3-112">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d21a3-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d21a3-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d21a3-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d21a3-114">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d21a3-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d21a3-115">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="d21a3-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d21a3-116">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="d21a3-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d21a3-117">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d21a3-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d21a3-118">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d21a3-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d21a3-119">C\#</span><span class="sxs-lookup"><span data-stu-id="d21a3-119">C\#</span></span>

<span data-ttu-id="d21a3-120">Pokud chcete zobrazit seznam všech spravovaných služeb pro zákazníka, použijte kolekci **IAggregatePartner.Customers** a zavolejte [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="d21a3-120">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="d21a3-121">Potom zavolejte [**vlastnost ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) následovanou [**metodami Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="d21a3-121">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="d21a3-122">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d21a3-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d21a3-123">**Project:** PartnerCenterSDK.FeaturesSamples **– třída:** CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="d21a3-123">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d21a3-124">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="d21a3-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d21a3-125">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="d21a3-125">Request syntax</span></span>

| <span data-ttu-id="d21a3-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="d21a3-126">Method</span></span>  | <span data-ttu-id="d21a3-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d21a3-127">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d21a3-128">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="d21a3-128">**GET**</span></span> | <span data-ttu-id="d21a3-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/spravované_služby HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d21a3-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d21a3-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d21a3-130">URI parameter</span></span>

<span data-ttu-id="d21a3-131">Pomocí následujícího parametru dotazu získejte spravované služby zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d21a3-131">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="d21a3-132">Název</span><span class="sxs-lookup"><span data-stu-id="d21a3-132">Name</span></span>                   | <span data-ttu-id="d21a3-133">Typ</span><span class="sxs-lookup"><span data-stu-id="d21a3-133">Type</span></span>     | <span data-ttu-id="d21a3-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d21a3-134">Required</span></span> | <span data-ttu-id="d21a3-135">Popis</span><span class="sxs-lookup"><span data-stu-id="d21a3-135">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="d21a3-136">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="d21a3-136">**customer-tenant-id**</span></span> | <span data-ttu-id="d21a3-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="d21a3-137">**guid**</span></span> | <span data-ttu-id="d21a3-138">Y</span><span class="sxs-lookup"><span data-stu-id="d21a3-138">Y</span></span>        | <span data-ttu-id="d21a3-139">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="d21a3-139">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d21a3-140">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d21a3-140">Request headers</span></span>

<span data-ttu-id="d21a3-141">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d21a3-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d21a3-142">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d21a3-142">Request body</span></span>

<span data-ttu-id="d21a3-143">Žádné</span><span class="sxs-lookup"><span data-stu-id="d21a3-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d21a3-144">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d21a3-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="d21a3-145">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d21a3-145">REST response</span></span>

<span data-ttu-id="d21a3-146">V případě úspěchu tato metoda vrátí kolekci objektů **spravované** služby v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="d21a3-146">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d21a3-147">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="d21a3-147">Response success and error codes</span></span>

<span data-ttu-id="d21a3-148">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d21a3-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d21a3-149">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="d21a3-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d21a3-150">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d21a3-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d21a3-151">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d21a3-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 10588
Content-Type: application/json
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
Date: Mon, 23 Nov 2015 18:02:12 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "Exchange",
        "name": "Exchange",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Exchange&InitialDomain=<domain>&PrimaryDomain=<domain>",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    },
    {
        "id": "MicrosoftCommunicationsOnline",
        "name": "SkypeforBusiness",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=MicrosoftCommunicationsOnline",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    }
```
