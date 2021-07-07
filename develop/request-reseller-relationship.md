---
title: Načtení adresy URL žádosti o vztah
description: Jak načíst adresu URL požadavku vztahu pro odeslání zákazníkovi.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07804b36dfe0892cf8b531e0731188260c014f49
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547442"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="24321-103">Načtení adresy URL žádosti o vztah</span><span class="sxs-lookup"><span data-stu-id="24321-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="24321-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo</span><span class="sxs-lookup"><span data-stu-id="24321-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="24321-105">Jak načíst adresu URL požadavku vztahu pro odeslání zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="24321-105">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24321-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="24321-106">Prerequisites</span></span>

- <span data-ttu-id="24321-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="24321-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="24321-108">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="24321-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="24321-109">C\#</span><span class="sxs-lookup"><span data-stu-id="24321-109">C\#</span></span>

<span data-ttu-id="24321-110">Pokud chcete načíst adresu URL požadavku vztahu, nejdřív použijte [**IAggregatePartner. zákazníci**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby získali rozhraní pro zákaznické operace partnera.</span><span class="sxs-lookup"><span data-stu-id="24321-110">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="24321-111">Potom pomocí vlastnosti [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) Získejte rozhraní pro operace požadavku na vztah zákazníka.</span><span class="sxs-lookup"><span data-stu-id="24321-111">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="24321-112">Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) nebo [**GETASYNC**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) načte adresu URL.</span><span class="sxs-lookup"><span data-stu-id="24321-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="24321-113">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="24321-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="24321-114">**Project**: **třída** microsoft Partner SDK samples: GetCustomerRelationshipRequest. cs</span><span class="sxs-lookup"><span data-stu-id="24321-114">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="24321-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="24321-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="24321-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="24321-116">Request syntax</span></span>

| <span data-ttu-id="24321-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="24321-117">Method</span></span>  | <span data-ttu-id="24321-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="24321-118">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="24321-119">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="24321-119">**GET**</span></span> | <span data-ttu-id="24321-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/relationshiprequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="24321-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="24321-121">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="24321-121">Request headers</span></span>

<span data-ttu-id="24321-122">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="24321-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="24321-123">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="24321-123">Request body</span></span>

<span data-ttu-id="24321-124">Žádná</span><span class="sxs-lookup"><span data-stu-id="24321-124">None</span></span>

### <a name="request-example"></a><span data-ttu-id="24321-125">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="24321-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="24321-126">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="24321-126">REST response</span></span>

<span data-ttu-id="24321-127">V případě úspěchu obsahuje odpověď objekt [RelationshipRequest](relationships-resources.md#relationshiprequest) .</span><span class="sxs-lookup"><span data-stu-id="24321-127">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="24321-128">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="24321-128">Response success and error codes</span></span>

<span data-ttu-id="24321-129">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="24321-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="24321-130">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="24321-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="24321-131">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="24321-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="24321-132">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="24321-132">Response example</span></span>

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
