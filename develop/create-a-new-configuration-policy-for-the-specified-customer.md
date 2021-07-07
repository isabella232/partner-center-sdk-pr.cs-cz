---
title: Vytvořit nové zásady konfigurace pro zákazníky
description: Naučte se používat rozhraní API partnerského centra k vytvoření nové zásady konfigurace pro určitého zákazníka. Článek obsahuje požadavky, kroky a příklady.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 530ff72862204bda093385252450f4eb81b63160
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973668"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="63078-104">Vytvoření nových zásad konfigurace pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="63078-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="63078-105">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="63078-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="63078-106">Vytvoření nové zásady konfigurace pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="63078-106">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63078-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="63078-107">Prerequisites</span></span>

- <span data-ttu-id="63078-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="63078-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="63078-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="63078-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="63078-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="63078-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="63078-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="63078-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="63078-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="63078-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="63078-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="63078-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="63078-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="63078-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="63078-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="63078-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="63078-116">C\#</span><span class="sxs-lookup"><span data-stu-id="63078-116">C\#</span></span>

<span data-ttu-id="63078-117">Vytvoření nové zásady konfigurace pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="63078-117">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="63078-118">Vytvořte instanci nového objektu [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) , jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="63078-118">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="63078-119">Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní k operacím na zadaném zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="63078-119">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="63078-120">Načte vlastnost [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) , aby se získalo rozhraní pro operace shromažďování zásad konfigurace.</span><span class="sxs-lookup"><span data-stu-id="63078-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="63078-121">Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) vytvořte zásadu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="63078-121">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="63078-122">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="63078-122">C\# example</span></span>

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

<span data-ttu-id="63078-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="63078-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="63078-124">**Project**: **třída** microsoft Partner SDK samples: CreateConfigurationPolicy. cs</span><span class="sxs-lookup"><span data-stu-id="63078-124">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="63078-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="63078-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="63078-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="63078-126">Request syntax</span></span>

| <span data-ttu-id="63078-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="63078-127">Method</span></span>   | <span data-ttu-id="63078-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="63078-128">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="63078-129">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="63078-129">**POST**</span></span> | <span data-ttu-id="63078-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="63078-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="63078-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="63078-131">URI parameter</span></span>

<span data-ttu-id="63078-132">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="63078-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="63078-133">Název</span><span class="sxs-lookup"><span data-stu-id="63078-133">Name</span></span>        | <span data-ttu-id="63078-134">Typ</span><span class="sxs-lookup"><span data-stu-id="63078-134">Type</span></span>   | <span data-ttu-id="63078-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="63078-135">Required</span></span> | <span data-ttu-id="63078-136">Popis</span><span class="sxs-lookup"><span data-stu-id="63078-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="63078-137">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="63078-137">customer-id</span></span> | <span data-ttu-id="63078-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="63078-138">string</span></span> | <span data-ttu-id="63078-139">Yes</span><span class="sxs-lookup"><span data-stu-id="63078-139">Yes</span></span>      | <span data-ttu-id="63078-140">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="63078-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="63078-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="63078-141">Request headers</span></span>

<span data-ttu-id="63078-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="63078-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="63078-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="63078-143">Request body</span></span>

<span data-ttu-id="63078-144">Tělo žádosti musí obsahovat objekt s informacemi o zásadách konfigurace, jak je popsáno v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="63078-144">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="63078-145">Název</span><span class="sxs-lookup"><span data-stu-id="63078-145">Name</span></span>           | <span data-ttu-id="63078-146">Typ</span><span class="sxs-lookup"><span data-stu-id="63078-146">Type</span></span>             | <span data-ttu-id="63078-147">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="63078-147">Required</span></span> | <span data-ttu-id="63078-148">Popis</span><span class="sxs-lookup"><span data-stu-id="63078-148">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="63078-149">name</span><span class="sxs-lookup"><span data-stu-id="63078-149">name</span></span>           | <span data-ttu-id="63078-150">řetězec</span><span class="sxs-lookup"><span data-stu-id="63078-150">string</span></span>           | <span data-ttu-id="63078-151">Yes</span><span class="sxs-lookup"><span data-stu-id="63078-151">Yes</span></span>      | <span data-ttu-id="63078-152">Popisný název zásady.</span><span class="sxs-lookup"><span data-stu-id="63078-152">The friendly name of the policy.</span></span> |
| <span data-ttu-id="63078-153">category</span><span class="sxs-lookup"><span data-stu-id="63078-153">category</span></span>       | <span data-ttu-id="63078-154">řetězec</span><span class="sxs-lookup"><span data-stu-id="63078-154">string</span></span>           | <span data-ttu-id="63078-155">Yes</span><span class="sxs-lookup"><span data-stu-id="63078-155">Yes</span></span>      | <span data-ttu-id="63078-156">Kategorie zásad</span><span class="sxs-lookup"><span data-stu-id="63078-156">The policy category.</span></span>             |
| <span data-ttu-id="63078-157">description</span><span class="sxs-lookup"><span data-stu-id="63078-157">description</span></span>    | <span data-ttu-id="63078-158">řetězec</span><span class="sxs-lookup"><span data-stu-id="63078-158">string</span></span>           | <span data-ttu-id="63078-159">No</span><span class="sxs-lookup"><span data-stu-id="63078-159">No</span></span>       | <span data-ttu-id="63078-160">Popis zásady.</span><span class="sxs-lookup"><span data-stu-id="63078-160">The policy description.</span></span>          |
| <span data-ttu-id="63078-161">policySettings</span><span class="sxs-lookup"><span data-stu-id="63078-161">policySettings</span></span> | <span data-ttu-id="63078-162">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="63078-162">array of strings</span></span> | <span data-ttu-id="63078-163">Yes</span><span class="sxs-lookup"><span data-stu-id="63078-163">Yes</span></span>      | <span data-ttu-id="63078-164">Nastavení zásad</span><span class="sxs-lookup"><span data-stu-id="63078-164">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="63078-165">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="63078-165">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="63078-166">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="63078-166">REST response</span></span>

<span data-ttu-id="63078-167">V případě úspěchu obsahuje tělo odpovědi prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pro novou zásadu.</span><span class="sxs-lookup"><span data-stu-id="63078-167">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="63078-168">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="63078-168">Response success and error codes</span></span>

<span data-ttu-id="63078-169">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="63078-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="63078-170">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="63078-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="63078-171">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="63078-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="63078-172">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="63078-172">Response example</span></span>

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
