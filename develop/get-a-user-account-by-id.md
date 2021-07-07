---
title: Získání uživatelského účtu podle ID
description: Získejte konkrétní uživatelský účet pro zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 3a7cac98a8081a8557dcadfb0724f5497be7d14c
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760262"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="45ad2-103">Získání uživatelského účtu podle ID</span><span class="sxs-lookup"><span data-stu-id="45ad2-103">Get a user account by ID</span></span>

<span data-ttu-id="45ad2-104">Získejte konkrétní uživatelský účet pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="45ad2-104">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="45ad2-105">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="45ad2-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="45ad2-106">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="45ad2-106">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="45ad2-107">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="45ad2-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="45ad2-108">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="45ad2-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="45ad2-109">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="45ad2-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="45ad2-110">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="45ad2-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="45ad2-111">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="45ad2-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="45ad2-112">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="45ad2-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="45ad2-113">C\#</span><span class="sxs-lookup"><span data-stu-id="45ad2-113">C\#</span></span>

<span data-ttu-id="45ad2-114">Pokud chcete načíst uživatelský účet zákazníka, zavolejte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="45ad2-114">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="45ad2-115">Dále zavolejte [**metodu Users.ById,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) která načte konkrétního uživatele.</span><span class="sxs-lookup"><span data-stu-id="45ad2-115">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="45ad2-116">Nakonec zavolejte [**metodu Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) a načtěte uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="45ad2-116">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="45ad2-117">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="45ad2-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="45ad2-118">**Project:** SDK pro Partnerské centrum Samples **Class:** GetCustomerUserDetails.cs</span><span class="sxs-lookup"><span data-stu-id="45ad2-118">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="45ad2-119">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="45ad2-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="45ad2-120">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="45ad2-120">Request syntax</span></span>

| <span data-ttu-id="45ad2-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="45ad2-121">Method</span></span>  | <span data-ttu-id="45ad2-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="45ad2-122">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="45ad2-123">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="45ad2-123">**GET**</span></span> | <span data-ttu-id="45ad2-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/users/{ID_uživatele} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="45ad2-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="45ad2-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="45ad2-125">URI parameter</span></span>

<span data-ttu-id="45ad2-126">Pomocí následujících parametrů identifikátoru URI identifikujte správného zákazníka a uživatele.</span><span class="sxs-lookup"><span data-stu-id="45ad2-126">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="45ad2-127">Název</span><span class="sxs-lookup"><span data-stu-id="45ad2-127">Name</span></span>                   | <span data-ttu-id="45ad2-128">Typ</span><span class="sxs-lookup"><span data-stu-id="45ad2-128">Type</span></span>     | <span data-ttu-id="45ad2-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="45ad2-129">Required</span></span> | <span data-ttu-id="45ad2-130">Popis</span><span class="sxs-lookup"><span data-stu-id="45ad2-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="45ad2-131">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="45ad2-131">**customer-tenant-id**</span></span> | <span data-ttu-id="45ad2-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="45ad2-132">**guid**</span></span> | <span data-ttu-id="45ad2-133">Y</span><span class="sxs-lookup"><span data-stu-id="45ad2-133">Y</span></span>        | <span data-ttu-id="45ad2-134">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="45ad2-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="45ad2-135">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="45ad2-135">**user-id**</span></span>            | <span data-ttu-id="45ad2-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="45ad2-136">**guid**</span></span> | <span data-ttu-id="45ad2-137">Y</span><span class="sxs-lookup"><span data-stu-id="45ad2-137">Y</span></span>        | <span data-ttu-id="45ad2-138">Hodnota je ID uživatele ve **formátu** GUID, které patří jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="45ad2-138">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="45ad2-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="45ad2-139">Request headers</span></span>

<span data-ttu-id="45ad2-140">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="45ad2-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="45ad2-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="45ad2-141">Request body</span></span>

<span data-ttu-id="45ad2-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="45ad2-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="45ad2-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="45ad2-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="45ad2-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="45ad2-144">REST response</span></span>

<span data-ttu-id="45ad2-145">V případě úspěchu tato metoda vrátí uživatelský účet zákazníka.</span><span class="sxs-lookup"><span data-stu-id="45ad2-145">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="45ad2-146">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="45ad2-146">Response success and error codes</span></span>

<span data-ttu-id="45ad2-147">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="45ad2-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="45ad2-148">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="45ad2-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="45ad2-149">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="45ad2-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="45ad2-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="45ad2-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 432
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CV: uWM1EGU7+0aI2MvV.0
MS-ServerId: 020021921
Date: Wed, 21 Dec 2016 22:59:10 GMT

{
    "usageLocation": "US",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Daniel",
    "lastName": "Tsai",
    "displayName": "Daniel Tsai",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
