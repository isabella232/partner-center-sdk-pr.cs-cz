---
title: Získání licencí přiřazených uživateli
description: Zjistěte, jak pomocí Partnerské centrum API získat seznam licencí přiřazených uživateli v rámci zákaznického účtu.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a51fc4493e2476107206b03be66004d030e2aa47
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974059"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="7d444-103">Získání licencí přiřazených uživateli v rámci zákaznického účtu</span><span class="sxs-lookup"><span data-stu-id="7d444-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="7d444-104">Jak získat seznam licencí přiřazených uživateli v rámci zákaznického účtu</span><span class="sxs-lookup"><span data-stu-id="7d444-104">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="7d444-105">Uvedené příklady vrátí licence přiřazené ze skupiny group1, výchozí skupiny licencí, která představuje licence spravované Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d444-105">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="7d444-106">Pokud chcete získat licence přiřazené ze zadaných skupin licencí, podívejte se na stránku [Získání licencí přiřazených uživateli podle skupiny licencí.](get-licenses-assigned-to-a-user-by-license-group.md)</span><span class="sxs-lookup"><span data-stu-id="7d444-106">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d444-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7d444-107">Prerequisites</span></span>

- <span data-ttu-id="7d444-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7d444-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7d444-109">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="7d444-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7d444-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7d444-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7d444-111">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="7d444-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7d444-112">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="7d444-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7d444-113">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="7d444-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7d444-114">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7d444-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7d444-115">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7d444-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7d444-116">Identifikátor uživatele.</span><span class="sxs-lookup"><span data-stu-id="7d444-116">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="7d444-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7d444-117">C\#</span></span>

<span data-ttu-id="7d444-118">Pokud chcete zjistit, které licence jsou přiřazeny uživateli z výchozí skupiny licencí group1, nejprve pomocí metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7d444-118">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="7d444-119">Potom zavolejte [**metodu Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID uživatele a identifikujte uživatele.</span><span class="sxs-lookup"><span data-stu-id="7d444-119">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="7d444-120">Dále z vlastnosti [**Licence**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) získejte rozhraní operací s uživatelskými licencemi zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7d444-120">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="7d444-121">Nakonec zavolejte [**metodu Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) a načtěte kolekci licencí přiřazených uživateli.</span><span class="sxs-lookup"><span data-stu-id="7d444-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="7d444-122">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7d444-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7d444-123">**Project:** SDK pro Partnerské centrum Samples **Class:** CustomerUserAssignedLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="7d444-123">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7d444-124">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="7d444-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7d444-125">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="7d444-125">Request syntax</span></span>

| <span data-ttu-id="7d444-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="7d444-126">Method</span></span>  | <span data-ttu-id="7d444-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="7d444-127">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7d444-128">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="7d444-128">**GET**</span></span> | <span data-ttu-id="7d444-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/users/{ID_uživatele}/licence HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7d444-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7d444-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="7d444-130">URI parameter</span></span>

<span data-ttu-id="7d444-131">K identifikaci zákazníka a uživatele použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="7d444-131">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="7d444-132">Název</span><span class="sxs-lookup"><span data-stu-id="7d444-132">Name</span></span>        | <span data-ttu-id="7d444-133">Typ</span><span class="sxs-lookup"><span data-stu-id="7d444-133">Type</span></span>   | <span data-ttu-id="7d444-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="7d444-134">Required</span></span> | <span data-ttu-id="7d444-135">Popis</span><span class="sxs-lookup"><span data-stu-id="7d444-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7d444-136">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="7d444-136">customer-id</span></span> | <span data-ttu-id="7d444-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="7d444-137">string</span></span> | <span data-ttu-id="7d444-138">Yes</span><span class="sxs-lookup"><span data-stu-id="7d444-138">Yes</span></span>      | <span data-ttu-id="7d444-139">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7d444-139">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="7d444-140">user-id</span><span class="sxs-lookup"><span data-stu-id="7d444-140">user-id</span></span>     | <span data-ttu-id="7d444-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="7d444-141">string</span></span> | <span data-ttu-id="7d444-142">Yes</span><span class="sxs-lookup"><span data-stu-id="7d444-142">Yes</span></span>      | <span data-ttu-id="7d444-143">Řetězec formátovaný identifikátorem GUID, který identifikuje uživatele.</span><span class="sxs-lookup"><span data-stu-id="7d444-143">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="7d444-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="7d444-144">Request headers</span></span>

<span data-ttu-id="7d444-145">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7d444-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7d444-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="7d444-146">Request body</span></span>

<span data-ttu-id="7d444-147">Žádné</span><span class="sxs-lookup"><span data-stu-id="7d444-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7d444-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="7d444-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7d444-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="7d444-149">REST response</span></span>

<span data-ttu-id="7d444-150">V případě úspěchu bude text odpovědi obsahovat kolekci prostředků [licence.](license-resources.md#license)</span><span class="sxs-lookup"><span data-stu-id="7d444-150">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7d444-151">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="7d444-151">Response success and error codes</span></span>

<span data-ttu-id="7d444-152">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="7d444-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7d444-153">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="7d444-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7d444-154">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7d444-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7d444-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="7d444-155">Response example</span></span>

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