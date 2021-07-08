---
title: Získání seznamu dostupných licencí
description: Jak získat seznam licencí dostupných pro uživatele zadaného zákazníka.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 02a6fccc2cf7f3f4dc929b96ec0f17e0f4a31b06
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874495"
---
# <a name="get-a-list-of-available-licenses"></a><span data-ttu-id="ca434-103">Získání seznamu dostupných licencí</span><span class="sxs-lookup"><span data-stu-id="ca434-103">Get a list of available licenses</span></span>

<span data-ttu-id="ca434-104">Tento článek popisuje, jak získat seznam licencí dostupných pro uživatele zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ca434-104">This article describes how to get a list of licenses available to users of the specified customer.</span></span>

<span data-ttu-id="ca434-105">Následující příklady vrátí licence dostupné z **Group1**, výchozí skupinu licencí, která představuje licence spravované službou Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ca434-105">The following examples return licenses available from **group1**, the default license group that represents licenses managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ca434-106">Pokud chcete získat dostupné licence pro zadanou skupinu licencí, přečtěte si téma [získání seznamu dostupných licencí podle skupiny licencí](get-a-list-of-available-licenses-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="ca434-106">To get available licenses for a specified license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca434-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ca434-107">Prerequisites</span></span>

- <span data-ttu-id="ca434-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ca434-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ca434-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ca434-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ca434-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ca434-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ca434-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="ca434-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ca434-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="ca434-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ca434-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="ca434-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ca434-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="ca434-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ca434-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ca434-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ca434-116">C\#</span><span class="sxs-lookup"><span data-stu-id="ca434-116">C\#</span></span>

<span data-ttu-id="ca434-117">Načtení seznamu licencí dostupných z výchozí skupiny licencí uživatelům zákazníka:</span><span class="sxs-lookup"><span data-stu-id="ca434-117">To retrieve the list of licenses available from the default license group to users of a customer:</span></span>

1. <span data-ttu-id="ca434-118">K identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ca434-118">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="ca434-119">Získat hodnotu vlastnosti [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) , která načte rozhraní pro operace shromažďování skladových položek s předplacenou odběrateli.</span><span class="sxs-lookup"><span data-stu-id="ca434-119">Get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span>

3. <span data-ttu-id="ca434-120">Pro načtení seznamu licencí zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="ca434-120">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of licenses.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
```

<span data-ttu-id="ca434-121">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="ca434-121">For an example, see the following:</span></span>

- <span data-ttu-id="ca434-122">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ca434-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ca434-123">Project: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="ca434-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="ca434-124">Třída: **GetCustomerSubscribedSkus. cs**</span><span class="sxs-lookup"><span data-stu-id="ca434-124">Class: **GetCustomerSubscribedSkus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="ca434-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ca434-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ca434-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ca434-126">Request syntax</span></span>

| <span data-ttu-id="ca434-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="ca434-127">Method</span></span>  | <span data-ttu-id="ca434-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ca434-128">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ca434-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="ca434-129">**GET**</span></span> | <span data-ttu-id="ca434-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscribedskus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ca434-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="ca434-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ca434-131">URI parameter</span></span>

<span data-ttu-id="ca434-132">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="ca434-132">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="ca434-133">Název</span><span class="sxs-lookup"><span data-stu-id="ca434-133">Name</span></span>        | <span data-ttu-id="ca434-134">Typ</span><span class="sxs-lookup"><span data-stu-id="ca434-134">Type</span></span>   | <span data-ttu-id="ca434-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ca434-135">Required</span></span> | <span data-ttu-id="ca434-136">Popis</span><span class="sxs-lookup"><span data-stu-id="ca434-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="ca434-137">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="ca434-137">customer-id</span></span> | <span data-ttu-id="ca434-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="ca434-138">string</span></span> | <span data-ttu-id="ca434-139">Yes</span><span class="sxs-lookup"><span data-stu-id="ca434-139">Yes</span></span>      | <span data-ttu-id="ca434-140">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ca434-140">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ca434-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ca434-141">Request headers</span></span>

<span data-ttu-id="ca434-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ca434-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ca434-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ca434-143">Request body</span></span>

<span data-ttu-id="ca434-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="ca434-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ca434-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ca434-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ca434-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ca434-146">REST response</span></span>

<span data-ttu-id="ca434-147">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [SubscribedSku](license-resources.md#subscribedsku) .</span><span class="sxs-lookup"><span data-stu-id="ca434-147">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ca434-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ca434-148">Response success and error codes</span></span>

<span data-ttu-id="ca434-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ca434-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ca434-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ca434-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ca434-151">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ca434-151">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ca434-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ca434-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CV: 7BQ0jitzXUCLwRM6.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 17:50:46 GMT

 {
    "totalCount": 2,
    "items": [{
            "availableUnits": 4,
            "activeUnits": 5,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 5,
            "warningUnits": 0,
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
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
        },  {
            "availableUnits": 0,
            "activeUnits": 1,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "f8a1db68-be16-40ed-86d5-cb42ce701560",
                "name": "Power BI Pro",
                "skuPartNumber": "POWER_BI_PRO",
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
                    "displayName": "Power BI Pro",
                    "serviceName": "BI_AZURE_P2",
                    "id": "70d33638-9c74-4d01-bfd3-562de28bd4ba",
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
