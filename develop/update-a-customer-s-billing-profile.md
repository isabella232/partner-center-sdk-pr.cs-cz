---
title: Aktualizace fakturačního profilu zákazníka
description: Aktualizuje Fakturační profil zákazníka, včetně adresy přidružené k profilu.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: adf4e3de9941fded632e0561624d91d854c5aa24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767010"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="589e7-103">Aktualizace fakturačního profilu zákazníka</span><span class="sxs-lookup"><span data-stu-id="589e7-103">Update a customer's billing profile</span></span>

<span data-ttu-id="589e7-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="589e7-104">**Applies To**</span></span>

- <span data-ttu-id="589e7-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="589e7-105">Partner Center</span></span>
- <span data-ttu-id="589e7-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="589e7-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="589e7-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="589e7-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="589e7-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="589e7-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="589e7-109">Aktualizuje Fakturační profil zákazníka, včetně adresy přidružené k profilu.</span><span class="sxs-lookup"><span data-stu-id="589e7-109">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="589e7-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="589e7-110">Prerequisites</span></span>

- <span data-ttu-id="589e7-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="589e7-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="589e7-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="589e7-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="589e7-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="589e7-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="589e7-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="589e7-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="589e7-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="589e7-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="589e7-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="589e7-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="589e7-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="589e7-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="589e7-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="589e7-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="589e7-119">C\#</span><span class="sxs-lookup"><span data-stu-id="589e7-119">C\#</span></span>

<span data-ttu-id="589e7-120">Pokud chcete aktualizovat fakturační profil zákazníka, načtěte profil fakturace a podle potřeby aktualizujte vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="589e7-120">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="589e7-121">Pak načtěte kolekci [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a potom zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="589e7-121">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="589e7-122">Pak zavolejte vlastnost [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) a vlastnost [**fakturace**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) .</span><span class="sxs-lookup"><span data-stu-id="589e7-122">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="589e7-123">Potom dokončete voláním metod [**Update ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) nebo [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) .</span><span class="sxs-lookup"><span data-stu-id="589e7-123">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="589e7-124">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="589e7-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="589e7-125">**Projekt**: PartnerSDK. FeatureSamples **Třída**: UpdateCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="589e7-125">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="589e7-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="589e7-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="589e7-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="589e7-127">Request syntax</span></span>

| <span data-ttu-id="589e7-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="589e7-128">Method</span></span>  | <span data-ttu-id="589e7-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="589e7-129">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="589e7-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="589e7-130">**PUT**</span></span> | <span data-ttu-id="589e7-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Profiles/Billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="589e7-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="589e7-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="589e7-132">URI parameter</span></span>

<span data-ttu-id="589e7-133">Pro aktualizaci fakturačního profilu použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="589e7-133">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="589e7-134">Název</span><span class="sxs-lookup"><span data-stu-id="589e7-134">Name</span></span>                   | <span data-ttu-id="589e7-135">Typ</span><span class="sxs-lookup"><span data-stu-id="589e7-135">Type</span></span>     | <span data-ttu-id="589e7-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="589e7-136">Required</span></span> | <span data-ttu-id="589e7-137">Popis</span><span class="sxs-lookup"><span data-stu-id="589e7-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="589e7-138">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="589e7-138">**customer-tenant-id**</span></span> | <span data-ttu-id="589e7-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="589e7-139">**guid**</span></span> | <span data-ttu-id="589e7-140">Y</span><span class="sxs-lookup"><span data-stu-id="589e7-140">Y</span></span>        | <span data-ttu-id="589e7-141">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="589e7-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="589e7-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="589e7-142">Request headers</span></span>

- <span data-ttu-id="589e7-143">**If-Match**: &lt; &gt; pro detekci souběžnosti se vyžaduje "ETag".</span><span class="sxs-lookup"><span data-stu-id="589e7-143">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="589e7-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="589e7-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="589e7-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="589e7-145">Request body</span></span>

<span data-ttu-id="589e7-146">Úplný prostředek.</span><span class="sxs-lookup"><span data-stu-id="589e7-146">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="589e7-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="589e7-147">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
Content-Type: application/json
Content-Length: 639
Expect: 100-continue

{
    "Id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "FirstName": "FirstName",
    "LastName": "LastName",
    "Email": "email@sample.com",
    "Culture": "en-US",
    "Language": "en",
    "CompanyName": "CompanyName",
    "DefaultAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "One Microsoft Way",
        "AddressLine2": null,
        "PostalCode": "98052",
        "FirstName": "FirstName",
        "LastName": "LastName",
        "PhoneNumber": "4255555555"
    },
    "Links": {
        "Self": {
            "Uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "CustomerBillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="589e7-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="589e7-148">REST response</span></span>

<span data-ttu-id="589e7-149">V případě úspěchu tato metoda vrátí aktualizované vlastnosti prostředku [profilu](profile-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="589e7-149">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="589e7-150">Toto volání vyžaduje ETag pro detekci souběžnosti.</span><span class="sxs-lookup"><span data-stu-id="589e7-150">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="589e7-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="589e7-151">Response success and error codes</span></span>

<span data-ttu-id="589e7-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="589e7-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="589e7-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="589e7-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="589e7-154">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="589e7-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="589e7-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="589e7-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1210
Content-Type: application/json
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
Date: Mon, 23 Nov 2015 18:20:43 GMT

{
    "id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "companyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "One Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
