---
title: Načtení zásad konfigurace zákazníka
description: Jak načíst zadané zásady konfigurace pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f9a8cb435c63d8d02c3b4633abc8723353116f37
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547491"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="f23bb-103">Načtení zásad konfigurace zákazníka</span><span class="sxs-lookup"><span data-stu-id="f23bb-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="f23bb-104">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="f23bb-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="f23bb-105">Jak načíst zadané zásady konfigurace pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f23bb-105">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f23bb-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f23bb-106">Prerequisites</span></span>

- <span data-ttu-id="f23bb-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f23bb-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f23bb-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="f23bb-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f23bb-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f23bb-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f23bb-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="f23bb-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f23bb-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="f23bb-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f23bb-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="f23bb-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f23bb-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="f23bb-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f23bb-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f23bb-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f23bb-115">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="f23bb-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="f23bb-116">C\#</span><span class="sxs-lookup"><span data-stu-id="f23bb-116">C\#</span></span>

<span data-ttu-id="f23bb-117">Pokud chcete načíst zásadu konfigurace pro zadaného zákazníka, nejdřív zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro konkrétního zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f23bb-117">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="f23bb-118">V dalším kroku zavolejte metodu [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady, aby se načetlo rozhraní pro operace zásad konfigurace pro zadané zásady.</span><span class="sxs-lookup"><span data-stu-id="f23bb-118">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="f23bb-119">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) načtěte zásady konfigurace.</span><span class="sxs-lookup"><span data-stu-id="f23bb-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="f23bb-120">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f23bb-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f23bb-121">**Project**: **třída** microsoft Partner SDK samples: GetConfigurationPolicy. cs</span><span class="sxs-lookup"><span data-stu-id="f23bb-121">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f23bb-122">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f23bb-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f23bb-123">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f23bb-123">Request syntax</span></span>

| <span data-ttu-id="f23bb-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="f23bb-124">Method</span></span>  | <span data-ttu-id="f23bb-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f23bb-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f23bb-126">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="f23bb-126">**GET**</span></span> | <span data-ttu-id="f23bb-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f23bb-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f23bb-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f23bb-128">URI parameter</span></span>

<span data-ttu-id="f23bb-129">Při vytváření žádosti použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="f23bb-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="f23bb-130">Název</span><span class="sxs-lookup"><span data-stu-id="f23bb-130">Name</span></span>        | <span data-ttu-id="f23bb-131">Typ</span><span class="sxs-lookup"><span data-stu-id="f23bb-131">Type</span></span>   | <span data-ttu-id="f23bb-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f23bb-132">Required</span></span> | <span data-ttu-id="f23bb-133">Popis</span><span class="sxs-lookup"><span data-stu-id="f23bb-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="f23bb-134">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="f23bb-134">customer-id</span></span> | <span data-ttu-id="f23bb-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="f23bb-135">string</span></span> | <span data-ttu-id="f23bb-136">Yes</span><span class="sxs-lookup"><span data-stu-id="f23bb-136">Yes</span></span>      | <span data-ttu-id="f23bb-137">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f23bb-137">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="f23bb-138">ID zásady</span><span class="sxs-lookup"><span data-stu-id="f23bb-138">policy-id</span></span>   | <span data-ttu-id="f23bb-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="f23bb-139">string</span></span> | <span data-ttu-id="f23bb-140">Yes</span><span class="sxs-lookup"><span data-stu-id="f23bb-140">Yes</span></span>      | <span data-ttu-id="f23bb-141">Řetězec ve formátu GUID, který identifikuje zásadu.</span><span class="sxs-lookup"><span data-stu-id="f23bb-141">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="f23bb-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f23bb-142">Request headers</span></span>

<span data-ttu-id="f23bb-143">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f23bb-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f23bb-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f23bb-144">Request body</span></span>

<span data-ttu-id="f23bb-145">Žádná</span><span class="sxs-lookup"><span data-stu-id="f23bb-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f23bb-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f23bb-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f23bb-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f23bb-147">REST response</span></span>

<span data-ttu-id="f23bb-148">V případě úspěchu odpověď obsahuje požadovaný prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) .</span><span class="sxs-lookup"><span data-stu-id="f23bb-148">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f23bb-149">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f23bb-149">Response success and error codes</span></span>

<span data-ttu-id="f23bb-150">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f23bb-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f23bb-151">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f23bb-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f23bb-152">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f23bb-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f23bb-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f23bb-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 443
MS-CorrelationId: abe150cf-c677-435c-b5d5-b34899a6d1ec
MS-RequestId: ab3abfe7-dce7-46c0-ab20-4fd49bc3e2f7
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:08:27 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API 1",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-07-25T11:03:03.8457116-07:00",
    "lastModifiedDate": "2017-07-25T11:04:00.8149974-07:00",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
