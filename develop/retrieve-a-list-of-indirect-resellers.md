---
title: Načtení seznamu nepřímých prodejců
description: Jak načíst seznam nepřímých prodejců partnera, který je přihlášený.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e53237b97fa26d3a987f0ee7de491084b596af4a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767013"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a><span data-ttu-id="8f035-103">Načtení seznamu nepřímých prodejců</span><span class="sxs-lookup"><span data-stu-id="8f035-103">Retrieve a list of indirect resellers</span></span>

<span data-ttu-id="8f035-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="8f035-104">**Applies To**</span></span>

- <span data-ttu-id="8f035-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="8f035-105">Partner Center</span></span>

<span data-ttu-id="8f035-106">Jak načíst seznam nepřímých prodejců partnera, který je přihlášený.</span><span class="sxs-lookup"><span data-stu-id="8f035-106">How to retrieve a list of the signed-in partner's indirect resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f035-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8f035-107">Prerequisites</span></span>

- <span data-ttu-id="8f035-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8f035-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8f035-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="8f035-109">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="8f035-110">C\#</span><span class="sxs-lookup"><span data-stu-id="8f035-110">C\#</span></span>

<span data-ttu-id="8f035-111">Chcete-li načíst seznam nepřímých prodejců, se kterými má přihlášený partner relaci, nejprve získejte rozhraní pro operace shromažďování relací z vlastnosti [**partnerOperations. relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) .</span><span class="sxs-lookup"><span data-stu-id="8f035-111">To retrieve a list of indirect resellers with whom the signed-in partner has a relationship, first get an interface to relationship collection operations from the [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property.</span></span> <span data-ttu-id="8f035-112">Pak zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) nebo [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) , předáním členu výčtu [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) Identifikujte typ vztahu.</span><span class="sxs-lookup"><span data-stu-id="8f035-112">Then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) method, passing a member of the [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumeration to identify the relationship type.</span></span> <span data-ttu-id="8f035-113">K načtení nepřímých prodejců musíte použít IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="8f035-113">To retrieve indirect resellers, you must use IsIndirectCloudSolutionProviderOf.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

<span data-ttu-id="8f035-114">**Ukázka**:**projekt** [aplikace testů konzoly](console-test-app.md): ukázkové **třídy** SDK pro partnerských Center: GetIndirectResellers.cs</span><span class="sxs-lookup"><span data-stu-id="8f035-114">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8f035-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="8f035-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8f035-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="8f035-116">Request syntax</span></span>

| <span data-ttu-id="8f035-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="8f035-117">Method</span></span>  | <span data-ttu-id="8f035-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8f035-118">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f035-119">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="8f035-119">**GET**</span></span> | <span data-ttu-id="8f035-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Relationships? \_ typ vztahu = IsIndirectCloudSolutionProviderOf HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8f035-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship\_type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8f035-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8f035-121">URI parameter</span></span>

<span data-ttu-id="8f035-122">K identifikaci typu vztahu použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="8f035-122">Use the following query parameter to identify the relationship type.</span></span>

| <span data-ttu-id="8f035-123">Název</span><span class="sxs-lookup"><span data-stu-id="8f035-123">Name</span></span>               | <span data-ttu-id="8f035-124">Typ</span><span class="sxs-lookup"><span data-stu-id="8f035-124">Type</span></span>    | <span data-ttu-id="8f035-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8f035-125">Required</span></span>  | <span data-ttu-id="8f035-126">Popis</span><span class="sxs-lookup"><span data-stu-id="8f035-126">Description</span></span>                         |
|--------------------|---------|-----------|-------------------------------------|
| <span data-ttu-id="8f035-127">relationship_type</span><span class="sxs-lookup"><span data-stu-id="8f035-127">relationship_type</span></span>  | <span data-ttu-id="8f035-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="8f035-128">string</span></span>  | <span data-ttu-id="8f035-129">Yes</span><span class="sxs-lookup"><span data-stu-id="8f035-129">Yes</span></span>       | <span data-ttu-id="8f035-130">Hodnota je řetězcová reprezentace jednoho z názvů členů nalezených v [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span><span class="sxs-lookup"><span data-stu-id="8f035-130">The value is the string representation of one of the member names found in [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span></span><br/><br/> <span data-ttu-id="8f035-131">Pokud je partner přihlášený jako poskytovatel a chcete získat seznam nepřímých prodejců, se kterými navázali relaci, použijte IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="8f035-131">If the partner is signed in as a provider and you want to get a list of the indirect resellers with whom they have established a relationship, use IsIndirectCloudSolutionProviderOf.</span></span><br/><br/> <span data-ttu-id="8f035-132">Pokud je partner přihlášený jako prodejce a chcete získat seznam nepřímých zprostředkovatelů, se kterými navázali relaci, použijte IsIndirectResellerOf.</span><span class="sxs-lookup"><span data-stu-id="8f035-132">If the partner is signed in as a reseller and you want to get a list of the indirect providers with whom they have established a relationship, use IsIndirectResellerOf.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="8f035-133">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8f035-133">Request headers</span></span>

<span data-ttu-id="8f035-134">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8f035-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8f035-135">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8f035-135">Request body</span></span>

<span data-ttu-id="8f035-136">Žádné</span><span class="sxs-lookup"><span data-stu-id="8f035-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8f035-137">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8f035-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8f035-138">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8f035-138">REST response</span></span>

<span data-ttu-id="8f035-139">V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [PartnerRelationship](relationships-resources.md) k identifikaci prodejců.</span><span class="sxs-lookup"><span data-stu-id="8f035-139">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8f035-140">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="8f035-140">Response success and error codes</span></span>

<span data-ttu-id="8f035-141">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8f035-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8f035-142">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="8f035-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8f035-143">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8f035-143">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8f035-144">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8f035-144">Response example</span></span>

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