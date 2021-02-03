---
title: Získání seznamu všech uživatelských účtů pro zákazníka
description: Jak získat seznam všech uživatelských účtů, které patří jednomu z vašich zákazníků.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f2b1bcf9926e02232b6e2cc68b71e992b015324
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766862"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="cb491-103">Získání seznamu všech uživatelských účtů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="cb491-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="cb491-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="cb491-104">**Applies to:**</span></span>

- <span data-ttu-id="cb491-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="cb491-105">Partner Center</span></span>

<span data-ttu-id="cb491-106">Tento článek popisuje, jak získat seznam všech uživatelských účtů, které patří jednomu z vašich zákazníků.</span><span class="sxs-lookup"><span data-stu-id="cb491-106">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="cb491-107">Pokud chcete vyhledat jeden uživatelský účet podle ID, přečtěte si téma [Získání uživatelského účtu podle ID](get-a-user-account-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="cb491-107">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb491-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="cb491-108">Prerequisites</span></span>

- <span data-ttu-id="cb491-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cb491-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cb491-110">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="cb491-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cb491-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb491-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cb491-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="cb491-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cb491-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="cb491-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cb491-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="cb491-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cb491-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="cb491-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cb491-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb491-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="cb491-117">C\#</span><span class="sxs-lookup"><span data-stu-id="cb491-117">C\#</span></span>

<span data-ttu-id="cb491-118">Načtení kolekce všech uživatelských účtů pro určitého zákazníka:</span><span class="sxs-lookup"><span data-stu-id="cb491-118">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="cb491-119">Pro identifikaci zákazníka zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) se zadaným ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="cb491-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="cb491-120">Pro načtení kolekce zavolejte metodu [**uživatel. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="cb491-120">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="cb491-121">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="cb491-121">For an example, see the following:</span></span>

- <span data-ttu-id="cb491-122">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="cb491-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="cb491-123">Projekt: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="cb491-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="cb491-124">Třída: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="cb491-124">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="cb491-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="cb491-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cb491-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="cb491-126">Request syntax</span></span>

| <span data-ttu-id="cb491-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="cb491-127">Method</span></span>  | <span data-ttu-id="cb491-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="cb491-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb491-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="cb491-129">**GET**</span></span> | <span data-ttu-id="cb491-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cb491-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="cb491-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="cb491-131">URI parameter</span></span>

<span data-ttu-id="cb491-132">Pro identifikaci správného zákazníka použijte následující parametr identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="cb491-132">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="cb491-133">Název</span><span class="sxs-lookup"><span data-stu-id="cb491-133">Name</span></span>                   | <span data-ttu-id="cb491-134">Typ</span><span class="sxs-lookup"><span data-stu-id="cb491-134">Type</span></span>     | <span data-ttu-id="cb491-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="cb491-135">Required</span></span> | <span data-ttu-id="cb491-136">Popis</span><span class="sxs-lookup"><span data-stu-id="cb491-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb491-137">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="cb491-137">**customer-tenant-id**</span></span> | <span data-ttu-id="cb491-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="cb491-138">**guid**</span></span> | <span data-ttu-id="cb491-139">Y</span><span class="sxs-lookup"><span data-stu-id="cb491-139">Y</span></span>        | <span data-ttu-id="cb491-140">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="cb491-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cb491-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="cb491-141">Request headers</span></span>

<span data-ttu-id="cb491-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cb491-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cb491-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="cb491-143">Request body</span></span>

<span data-ttu-id="cb491-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="cb491-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cb491-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="cb491-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="cb491-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="cb491-146">REST response</span></span>

<span data-ttu-id="cb491-147">V případě úspěchu vrátí tato metoda kolekci uživatelských účtů pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="cb491-147">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cb491-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="cb491-148">Response success and error codes</span></span>

<span data-ttu-id="cb491-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="cb491-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cb491-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="cb491-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cb491-151">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cb491-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cb491-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="cb491-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1030
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CV: 6zmKqrSFB0+t7m3y.0
MS-ServerId: 101112616
Date: Wed, 21 Dec 2016 21:13:24 GMT

 {
    "totalCount": 2,
    "items": [{
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
        }, {
            "id": "6e668259-1f09-479d-bcb8-d9b03e826b8d",
            "userPrincipalName": "admin@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "DT Demo CSP Customer 005",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/6e668259-1f09-479d-bcb8-d9b03e826b8d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
