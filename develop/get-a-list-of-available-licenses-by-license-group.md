---
title: Získání seznamu dostupných licencí podle skupiny licencí
description: Jak získat seznam licencí pro zadané skupiny licencí, kteří jsou k dispozici pro uživatele zadaného zákazníka.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 5092bc73107231d602c1465c8d157cdf5499c913
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766936"
---
# <a name="get-a-list-of-available-licenses-by-license-group"></a><span data-ttu-id="86fa1-103">Získání seznamu dostupných licencí podle skupiny licencí</span><span class="sxs-lookup"><span data-stu-id="86fa1-103">Get a list of available licenses by license group</span></span>

<span data-ttu-id="86fa1-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="86fa1-104">**Applies To**</span></span>

- <span data-ttu-id="86fa1-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="86fa1-105">Partner Center</span></span>

<span data-ttu-id="86fa1-106">Jak získat seznam licencí pro zadané skupiny licencí, kteří jsou k dispozici pro uživatele zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="86fa1-106">How to get a list of licenses for the specified license groups available to users of the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86fa1-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="86fa1-107">Prerequisites</span></span>

- <span data-ttu-id="86fa1-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="86fa1-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="86fa1-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="86fa1-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="86fa1-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="86fa1-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="86fa1-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="86fa1-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="86fa1-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="86fa1-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="86fa1-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="86fa1-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="86fa1-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="86fa1-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="86fa1-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="86fa1-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="86fa1-116">Seznam jednoho nebo více identifikátorů skupin licencí.</span><span class="sxs-lookup"><span data-stu-id="86fa1-116">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="86fa1-117">C\#</span><span class="sxs-lookup"><span data-stu-id="86fa1-117">C\#</span></span>

<span data-ttu-id="86fa1-118">Pokud chcete získat seznam dostupných licencí pro zadané skupiny licencí, začněte tím, že vytvoříte instanci [seznamu](/dotnet/api/system.collections.generic.list-1) typu [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)a pak do seznamu přidáte skupiny licencí.</span><span class="sxs-lookup"><span data-stu-id="86fa1-118">To get a list of available licenses for the specified license groups, start by instantiating a [List](/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="86fa1-119">V dalším kroku použijte k identifikaci zákazníka metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="86fa1-119">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="86fa1-120">Potom Získejte hodnotu vlastnosti [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) , která načte rozhraní pro operace shromažďování skladových položek s předplacenou odběrateli.</span><span class="sxs-lookup"><span data-stu-id="86fa1-120">Then, get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span> <span data-ttu-id="86fa1-121">Nakonec předejte seznam skupin licencí do metody [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) a načtěte seznam předplacených skladových položek s podrobnostmi o dostupných licenčních jednotkách.</span><span class="sxs-lookup"><span data-stu-id="86fa1-121">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of subscribed SKUs with details on available license units.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get subscribed SKUs available for group1, the license group for Azure Active Directory (AAD).
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1};
var customerUserAadSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get subscribed SKUs available for group2, the license group for Minecraft product licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group2};
var customerUserSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get both AAD and Minecraft subscribed SKUs.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1, LicenseGroupId.Group2};
var customerUserBothAadAndSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="86fa1-122">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="86fa1-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="86fa1-123">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="86fa1-123">Request syntax</span></span>

| <span data-ttu-id="86fa1-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="86fa1-124">Method</span></span>  | <span data-ttu-id="86fa1-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="86fa1-125">Request URI</span></span>                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="86fa1-126">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="86fa1-126">**GET**</span></span> | <span data-ttu-id="86fa1-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscribedskus? LicenseGroupIds = Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="86fa1-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="86fa1-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="86fa1-128">**GET**</span></span> | <span data-ttu-id="86fa1-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscribedskus? LicenseGroupIds = skupina2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="86fa1-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="86fa1-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="86fa1-130">**GET**</span></span> | <span data-ttu-id="86fa1-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscribedskus? LicenseGroupIds = Group1&LicenseGroupIds = skupina2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="86fa1-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="86fa1-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="86fa1-132">URI parameter</span></span>

<span data-ttu-id="86fa1-133">K identifikaci zákazníka a skupin licencí použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="86fa1-133">Use the following path and query parameters to identify the customer and the license groups.</span></span>

