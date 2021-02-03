---
title: Aktualizace zásad konfigurace pro konkrétního zákazníka
description: Jak aktualizovat zadané zásady konfigurace pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 42c57a92020723415b4621e9f9d7c5c3278bfb77
ms.sourcegitcommit: 970031473b2e8cd3d08c6c097949c057a51df3ef
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505335"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="62171-103">Aktualizace zásad konfigurace pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="62171-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="62171-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="62171-104">**Applies To**</span></span>

- <span data-ttu-id="62171-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="62171-105">Partner Center</span></span>
- <span data-ttu-id="62171-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="62171-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="62171-107">Jak aktualizovat zadané zásady konfigurace pro zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="62171-107">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62171-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="62171-108">Prerequisites</span></span>

- <span data-ttu-id="62171-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="62171-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="62171-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="62171-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="62171-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="62171-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="62171-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="62171-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="62171-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="62171-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="62171-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="62171-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="62171-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="62171-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="62171-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="62171-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="62171-117">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="62171-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="62171-118">C\#</span><span class="sxs-lookup"><span data-stu-id="62171-118">C\#</span></span>

<span data-ttu-id="62171-119">Chcete-li aktualizovat existující zásady konfigurace pro zadaného zákazníka, vytvořte instanci nového objektu [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) , jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="62171-119">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="62171-120">Hodnoty v tomto novém objektu nahradí odpovídající hodnoty v existujícím objektu.</span><span class="sxs-lookup"><span data-stu-id="62171-120">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="62171-121">Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro operace zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="62171-121">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="62171-122">V dalším kroku zavolejte metodu [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady, aby se načetlo rozhraní pro operace zásad konfigurace pro zadané zásady.</span><span class="sxs-lookup"><span data-stu-id="62171-122">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="62171-123">Nakonec zavolejte metodu [**patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) nebo [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) a aktualizujte zásady konfigurace.</span><span class="sxs-lookup"><span data-stu-id="62171-123">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

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

<span data-ttu-id="62171-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="62171-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="62171-125">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="62171-125">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="62171-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="62171-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="62171-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="62171-127">Request syntax</span></span>

| <span data-ttu-id="62171-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="62171-128">Method</span></span>  | <span data-ttu-id="62171-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="62171-129">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="62171-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="62171-130">**PUT**</span></span> | <span data-ttu-id="62171-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="62171-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="62171-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="62171-132">URI parameter</span></span>

<span data-ttu-id="62171-133">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="62171-133">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="62171-134">Název</span><span class="sxs-lookup"><span data-stu-id="62171-134">Name</span></span>        | <span data-ttu-id="62171-135">Typ</span><span class="sxs-lookup"><span data-stu-id="62171-135">Type</span></span>   | <span data-ttu-id="62171-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="62171-136">Required</span></span> | <span data-ttu-id="62171-137">Popis</span><span class="sxs-lookup"><span data-stu-id="62171-137">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="62171-138">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="62171-138">customer-id</span></span> | <span data-ttu-id="62171-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="62171-139">string</span></span> | <span data-ttu-id="62171-140">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-140">Yes</span></span>      | <span data-ttu-id="62171-141">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="62171-141">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="62171-142">ID zásady</span><span class="sxs-lookup"><span data-stu-id="62171-142">policy-id</span></span>   | <span data-ttu-id="62171-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="62171-143">string</span></span> | <span data-ttu-id="62171-144">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-144">Yes</span></span>      | <span data-ttu-id="62171-145">Řetězec ve formátu GUID, který identifikuje zásadu, která se má aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="62171-145">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="62171-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="62171-146">Request headers</span></span>

<span data-ttu-id="62171-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="62171-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="62171-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="62171-148">Request body</span></span>

<span data-ttu-id="62171-149">Tělo žádosti musí obsahovat objekt, který poskytuje informace o zásadách.</span><span class="sxs-lookup"><span data-stu-id="62171-149">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="62171-150">Název</span><span class="sxs-lookup"><span data-stu-id="62171-150">Name</span></span>            | <span data-ttu-id="62171-151">Typ</span><span class="sxs-lookup"><span data-stu-id="62171-151">Type</span></span>             | <span data-ttu-id="62171-152">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="62171-152">Required</span></span> | <span data-ttu-id="62171-153">Aktualizovat</span><span class="sxs-lookup"><span data-stu-id="62171-153">Updatable</span></span> | <span data-ttu-id="62171-154">Description</span><span class="sxs-lookup"><span data-stu-id="62171-154">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="62171-155">id</span><span class="sxs-lookup"><span data-stu-id="62171-155">id</span></span>              | <span data-ttu-id="62171-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="62171-156">string</span></span>           | <span data-ttu-id="62171-157">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-157">Yes</span></span>      | <span data-ttu-id="62171-158">No</span><span class="sxs-lookup"><span data-stu-id="62171-158">No</span></span>        | <span data-ttu-id="62171-159">Řetězec ve formátu GUID, který identifikuje zásadu.</span><span class="sxs-lookup"><span data-stu-id="62171-159">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="62171-160">name</span><span class="sxs-lookup"><span data-stu-id="62171-160">name</span></span>            | <span data-ttu-id="62171-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="62171-161">string</span></span>           | <span data-ttu-id="62171-162">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-162">Yes</span></span>      | <span data-ttu-id="62171-163">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-163">Yes</span></span>       | <span data-ttu-id="62171-164">Popisný název zásady.</span><span class="sxs-lookup"><span data-stu-id="62171-164">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="62171-165">category</span><span class="sxs-lookup"><span data-stu-id="62171-165">category</span></span>        | <span data-ttu-id="62171-166">řetězec</span><span class="sxs-lookup"><span data-stu-id="62171-166">string</span></span>           | <span data-ttu-id="62171-167">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-167">Yes</span></span>      | <span data-ttu-id="62171-168">No</span><span class="sxs-lookup"><span data-stu-id="62171-168">No</span></span>        | <span data-ttu-id="62171-169">Kategorie zásad</span><span class="sxs-lookup"><span data-stu-id="62171-169">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="62171-170">description</span><span class="sxs-lookup"><span data-stu-id="62171-170">description</span></span>     | <span data-ttu-id="62171-171">řetězec</span><span class="sxs-lookup"><span data-stu-id="62171-171">string</span></span>           | <span data-ttu-id="62171-172">No</span><span class="sxs-lookup"><span data-stu-id="62171-172">No</span></span>       | <span data-ttu-id="62171-173">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-173">Yes</span></span>       | <span data-ttu-id="62171-174">Popis zásady.</span><span class="sxs-lookup"><span data-stu-id="62171-174">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="62171-175">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="62171-175">devicesAssigned</span></span> | <span data-ttu-id="62171-176">číslo</span><span class="sxs-lookup"><span data-stu-id="62171-176">number</span></span>           | <span data-ttu-id="62171-177">No</span><span class="sxs-lookup"><span data-stu-id="62171-177">No</span></span>       | <span data-ttu-id="62171-178">No</span><span class="sxs-lookup"><span data-stu-id="62171-178">No</span></span>        | <span data-ttu-id="62171-179">Počet zařízení.</span><span class="sxs-lookup"><span data-stu-id="62171-179">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="62171-180">policySettings</span><span class="sxs-lookup"><span data-stu-id="62171-180">policySettings</span></span>  | <span data-ttu-id="62171-181">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="62171-181">array of strings</span></span> | <span data-ttu-id="62171-182">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-182">Yes</span></span>      | <span data-ttu-id="62171-183">Yes</span><span class="sxs-lookup"><span data-stu-id="62171-183">Yes</span></span>       | <span data-ttu-id="62171-184">Nastavení zásad: "žádné", "odebrat \_ \_ předinstalované výrobci OEM", "OOBE \_ User \_ Not \_ Local \_ admin", "Přeskočit \_ expresní \_ nastavení", "Přeskočit \_ registraci OEM" \_ Přeskočit \_ smlouvu EULA ".</span><span class="sxs-lookup"><span data-stu-id="62171-184">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="62171-185">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="62171-185">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="62171-186">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="62171-186">REST response</span></span>

<span data-ttu-id="62171-187">V případě úspěchu obsahuje tělo odpovědi prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pro novou zásadu.</span><span class="sxs-lookup"><span data-stu-id="62171-187">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="62171-188">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="62171-188">Response success and error codes</span></span>

<span data-ttu-id="62171-189">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="62171-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="62171-190">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="62171-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="62171-191">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="62171-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="62171-192">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="62171-192">Response example</span></span>

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
