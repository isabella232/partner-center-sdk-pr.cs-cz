---
title: Získání nepřímých prodejců zákazníka
description: Jak získat seznam nepřímých prodejců, kteří mají relaci se zadaným zákazníkem.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 8697c40c22d5c19979c066b8d3a1de733e211f71
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446237"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="35c5e-103">Získání nepřímých prodejců zákazníka</span><span class="sxs-lookup"><span data-stu-id="35c5e-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="35c5e-104">Jak získat seznam nepřímých prodejců, kteří mají relaci se zadaným zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="35c5e-104">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35c5e-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="35c5e-105">Prerequisites</span></span>

- <span data-ttu-id="35c5e-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="35c5e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="35c5e-107">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="35c5e-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="35c5e-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="35c5e-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="35c5e-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="35c5e-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="35c5e-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="35c5e-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="35c5e-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="35c5e-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="35c5e-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="35c5e-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="35c5e-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="35c5e-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="35c5e-114">C\#</span><span class="sxs-lookup"><span data-stu-id="35c5e-114">C\#</span></span>

<span data-ttu-id="35c5e-115">Pokud chcete načíst seznam nepřímých prodejců, se kterými má zadaný zákazník vztah, napřed pro konkrétního zákazníka z vlastnosti [**partnerOperations. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) pro konkrétního zákazníka, který poskytuje ID zákazníka k identifikaci zákazníka, nejprve získejte rozhraní pro operace shromažďování zákazníka.</span><span class="sxs-lookup"><span data-stu-id="35c5e-115">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="35c5e-116">Pak zavolejte [**relaci. Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) nebo [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) pro získání seznamu nepřímých prodejců.</span><span class="sxs-lookup"><span data-stu-id="35c5e-116">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="35c5e-117">**ukázka**: [konzola test app](console-test-app.md)**Project**: **třída** pro ukázkové sady SDK partnerského centra: GetIndirectResellersOfCustomer. cs</span><span class="sxs-lookup"><span data-stu-id="35c5e-117">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="35c5e-118">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="35c5e-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="35c5e-119">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="35c5e-119">Request syntax</span></span>

| <span data-ttu-id="35c5e-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="35c5e-120">Method</span></span>  | <span data-ttu-id="35c5e-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="35c5e-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="35c5e-122">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="35c5e-122">**GET**</span></span> | <span data-ttu-id="35c5e-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Relationships HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="35c5e-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="35c5e-124">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="35c5e-124">URI parameter</span></span>

<span data-ttu-id="35c5e-125">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="35c5e-125">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="35c5e-126">Název</span><span class="sxs-lookup"><span data-stu-id="35c5e-126">Name</span></span>        | <span data-ttu-id="35c5e-127">Typ</span><span class="sxs-lookup"><span data-stu-id="35c5e-127">Type</span></span>   | <span data-ttu-id="35c5e-128">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="35c5e-128">Required</span></span> | <span data-ttu-id="35c5e-129">Popis</span><span class="sxs-lookup"><span data-stu-id="35c5e-129">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="35c5e-130">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="35c5e-130">customer-id</span></span> | <span data-ttu-id="35c5e-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="35c5e-131">string</span></span> | <span data-ttu-id="35c5e-132">Yes</span><span class="sxs-lookup"><span data-stu-id="35c5e-132">Yes</span></span>      | <span data-ttu-id="35c5e-133">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="35c5e-133">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="35c5e-134">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="35c5e-134">Request headers</span></span>

<span data-ttu-id="35c5e-135">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="35c5e-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="35c5e-136">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="35c5e-136">Request body</span></span>

<span data-ttu-id="35c5e-137">Žádné</span><span class="sxs-lookup"><span data-stu-id="35c5e-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="35c5e-138">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="35c5e-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="35c5e-139">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="35c5e-139">REST response</span></span>

<span data-ttu-id="35c5e-140">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [PartnerRelationship](relationships-resources.md) k identifikaci prodejců.</span><span class="sxs-lookup"><span data-stu-id="35c5e-140">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="35c5e-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="35c5e-141">Response success and error codes</span></span>

<span data-ttu-id="35c5e-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="35c5e-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="35c5e-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="35c5e-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="35c5e-144">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="35c5e-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="35c5e-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="35c5e-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
