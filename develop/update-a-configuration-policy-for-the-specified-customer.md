---
title: Aktualizace zásad konfigurace pro konkrétního zákazníka
description: Jak aktualizovat zadané zásady konfigurace pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bf3b6f4db7516779c157b647725368ff0e4a570
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767015"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="1d16d-103">Aktualizace zásad konfigurace pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="1d16d-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="1d16d-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="1d16d-104">**Applies To**</span></span>

- <span data-ttu-id="1d16d-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="1d16d-105">Partner Center</span></span>
- <span data-ttu-id="1d16d-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="1d16d-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="1d16d-107">Jak aktualizovat zadané zásady konfigurace pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1d16d-107">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d16d-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1d16d-108">Prerequisites</span></span>

- <span data-ttu-id="1d16d-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1d16d-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1d16d-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="1d16d-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1d16d-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1d16d-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1d16d-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="1d16d-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1d16d-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="1d16d-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1d16d-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="1d16d-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1d16d-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="1d16d-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1d16d-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1d16d-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1d16d-117">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="1d16d-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="1d16d-118">C\#</span><span class="sxs-lookup"><span data-stu-id="1d16d-118">C\#</span></span>

<span data-ttu-id="1d16d-119">Chcete-li aktualizovat existující zásady konfigurace pro zadaného zákazníka, vytvořte instanci nového objektu [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) , jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="1d16d-119">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="1d16d-120">Hodnoty v tomto novém objektu nahradí odpovídající hodnoty v existujícím objektu.</span><span class="sxs-lookup"><span data-stu-id="1d16d-120">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="1d16d-121">Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro operace zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1d16d-121">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="1d16d-122">V dalším kroku zavolejte metodu [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady, aby se načetlo rozhraní pro operace zásad konfigurace pro zadané zásady.</span><span class="sxs-lookup"><span data-stu-id="1d16d-122">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="1d16d-123">Nakonec zavolejte metodu [**patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) nebo [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) a aktualizujte zásady konfigurace.</span><span class="sxs-lookup"><span data-stu-id="1d16d-123">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

<span data-ttu-id="1d16d-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1d16d-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1d16d-125">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="1d16d-125">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1d16d-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1d16d-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1d16d-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="1d16d-127">Request syntax</span></span>

| <span data-ttu-id="1d16d-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="1d16d-128">Method</span></span>  | <span data-ttu-id="1d16d-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1d16d-129">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1d16d-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="1d16d-130">**PUT**</span></span> | <span data-ttu-id="1d16d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1d16d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1d16d-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1d16d-132">URI parameter</span></span>

<span data-ttu-id="1d16d-133">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="1d16d-133">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="1d16d-134">Název</span><span class="sxs-lookup"><span data-stu-id="1d16d-134">Name</span></span>        | <span data-ttu-id="1d16d-135">Typ</span><span class="sxs-lookup"><span data-stu-id="1d16d-135">Type</span></span>   | <span data-ttu-id="1d16d-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1d16d-136">Required</span></span> | <span data-ttu-id="1d16d-137">Popis</span><span class="sxs-lookup"><span data-stu-id="1d16d-137">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="1d16d-138">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="1d16d-138">customer-id</span></span> | <span data-ttu-id="1d16d-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="1d16d-139">string</span></span> | <span data-ttu-id="1d16d-140">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-140">Yes</span></span>      | <span data-ttu-id="1d16d-141">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1d16d-141">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="1d16d-142">ID zásady</span><span class="sxs-lookup"><span data-stu-id="1d16d-142">policy-id</span></span>   | <span data-ttu-id="1d16d-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="1d16d-143">string</span></span> | <span data-ttu-id="1d16d-144">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-144">Yes</span></span>      | <span data-ttu-id="1d16d-145">Řetězec ve formátu GUID, který identifikuje zásadu, která se má aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="1d16d-145">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1d16d-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1d16d-146">Request headers</span></span>

<span data-ttu-id="1d16d-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1d16d-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1d16d-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1d16d-148">Request body</span></span>

