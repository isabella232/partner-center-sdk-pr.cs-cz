---
title: Získání spravovaných služeb pro zákazníka podle ID
description: Načte spravované služby pro zákazníka. Jinými slovy, získáte odkazy na všechna předplatná zákazníka, ke kterým máte delegovaná oprávnění správce. Pomocí těchto odkazů můžete poskytovat podporu a žádosti o souborové služby společnosti Microsoft.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4764fce6a80035ea4b9dcc6677a3da28fc863eb7
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767018"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="9f32c-105">Získání spravovaných služeb pro zákazníka podle ID</span><span class="sxs-lookup"><span data-stu-id="9f32c-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="9f32c-106">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="9f32c-106">**Applies To**</span></span>

- <span data-ttu-id="9f32c-107">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="9f32c-107">Partner Center</span></span>
- <span data-ttu-id="9f32c-108">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="9f32c-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9f32c-109">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9f32c-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9f32c-110">Načte spravované služby pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9f32c-110">Gets the managed services for a customer.</span></span> <span data-ttu-id="9f32c-111">Jinými slovy, získáte odkazy na všechna předplatná zákazníka, ke kterým máte delegovaná oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="9f32c-111">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="9f32c-112">Pomocí těchto odkazů můžete poskytovat podporu a žádosti o souborové služby společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f32c-112">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f32c-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9f32c-113">Prerequisites</span></span>

- <span data-ttu-id="9f32c-114">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9f32c-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9f32c-115">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="9f32c-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9f32c-116">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9f32c-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9f32c-117">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="9f32c-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9f32c-118">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="9f32c-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9f32c-119">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="9f32c-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9f32c-120">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="9f32c-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9f32c-121">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9f32c-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9f32c-122">C\#</span><span class="sxs-lookup"><span data-stu-id="9f32c-122">C\#</span></span>

<span data-ttu-id="9f32c-123">Pokud chcete zobrazit seznam všech spravovaných služeb pro zákazníka, použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="9f32c-123">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="9f32c-124">Potom zavolejte vlastnost [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) a za ní volejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="9f32c-124">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="9f32c-125">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9f32c-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9f32c-126">**Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="9f32c-126">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9f32c-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="9f32c-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9f32c-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="9f32c-128">Request syntax</span></span>

| <span data-ttu-id="9f32c-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="9f32c-129">Method</span></span>  | <span data-ttu-id="9f32c-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9f32c-130">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9f32c-131">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="9f32c-131">**GET**</span></span> | <span data-ttu-id="9f32c-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/managedservices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9f32c-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9f32c-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9f32c-133">URI parameter</span></span>

<span data-ttu-id="9f32c-134">K získání spravovaných služeb zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="9f32c-134">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="9f32c-135">Název</span><span class="sxs-lookup"><span data-stu-id="9f32c-135">Name</span></span>                   | <span data-ttu-id="9f32c-136">Typ</span><span class="sxs-lookup"><span data-stu-id="9f32c-136">Type</span></span>     | <span data-ttu-id="9f32c-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9f32c-137">Required</span></span> | <span data-ttu-id="9f32c-138">Popis</span><span class="sxs-lookup"><span data-stu-id="9f32c-138">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="9f32c-139">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="9f32c-139">**customer-tenant-id**</span></span> | <span data-ttu-id="9f32c-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="9f32c-140">**guid**</span></span> | <span data-ttu-id="9f32c-141">Y</span><span class="sxs-lookup"><span data-stu-id="9f32c-141">Y</span></span>        | <span data-ttu-id="9f32c-142">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="9f32c-142">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9f32c-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9f32c-143">Request headers</span></span>

<span data-ttu-id="9f32c-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9f32c-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9f32c-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9f32c-145">Request body</span></span>

<span data-ttu-id="9f32c-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="9f32c-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9f32c-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9f32c-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="9f32c-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9f32c-148">REST response</span></span>

<span data-ttu-id="9f32c-149">V případě úspěchu tato metoda vrátí kolekci objektů **spravované služby** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9f32c-149">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9f32c-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="9f32c-150">Response success and error codes</span></span>

<span data-ttu-id="9f32c-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9f32c-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9f32c-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="9f32c-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9f32c-153">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9f32c-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9f32c-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9f32c-154">Response example</span></span>

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