| <span data-ttu-id="86fa1-134">Název</span><span class="sxs-lookup"><span data-stu-id="86fa1-134">Name</span></span>            | <span data-ttu-id="86fa1-135">Typ</span><span class="sxs-lookup"><span data-stu-id="86fa1-135">Type</span></span>   | <span data-ttu-id="86fa1-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="86fa1-136">Required</span></span> | <span data-ttu-id="86fa1-137">Popis</span><span class="sxs-lookup"><span data-stu-id="86fa1-137">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="86fa1-138">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="86fa1-138">customer-id</span></span>     | <span data-ttu-id="86fa1-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="86fa1-139">string</span></span> | <span data-ttu-id="86fa1-140">Yes</span><span class="sxs-lookup"><span data-stu-id="86fa1-140">Yes</span></span>      | <span data-ttu-id="86fa1-141">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="86fa1-141">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="86fa1-142">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="86fa1-142">licenseGroupIds</span></span> | <span data-ttu-id="86fa1-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="86fa1-143">string</span></span> | <span data-ttu-id="86fa1-144">No</span><span class="sxs-lookup"><span data-stu-id="86fa1-144">No</span></span>       | <span data-ttu-id="86fa1-145">Hodnota výčtu, která označuje skupinu licencí přiřazených licencí.</span><span class="sxs-lookup"><span data-stu-id="86fa1-145">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="86fa1-146">Platné hodnoty: group1, Skupina2 Group1 – Tato skupina obsahuje všechny produkty, jejichž licence se dají spravovat v Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="86fa1-146">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="86fa1-147">Skupina2 – Tato skupina má pouze licence na produkty Minecraftu.</span><span class="sxs-lookup"><span data-stu-id="86fa1-147">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="86fa1-148">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="86fa1-148">Request headers</span></span>

<span data-ttu-id="86fa1-149">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="86fa1-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="86fa1-150">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="86fa1-150">Request body</span></span>

<span data-ttu-id="86fa1-151">Žádné</span><span class="sxs-lookup"><span data-stu-id="86fa1-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="86fa1-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="86fa1-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="86fa1-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="86fa1-153">REST response</span></span>

<span data-ttu-id="86fa1-154">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [SubscribedSku](license-resources.md#subscribedsku) .</span><span class="sxs-lookup"><span data-stu-id="86fa1-154">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="86fa1-155">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="86fa1-155">Response success and error codes</span></span>

<span data-ttu-id="86fa1-156">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="86fa1-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="86fa1-157">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="86fa1-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="86fa1-158">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="86fa1-158">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="86fa1-159">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="86fa1-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: S6Pd5XQAx0Ss/zQi.0
MS-ServerId: 030011719
Date: Sat, 10 Jun 2017 00:19:44 GMT

{
    "totalCount": 04,
    "items": [{
            "availableUnits": 15,
            "activeUnits": 15,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 15,
            "warningUnits": 0,
            "productSku": {
                "id": "078d2b04-f1bd-4111-bbd4-b4b1b354cef4",
                "name": "Azure Active Directory Premium P1",
                "skuPartNumber": "AAD_PREMIUM",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Exchange Foundation",
                    "serviceName": "EXCHANGE_S_FOUNDATION",
                    "id": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "capabilityStatus": "Enabled",
                    "targetType": "Tenant"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 1,
            "activeUnits": 1,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "54b84594-9c77-4499-8d65-5e0d5f410e78",
                "name": "Dynamics AX Task",
                "skuPartNumber": "AX_TASK_USER",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 23,
            "activeUnits": 72,
            "consumedUnits": 49,
            "suspendedUnits": 0,
            "totalUnits": 72,
            "warningUnits": 0,
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "targetType": "User",
                "licenseGroupId": "group2"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 71,
            "activeUnits": 112,
            "consumedUnits": 41,
            "suspendedUnits": 0,
            "totalUnits": 112,
            "warningUnits": 0,
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-skus-found"></a><span data-ttu-id="86fa1-160">Příklad odpovědi (nenašly se žádné vyhovující SKU)</span><span class="sxs-lookup"><span data-stu-id="86fa1-160">Response example (no matching SKUs found)</span></span>

<span data-ttu-id="86fa1-161">Pokud se pro zadané skupiny licencí nenašly žádné vyhovující odběry SKU, odpověď obsahuje prázdnou kolekci s elementem totalCount, jehož hodnota je 0.</span><span class="sxs-lookup"><span data-stu-id="86fa1-161">If no matching subscribed SKUs can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
