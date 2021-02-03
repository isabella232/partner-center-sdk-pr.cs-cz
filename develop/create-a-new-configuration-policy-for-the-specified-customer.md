---
title: Vytvořit nové zásady konfigurace pro zákazníky
description: Naučte se používat rozhraní API partnerského centra k vytvoření nové zásady konfigurace pro určitého zákazníka. Článek obsahuje požadavky, kroky a příklady.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 21a0bfde7f931371ff09d6c27de0281a4ed3b3cb
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767137"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="8d587-104">Vytvoření nových zásad konfigurace pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="8d587-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="8d587-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="8d587-105">**Applies to:**</span></span>

- <span data-ttu-id="8d587-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="8d587-106">Partner Center</span></span>
- <span data-ttu-id="8d587-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="8d587-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8d587-108">Vytvoření nové zásady konfigurace pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8d587-108">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d587-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8d587-109">Prerequisites</span></span>

- <span data-ttu-id="8d587-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8d587-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8d587-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="8d587-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8d587-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8d587-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8d587-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="8d587-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8d587-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="8d587-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8d587-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="8d587-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8d587-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="8d587-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8d587-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8d587-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="8d587-118">C\#</span><span class="sxs-lookup"><span data-stu-id="8d587-118">C\#</span></span>

<span data-ttu-id="8d587-119">Vytvoření nové zásady konfigurace pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="8d587-119">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="8d587-120">Vytvořte instanci nového objektu [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) , jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="8d587-120">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="8d587-121">Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní k operacím na zadaném zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="8d587-121">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="8d587-122">Načte vlastnost [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) , aby se získalo rozhraní pro operace shromažďování zásad konfigurace.</span><span class="sxs-lookup"><span data-stu-id="8d587-122">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="8d587-123">Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) vytvořte zásadu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="8d587-123">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="8d587-124">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="8d587-124">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

<span data-ttu-id="8d587-125">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8d587-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8d587-126">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="8d587-126">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8d587-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="8d587-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8d587-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="8d587-128">Request syntax</span></span>

| <span data-ttu-id="8d587-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="8d587-129">Method</span></span>   | <span data-ttu-id="8d587-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8d587-130">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="8d587-131">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="8d587-131">**POST**</span></span> | <span data-ttu-id="8d587-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8d587-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="8d587-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8d587-133">URI parameter</span></span>

<span data-ttu-id="8d587-134">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="8d587-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="8d587-135">Název</span><span class="sxs-lookup"><span data-stu-id="8d587-135">Name</span></span>        | <span data-ttu-id="8d587-136">Typ</span><span class="sxs-lookup"><span data-stu-id="8d587-136">Type</span></span>   | <span data-ttu-id="8d587-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8d587-137">Required</span></span> | <span data-ttu-id="8d587-138">Popis</span><span class="sxs-lookup"><span data-stu-id="8d587-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8d587-139">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="8d587-139">customer-id</span></span> | <span data-ttu-id="8d587-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="8d587-140">string</span></span> | <span data-ttu-id="8d587-141">Yes</span><span class="sxs-lookup"><span data-stu-id="8d587-141">Yes</span></span>      | <span data-ttu-id="8d587-142">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8d587-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8d587-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8d587-143">Request headers</span></span>

<span data-ttu-id="8d587-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8d587-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8d587-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8d587-145">Request body</span></span>

<span data-ttu-id="8d587-146">Tělo žádosti musí obsahovat objekt s informacemi o zásadách konfigurace, jak je popsáno v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="8d587-146">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="8d587-147">Název</span><span class="sxs-lookup"><span data-stu-id="8d587-147">Name</span></span>           | <span data-ttu-id="8d587-148">Typ</span><span class="sxs-lookup"><span data-stu-id="8d587-148">Type</span></span>             | <span data-ttu-id="8d587-149">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8d587-149">Required</span></span> | <span data-ttu-id="8d587-150">Popis</span><span class="sxs-lookup"><span data-stu-id="8d587-150">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="8d587-151">name</span><span class="sxs-lookup"><span data-stu-id="8d587-151">name</span></span>           | <span data-ttu-id="8d587-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="8d587-152">string</span></span>           | <span data-ttu-id="8d587-153">Yes</span><span class="sxs-lookup"><span data-stu-id="8d587-153">Yes</span></span>      | <span data-ttu-id="8d587-154">Popisný název zásady.</span><span class="sxs-lookup"><span data-stu-id="8d587-154">The friendly name of the policy.</span></span> |
| <span data-ttu-id="8d587-155">category</span><span class="sxs-lookup"><span data-stu-id="8d587-155">category</span></span>       | <span data-ttu-id="8d587-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="8d587-156">string</span></span>           | <span data-ttu-id="8d587-157">Yes</span><span class="sxs-lookup"><span data-stu-id="8d587-157">Yes</span></span>      | <span data-ttu-id="8d587-158">Kategorie zásad</span><span class="sxs-lookup"><span data-stu-id="8d587-158">The policy category.</span></span>             |
| <span data-ttu-id="8d587-159">description</span><span class="sxs-lookup"><span data-stu-id="8d587-159">description</span></span>    | <span data-ttu-id="8d587-160">řetězec</span><span class="sxs-lookup"><span data-stu-id="8d587-160">string</span></span>           | <span data-ttu-id="8d587-161">No</span><span class="sxs-lookup"><span data-stu-id="8d587-161">No</span></span>       | <span data-ttu-id="8d587-162">Popis zásady.</span><span class="sxs-lookup"><span data-stu-id="8d587-162">The policy description.</span></span>          |
| <span data-ttu-id="8d587-163">policySettings</span><span class="sxs-lookup"><span data-stu-id="8d587-163">policySettings</span></span> | <span data-ttu-id="8d587-164">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="8d587-164">array of strings</span></span> | <span data-ttu-id="8d587-165">Yes</span><span class="sxs-lookup"><span data-stu-id="8d587-165">Yes</span></span>      | <span data-ttu-id="8d587-166">Nastavení zásad</span><span class="sxs-lookup"><span data-stu-id="8d587-166">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="8d587-167">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8d587-167">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="8d587-168">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8d587-168">REST response</span></span>

<span data-ttu-id="8d587-169">V případě úspěchu obsahuje tělo odpovědi prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pro novou zásadu.</span><span class="sxs-lookup"><span data-stu-id="8d587-169">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8d587-170">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="8d587-170">Response success and error codes</span></span>

<span data-ttu-id="8d587-171">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8d587-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8d587-172">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="8d587-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8d587-173">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8d587-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8d587-174">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8d587-174">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
