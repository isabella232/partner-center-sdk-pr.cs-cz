---
title: Načtení adresy URL žádosti o vztah
description: Jak načíst adresu URL požadavku vztahu pro odeslání zákazníkovi.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5f899734b774ff460e005e20df8658275b2ce9d5
ms.sourcegitcommit: d4e652e3b73c6137704d43d4a472cc5aa5549f11
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/09/2020
ms.locfileid: "97767664"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="5c40a-103">Načtení adresy URL žádosti o vztah</span><span class="sxs-lookup"><span data-stu-id="5c40a-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="5c40a-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="5c40a-104">**Applies To**</span></span>

- <span data-ttu-id="5c40a-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="5c40a-105">Partner Center</span></span>
- <span data-ttu-id="5c40a-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="5c40a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5c40a-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="5c40a-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="5c40a-108">Jak načíst adresu URL požadavku vztahu pro odeslání zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="5c40a-108">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c40a-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5c40a-109">Prerequisites</span></span>

- <span data-ttu-id="5c40a-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5c40a-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5c40a-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="5c40a-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="5c40a-112">C\#</span><span class="sxs-lookup"><span data-stu-id="5c40a-112">C\#</span></span>

<span data-ttu-id="5c40a-113">Pokud chcete načíst adresu URL požadavku vztahu, nejdřív použijte [**IAggregatePartner. zákazníci**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby získali rozhraní pro zákaznické operace partnera.</span><span class="sxs-lookup"><span data-stu-id="5c40a-113">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="5c40a-114">Potom pomocí vlastnosti [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) Získejte rozhraní pro operace požadavku na vztah zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c40a-114">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="5c40a-115">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) nebo [**GETASYNC**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) načte adresu URL.</span><span class="sxs-lookup"><span data-stu-id="5c40a-115">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="5c40a-116">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5c40a-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5c40a-117">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetCustomerRelationshipRequest.cs</span><span class="sxs-lookup"><span data-stu-id="5c40a-117">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5c40a-118">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="5c40a-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5c40a-119">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="5c40a-119">Request syntax</span></span>

| <span data-ttu-id="5c40a-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="5c40a-120">Method</span></span>  | <span data-ttu-id="5c40a-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5c40a-121">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="5c40a-122">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="5c40a-122">**GET**</span></span> | <span data-ttu-id="5c40a-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/relationshiprequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5c40a-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5c40a-124">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5c40a-124">Request headers</span></span>

<span data-ttu-id="5c40a-125">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5c40a-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5c40a-126">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="5c40a-126">Request body</span></span>

<span data-ttu-id="5c40a-127">Žádné</span><span class="sxs-lookup"><span data-stu-id="5c40a-127">None</span></span>

### <a name="request-example"></a><span data-ttu-id="5c40a-128">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="5c40a-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="5c40a-129">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5c40a-129">REST response</span></span>

<span data-ttu-id="5c40a-130">V případě úspěchu obsahuje odpověď objekt [RelationshipRequest](relationships-resources.md#relationshiprequest) .</span><span class="sxs-lookup"><span data-stu-id="5c40a-130">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5c40a-131">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="5c40a-131">Response success and error codes</span></span>

<span data-ttu-id="5c40a-132">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5c40a-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5c40a-133">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="5c40a-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5c40a-134">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5c40a-134">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5c40a-135">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="5c40a-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=3b33e682-00c3-41ee-9dd2-a548adf56438&msppId=0&DAP=false#/BillingAccounts/partner-invitation",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
