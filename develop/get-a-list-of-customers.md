---
title: Získání seznamu zákazníků
description: Jak získat kolekci prostředků, které představují všechny zákazníky partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 2dd8469458809ab38b6d6081adc91d6d1184d2d0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766961"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="e1270-103">Získání seznamu zákazníků</span><span class="sxs-lookup"><span data-stu-id="e1270-103">Get a list of customers</span></span>

<span data-ttu-id="e1270-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="e1270-104">**Applies to:**</span></span>

- <span data-ttu-id="e1270-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e1270-105">Partner Center</span></span>
- <span data-ttu-id="e1270-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e1270-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e1270-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="e1270-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e1270-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e1270-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e1270-109">Tento článek popisuje, jak získat kolekci prostředků, které představují všechny zákazníky partnera.</span><span class="sxs-lookup"><span data-stu-id="e1270-109">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="e1270-110">Tuto operaci můžete provést i na řídicím panelu partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e1270-110">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="e1270-111">Na hlavní stránce v části **Správa zákazníků** vyberte možnost **Zobrazit zákazníky**.</span><span class="sxs-lookup"><span data-stu-id="e1270-111">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="e1270-112">Nebo na bočním panelu vyberte **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e1270-112">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1270-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e1270-113">Prerequisites</span></span>

- <span data-ttu-id="e1270-114">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e1270-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e1270-115">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1270-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e1270-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e1270-116">C\#</span></span>

<span data-ttu-id="e1270-117">Pokud chcete získat seznam všech zákazníků:</span><span class="sxs-lookup"><span data-stu-id="e1270-117">To get a list of all customers:</span></span>

1. <span data-ttu-id="e1270-118">Pomocí kolekce [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) vytvořte objekt **IPartner** .</span><span class="sxs-lookup"><span data-stu-id="e1270-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="e1270-119">Seznam zákazníků načtěte pomocí metod [**Query ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo [**QueryAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .</span><span class="sxs-lookup"><span data-stu-id="e1270-119">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="e1270-120">(Pokyny k vytvoření dotazu naleznete v tématu Třída [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .)</span><span class="sxs-lookup"><span data-stu-id="e1270-120">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="e1270-121">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="e1270-121">For an example, see the following:</span></span>

- <span data-ttu-id="e1270-122">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e1270-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e1270-123">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="e1270-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="e1270-124">Třída: **CustomerPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="e1270-124">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="e1270-125">Java</span><span class="sxs-lookup"><span data-stu-id="e1270-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e1270-126">Pokud chcete získat seznam všech zákazníků:</span><span class="sxs-lookup"><span data-stu-id="e1270-126">To get a list of all customers:</span></span>

1. <span data-ttu-id="e1270-127">Pomocí funkce [**IAggregatePartner. GetCustomers**] získáte odkaz na operace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e1270-127">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="e1270-128">Pomocí funkce **Query ()** načtěte seznam zákazníků.</span><span class="sxs-lookup"><span data-stu-id="e1270-128">Retrieve the customer list using the **query()** function.</span></span>

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="e1270-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1270-129">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e1270-130">Pokud chcete získat úplný seznam zákazníků, spusťte příkaz [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="e1270-130">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="e1270-131">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e1270-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e1270-132">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e1270-132">Request syntax</span></span>

| <span data-ttu-id="e1270-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="e1270-133">Method</span></span>  | <span data-ttu-id="e1270-134">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e1270-134">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="e1270-135">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="e1270-135">**GET**</span></span> | <span data-ttu-id="e1270-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e1270-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e1270-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e1270-137">URI parameter</span></span>

<span data-ttu-id="e1270-138">Chcete-li získat seznam zákazníků, použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="e1270-138">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="e1270-139">Název</span><span class="sxs-lookup"><span data-stu-id="e1270-139">Name</span></span>     | <span data-ttu-id="e1270-140">Typ</span><span class="sxs-lookup"><span data-stu-id="e1270-140">Type</span></span>    | <span data-ttu-id="e1270-141">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e1270-141">Required</span></span> | <span data-ttu-id="e1270-142">Popis</span><span class="sxs-lookup"><span data-stu-id="e1270-142">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="e1270-143">**hodnota**</span><span class="sxs-lookup"><span data-stu-id="e1270-143">**size**</span></span> | <span data-ttu-id="e1270-144">**int**</span><span class="sxs-lookup"><span data-stu-id="e1270-144">**int**</span></span> | <span data-ttu-id="e1270-145">Y</span><span class="sxs-lookup"><span data-stu-id="e1270-145">Y</span></span>        | <span data-ttu-id="e1270-146">Počet výsledků, které se mají zobrazit v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="e1270-146">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e1270-147">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e1270-147">Request headers</span></span>

<span data-ttu-id="e1270-148">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e1270-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e1270-149">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e1270-149">Request body</span></span>

<span data-ttu-id="e1270-150">Žádné</span><span class="sxs-lookup"><span data-stu-id="e1270-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e1270-151">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e1270-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="e1270-152">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e1270-152">REST response</span></span>

<span data-ttu-id="e1270-153">V případě úspěchu tato metoda vrátí kolekci [zákaznických](customer-resources.md#customer) prostředků v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e1270-153">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e1270-154">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e1270-154">Response success and error codes</span></span>

<span data-ttu-id="e1270-155">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e1270-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e1270-156">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e1270-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e1270-157">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e1270-157">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e1270-158">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e1270-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
