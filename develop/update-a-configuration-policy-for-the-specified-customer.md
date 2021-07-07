---
title: Aktualizace zásad konfigurace pro konkrétního zákazníka
description: Postup aktualizace zadaných zásad konfigurace pro zadaného zákazníka
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5e008f41a44f2b7cf3ddfd705505175c69bbad38
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530224"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="8cb24-103">Aktualizace zásad konfigurace pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="8cb24-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="8cb24-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)</span><span class="sxs-lookup"><span data-stu-id="8cb24-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8cb24-105">Postup aktualizace zadaných zásad konfigurace pro zadaného zákazníka</span><span class="sxs-lookup"><span data-stu-id="8cb24-105">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cb24-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8cb24-106">Prerequisites</span></span>

- <span data-ttu-id="8cb24-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8cb24-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8cb24-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="8cb24-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8cb24-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8cb24-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8cb24-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8cb24-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8cb24-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="8cb24-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8cb24-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="8cb24-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8cb24-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8cb24-113">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8cb24-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8cb24-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8cb24-115">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="8cb24-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="8cb24-116">C\#</span><span class="sxs-lookup"><span data-stu-id="8cb24-116">C\#</span></span>

<span data-ttu-id="8cb24-117">Pokud chcete aktualizovat existující zásady konfigurace pro zadaného zákazníka, vytvořte instanci nového objektu [**ConfigurationPolicy,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="8cb24-117">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="8cb24-118">Hodnoty v tomto novém objektu nahradí odpovídající hodnoty v existujícím objektu.</span><span class="sxs-lookup"><span data-stu-id="8cb24-118">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="8cb24-119">Potom zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a načtěte rozhraní pro operace v zadaném zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="8cb24-119">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="8cb24-120">Dále zavolejte [**metodu ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady a načtěte rozhraní pro operace zásad konfigurace pro zadané zásady.</span><span class="sxs-lookup"><span data-stu-id="8cb24-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="8cb24-121">Nakonec zavolejte [**metodu Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) nebo [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) a aktualizujte zásady konfigurace.</span><span class="sxs-lookup"><span data-stu-id="8cb24-121">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

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

<span data-ttu-id="8cb24-122">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8cb24-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8cb24-123">**Project**: SDK pro Partnerské centrum Samples **– třída:** UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="8cb24-123">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8cb24-124">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="8cb24-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8cb24-125">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="8cb24-125">Request syntax</span></span>

| <span data-ttu-id="8cb24-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="8cb24-126">Method</span></span>  | <span data-ttu-id="8cb24-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8cb24-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8cb24-128">**PUT**</span><span class="sxs-lookup"><span data-stu-id="8cb24-128">**PUT**</span></span> | <span data-ttu-id="8cb24-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/policies/{ID_zásad} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8cb24-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8cb24-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8cb24-130">URI parameter</span></span>

<span data-ttu-id="8cb24-131">Při vytváření požadavku použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="8cb24-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="8cb24-132">Název</span><span class="sxs-lookup"><span data-stu-id="8cb24-132">Name</span></span>        | <span data-ttu-id="8cb24-133">Typ</span><span class="sxs-lookup"><span data-stu-id="8cb24-133">Type</span></span>   | <span data-ttu-id="8cb24-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8cb24-134">Required</span></span> | <span data-ttu-id="8cb24-135">Popis</span><span class="sxs-lookup"><span data-stu-id="8cb24-135">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="8cb24-136">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="8cb24-136">customer-id</span></span> | <span data-ttu-id="8cb24-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="8cb24-137">string</span></span> | <span data-ttu-id="8cb24-138">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-138">Yes</span></span>      | <span data-ttu-id="8cb24-139">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8cb24-139">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="8cb24-140">ID zásady</span><span class="sxs-lookup"><span data-stu-id="8cb24-140">policy-id</span></span>   | <span data-ttu-id="8cb24-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="8cb24-141">string</span></span> | <span data-ttu-id="8cb24-142">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-142">Yes</span></span>      | <span data-ttu-id="8cb24-143">Řetězec formátovaný identifikátorem GUID, který identifikuje zásadu, která se má aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="8cb24-143">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8cb24-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8cb24-144">Request headers</span></span>

<span data-ttu-id="8cb24-145">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8cb24-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8cb24-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8cb24-146">Request body</span></span>

<span data-ttu-id="8cb24-147">Text požadavku musí obsahovat objekt, který poskytuje informace o zásadách.</span><span class="sxs-lookup"><span data-stu-id="8cb24-147">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="8cb24-148">Název</span><span class="sxs-lookup"><span data-stu-id="8cb24-148">Name</span></span>            | <span data-ttu-id="8cb24-149">Typ</span><span class="sxs-lookup"><span data-stu-id="8cb24-149">Type</span></span>             | <span data-ttu-id="8cb24-150">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8cb24-150">Required</span></span> | <span data-ttu-id="8cb24-151">Aktualizovatelné</span><span class="sxs-lookup"><span data-stu-id="8cb24-151">Updatable</span></span> | <span data-ttu-id="8cb24-152">Description</span><span class="sxs-lookup"><span data-stu-id="8cb24-152">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8cb24-153">id</span><span class="sxs-lookup"><span data-stu-id="8cb24-153">id</span></span>              | <span data-ttu-id="8cb24-154">řetězec</span><span class="sxs-lookup"><span data-stu-id="8cb24-154">string</span></span>           | <span data-ttu-id="8cb24-155">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-155">Yes</span></span>      | <span data-ttu-id="8cb24-156">No</span><span class="sxs-lookup"><span data-stu-id="8cb24-156">No</span></span>        | <span data-ttu-id="8cb24-157">Řetězec ve formátu GUID, který identifikuje zásadu.</span><span class="sxs-lookup"><span data-stu-id="8cb24-157">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="8cb24-158">name</span><span class="sxs-lookup"><span data-stu-id="8cb24-158">name</span></span>            | <span data-ttu-id="8cb24-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="8cb24-159">string</span></span>           | <span data-ttu-id="8cb24-160">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-160">Yes</span></span>      | <span data-ttu-id="8cb24-161">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-161">Yes</span></span>       | <span data-ttu-id="8cb24-162">Popisný název zásady.</span><span class="sxs-lookup"><span data-stu-id="8cb24-162">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="8cb24-163">category</span><span class="sxs-lookup"><span data-stu-id="8cb24-163">category</span></span>        | <span data-ttu-id="8cb24-164">řetězec</span><span class="sxs-lookup"><span data-stu-id="8cb24-164">string</span></span>           | <span data-ttu-id="8cb24-165">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-165">Yes</span></span>      | <span data-ttu-id="8cb24-166">No</span><span class="sxs-lookup"><span data-stu-id="8cb24-166">No</span></span>        | <span data-ttu-id="8cb24-167">Kategorie zásad.</span><span class="sxs-lookup"><span data-stu-id="8cb24-167">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="8cb24-168">description</span><span class="sxs-lookup"><span data-stu-id="8cb24-168">description</span></span>     | <span data-ttu-id="8cb24-169">řetězec</span><span class="sxs-lookup"><span data-stu-id="8cb24-169">string</span></span>           | <span data-ttu-id="8cb24-170">No</span><span class="sxs-lookup"><span data-stu-id="8cb24-170">No</span></span>       | <span data-ttu-id="8cb24-171">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-171">Yes</span></span>       | <span data-ttu-id="8cb24-172">Popis zásady.</span><span class="sxs-lookup"><span data-stu-id="8cb24-172">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="8cb24-173">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="8cb24-173">devicesAssigned</span></span> | <span data-ttu-id="8cb24-174">číslo</span><span class="sxs-lookup"><span data-stu-id="8cb24-174">number</span></span>           | <span data-ttu-id="8cb24-175">No</span><span class="sxs-lookup"><span data-stu-id="8cb24-175">No</span></span>       | <span data-ttu-id="8cb24-176">No</span><span class="sxs-lookup"><span data-stu-id="8cb24-176">No</span></span>        | <span data-ttu-id="8cb24-177">Počet zařízení</span><span class="sxs-lookup"><span data-stu-id="8cb24-177">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="8cb24-178">nastavení zásad</span><span class="sxs-lookup"><span data-stu-id="8cb24-178">policySettings</span></span>  | <span data-ttu-id="8cb24-179">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="8cb24-179">array of strings</span></span> | <span data-ttu-id="8cb24-180">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-180">Yes</span></span>      | <span data-ttu-id="8cb24-181">Yes</span><span class="sxs-lookup"><span data-stu-id="8cb24-181">Yes</span></span>       | <span data-ttu-id="8cb24-182">Nastavení zásad: none,"remove \_ oem \_ preinstalls", "oobe \_ user not local \_ \_ \_ admin", "skip \_ express \_ settings", "skip \_ oem \_ registration,"skip \_ eula".</span><span class="sxs-lookup"><span data-stu-id="8cb24-182">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="8cb24-183">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8cb24-183">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8cb24-184">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8cb24-184">REST response</span></span>

<span data-ttu-id="8cb24-185">V případě úspěchu bude text odpovědi obsahovat prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pro novou zásadu.</span><span class="sxs-lookup"><span data-stu-id="8cb24-185">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8cb24-186">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="8cb24-186">Response success and error codes</span></span>

<span data-ttu-id="8cb24-187">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8cb24-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8cb24-188">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="8cb24-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8cb24-189">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8cb24-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8cb24-190">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8cb24-190">Response example</span></span>

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
