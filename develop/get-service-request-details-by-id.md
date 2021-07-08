---
title: Získejte podrobnosti o žádosti o služby podle ID.
description: Jak načíst podrobnosti o existující žádosti o služby zákazníkům podle ID.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66488cf9592d630cb1f0237d379e8df5ead6a3a8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548766"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="ba844-103">Získání podrobností žádostí o službu podle ID</span><span class="sxs-lookup"><span data-stu-id="ba844-103">Get service request details by ID</span></span>

<span data-ttu-id="ba844-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ba844-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ba844-105">Jak načíst podrobnosti o existující žádosti o služby zákazníkům pomocí identifikátoru žádosti o služby.</span><span class="sxs-lookup"><span data-stu-id="ba844-105">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba844-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ba844-106">Prerequisites</span></span>

- <span data-ttu-id="ba844-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ba844-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ba844-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ba844-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ba844-109">ID žádosti o služby.</span><span class="sxs-lookup"><span data-stu-id="ba844-109">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="ba844-110">C\#</span><span class="sxs-lookup"><span data-stu-id="ba844-110">C\#</span></span>

<span data-ttu-id="ba844-111">Pokud chcete načíst podrobnosti o existující žádosti o služby zákazníkům, zavolejte metodu [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) a předejte [**ServiceRequest.Id,**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) abyste identifikovali a vrátili rozhraní pro konkrétní objekt [**ServiceRequest.**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)</span><span class="sxs-lookup"><span data-stu-id="ba844-111">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest as ServiceRequest;

ServiceRequest serviceRequestDetails = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Get();

Console.WriteLine(string.Format("The primary contact for the service request {0} is {1} {2}.",
    serviceRequestDetails.Title,
    serviceRequestDetails.PrimaryContact.FirstName,
    serviceRequestDetails.PrimaryContact.LastName,
));
```

## <a name="rest-request"></a><span data-ttu-id="ba844-112">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="ba844-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ba844-113">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="ba844-113">Request syntax</span></span>

| <span data-ttu-id="ba844-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="ba844-114">Method</span></span>    | <span data-ttu-id="ba844-115">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ba844-115">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="ba844-116">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="ba844-116">**GET**</span></span> | <span data-ttu-id="ba844-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{id_požadavku_služby} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ba844-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="ba844-118">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ba844-118">URI parameter</span></span>

<span data-ttu-id="ba844-119">Pomocí následujícího parametru URI získejte zadaný požadavek na službu.</span><span class="sxs-lookup"><span data-stu-id="ba844-119">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="ba844-120">Název</span><span class="sxs-lookup"><span data-stu-id="ba844-120">Name</span></span>                  | <span data-ttu-id="ba844-121">Typ</span><span class="sxs-lookup"><span data-stu-id="ba844-121">Type</span></span>     | <span data-ttu-id="ba844-122">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ba844-122">Required</span></span> | <span data-ttu-id="ba844-123">Popis</span><span class="sxs-lookup"><span data-stu-id="ba844-123">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="ba844-124">**id_události_služby**</span><span class="sxs-lookup"><span data-stu-id="ba844-124">**servicerequest-id**</span></span> | <span data-ttu-id="ba844-125">**guid**</span><span class="sxs-lookup"><span data-stu-id="ba844-125">**guid**</span></span> | <span data-ttu-id="ba844-126">Y</span><span class="sxs-lookup"><span data-stu-id="ba844-126">Y</span></span>        | <span data-ttu-id="ba844-127">Identifikátor GUID, který identifikuje požadavek na službu.</span><span class="sxs-lookup"><span data-stu-id="ba844-127">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ba844-128">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ba844-128">Request headers</span></span>

<span data-ttu-id="ba844-129">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ba844-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ba844-130">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ba844-130">Request body</span></span>

<span data-ttu-id="ba844-131">Žádné</span><span class="sxs-lookup"><span data-stu-id="ba844-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ba844-132">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ba844-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="ba844-133">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ba844-133">REST response</span></span>

<span data-ttu-id="ba844-134">V případě úspěchu vrátí tato metoda **v** textu odpovědi prostředek žádosti o služby.</span><span class="sxs-lookup"><span data-stu-id="ba844-134">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ba844-135">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="ba844-135">Response success and error codes</span></span>

<span data-ttu-id="ba844-136">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ba844-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ba844-137">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="ba844-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ba844-138">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ba844-138">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ba844-139">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ba844-139">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
