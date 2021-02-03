---
title: Načtení zásad konfigurace zákazníka
description: Jak načíst zadané zásady konfigurace pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d5d4ee83d1a66f33872d8b1f1327f47eeb4465e
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767014"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="c70cb-103">Načtení zásad konfigurace zákazníka</span><span class="sxs-lookup"><span data-stu-id="c70cb-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="c70cb-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="c70cb-104">**Applies To**</span></span>

- <span data-ttu-id="c70cb-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="c70cb-105">Partner Center</span></span>
- <span data-ttu-id="c70cb-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="c70cb-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="c70cb-107">Jak načíst zadané zásady konfigurace pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="c70cb-107">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c70cb-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c70cb-108">Prerequisites</span></span>

- <span data-ttu-id="c70cb-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c70cb-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c70cb-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="c70cb-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c70cb-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c70cb-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c70cb-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="c70cb-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c70cb-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="c70cb-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c70cb-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="c70cb-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c70cb-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="c70cb-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c70cb-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c70cb-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c70cb-117">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="c70cb-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="c70cb-118">C\#</span><span class="sxs-lookup"><span data-stu-id="c70cb-118">C\#</span></span>

<span data-ttu-id="c70cb-119">Pokud chcete načíst zásadu konfigurace pro zadaného zákazníka, nejdřív zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro konkrétního zákazníka.</span><span class="sxs-lookup"><span data-stu-id="c70cb-119">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="c70cb-120">V dalším kroku zavolejte metodu [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady, aby se načetlo rozhraní pro operace zásad konfigurace pro zadané zásady.</span><span class="sxs-lookup"><span data-stu-id="c70cb-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="c70cb-121">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) načtěte zásady konfigurace.</span><span class="sxs-lookup"><span data-stu-id="c70cb-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="c70cb-122">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c70cb-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c70cb-123">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="c70cb-123">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c70cb-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="c70cb-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c70cb-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="c70cb-125">Request syntax</span></span>

| <span data-ttu-id="c70cb-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="c70cb-126">Method</span></span>  | <span data-ttu-id="c70cb-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="c70cb-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c70cb-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="c70cb-128">**GET**</span></span> | <span data-ttu-id="c70cb-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c70cb-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c70cb-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c70cb-130">URI parameter</span></span>

<span data-ttu-id="c70cb-131">Při vytváření žádosti použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="c70cb-131">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="c70cb-132">Název</span><span class="sxs-lookup"><span data-stu-id="c70cb-132">Name</span></span>        | <span data-ttu-id="c70cb-133">Typ</span><span class="sxs-lookup"><span data-stu-id="c70cb-133">Type</span></span>   | <span data-ttu-id="c70cb-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="c70cb-134">Required</span></span> | <span data-ttu-id="c70cb-135">Popis</span><span class="sxs-lookup"><span data-stu-id="c70cb-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="c70cb-136">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="c70cb-136">customer-id</span></span> | <span data-ttu-id="c70cb-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="c70cb-137">string</span></span> | <span data-ttu-id="c70cb-138">Yes</span><span class="sxs-lookup"><span data-stu-id="c70cb-138">Yes</span></span>      | <span data-ttu-id="c70cb-139">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="c70cb-139">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="c70cb-140">ID zásady</span><span class="sxs-lookup"><span data-stu-id="c70cb-140">policy-id</span></span>   | <span data-ttu-id="c70cb-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="c70cb-141">string</span></span> | <span data-ttu-id="c70cb-142">Yes</span><span class="sxs-lookup"><span data-stu-id="c70cb-142">Yes</span></span>      | <span data-ttu-id="c70cb-143">Řetězec ve formátu GUID, který identifikuje zásadu.</span><span class="sxs-lookup"><span data-stu-id="c70cb-143">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="c70cb-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="c70cb-144">Request headers</span></span>

<span data-ttu-id="c70cb-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c70cb-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c70cb-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="c70cb-146">Request body</span></span>

<span data-ttu-id="c70cb-147">Žádné</span><span class="sxs-lookup"><span data-stu-id="c70cb-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="c70cb-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="c70cb-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c70cb-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="c70cb-149">REST response</span></span>

<span data-ttu-id="c70cb-150">V případě úspěchu odpověď obsahuje požadovaný prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) .</span><span class="sxs-lookup"><span data-stu-id="c70cb-150">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c70cb-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="c70cb-151">Response success and error codes</span></span>

<span data-ttu-id="c70cb-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="c70cb-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c70cb-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="c70cb-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c70cb-154">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c70cb-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c70cb-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="c70cb-155">Response example</span></span>

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
