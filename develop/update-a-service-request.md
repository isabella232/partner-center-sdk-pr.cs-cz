---
title: Aktualizace žádosti o službu
description: Jak aktualizovat existující žádost o služby zákazníkům, Cloud Solution Provider zákazník jménem zákazníka podal u Microsoftu.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: efa7b2a98b6f95a763ca6e3811c43cc655c18e2b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530085"
---
# <a name="update-a-service-request"></a><span data-ttu-id="2324a-103">Aktualizace žádosti o službu</span><span class="sxs-lookup"><span data-stu-id="2324a-103">Update a service request</span></span>

<span data-ttu-id="2324a-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2324a-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2324a-105">Jak aktualizovat existující žádost o služby zákazníkům, Cloud Solution Provider zákazník jménem zákazníka podal u Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="2324a-105">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="2324a-106">Na řídicím Partnerské centrum můžete tuto operaci provést tak, že nejprve [vyberete zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="2324a-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="2324a-107">Pak na levém **bočním** panelu vyberte Správa služeb.</span><span class="sxs-lookup"><span data-stu-id="2324a-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="2324a-108">V **hlavičce Žádosti o** podporu vyberte požadovanou žádost o služby.</span><span class="sxs-lookup"><span data-stu-id="2324a-108">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="2324a-109">Dokončete požadované změny žádosti o služby a pak vyberte **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="2324a-109">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2324a-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2324a-110">Prerequisites</span></span>

- <span data-ttu-id="2324a-111">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2324a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2324a-112">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="2324a-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2324a-113">ID žádosti o služby.</span><span class="sxs-lookup"><span data-stu-id="2324a-113">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="2324a-114">C\#</span><span class="sxs-lookup"><span data-stu-id="2324a-114">C\#</span></span>

<span data-ttu-id="2324a-115">Pokud chcete aktualizovat požadavek na služby zákazníka, zavolejte metodu [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) s ID žádosti o službu, abyste identifikovali a vrátili rozhraní žádosti o služby.</span><span class="sxs-lookup"><span data-stu-id="2324a-115">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request ID to identify and return the service request interface.</span></span> <span data-ttu-id="2324a-116">Potom zavolejte [**metodu IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) nebo [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) a aktualizujte žádost o službu.</span><span class="sxs-lookup"><span data-stu-id="2324a-116">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="2324a-117">Pokud chcete zadat aktualizované hodnoty, vytvořte nový prázdný objekt [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) a nastavte pouze hodnoty vlastností, které chcete změnit.</span><span class="sxs-lookup"><span data-stu-id="2324a-117">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="2324a-118">Pak tento objekt předejte ve volání metody Patch nebo PatchAsync.</span><span class="sxs-lookup"><span data-stu-id="2324a-118">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="2324a-119">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2324a-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2324a-120">**Project:** SDK pro Partnerské centrum Samples **– třída:** UpdatePartnerServiceRequest.cs</span><span class="sxs-lookup"><span data-stu-id="2324a-120">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2324a-121">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="2324a-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2324a-122">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="2324a-122">Request syntax</span></span>

| <span data-ttu-id="2324a-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="2324a-123">Method</span></span>    | <span data-ttu-id="2324a-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2324a-124">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="2324a-125">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="2324a-125">**PATCH**</span></span> | <span data-ttu-id="2324a-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{id_požadavku_služby} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2324a-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2324a-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2324a-127">URI parameter</span></span>

<span data-ttu-id="2324a-128">Pomocí následujícího parametru URI aktualizujte požadavek na službu.</span><span class="sxs-lookup"><span data-stu-id="2324a-128">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="2324a-129">Název</span><span class="sxs-lookup"><span data-stu-id="2324a-129">Name</span></span>                  | <span data-ttu-id="2324a-130">Typ</span><span class="sxs-lookup"><span data-stu-id="2324a-130">Type</span></span>     | <span data-ttu-id="2324a-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="2324a-131">Required</span></span> | <span data-ttu-id="2324a-132">Popis</span><span class="sxs-lookup"><span data-stu-id="2324a-132">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="2324a-133">**id_události_služby**</span><span class="sxs-lookup"><span data-stu-id="2324a-133">**servicerequest-id**</span></span> | <span data-ttu-id="2324a-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="2324a-134">**guid**</span></span> | <span data-ttu-id="2324a-135">Y</span><span class="sxs-lookup"><span data-stu-id="2324a-135">Y</span></span>        | <span data-ttu-id="2324a-136">Identifikátor GUID, který identifikuje požadavek na službu.</span><span class="sxs-lookup"><span data-stu-id="2324a-136">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2324a-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2324a-137">Request headers</span></span>

<span data-ttu-id="2324a-138">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2324a-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2324a-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2324a-139">Request body</span></span>

<span data-ttu-id="2324a-140">Text požadavku by měl obsahovat [prostředek ServiceRequest.](service-request-resources.md)</span><span class="sxs-lookup"><span data-stu-id="2324a-140">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="2324a-141">Jediné požadované hodnoty jsou hodnoty, které se mají aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="2324a-141">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="2324a-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="2324a-142">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="2324a-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2324a-143">REST response</span></span>

<span data-ttu-id="2324a-144">V případě úspěchu tato metoda vrátí **prostředek žádosti** o služby s aktualizovanými vlastnostmi v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="2324a-144">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2324a-145">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="2324a-145">Response success and error codes</span></span>

<span data-ttu-id="2324a-146">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2324a-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2324a-147">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="2324a-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2324a-148">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2324a-148">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2324a-149">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="2324a-149">Response example</span></span>

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
