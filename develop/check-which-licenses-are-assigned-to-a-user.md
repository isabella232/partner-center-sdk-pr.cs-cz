---
title: Získání licencí přiřazených uživateli
description: Naučte se používat rozhraní API partnerského centra k získání seznamu licencí přiřazených uživateli v rámci účtu zákazníka.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b754ba4ecba7067f78c6868b387bac0190bfd230
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767116"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="075f9-103">Získání licencí přiřazených uživateli v rámci účtu zákazníka</span><span class="sxs-lookup"><span data-stu-id="075f9-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="075f9-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="075f9-104">**Applies to:**</span></span>

- <span data-ttu-id="075f9-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="075f9-105">Partner Center</span></span>

<span data-ttu-id="075f9-106">Jak získat seznam licencí přiřazených uživateli v rámci účtu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="075f9-106">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="075f9-107">Uvedené příklady vrátí licence přiřazené z Group1, výchozí skupinu licencí, která představuje licence spravované serverem Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="075f9-107">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="075f9-108">Pokud chcete získat licence přiřazené ze zadaných skupin licencí, přečtěte si téma [získání licencí přiřazených uživateli podle skupiny licencí](get-licenses-assigned-to-a-user-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="075f9-108">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="075f9-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="075f9-109">Prerequisites</span></span>

- <span data-ttu-id="075f9-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="075f9-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="075f9-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="075f9-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="075f9-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="075f9-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="075f9-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="075f9-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="075f9-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="075f9-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="075f9-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="075f9-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="075f9-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="075f9-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="075f9-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="075f9-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="075f9-118">Identifikátor uživatele</span><span class="sxs-lookup"><span data-stu-id="075f9-118">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="075f9-119">C\#</span><span class="sxs-lookup"><span data-stu-id="075f9-119">C\#</span></span>

<span data-ttu-id="075f9-120">Chcete-li zjistit, které licence jsou přiřazeny uživateli z výchozí skupiny licencí Group1, nejprve použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="075f9-120">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="075f9-121">Pak zavolejte metodu User [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID uživatele k identifikaci uživatele.</span><span class="sxs-lookup"><span data-stu-id="075f9-121">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="075f9-122">Pak z vlastnosti [**licence**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) Získejte rozhraní pro uživatelské operace s uživatelskými licencemi.</span><span class="sxs-lookup"><span data-stu-id="075f9-122">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="075f9-123">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) načtěte kolekci licencí přiřazených uživateli.</span><span class="sxs-lookup"><span data-stu-id="075f9-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="075f9-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="075f9-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="075f9-125">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: CustomerUserAssignedLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="075f9-125">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="075f9-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="075f9-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="075f9-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="075f9-127">Request syntax</span></span>

| <span data-ttu-id="075f9-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="075f9-128">Method</span></span>  | <span data-ttu-id="075f9-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="075f9-129">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="075f9-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="075f9-130">**GET**</span></span> | <span data-ttu-id="075f9-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="075f9-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="075f9-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="075f9-132">URI parameter</span></span>

<span data-ttu-id="075f9-133">K identifikaci zákazníka a uživatele použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="075f9-133">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="075f9-134">Název</span><span class="sxs-lookup"><span data-stu-id="075f9-134">Name</span></span>        | <span data-ttu-id="075f9-135">Typ</span><span class="sxs-lookup"><span data-stu-id="075f9-135">Type</span></span>   | <span data-ttu-id="075f9-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="075f9-136">Required</span></span> | <span data-ttu-id="075f9-137">Popis</span><span class="sxs-lookup"><span data-stu-id="075f9-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="075f9-138">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="075f9-138">customer-id</span></span> | <span data-ttu-id="075f9-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="075f9-139">string</span></span> | <span data-ttu-id="075f9-140">Yes</span><span class="sxs-lookup"><span data-stu-id="075f9-140">Yes</span></span>      | <span data-ttu-id="075f9-141">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="075f9-141">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="075f9-142">user-id</span><span class="sxs-lookup"><span data-stu-id="075f9-142">user-id</span></span>     | <span data-ttu-id="075f9-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="075f9-143">string</span></span> | <span data-ttu-id="075f9-144">Yes</span><span class="sxs-lookup"><span data-stu-id="075f9-144">Yes</span></span>      | <span data-ttu-id="075f9-145">Řetězec ve formátu GUID, který identifikuje uživatele.</span><span class="sxs-lookup"><span data-stu-id="075f9-145">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="075f9-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="075f9-146">Request headers</span></span>

<span data-ttu-id="075f9-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="075f9-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="075f9-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="075f9-148">Request body</span></span>

<span data-ttu-id="075f9-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="075f9-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="075f9-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="075f9-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="075f9-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="075f9-151">REST response</span></span>

<span data-ttu-id="075f9-152">V případě úspěchu obsahuje tělo odpovědi kolekci [licenčních](license-resources.md#license) prostředků.</span><span class="sxs-lookup"><span data-stu-id="075f9-152">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="075f9-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="075f9-153">Response success and error codes</span></span>

<span data-ttu-id="075f9-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="075f9-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="075f9-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="075f9-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="075f9-156">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="075f9-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="075f9-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="075f9-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3883
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CV: WYkHYMfWTUajFosK.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 00:29:24 GMT

{
    "totalCount": 1,
    "items": [{
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
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