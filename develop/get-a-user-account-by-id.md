---
title: Získání uživatelského účtu podle ID
description: Získat konkrétní uživatelský účet pro zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a2f42001365324a65376318cb1f2d57dc123df0c
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766841"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="ea3f0-103">Získání uživatelského účtu podle ID</span><span class="sxs-lookup"><span data-stu-id="ea3f0-103">Get a user account by ID</span></span>

<span data-ttu-id="ea3f0-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="ea3f0-104">**Applies To**</span></span>

- <span data-ttu-id="ea3f0-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="ea3f0-105">Partner Center</span></span>

<span data-ttu-id="ea3f0-106">Získat konkrétní uživatelský účet pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-106">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="ea3f0-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ea3f0-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ea3f0-108">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ea3f0-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ea3f0-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ea3f0-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ea3f0-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ea3f0-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ea3f0-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="ea3f0-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ea3f0-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ea3f0-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ea3f0-115">C\#</span><span class="sxs-lookup"><span data-stu-id="ea3f0-115">C\#</span></span>

<span data-ttu-id="ea3f0-116">Chcete-li načíst uživatelský účet pro zákazníka, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-116">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ea3f0-117">Dále zavolejte metodu User [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , která načte konkrétního uživatele.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-117">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="ea3f0-118">Nakonec voláním metody User [**. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) načtěte uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-118">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="ea3f0-119">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ea3f0-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ea3f0-120">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetCustomerUserDetails.cs</span><span class="sxs-lookup"><span data-stu-id="ea3f0-120">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ea3f0-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ea3f0-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ea3f0-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ea3f0-122">Request syntax</span></span>

| <span data-ttu-id="ea3f0-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="ea3f0-123">Method</span></span>  | <span data-ttu-id="ea3f0-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ea3f0-124">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ea3f0-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="ea3f0-125">**GET**</span></span> | <span data-ttu-id="ea3f0-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ea3f0-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ea3f0-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ea3f0-127">URI parameter</span></span>

<span data-ttu-id="ea3f0-128">K identifikaci správného zákazníka a uživatele použijte následující parametry identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-128">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="ea3f0-129">Název</span><span class="sxs-lookup"><span data-stu-id="ea3f0-129">Name</span></span>                   | <span data-ttu-id="ea3f0-130">Typ</span><span class="sxs-lookup"><span data-stu-id="ea3f0-130">Type</span></span>     | <span data-ttu-id="ea3f0-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ea3f0-131">Required</span></span> | <span data-ttu-id="ea3f0-132">Popis</span><span class="sxs-lookup"><span data-stu-id="ea3f0-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ea3f0-133">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="ea3f0-133">**customer-tenant-id**</span></span> | <span data-ttu-id="ea3f0-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="ea3f0-134">**guid**</span></span> | <span data-ttu-id="ea3f0-135">Y</span><span class="sxs-lookup"><span data-stu-id="ea3f0-135">Y</span></span>        | <span data-ttu-id="ea3f0-136">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="ea3f0-137">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="ea3f0-137">**user-id**</span></span>            | <span data-ttu-id="ea3f0-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="ea3f0-138">**guid**</span></span> | <span data-ttu-id="ea3f0-139">Y</span><span class="sxs-lookup"><span data-stu-id="ea3f0-139">Y</span></span>        | <span data-ttu-id="ea3f0-140">Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="ea3f0-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ea3f0-141">Request headers</span></span>

<span data-ttu-id="ea3f0-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ea3f0-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ea3f0-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ea3f0-143">Request body</span></span>

<span data-ttu-id="ea3f0-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="ea3f0-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ea3f0-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ea3f0-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ea3f0-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ea3f0-146">REST response</span></span>

<span data-ttu-id="ea3f0-147">V případě úspěchu vrátí tato metoda uživatelský účet pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-147">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ea3f0-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ea3f0-148">Response success and error codes</span></span>

<span data-ttu-id="ea3f0-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ea3f0-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ea3f0-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ea3f0-151">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ea3f0-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ea3f0-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ea3f0-152">Response example</span></span>

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