<span data-ttu-id="1d16d-149">Tělo žádosti musí obsahovat objekt, který poskytuje informace o zásadách.</span><span class="sxs-lookup"><span data-stu-id="1d16d-149">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="1d16d-150">Název</span><span class="sxs-lookup"><span data-stu-id="1d16d-150">Name</span></span>            | <span data-ttu-id="1d16d-151">Typ</span><span class="sxs-lookup"><span data-stu-id="1d16d-151">Type</span></span>             | <span data-ttu-id="1d16d-152">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1d16d-152">Required</span></span> | <span data-ttu-id="1d16d-153">Aktualizovat</span><span class="sxs-lookup"><span data-stu-id="1d16d-153">Updatable</span></span> | <span data-ttu-id="1d16d-154">Description</span><span class="sxs-lookup"><span data-stu-id="1d16d-154">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1d16d-155">id</span><span class="sxs-lookup"><span data-stu-id="1d16d-155">id</span></span>              | <span data-ttu-id="1d16d-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="1d16d-156">string</span></span>           | <span data-ttu-id="1d16d-157">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-157">Yes</span></span>      | <span data-ttu-id="1d16d-158">No</span><span class="sxs-lookup"><span data-stu-id="1d16d-158">No</span></span>        | <span data-ttu-id="1d16d-159">Řetězec ve formátu GUID, který identifikuje zásadu.</span><span class="sxs-lookup"><span data-stu-id="1d16d-159">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="1d16d-160">name</span><span class="sxs-lookup"><span data-stu-id="1d16d-160">name</span></span>            | <span data-ttu-id="1d16d-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="1d16d-161">string</span></span>           | <span data-ttu-id="1d16d-162">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-162">Yes</span></span>      | <span data-ttu-id="1d16d-163">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-163">Yes</span></span>       | <span data-ttu-id="1d16d-164">Popisný název zásady.</span><span class="sxs-lookup"><span data-stu-id="1d16d-164">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="1d16d-165">category</span><span class="sxs-lookup"><span data-stu-id="1d16d-165">category</span></span>        | <span data-ttu-id="1d16d-166">řetězec</span><span class="sxs-lookup"><span data-stu-id="1d16d-166">string</span></span>           | <span data-ttu-id="1d16d-167">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-167">Yes</span></span>      | <span data-ttu-id="1d16d-168">No</span><span class="sxs-lookup"><span data-stu-id="1d16d-168">No</span></span>        | <span data-ttu-id="1d16d-169">Kategorie zásad</span><span class="sxs-lookup"><span data-stu-id="1d16d-169">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="1d16d-170">description</span><span class="sxs-lookup"><span data-stu-id="1d16d-170">description</span></span>     | <span data-ttu-id="1d16d-171">řetězec</span><span class="sxs-lookup"><span data-stu-id="1d16d-171">string</span></span>           | <span data-ttu-id="1d16d-172">No</span><span class="sxs-lookup"><span data-stu-id="1d16d-172">No</span></span>       | <span data-ttu-id="1d16d-173">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-173">Yes</span></span>       | <span data-ttu-id="1d16d-174">Popis zásady.</span><span class="sxs-lookup"><span data-stu-id="1d16d-174">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="1d16d-175">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="1d16d-175">devicesAssigned</span></span> | <span data-ttu-id="1d16d-176">číslo</span><span class="sxs-lookup"><span data-stu-id="1d16d-176">number</span></span>           | <span data-ttu-id="1d16d-177">No</span><span class="sxs-lookup"><span data-stu-id="1d16d-177">No</span></span>       | <span data-ttu-id="1d16d-178">No</span><span class="sxs-lookup"><span data-stu-id="1d16d-178">No</span></span>        | <span data-ttu-id="1d16d-179">Počet zařízení.</span><span class="sxs-lookup"><span data-stu-id="1d16d-179">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="1d16d-180">policySettings</span><span class="sxs-lookup"><span data-stu-id="1d16d-180">policySettings</span></span>  | <span data-ttu-id="1d16d-181">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="1d16d-181">array of strings</span></span> | <span data-ttu-id="1d16d-182">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-182">Yes</span></span>      | <span data-ttu-id="1d16d-183">Yes</span><span class="sxs-lookup"><span data-stu-id="1d16d-183">Yes</span></span>       | <span data-ttu-id="1d16d-184">Nastavení zásad: "žádné", "odebrat \_ \_ předinstalované výrobci OEM", "OOBE \_ User \_ Not \_ Local \_ admin", "Přeskočit \_ expresní \_ nastavení", "Přeskočit \_ registraci OEM" \_ Přeskočit \_ smlouvu EULA ".</span><span class="sxs-lookup"><span data-stu-id="1d16d-184">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="1d16d-185">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1d16d-185">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="1d16d-186">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1d16d-186">REST response</span></span>

<span data-ttu-id="1d16d-187">V případě úspěchu obsahuje tělo odpovědi prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pro novou zásadu.</span><span class="sxs-lookup"><span data-stu-id="1d16d-187">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1d16d-188">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="1d16d-188">Response success and error codes</span></span>

<span data-ttu-id="1d16d-189">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1d16d-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1d16d-190">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="1d16d-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1d16d-191">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1d16d-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1d16d-192">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1d16d-192">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
