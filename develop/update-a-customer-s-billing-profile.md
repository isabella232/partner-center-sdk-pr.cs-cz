---
title: Aktualizace fakturačního profilu zákazníka
description: Aktualizuje fakturační profil zákazníka, včetně adresy přidružené k tomuto profilu.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 1605c3e8cb050717209cb482d2299e2a42b9b186
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530034"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="d9db4-103">Aktualizace fakturačního profilu zákazníka</span><span class="sxs-lookup"><span data-stu-id="d9db4-103">Update a customer's billing profile</span></span>

<span data-ttu-id="d9db4-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d9db4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d9db4-105">Aktualizuje fakturační profil zákazníka, včetně adresy přidružené k tomuto profilu.</span><span class="sxs-lookup"><span data-stu-id="d9db4-105">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9db4-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d9db4-106">Prerequisites</span></span>

- <span data-ttu-id="d9db4-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d9db4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d9db4-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d9db4-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d9db4-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d9db4-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d9db4-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d9db4-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d9db4-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="d9db4-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d9db4-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="d9db4-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d9db4-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d9db4-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d9db4-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d9db4-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d9db4-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d9db4-115">C\#</span></span>

<span data-ttu-id="d9db4-116">Pokud chcete aktualizovat fakturační profil zákazníka, načtěte fakturační profil a podle potřeby aktualizujte vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="d9db4-116">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="d9db4-117">Potom načtěte [**kolekci IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a potom zavolejte [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="d9db4-117">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="d9db4-118">Potom zavolejte [**vlastnost Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) (Profily) a pak vlastnost [**Billing (Fakturace).**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing)</span><span class="sxs-lookup"><span data-stu-id="d9db4-118">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="d9db4-119">Potom dokončete voláním [**metod Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) nebo [**UpdateAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync)</span><span class="sxs-lookup"><span data-stu-id="d9db4-119">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="d9db4-120">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d9db4-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d9db4-121">**Project:** PartnerSDK.FeatureSamples – **třída:** UpdateCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="d9db4-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d9db4-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="d9db4-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d9db4-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="d9db4-123">Request syntax</span></span>

| <span data-ttu-id="d9db4-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="d9db4-124">Method</span></span>  | <span data-ttu-id="d9db4-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d9db4-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d9db4-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="d9db4-126">**PUT**</span></span> | <span data-ttu-id="d9db4-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d9db4-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d9db4-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d9db4-128">URI parameter</span></span>

<span data-ttu-id="d9db4-129">K aktualizaci fakturačního profilu použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="d9db4-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="d9db4-130">Název</span><span class="sxs-lookup"><span data-stu-id="d9db4-130">Name</span></span>                   | <span data-ttu-id="d9db4-131">Typ</span><span class="sxs-lookup"><span data-stu-id="d9db4-131">Type</span></span>     | <span data-ttu-id="d9db4-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d9db4-132">Required</span></span> | <span data-ttu-id="d9db4-133">Popis</span><span class="sxs-lookup"><span data-stu-id="d9db4-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d9db4-134">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="d9db4-134">**customer-tenant-id**</span></span> | <span data-ttu-id="d9db4-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="d9db4-135">**guid**</span></span> | <span data-ttu-id="d9db4-136">Y</span><span class="sxs-lookup"><span data-stu-id="d9db4-136">Y</span></span>        | <span data-ttu-id="d9db4-137">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="d9db4-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d9db4-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d9db4-138">Request headers</span></span>

- <span data-ttu-id="d9db4-139">**Pokud odpovídá :** Pro detekci souběžnosti se vyžaduje &lt; "ETag". &gt;</span><span class="sxs-lookup"><span data-stu-id="d9db4-139">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="d9db4-140">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d9db4-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d9db4-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d9db4-141">Request body</span></span>

<span data-ttu-id="d9db4-142">Úplný prostředek.</span><span class="sxs-lookup"><span data-stu-id="d9db4-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="d9db4-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d9db4-143">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d9db4-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d9db4-144">REST response</span></span>

<span data-ttu-id="d9db4-145">V případě úspěchu vrátí tato metoda [v](profile-resources.md) textu odpovědi aktualizované vlastnosti prostředku profilu.</span><span class="sxs-lookup"><span data-stu-id="d9db4-145">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="d9db4-146">Toto volání vyžaduje ETag pro detekci souběžnosti.</span><span class="sxs-lookup"><span data-stu-id="d9db4-146">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d9db4-147">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="d9db4-147">Response success and error codes</span></span>

<span data-ttu-id="d9db4-148">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d9db4-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d9db4-149">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="d9db4-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d9db4-150">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d9db4-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d9db4-151">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d9db4-151">Response example</span></span>

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
