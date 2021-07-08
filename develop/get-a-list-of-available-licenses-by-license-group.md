---
title: Získání seznamu dostupných licencí podle skupiny licencí
description: Jak získat seznam licencí pro zadané skupiny licencí dostupné uživatelům zadaného zákazníka.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: de59dfccf723c8f2411d9dadc51beb88688d5b02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874512"
---
# <a name="get-a-list-of-available-licenses-by-license-group"></a><span data-ttu-id="fa4ef-103">Získání seznamu dostupných licencí podle skupiny licencí</span><span class="sxs-lookup"><span data-stu-id="fa4ef-103">Get a list of available licenses by license group</span></span>

<span data-ttu-id="fa4ef-104">Jak získat seznam licencí pro zadané skupiny licencí dostupné uživatelům zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-104">How to get a list of licenses for the specified license groups available to users of the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa4ef-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fa4ef-105">Prerequisites</span></span>

- <span data-ttu-id="fa4ef-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fa4ef-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fa4ef-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="fa4ef-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fa4ef-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fa4ef-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="fa4ef-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fa4ef-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="fa4ef-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fa4ef-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="fa4ef-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fa4ef-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-112">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fa4ef-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fa4ef-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fa4ef-114">Seznam jednoho nebo více identifikátorů skupin licencí.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-114">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="fa4ef-115">C\#</span><span class="sxs-lookup"><span data-stu-id="fa4ef-115">C\#</span></span>

<span data-ttu-id="fa4ef-116">Pokud chcete získat seznam dostupných licencí pro zadané skupiny licencí, začněte vytvořením instance [seznamu](/dotnet/api/system.collections.generic.list-1) typu [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)a pak skupiny licencí přidejte do seznamu.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-116">To get a list of available licenses for the specified license groups, start by instantiating a [List](/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="fa4ef-117">Dále k identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-117">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="fa4ef-118">Pak získejte hodnotu vlastnosti [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) a načtěte rozhraní pro operace kolekce SKU odebíraných zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-118">Then, get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span> <span data-ttu-id="fa4ef-119">Nakonec předejte seznam skupin licencí metodě [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) nebo [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) která načte seznam předplacených skladových položek s podrobnostmi o dostupných licenčních jednotkách.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-119">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of subscribed SKUs with details on available license units.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="fa4ef-120">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="fa4ef-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fa4ef-121">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="fa4ef-121">Request syntax</span></span>

| <span data-ttu-id="fa4ef-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="fa4ef-122">Method</span></span>  | <span data-ttu-id="fa4ef-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fa4ef-123">Request URI</span></span>                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fa4ef-124">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="fa4ef-124">**GET**</span></span> | <span data-ttu-id="fa4ef-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{id_zákazníka}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fa4ef-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="fa4ef-126">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="fa4ef-126">**GET**</span></span> | <span data-ttu-id="fa4ef-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fa4ef-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="fa4ef-128">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="fa4ef-128">**GET**</span></span> | <span data-ttu-id="fa4ef-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fa4ef-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fa4ef-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fa4ef-130">URI parameter</span></span>

<span data-ttu-id="fa4ef-131">Pomocí následující cesty a parametrů dotazu identifikujte zákazníka a skupiny licencí.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-131">Use the following path and query parameters to identify the customer and the license groups.</span></span>

| <span data-ttu-id="fa4ef-132">Název</span><span class="sxs-lookup"><span data-stu-id="fa4ef-132">Name</span></span>            | <span data-ttu-id="fa4ef-133">Typ</span><span class="sxs-lookup"><span data-stu-id="fa4ef-133">Type</span></span>   | <span data-ttu-id="fa4ef-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fa4ef-134">Required</span></span> | <span data-ttu-id="fa4ef-135">Popis</span><span class="sxs-lookup"><span data-stu-id="fa4ef-135">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fa4ef-136">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="fa4ef-136">customer-id</span></span>     | <span data-ttu-id="fa4ef-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="fa4ef-137">string</span></span> | <span data-ttu-id="fa4ef-138">Yes</span><span class="sxs-lookup"><span data-stu-id="fa4ef-138">Yes</span></span>      | <span data-ttu-id="fa4ef-139">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-139">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="fa4ef-140">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="fa4ef-140">licenseGroupIds</span></span> | <span data-ttu-id="fa4ef-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="fa4ef-141">string</span></span> | <span data-ttu-id="fa4ef-142">No</span><span class="sxs-lookup"><span data-stu-id="fa4ef-142">No</span></span>       | <span data-ttu-id="fa4ef-143">Hodnota výčtu, která označuje skupinu licencí přiřazených licencí.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-143">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="fa4ef-144">Platné hodnoty: Group1, Group2 Group1 – tato skupina obsahuje všechny produkty, jejichž licenci je možné spravovat v Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="fa4ef-144">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="fa4ef-145">Skupina2 – Tato skupina má pouze Minecraft licence k produktu.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-145">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fa4ef-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fa4ef-146">Request headers</span></span>

<span data-ttu-id="fa4ef-147">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fa4ef-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fa4ef-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fa4ef-148">Request body</span></span>

<span data-ttu-id="fa4ef-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="fa4ef-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fa4ef-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fa4ef-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="fa4ef-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fa4ef-151">REST response</span></span>

<span data-ttu-id="fa4ef-152">V případě úspěchu bude tělo odpovědi obsahovat kolekci prostředků [SubscribedSku.](license-resources.md#subscribedsku)</span><span class="sxs-lookup"><span data-stu-id="fa4ef-152">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fa4ef-153">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="fa4ef-153">Response success and error codes</span></span>

<span data-ttu-id="fa4ef-154">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fa4ef-155">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fa4ef-156">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fa4ef-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fa4ef-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fa4ef-157">Response example</span></span>

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

### <a name="response-example-no-matching-skus-found"></a><span data-ttu-id="fa4ef-158">Příklad odpovědi (nenašly se žádné odpovídající skladové položky)</span><span class="sxs-lookup"><span data-stu-id="fa4ef-158">Response example (no matching SKUs found)</span></span>

<span data-ttu-id="fa4ef-159">Pokud pro zadané skupiny licencí nelze najít žádné odpovídající předplacené skladové položky, odpověď obsahuje prázdnou kolekci s elementem totalCount, jehož hodnota je 0.</span><span class="sxs-lookup"><span data-stu-id="fa4ef-159">If no matching subscribed SKUs can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
