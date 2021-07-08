---
title: Získání seznamu zákazníků
description: Jak získat kolekci prostředků, které představují všechny zákazníky partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 840c9d1a61451763d37a19639f99b12f1deb7521
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874342"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="0139e-103">Získání seznamu zákazníků</span><span class="sxs-lookup"><span data-stu-id="0139e-103">Get a list of customers</span></span>

<span data-ttu-id="0139e-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0139e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0139e-105">Tento článek popisuje, jak získat kolekci prostředků, které představují všechny zákazníky partnera.</span><span class="sxs-lookup"><span data-stu-id="0139e-105">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="0139e-106">Tuto operaci můžete provést i na řídicím panelu partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0139e-106">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="0139e-107">Na hlavní stránce v části **Správa zákazníků** vyberte možnost **Zobrazit zákazníky**.</span><span class="sxs-lookup"><span data-stu-id="0139e-107">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="0139e-108">Nebo na bočním panelu vyberte **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="0139e-108">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0139e-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0139e-109">Prerequisites</span></span>

- <span data-ttu-id="0139e-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0139e-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0139e-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="0139e-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="0139e-112">C\#</span><span class="sxs-lookup"><span data-stu-id="0139e-112">C\#</span></span>

<span data-ttu-id="0139e-113">Pokud chcete získat seznam všech zákazníků:</span><span class="sxs-lookup"><span data-stu-id="0139e-113">To get a list of all customers:</span></span>

1. <span data-ttu-id="0139e-114">Pomocí kolekce [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) vytvořte objekt **IPartner** .</span><span class="sxs-lookup"><span data-stu-id="0139e-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="0139e-115">Seznam zákazníků načtěte pomocí metod [**Query ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) nebo [**QueryAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .</span><span class="sxs-lookup"><span data-stu-id="0139e-115">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="0139e-116">(Pokyny k vytvoření dotazu naleznete v tématu Třída [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .)</span><span class="sxs-lookup"><span data-stu-id="0139e-116">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="0139e-117">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="0139e-117">For an example, see the following:</span></span>

- <span data-ttu-id="0139e-118">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="0139e-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="0139e-119">Project: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="0139e-119">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="0139e-120">Třída: **CustomerPaging. cs**</span><span class="sxs-lookup"><span data-stu-id="0139e-120">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="0139e-121">Java</span><span class="sxs-lookup"><span data-stu-id="0139e-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="0139e-122">Pokud chcete získat seznam všech zákazníků:</span><span class="sxs-lookup"><span data-stu-id="0139e-122">To get a list of all customers:</span></span>

1. <span data-ttu-id="0139e-123">Pomocí funkce [**IAggregatePartner. GetCustomers**] získáte odkaz na operace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0139e-123">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="0139e-124">Pomocí funkce **Query ()** načtěte seznam zákazníků.</span><span class="sxs-lookup"><span data-stu-id="0139e-124">Retrieve the customer list using the **query()** function.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="0139e-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0139e-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="0139e-126">Pokud chcete získat úplný seznam zákazníků, spusťte příkaz [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="0139e-126">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="0139e-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0139e-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0139e-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0139e-128">Request syntax</span></span>

| <span data-ttu-id="0139e-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="0139e-129">Method</span></span>  | <span data-ttu-id="0139e-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0139e-130">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="0139e-131">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="0139e-131">**GET**</span></span> | <span data-ttu-id="0139e-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0139e-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="0139e-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0139e-133">URI parameter</span></span>

<span data-ttu-id="0139e-134">Chcete-li získat seznam zákazníků, použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="0139e-134">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="0139e-135">Název</span><span class="sxs-lookup"><span data-stu-id="0139e-135">Name</span></span>     | <span data-ttu-id="0139e-136">Typ</span><span class="sxs-lookup"><span data-stu-id="0139e-136">Type</span></span>    | <span data-ttu-id="0139e-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0139e-137">Required</span></span> | <span data-ttu-id="0139e-138">Popis</span><span class="sxs-lookup"><span data-stu-id="0139e-138">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="0139e-139">**hodnota**</span><span class="sxs-lookup"><span data-stu-id="0139e-139">**size**</span></span> | <span data-ttu-id="0139e-140">**int**</span><span class="sxs-lookup"><span data-stu-id="0139e-140">**int**</span></span> | <span data-ttu-id="0139e-141">Y</span><span class="sxs-lookup"><span data-stu-id="0139e-141">Y</span></span>        | <span data-ttu-id="0139e-142">Počet výsledků, které se mají zobrazit v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="0139e-142">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0139e-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0139e-143">Request headers</span></span>

<span data-ttu-id="0139e-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0139e-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0139e-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0139e-145">Request body</span></span>

<span data-ttu-id="0139e-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="0139e-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0139e-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0139e-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="0139e-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0139e-148">REST response</span></span>

<span data-ttu-id="0139e-149">V případě úspěchu tato metoda vrátí kolekci [zákaznických](customer-resources.md#customer) prostředků v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="0139e-149">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0139e-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0139e-150">Response success and error codes</span></span>

<span data-ttu-id="0139e-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0139e-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0139e-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0139e-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0139e-153">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0139e-153">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0139e-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0139e-154">Response example</span></span>

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
