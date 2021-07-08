---
title: Získání seznamu všech uživatelských účtů pro zákazníka
description: Jak získat seznam všech uživatelských účtů, které patří jednomu z vašich zákazníků.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f3d5fcc610eae8c1bff056c1e4a9e7a74093c87d
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874563"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="3245e-103">Získání seznamu všech uživatelských účtů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="3245e-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="3245e-104">Tento článek popisuje, jak získat seznam všech uživatelských účtů, které patří jednomu z vašich zákazníků.</span><span class="sxs-lookup"><span data-stu-id="3245e-104">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="3245e-105">Informace o vyhledávání jednoho uživatelského účtu podle ID najdete v tématu [Získání uživatelského účtu podle ID](get-a-user-account-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="3245e-105">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3245e-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3245e-106">Prerequisites</span></span>

- <span data-ttu-id="3245e-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3245e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3245e-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="3245e-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3245e-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3245e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3245e-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="3245e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3245e-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="3245e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3245e-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="3245e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3245e-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3245e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3245e-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3245e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="3245e-115">C\#</span><span class="sxs-lookup"><span data-stu-id="3245e-115">C\#</span></span>

<span data-ttu-id="3245e-116">Načtení kolekce všech uživatelských účtů pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="3245e-116">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="3245e-117">Pokud chcete zákazníka identifikovat, zavolejte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) se zadaným ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3245e-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="3245e-118">Pro načtení kolekce volejte metodu [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) nebo [**GetAsync.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="3245e-118">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="3245e-119">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="3245e-119">For an example, see the following:</span></span>

- <span data-ttu-id="3245e-120">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3245e-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="3245e-121">Project: **SDK pro Partnerské centrum ukázky**</span><span class="sxs-lookup"><span data-stu-id="3245e-121">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="3245e-122">Třída: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="3245e-122">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3245e-123">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="3245e-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3245e-124">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="3245e-124">Request syntax</span></span>

| <span data-ttu-id="3245e-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="3245e-125">Method</span></span>  | <span data-ttu-id="3245e-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3245e-126">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="3245e-127">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="3245e-127">**GET**</span></span> | <span data-ttu-id="3245e-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/uživatelé HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3245e-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="3245e-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="3245e-129">URI parameter</span></span>

<span data-ttu-id="3245e-130">Pomocí následujícího parametru URI identifikujte správného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3245e-130">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="3245e-131">Název</span><span class="sxs-lookup"><span data-stu-id="3245e-131">Name</span></span>                   | <span data-ttu-id="3245e-132">Typ</span><span class="sxs-lookup"><span data-stu-id="3245e-132">Type</span></span>     | <span data-ttu-id="3245e-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3245e-133">Required</span></span> | <span data-ttu-id="3245e-134">Popis</span><span class="sxs-lookup"><span data-stu-id="3245e-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3245e-135">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="3245e-135">**customer-tenant-id**</span></span> | <span data-ttu-id="3245e-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="3245e-136">**guid**</span></span> | <span data-ttu-id="3245e-137">Y</span><span class="sxs-lookup"><span data-stu-id="3245e-137">Y</span></span>        | <span data-ttu-id="3245e-138">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="3245e-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3245e-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="3245e-139">Request headers</span></span>

<span data-ttu-id="3245e-140">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3245e-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3245e-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="3245e-141">Request body</span></span>

<span data-ttu-id="3245e-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="3245e-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3245e-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="3245e-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3245e-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3245e-144">REST response</span></span>

<span data-ttu-id="3245e-145">V případě úspěchu vrátí tato metoda kolekci uživatelských účtů pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3245e-145">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3245e-146">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="3245e-146">Response success and error codes</span></span>

<span data-ttu-id="3245e-147">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="3245e-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3245e-148">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="3245e-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3245e-149">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3245e-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3245e-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="3245e-150">Response example</span></span>

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
