---
title: Načtení seznamu nepřímých prodejců
description: Jak načíst seznam nepřímých prodejců přihlášených partnerů.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 58f5c3378b5b941fdc9dafcf28f5efbc58c29c7c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446560"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a><span data-ttu-id="ee448-103">Načtení seznamu nepřímých prodejců</span><span class="sxs-lookup"><span data-stu-id="ee448-103">Retrieve a list of indirect resellers</span></span>

<span data-ttu-id="ee448-104">Jak načíst seznam nepřímých prodejců přihlášených partnerů.</span><span class="sxs-lookup"><span data-stu-id="ee448-104">How to retrieve a list of the signed-in partner's indirect resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee448-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ee448-105">Prerequisites</span></span>

- <span data-ttu-id="ee448-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ee448-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ee448-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ee448-107">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="ee448-108">C\#</span><span class="sxs-lookup"><span data-stu-id="ee448-108">C\#</span></span>

<span data-ttu-id="ee448-109">Pokud chcete načíst seznam nepřímých prodejců, se kterými má přihlášený partner vztah, nejprve z vlastnosti [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) získejte rozhraní pro operace shromažďování relací.</span><span class="sxs-lookup"><span data-stu-id="ee448-109">To retrieve a list of indirect resellers with whom the signed-in partner has a relationship, first get an interface to relationship collection operations from the [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property.</span></span> <span data-ttu-id="ee448-110">Potom zavolejte [**metodu Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) nebo [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) a předáte člena výčtu [**PartnerRelationshipType,**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) abyste identifikovali typ vztahu.</span><span class="sxs-lookup"><span data-stu-id="ee448-110">Then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) method, passing a member of the [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumeration to identify the relationship type.</span></span> <span data-ttu-id="ee448-111">Pokud chcete načíst nepřímé prodejce, musíte použít IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="ee448-111">To retrieve indirect resellers, you must use IsIndirectCloudSolutionProviderOf.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

<span data-ttu-id="ee448-112">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md)**Project:** SDK pro Partnerské centrum Samples **Class:** GetIndirectResellers.cs</span><span class="sxs-lookup"><span data-stu-id="ee448-112">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ee448-113">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="ee448-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ee448-114">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="ee448-114">Request syntax</span></span>

| <span data-ttu-id="ee448-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="ee448-115">Method</span></span>  | <span data-ttu-id="ee448-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ee448-116">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ee448-117">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="ee448-117">**GET**</span></span> | <span data-ttu-id="ee448-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship \_ type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ee448-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship\_type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ee448-119">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ee448-119">URI parameter</span></span>

<span data-ttu-id="ee448-120">Pomocí následujícího parametru dotazu identifikujte typ relace.</span><span class="sxs-lookup"><span data-stu-id="ee448-120">Use the following query parameter to identify the relationship type.</span></span>

| <span data-ttu-id="ee448-121">Název</span><span class="sxs-lookup"><span data-stu-id="ee448-121">Name</span></span>               | <span data-ttu-id="ee448-122">Typ</span><span class="sxs-lookup"><span data-stu-id="ee448-122">Type</span></span>    | <span data-ttu-id="ee448-123">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ee448-123">Required</span></span>  | <span data-ttu-id="ee448-124">Popis</span><span class="sxs-lookup"><span data-stu-id="ee448-124">Description</span></span>                         |
|--------------------|---------|-----------|-------------------------------------|
| <span data-ttu-id="ee448-125">relationship_type</span><span class="sxs-lookup"><span data-stu-id="ee448-125">relationship_type</span></span>  | <span data-ttu-id="ee448-126">řetězec</span><span class="sxs-lookup"><span data-stu-id="ee448-126">string</span></span>  | <span data-ttu-id="ee448-127">Yes</span><span class="sxs-lookup"><span data-stu-id="ee448-127">Yes</span></span>       | <span data-ttu-id="ee448-128">Hodnota je řetězcová reprezentace jednoho z názvů členů nalezených v [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span><span class="sxs-lookup"><span data-stu-id="ee448-128">The value is the string representation of one of the member names found in [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span></span><br/><br/> <span data-ttu-id="ee448-129">Pokud je partner přihlášený jako poskytovatel a chcete získat seznam nepřímých prodejců, se kterými navázal vztah, použijte IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="ee448-129">If the partner is signed in as a provider and you want to get a list of the indirect resellers with whom they have established a relationship, use IsIndirectCloudSolutionProviderOf.</span></span><br/><br/> <span data-ttu-id="ee448-130">Pokud je partner přihlášený jako prodejce a chcete získat seznam nepřímých poskytovatelů, se kterými se na navázat vztah, použijte IsIndirectResellerOf.</span><span class="sxs-lookup"><span data-stu-id="ee448-130">If the partner is signed in as a reseller and you want to get a list of the indirect providers with whom they have established a relationship, use IsIndirectResellerOf.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="ee448-131">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ee448-131">Request headers</span></span>

<span data-ttu-id="ee448-132">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ee448-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ee448-133">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ee448-133">Request body</span></span>

<span data-ttu-id="ee448-134">Žádné</span><span class="sxs-lookup"><span data-stu-id="ee448-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ee448-135">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ee448-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ee448-136">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ee448-136">REST response</span></span>

<span data-ttu-id="ee448-137">V případě úspěchu obsahuje text odpovědi kolekci prostředků [PartnerRelationship,](relationships-resources.md) které identifikují prodejce.</span><span class="sxs-lookup"><span data-stu-id="ee448-137">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ee448-138">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="ee448-138">Response success and error codes</span></span>

<span data-ttu-id="ee448-139">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ee448-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ee448-140">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="ee448-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ee448-141">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ee448-141">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ee448-142">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ee448-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
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