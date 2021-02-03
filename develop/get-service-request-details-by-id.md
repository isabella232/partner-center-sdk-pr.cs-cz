---
title: Získejte podrobnosti žádosti o službu podle ID.
description: Jak načíst podrobnosti o existující žádosti o služby zákazníkům podle ID
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c79fd3f5e5609a1893891e9b2a8078f8678497b3
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767051"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="56f5d-103">Získání podrobností žádostí o službu podle ID</span><span class="sxs-lookup"><span data-stu-id="56f5d-103">Get service request details by ID</span></span>

<span data-ttu-id="56f5d-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="56f5d-104">**Applies To**</span></span>

- <span data-ttu-id="56f5d-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="56f5d-105">Partner Center</span></span>
- <span data-ttu-id="56f5d-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="56f5d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="56f5d-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="56f5d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="56f5d-108">Jak načíst podrobnosti o existující žádosti o služby zákazníkům pomocí identifikátoru žádosti o službu.</span><span class="sxs-lookup"><span data-stu-id="56f5d-108">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56f5d-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="56f5d-109">Prerequisites</span></span>

- <span data-ttu-id="56f5d-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="56f5d-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="56f5d-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="56f5d-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="56f5d-112">ID žádosti o službu.</span><span class="sxs-lookup"><span data-stu-id="56f5d-112">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="56f5d-113">C\#</span><span class="sxs-lookup"><span data-stu-id="56f5d-113">C\#</span></span>

<span data-ttu-id="56f5d-114">Chcete-li načíst podrobnosti o existující žádosti o služby zákazníkům, zavolejte metodu [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) a předejte [**ServiceRequest.ID**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) k identifikaci a vrácení rozhraní konkrétnímu objektu [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) .</span><span class="sxs-lookup"><span data-stu-id="56f5d-114">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="56f5d-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="56f5d-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="56f5d-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="56f5d-116">Request syntax</span></span>

| <span data-ttu-id="56f5d-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="56f5d-117">Method</span></span>    | <span data-ttu-id="56f5d-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="56f5d-118">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="56f5d-119">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="56f5d-119">**GET**</span></span> | <span data-ttu-id="56f5d-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{ServiceRequest-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="56f5d-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="56f5d-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="56f5d-121">URI parameter</span></span>

<span data-ttu-id="56f5d-122">K získání zadané žádosti o služby použijte následující parametr identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="56f5d-122">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="56f5d-123">Název</span><span class="sxs-lookup"><span data-stu-id="56f5d-123">Name</span></span>                  | <span data-ttu-id="56f5d-124">Typ</span><span class="sxs-lookup"><span data-stu-id="56f5d-124">Type</span></span>     | <span data-ttu-id="56f5d-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="56f5d-125">Required</span></span> | <span data-ttu-id="56f5d-126">Popis</span><span class="sxs-lookup"><span data-stu-id="56f5d-126">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="56f5d-127">**ServiceRequest-ID**</span><span class="sxs-lookup"><span data-stu-id="56f5d-127">**servicerequest-id**</span></span> | <span data-ttu-id="56f5d-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="56f5d-128">**guid**</span></span> | <span data-ttu-id="56f5d-129">Y</span><span class="sxs-lookup"><span data-stu-id="56f5d-129">Y</span></span>        | <span data-ttu-id="56f5d-130">Identifikátor GUID, který identifikuje požadavek služby.</span><span class="sxs-lookup"><span data-stu-id="56f5d-130">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="56f5d-131">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="56f5d-131">Request headers</span></span>

<span data-ttu-id="56f5d-132">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="56f5d-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="56f5d-133">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="56f5d-133">Request body</span></span>

<span data-ttu-id="56f5d-134">Žádné</span><span class="sxs-lookup"><span data-stu-id="56f5d-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="56f5d-135">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="56f5d-135">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="56f5d-136">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="56f5d-136">REST response</span></span>

<span data-ttu-id="56f5d-137">V případě úspěchu tato metoda vrátí prostředek **žádosti o službu** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="56f5d-137">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="56f5d-138">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="56f5d-138">Response success and error codes</span></span>

<span data-ttu-id="56f5d-139">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="56f5d-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="56f5d-140">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="56f5d-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="56f5d-141">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="56f5d-141">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="56f5d-142">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="56f5d-142">Response example</span></span>

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
