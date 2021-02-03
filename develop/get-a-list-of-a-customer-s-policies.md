---
title: Získání seznamu zásad zákazníka
description: Jak načíst kolekci zásad konfigurace zadaného zákazníka.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 16886b1adca393ed2967f2a4fe74a379bef1c1c7
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766864"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="1806f-103">Získání seznamu zásad zákazníka</span><span class="sxs-lookup"><span data-stu-id="1806f-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="1806f-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="1806f-104">**Applies to:**</span></span>

- <span data-ttu-id="1806f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="1806f-105">Partner Center</span></span>
- <span data-ttu-id="1806f-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="1806f-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="1806f-107">Tento článek popisuje, jak načíst kolekci zásad konfigurace zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1806f-107">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1806f-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1806f-108">Prerequisites</span></span>

- <span data-ttu-id="1806f-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1806f-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1806f-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="1806f-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1806f-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1806f-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1806f-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="1806f-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1806f-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="1806f-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1806f-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="1806f-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1806f-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="1806f-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1806f-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1806f-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1806f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="1806f-117">C\#</span></span>

<span data-ttu-id="1806f-118">Seznam všech zásad zákazníka získáte v těchto zásadách:</span><span class="sxs-lookup"><span data-stu-id="1806f-118">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="1806f-119">Zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro operace zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1806f-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="1806f-120">Načte vlastnost [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) , aby se získalo rozhraní pro operace shromažďování zásad konfigurace.</span><span class="sxs-lookup"><span data-stu-id="1806f-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="1806f-121">Pro načtení kolekce zásad zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="1806f-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="1806f-122">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="1806f-122">For an example, see the following:</span></span>

- <span data-ttu-id="1806f-123">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1806f-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1806f-124">Projekt: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="1806f-124">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="1806f-125">Třída: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="1806f-125">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1806f-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1806f-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1806f-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="1806f-127">Request syntax</span></span>

| <span data-ttu-id="1806f-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="1806f-128">Method</span></span>  | <span data-ttu-id="1806f-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1806f-129">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="1806f-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="1806f-130">**GET**</span></span> | <span data-ttu-id="1806f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1806f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="1806f-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1806f-132">URI parameter</span></span>

<span data-ttu-id="1806f-133">Při vytváření žádosti použít následující parametr cesty:</span><span class="sxs-lookup"><span data-stu-id="1806f-133">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="1806f-134">Název</span><span class="sxs-lookup"><span data-stu-id="1806f-134">Name</span></span>        | <span data-ttu-id="1806f-135">Typ</span><span class="sxs-lookup"><span data-stu-id="1806f-135">Type</span></span>   | <span data-ttu-id="1806f-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1806f-136">Required</span></span> | <span data-ttu-id="1806f-137">Popis</span><span class="sxs-lookup"><span data-stu-id="1806f-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="1806f-138">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="1806f-138">customer-id</span></span> | <span data-ttu-id="1806f-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="1806f-139">string</span></span> | <span data-ttu-id="1806f-140">Yes</span><span class="sxs-lookup"><span data-stu-id="1806f-140">Yes</span></span>      | <span data-ttu-id="1806f-141">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1806f-141">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1806f-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1806f-142">Request headers</span></span>

<span data-ttu-id="1806f-143">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1806f-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1806f-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1806f-144">Request body</span></span>

<span data-ttu-id="1806f-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="1806f-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="1806f-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1806f-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="1806f-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1806f-147">REST response</span></span>

<span data-ttu-id="1806f-148">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) .</span><span class="sxs-lookup"><span data-stu-id="1806f-148">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1806f-149">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="1806f-149">Response success and error codes</span></span>

<span data-ttu-id="1806f-150">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1806f-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1806f-151">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="1806f-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1806f-152">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1806f-152">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1806f-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1806f-153">Response example</span></span>

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
