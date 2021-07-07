---
title: Získání licencí přiřazených uživateli podle skupiny licencí
description: Jak získat seznam licencí přiřazených uživateli pro zadané skupiny licencí.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 54acf6f315e3062d03903a98d0c6c1946065f95e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445999"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="15a70-103">Získání licencí přiřazených uživateli podle skupiny licencí</span><span class="sxs-lookup"><span data-stu-id="15a70-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="15a70-104">Jak získat seznam licencí přiřazených uživateli pro zadané skupiny licencí.</span><span class="sxs-lookup"><span data-stu-id="15a70-104">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15a70-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="15a70-105">Prerequisites</span></span>

- <span data-ttu-id="15a70-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="15a70-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="15a70-107">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="15a70-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="15a70-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="15a70-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="15a70-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="15a70-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="15a70-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="15a70-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="15a70-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="15a70-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="15a70-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="15a70-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="15a70-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="15a70-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="15a70-114">Identifikátor uživatele</span><span class="sxs-lookup"><span data-stu-id="15a70-114">A user identifier.</span></span>

- <span data-ttu-id="15a70-115">Seznam jednoho nebo více identifikátorů skupin licencí.</span><span class="sxs-lookup"><span data-stu-id="15a70-115">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="15a70-116">C\#</span><span class="sxs-lookup"><span data-stu-id="15a70-116">C\#</span></span>

<span data-ttu-id="15a70-117">Chcete-li zjistit, které licence jsou přiřazeny uživateli ze zadaných skupin licencí, Začněte vytvořením instance [list/dotnet/API/System. Collections. Generic. list -1) typu [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)a poté přidejte do seznamu skupiny licencí.</span><span class="sxs-lookup"><span data-stu-id="15a70-117">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="15a70-118">Potom k identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="15a70-118">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="15a70-119">Dále zavolejte metodu User [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID uživatele k identifikaci uživatele.</span><span class="sxs-lookup"><span data-stu-id="15a70-119">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="15a70-120">Pak z vlastnosti [**licence**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) Získejte rozhraní pro uživatelské operace s uživatelskými licencemi.</span><span class="sxs-lookup"><span data-stu-id="15a70-120">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="15a70-121">Nakonec předejte seznam skupin licencí do metody [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) , aby se načetla kolekce licencí přiřazených uživateli.</span><span class="sxs-lookup"><span data-stu-id="15a70-121">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="15a70-122">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="15a70-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="15a70-123">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="15a70-123">Request syntax</span></span>

| <span data-ttu-id="15a70-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="15a70-124">Method</span></span>  | <span data-ttu-id="15a70-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="15a70-125">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="15a70-126">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="15a70-126">**GET**</span></span> | <span data-ttu-id="15a70-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="15a70-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="15a70-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="15a70-128">**GET**</span></span> | <span data-ttu-id="15a70-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = skupina2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="15a70-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="15a70-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="15a70-130">**GET**</span></span> | <span data-ttu-id="15a70-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Group1&LicenseGroupIds = skupina2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="15a70-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="15a70-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="15a70-132">URI parameter</span></span>

<span data-ttu-id="15a70-133">K identifikaci zákazníka, uživatele a skupin licencí použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="15a70-133">Use the following path and query parameters to identify the customer, user, and license groups.</span></span>

| <span data-ttu-id="15a70-134">Název</span><span class="sxs-lookup"><span data-stu-id="15a70-134">Name</span></span>            | <span data-ttu-id="15a70-135">Typ</span><span class="sxs-lookup"><span data-stu-id="15a70-135">Type</span></span>   | <span data-ttu-id="15a70-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="15a70-136">Required</span></span> | <span data-ttu-id="15a70-137">Popis</span><span class="sxs-lookup"><span data-stu-id="15a70-137">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="15a70-138">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="15a70-138">customer-id</span></span>     | <span data-ttu-id="15a70-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="15a70-139">string</span></span> | <span data-ttu-id="15a70-140">Yes</span><span class="sxs-lookup"><span data-stu-id="15a70-140">Yes</span></span>      | <span data-ttu-id="15a70-141">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="15a70-141">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="15a70-142">user-id</span><span class="sxs-lookup"><span data-stu-id="15a70-142">user-id</span></span>         | <span data-ttu-id="15a70-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="15a70-143">string</span></span> | <span data-ttu-id="15a70-144">Yes</span><span class="sxs-lookup"><span data-stu-id="15a70-144">Yes</span></span>      | <span data-ttu-id="15a70-145">Řetězec ve formátu GUID, který identifikuje uživatele.</span><span class="sxs-lookup"><span data-stu-id="15a70-145">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="15a70-146">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="15a70-146">licenseGroupIds</span></span> | <span data-ttu-id="15a70-147">řetězec</span><span class="sxs-lookup"><span data-stu-id="15a70-147">string</span></span> | <span data-ttu-id="15a70-148">No</span><span class="sxs-lookup"><span data-stu-id="15a70-148">No</span></span>       | <span data-ttu-id="15a70-149">Hodnota výčtu, která označuje skupinu licencí přiřazených licencí.</span><span class="sxs-lookup"><span data-stu-id="15a70-149">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="15a70-150">Platné hodnoty: group1, Skupina2 Group1 – Tato skupina obsahuje všechny produkty, jejichž licence se dají spravovat v Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="15a70-150">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="15a70-151">skupina2 – tato skupina má pouze licence na produkt Minecraft.</span><span class="sxs-lookup"><span data-stu-id="15a70-151">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="15a70-152">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="15a70-152">Request headers</span></span>

<span data-ttu-id="15a70-153">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="15a70-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="15a70-154">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="15a70-154">Request body</span></span>

<span data-ttu-id="15a70-155">Žádné</span><span class="sxs-lookup"><span data-stu-id="15a70-155">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="15a70-156">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="15a70-156">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="15a70-157">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="15a70-157">REST response</span></span>

<span data-ttu-id="15a70-158">V případě úspěchu obsahuje tělo odpovědi kolekci [licenčních](license-resources.md#license) prostředků.</span><span class="sxs-lookup"><span data-stu-id="15a70-158">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="15a70-159">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="15a70-159">Response success and error codes</span></span>

<span data-ttu-id="15a70-160">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="15a70-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="15a70-161">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="15a70-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="15a70-162">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="15a70-162">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="15a70-163">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="15a70-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="15a70-164">Příklad odpovědi (nenašly se žádné vyhovující licence)</span><span class="sxs-lookup"><span data-stu-id="15a70-164">Response example (no matching licenses found)</span></span>

<span data-ttu-id="15a70-165">Pokud pro zadané skupiny licencí nenajdete žádné vyhovující licence, odpověď obsahuje prázdnou kolekci s elementem totalCount, jehož hodnota je 0.</span><span class="sxs-lookup"><span data-stu-id="15a70-165">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
