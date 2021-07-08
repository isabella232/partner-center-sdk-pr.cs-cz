---
title: Získání fakturačního profilu zákazníka
description: Získá Fakturační profil zákazníka. Na řídicím panelu partnerského centra se tato operace dá provést při prvním výběru zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d22be53a5be4efcda76a568578468615495febb6
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760585"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="57b7a-104">Získání fakturačního profilu zákazníka</span><span class="sxs-lookup"><span data-stu-id="57b7a-104">Get a customer's billing profile</span></span>

<span data-ttu-id="57b7a-105">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="57b7a-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="57b7a-106">Získá Fakturační profil zákazníka.</span><span class="sxs-lookup"><span data-stu-id="57b7a-106">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="57b7a-107">Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="57b7a-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="57b7a-108">Pak pod jménem zákazníka na levém bočním panelu vyberte **účet**.</span><span class="sxs-lookup"><span data-stu-id="57b7a-108">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="57b7a-109">Fakturační profil najdete pod nadpisem **informace** o fakturaci.</span><span class="sxs-lookup"><span data-stu-id="57b7a-109">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57b7a-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="57b7a-110">Prerequisites</span></span>

- <span data-ttu-id="57b7a-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="57b7a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="57b7a-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="57b7a-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="57b7a-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="57b7a-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="57b7a-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="57b7a-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="57b7a-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="57b7a-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="57b7a-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="57b7a-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="57b7a-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="57b7a-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="57b7a-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="57b7a-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="57b7a-119">C\#</span><span class="sxs-lookup"><span data-stu-id="57b7a-119">C\#</span></span>

<span data-ttu-id="57b7a-120">Pokud chcete získat Fakturační profil zákazníka, použijte svou kolekci [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="57b7a-120">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="57b7a-121">Pak zavolejte vlastnost [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) a vlastnost [**fakturace**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) .</span><span class="sxs-lookup"><span data-stu-id="57b7a-121">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="57b7a-122">Nakonec zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) .</span><span class="sxs-lookup"><span data-stu-id="57b7a-122">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="57b7a-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="57b7a-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="57b7a-124">**Project**: PartnerSDK. FeatureSamples **třída**: GetCustomerBillingProfile. cs</span><span class="sxs-lookup"><span data-stu-id="57b7a-124">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="57b7a-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="57b7a-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="57b7a-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="57b7a-126">Request syntax</span></span>

| <span data-ttu-id="57b7a-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="57b7a-127">Method</span></span>  | <span data-ttu-id="57b7a-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="57b7a-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="57b7a-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="57b7a-129">**GET**</span></span> | <span data-ttu-id="57b7a-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Profiles/Billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="57b7a-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="57b7a-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="57b7a-131">URI parameter</span></span>

<span data-ttu-id="57b7a-132">K získání fakturačního profilu použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="57b7a-132">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="57b7a-133">Název</span><span class="sxs-lookup"><span data-stu-id="57b7a-133">Name</span></span>                   | <span data-ttu-id="57b7a-134">Typ</span><span class="sxs-lookup"><span data-stu-id="57b7a-134">Type</span></span>     | <span data-ttu-id="57b7a-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="57b7a-135">Required</span></span> | <span data-ttu-id="57b7a-136">Popis</span><span class="sxs-lookup"><span data-stu-id="57b7a-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="57b7a-137">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="57b7a-137">**customer-tenant-id**</span></span> | <span data-ttu-id="57b7a-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="57b7a-138">**guid**</span></span> | <span data-ttu-id="57b7a-139">Y</span><span class="sxs-lookup"><span data-stu-id="57b7a-139">Y</span></span>        | <span data-ttu-id="57b7a-140">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="57b7a-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="57b7a-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="57b7a-141">Request headers</span></span>

<span data-ttu-id="57b7a-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="57b7a-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="57b7a-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="57b7a-143">Request body</span></span>

<span data-ttu-id="57b7a-144">Žádná</span><span class="sxs-lookup"><span data-stu-id="57b7a-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="57b7a-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="57b7a-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="57b7a-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="57b7a-146">REST response</span></span>

<span data-ttu-id="57b7a-147">V případě úspěchu tato metoda vrátí kolekci prostředků [profilu](profile-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="57b7a-147">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="57b7a-148">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="57b7a-148">Response success and error codes</span></span>

<span data-ttu-id="57b7a-149">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="57b7a-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="57b7a-150">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="57b7a-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="57b7a-151">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="57b7a-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="57b7a-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="57b7a-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
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
