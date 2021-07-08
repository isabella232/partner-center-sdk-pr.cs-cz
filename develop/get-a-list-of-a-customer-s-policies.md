---
title: Získání seznamu zásad zákazníka
description: Jak načíst kolekci zadaných zásad konfigurace zákazníka.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bf6ace0d2425e28d80c4f2310878c2d2a9e2a876
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874580"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="8c4c1-103">Získání seznamu zásad zákazníka</span><span class="sxs-lookup"><span data-stu-id="8c4c1-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="8c4c1-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)</span><span class="sxs-lookup"><span data-stu-id="8c4c1-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8c4c1-105">Tento článek popisuje, jak načíst kolekci zadaných zásad konfigurace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-105">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c4c1-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8c4c1-106">Prerequisites</span></span>

- <span data-ttu-id="8c4c1-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8c4c1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8c4c1-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8c4c1-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8c4c1-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8c4c1-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8c4c1-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8c4c1-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="8c4c1-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8c4c1-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="8c4c1-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8c4c1-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8c4c1-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8c4c1-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="8c4c1-115">C\#</span><span class="sxs-lookup"><span data-stu-id="8c4c1-115">C\#</span></span>

<span data-ttu-id="8c4c1-116">Seznam všech zásad zákazníka získáte tak, že:</span><span class="sxs-lookup"><span data-stu-id="8c4c1-116">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="8c4c1-117">Voláním [**metody IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka načtěte rozhraní pro operace u zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="8c4c1-118">[**Načtěte vlastnost ConfigurationPolicies,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) abyste získali rozhraní pro operace shromažďování zásad konfigurace.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-118">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="8c4c1-119">Voláním [**metody Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) načtěte kolekci zásad.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="8c4c1-120">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="8c4c1-120">For an example, see the following:</span></span>

- <span data-ttu-id="8c4c1-121">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="8c4c1-121">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="8c4c1-122">Project: **SDK pro Partnerské centrum ukázky**</span><span class="sxs-lookup"><span data-stu-id="8c4c1-122">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="8c4c1-123">Třída: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="8c4c1-123">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="8c4c1-124">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="8c4c1-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8c4c1-125">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="8c4c1-125">Request syntax</span></span>

| <span data-ttu-id="8c4c1-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="8c4c1-126">Method</span></span>  | <span data-ttu-id="8c4c1-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8c4c1-127">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="8c4c1-128">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="8c4c1-128">**GET**</span></span> | <span data-ttu-id="8c4c1-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8c4c1-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="8c4c1-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8c4c1-130">URI parameter</span></span>

<span data-ttu-id="8c4c1-131">Při vytváření požadavku použijte následující parametr cesty:</span><span class="sxs-lookup"><span data-stu-id="8c4c1-131">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="8c4c1-132">Název</span><span class="sxs-lookup"><span data-stu-id="8c4c1-132">Name</span></span>        | <span data-ttu-id="8c4c1-133">Typ</span><span class="sxs-lookup"><span data-stu-id="8c4c1-133">Type</span></span>   | <span data-ttu-id="8c4c1-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8c4c1-134">Required</span></span> | <span data-ttu-id="8c4c1-135">Popis</span><span class="sxs-lookup"><span data-stu-id="8c4c1-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8c4c1-136">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="8c4c1-136">customer-id</span></span> | <span data-ttu-id="8c4c1-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="8c4c1-137">string</span></span> | <span data-ttu-id="8c4c1-138">Yes</span><span class="sxs-lookup"><span data-stu-id="8c4c1-138">Yes</span></span>      | <span data-ttu-id="8c4c1-139">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8c4c1-140">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8c4c1-140">Request headers</span></span>

<span data-ttu-id="8c4c1-141">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8c4c1-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8c4c1-142">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8c4c1-142">Request body</span></span>

<span data-ttu-id="8c4c1-143">Žádná</span><span class="sxs-lookup"><span data-stu-id="8c4c1-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="8c4c1-144">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8c4c1-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
Content-Length:0
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8c4c1-145">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8c4c1-145">REST response</span></span>

<span data-ttu-id="8c4c1-146">V případě úspěchu bude tělo odpovědi obsahovat kolekci prostředků [ConfigurationPolicy.](device-deployment-resources.md#configurationpolicy)</span><span class="sxs-lookup"><span data-stu-id="8c4c1-146">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8c4c1-147">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="8c4c1-147">Response success and error codes</span></span>

<span data-ttu-id="8c4c1-148">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8c4c1-149">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="8c4c1-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8c4c1-150">Úplný seznam najdete v tématu Partnerské centrum [kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8c4c1-150">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8c4c1-151">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8c4c1-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1221
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d5ff2573-3ef8-4553-aac4-4b73d97dce1b
MS-RequestId: 6eb7383d-eeb5-44d7-8570-e0ed12c0547a
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:49 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "8c7d25aa-2dbb-409c-a1f0-f55bd9108fa9",
            "name": "Windows 10 Enterprise E3",
            "category": "o_o_b_e",
            "description": "P462017 description",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-04-27T11:30:34.1944704-07:00",
            "lastModifiedDate": "2017-04-27T11:30:34.1944704-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
            "name": "Test policy",
            "category": "o_o_b_e",
            "description": "Test policy creation from API 1",
            "devicesAssigned": 0,
            "policySettings": ["skip_express_settings"],
            "createdDate": "2017-07-25T11:03:03.8457088-07:00",
            "lastModifiedDate": "2017-07-25T11:04:00.8150016-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "a96b5fd9-0f3a-419a-b55c-a8aecd6b1f00",
            "name": "Windows 10 Enterprise E5",
            "category": "o_o_b_e",
            "description": "test policy creation from API",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-07-25T11:07:36.1501184-07:00",
            "lastModifiedDate": "2017-07-25T11:07:36.1501184-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
