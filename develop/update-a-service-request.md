---
title: Aktualizace žádosti o službu
description: Jak aktualizovat existující žádost o služby zákazníkům, kterou poskytovatel cloudového řešení uzavřel s Microsoftem jménem zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1df0d1f5fa4630b346d1c8b9cffabb86ce34cfb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766998"
---
# <a name="update-a-service-request"></a><span data-ttu-id="9da42-103">Aktualizace žádosti o službu</span><span class="sxs-lookup"><span data-stu-id="9da42-103">Update a service request</span></span>

<span data-ttu-id="9da42-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="9da42-104">**Applies To**</span></span>

- <span data-ttu-id="9da42-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="9da42-105">Partner Center</span></span>
- <span data-ttu-id="9da42-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="9da42-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9da42-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9da42-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9da42-108">Jak aktualizovat existující žádost o služby zákazníkům, kterou poskytovatel cloudového řešení uzavřel s Microsoftem jménem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9da42-108">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="9da42-109">Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="9da42-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="9da42-110">Pak na levém bočním panelu vyberte **Správa služeb** .</span><span class="sxs-lookup"><span data-stu-id="9da42-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="9da42-111">V části **žádosti o podporu** vyberte příslušný požadavek služby.</span><span class="sxs-lookup"><span data-stu-id="9da42-111">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="9da42-112">Chcete-li dokončit, proveďte požadované změny žádosti o služby a pak vyberte **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="9da42-112">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9da42-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9da42-113">Prerequisites</span></span>

- <span data-ttu-id="9da42-114">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9da42-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9da42-115">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="9da42-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9da42-116">ID žádosti o službu.</span><span class="sxs-lookup"><span data-stu-id="9da42-116">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="9da42-117">C\#</span><span class="sxs-lookup"><span data-stu-id="9da42-117">C\#</span></span>

<span data-ttu-id="9da42-118">Chcete-li aktualizovat žádost o služby zákazníka, zavolejte metodu [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) s ID žádosti služby a identifikujte a vraťte rozhraní žádosti o služby.</span><span class="sxs-lookup"><span data-stu-id="9da42-118">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request id to identify and return the service request interface.</span></span> <span data-ttu-id="9da42-119">Pak zavolejte metodu [**IServiceRequest. patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) nebo [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) a aktualizujte žádost o službu.</span><span class="sxs-lookup"><span data-stu-id="9da42-119">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="9da42-120">Chcete-li zadat aktualizované hodnoty, vytvořte nový prázdný objekt [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) a nastavte pouze hodnoty vlastností, které chcete změnit.</span><span class="sxs-lookup"><span data-stu-id="9da42-120">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="9da42-121">Pak předejte tento objekt ve volání metody patch nebo PatchAsync.</span><span class="sxs-lookup"><span data-stu-id="9da42-121">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="9da42-122">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9da42-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9da42-123">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdatePartnerServiceRequest.cs</span><span class="sxs-lookup"><span data-stu-id="9da42-123">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9da42-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="9da42-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9da42-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="9da42-125">Request syntax</span></span>

| <span data-ttu-id="9da42-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="9da42-126">Method</span></span>    | <span data-ttu-id="9da42-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9da42-127">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="9da42-128">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="9da42-128">**PATCH**</span></span> | <span data-ttu-id="9da42-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{ServiceRequest-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9da42-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9da42-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9da42-130">URI parameter</span></span>

<span data-ttu-id="9da42-131">K aktualizaci žádosti o službu použijte následující parametr identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="9da42-131">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="9da42-132">Název</span><span class="sxs-lookup"><span data-stu-id="9da42-132">Name</span></span>                  | <span data-ttu-id="9da42-133">Typ</span><span class="sxs-lookup"><span data-stu-id="9da42-133">Type</span></span>     | <span data-ttu-id="9da42-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9da42-134">Required</span></span> | <span data-ttu-id="9da42-135">Popis</span><span class="sxs-lookup"><span data-stu-id="9da42-135">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="9da42-136">**ServiceRequest-ID**</span><span class="sxs-lookup"><span data-stu-id="9da42-136">**servicerequest-id**</span></span> | <span data-ttu-id="9da42-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="9da42-137">**guid**</span></span> | <span data-ttu-id="9da42-138">Y</span><span class="sxs-lookup"><span data-stu-id="9da42-138">Y</span></span>        | <span data-ttu-id="9da42-139">Identifikátor GUID, který identifikuje požadavek služby.</span><span class="sxs-lookup"><span data-stu-id="9da42-139">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9da42-140">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9da42-140">Request headers</span></span>

<span data-ttu-id="9da42-141">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9da42-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9da42-142">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9da42-142">Request body</span></span>

<span data-ttu-id="9da42-143">Text žádosti by měl obsahovat prostředek [ServiceRequest](service-request-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="9da42-143">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="9da42-144">Jediné požadované hodnoty jsou ty, které se mají aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="9da42-144">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="9da42-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9da42-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9da42-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9da42-146">REST response</span></span>

<span data-ttu-id="9da42-147">V případě úspěchu tato metoda vrátí prostředek **žádosti o službu** s aktualizovanými vlastnostmi v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9da42-147">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9da42-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="9da42-148">Response success and error codes</span></span>

<span data-ttu-id="9da42-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9da42-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9da42-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="9da42-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9da42-151">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9da42-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9da42-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9da42-152">Response example</span></span>

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
