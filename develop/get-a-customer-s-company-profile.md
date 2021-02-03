---
title: Získání firemního profilu zákazníka
description: Získá profil společnosti zákazníka.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c26a86ecb96e5e7942ba179f8a3cc704abab7df5
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766875"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="ce3fd-103">Získání firemního profilu zákazníka</span><span class="sxs-lookup"><span data-stu-id="ce3fd-103">Get a customer's company profile</span></span>

<span data-ttu-id="ce3fd-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="ce3fd-104">**Applies To**</span></span>

- <span data-ttu-id="ce3fd-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="ce3fd-105">Partner Center</span></span>
- <span data-ttu-id="ce3fd-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="ce3fd-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ce3fd-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="ce3fd-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ce3fd-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ce3fd-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ce3fd-109">Získá profil společnosti zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-109">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce3fd-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ce3fd-110">Prerequisites</span></span>

- <span data-ttu-id="ce3fd-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ce3fd-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ce3fd-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ce3fd-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ce3fd-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ce3fd-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ce3fd-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ce3fd-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ce3fd-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="ce3fd-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ce3fd-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ce3fd-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ce3fd-119">C\#</span><span class="sxs-lookup"><span data-stu-id="ce3fd-119">C\#</span></span>

<span data-ttu-id="ce3fd-120">Chcete-li získat profil společnosti pro zákazníka, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka pro identifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-120">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ce3fd-121">Pak Získejte rozhraní [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) zákazníka z vlastnosti [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) , aby bylo možné získat přístup k vlastnosti společnosti.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-121">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="ce3fd-122">Dále Získejte rozhraní [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) z vlastnosti [**ICustomerProfileCollection. Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) a zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) .</span><span class="sxs-lookup"><span data-stu-id="ce3fd-122">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="ce3fd-123">**Ukázka**: [Stáhněte si sadu SDK partnerského centra](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span><span class="sxs-lookup"><span data-stu-id="ce3fd-123">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="ce3fd-124">**Projekt**: PartnerSdk. FeatureSamples **Třída**: GetCustomerCompanyProfile.cs</span><span class="sxs-lookup"><span data-stu-id="ce3fd-124">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="ce3fd-125">Java</span><span class="sxs-lookup"><span data-stu-id="ce3fd-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="ce3fd-126">Chcete-li získat profil společnosti pro zákazníka, zavolejte funkci **IAggregatePartner. GetCustomers (). byId** s identifikátorem zákazníka a Identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-126">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="ce3fd-127">Pak Získejte rozhraní **ICustomerProfileCollection** zákazníka ze funkce [**getprofiles**], aby bylo možné získat přístup k vlastnosti společnosti.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-127">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="ce3fd-128">Dále Získejte rozhraní **ICustomerReadonlyProfile** z funkce **ICustomerProfileCollection. getcompany** a zavolejte funkci **Get** .</span><span class="sxs-lookup"><span data-stu-id="ce3fd-128">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="ce3fd-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ce3fd-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ce3fd-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ce3fd-130">Request syntax</span></span>

| <span data-ttu-id="ce3fd-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="ce3fd-131">Method</span></span>  | <span data-ttu-id="ce3fd-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ce3fd-132">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="ce3fd-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="ce3fd-133">**GET**</span></span> | <span data-ttu-id="ce3fd-134">*{baseURL}*/v1/Customers/{Customer-tenant-ID}/Profiles/Company HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ce3fd-134">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ce3fd-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ce3fd-135">URI parameter</span></span>

<span data-ttu-id="ce3fd-136">K získání profilu společnosti použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-136">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="ce3fd-137">Název</span><span class="sxs-lookup"><span data-stu-id="ce3fd-137">Name</span></span>                   | <span data-ttu-id="ce3fd-138">Typ</span><span class="sxs-lookup"><span data-stu-id="ce3fd-138">Type</span></span>     | <span data-ttu-id="ce3fd-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ce3fd-139">Required</span></span> | <span data-ttu-id="ce3fd-140">Popis</span><span class="sxs-lookup"><span data-stu-id="ce3fd-140">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ce3fd-141">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="ce3fd-141">**customer-tenant-id**</span></span> | <span data-ttu-id="ce3fd-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="ce3fd-142">**guid**</span></span> | <span data-ttu-id="ce3fd-143">Y</span><span class="sxs-lookup"><span data-stu-id="ce3fd-143">Y</span></span>        | <span data-ttu-id="ce3fd-144">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-144">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ce3fd-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ce3fd-145">Request headers</span></span>

<span data-ttu-id="ce3fd-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ce3fd-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ce3fd-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ce3fd-147">Request body</span></span>

<span data-ttu-id="ce3fd-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="ce3fd-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="ce3fd-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ce3fd-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="ce3fd-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ce3fd-150">REST response</span></span>

<span data-ttu-id="ce3fd-151">V případě úspěchu vrátí tato metoda informace v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-151">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ce3fd-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ce3fd-152">Response success and error codes</span></span>

<span data-ttu-id="ce3fd-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ce3fd-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ce3fd-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ce3fd-155">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ce3fd-155">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ce3fd-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ce3fd-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```
