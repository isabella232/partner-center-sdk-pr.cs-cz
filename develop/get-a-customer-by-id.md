---
title: Získání zákazníka podle ID
description: Získá prostředek zákazníka, který odpovídá ID zákazníka.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 196d653c789c4b4e1327f0c6e5d2531a18681a71
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874988"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="e6813-103">Získání zákazníka podle ID</span><span class="sxs-lookup"><span data-stu-id="e6813-103">Get a customer by ID</span></span>

<span data-ttu-id="e6813-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e6813-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e6813-105">Získá **prostředek zákazníka,** který odpovídá ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6813-105">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6813-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e6813-106">Prerequisites</span></span>

- <span data-ttu-id="e6813-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e6813-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e6813-108">Tento scénář podporuje přihlašovací údaje aplikace a uživatele nebo ověřování pouze na základě aplikace.</span><span class="sxs-lookup"><span data-stu-id="e6813-108">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="e6813-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6813-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e6813-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e6813-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e6813-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="e6813-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e6813-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="e6813-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e6813-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6813-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e6813-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6813-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e6813-115">C\#</span><span class="sxs-lookup"><span data-stu-id="e6813-115">C\#</span></span>

<span data-ttu-id="e6813-116">Pokud chcete získat zákazníka podle ID, použijte kolekci [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) zavolejte metodu [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) a pak zavolejte metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync)</span><span class="sxs-lookup"><span data-stu-id="e6813-116">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="e6813-117">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e6813-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e6813-118">**Project:** PartnerSDK.FeatureSamples **– třída:** CustomerInformation.cs</span><span class="sxs-lookup"><span data-stu-id="e6813-118">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="e6813-119">Java</span><span class="sxs-lookup"><span data-stu-id="e6813-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e6813-120">Pokud chcete získat zákazníka podle ID, použijte funkci **IAggregatePartner.getCustomers,** zavolejte funkci **byId()** a pak zavolejte **funkci get().**</span><span class="sxs-lookup"><span data-stu-id="e6813-120">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="e6813-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6813-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e6813-122">Pokud chcete získat zákazníka podle ID, spusťte příkaz [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) a zadejte **parametr CustomerId.**</span><span class="sxs-lookup"><span data-stu-id="e6813-122">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="e6813-123">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="e6813-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e6813-124">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="e6813-124">Request syntax</span></span>

| <span data-ttu-id="e6813-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="e6813-125">Method</span></span>  | <span data-ttu-id="e6813-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e6813-126">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="e6813-127">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="e6813-127">**GET**</span></span> | <span data-ttu-id="e6813-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e6813-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e6813-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e6813-129">URI parameter</span></span>

<span data-ttu-id="e6813-130">Pro konkrétního zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="e6813-130">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="e6813-131">Název</span><span class="sxs-lookup"><span data-stu-id="e6813-131">Name</span></span>                   | <span data-ttu-id="e6813-132">Typ</span><span class="sxs-lookup"><span data-stu-id="e6813-132">Type</span></span>     | <span data-ttu-id="e6813-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e6813-133">Required</span></span> | <span data-ttu-id="e6813-134">Popis</span><span class="sxs-lookup"><span data-stu-id="e6813-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e6813-135">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="e6813-135">**customer-tenant-id**</span></span> | <span data-ttu-id="e6813-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="e6813-136">**guid**</span></span> | <span data-ttu-id="e6813-137">Y</span><span class="sxs-lookup"><span data-stu-id="e6813-137">Y</span></span>        | <span data-ttu-id="e6813-138">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="e6813-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e6813-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e6813-139">Request headers</span></span>

<span data-ttu-id="e6813-140">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e6813-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e6813-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e6813-141">Request body</span></span>

<span data-ttu-id="e6813-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="e6813-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e6813-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e6813-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="e6813-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e6813-144">REST response</span></span>

<span data-ttu-id="e6813-145">V případě úspěchu vrátí tato metoda [v](customer-resources.md#customer) textu odpovědi prostředek Customer.</span><span class="sxs-lookup"><span data-stu-id="e6813-145">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e6813-146">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="e6813-146">Response success and error codes</span></span>

<span data-ttu-id="e6813-147">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e6813-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e6813-148">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="e6813-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e6813-149">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e6813-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e6813-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e6813-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1530
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b

{
  "id": "eebd1b55-5360-4438-a11d-5c06918c3014",
  "commerceId": "99e6a635-48e7-424d-9059-c9db944e3c54",
  "companyProfile": {
    "tenantId": "eebd1b55-5360-4438-a11d-5c06918c3014",
    "domain": "abcdefgh1234.ccsctp.net",
    "companyName": "1kl as kjk",
    "address": {
      "country": "US",
      "region": "wa",
      "city": "redmond",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "phoneNumber": "1234567890"
    },
    "email": "a@a.com",
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/company",
        "method": "GET",
        "headers": []
      }
    },
    "attributes": {
      "objectType": "CustomerCompanyProfile"
    }
  },
  "billingProfile": {
    "id": "eeada110-69d6-4cc9-b093-75feb7ca9d3f",
    "firstName": "d0d89d776d03471c819bf772191ed728",
    "lastName": "kjkAJJAAAAAAAAAAAAAAAAAAAA",
    "email": "a@a.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "1kl as kjkAAAAAAAAAAAAAAAJJJJJJJJJJJAAAAAJJJJJJJJJJJAAJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJAJJJJJAJJAAAAJAJJAAAAAAAAAAAAAAAAAAAA",
    "defaultAddress": {
      "country": "US",
      "city": "redmond",
      "state": "WA",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "firstName": "1kl as",
      "lastName": "kjk",
      "phoneNumber": "1234567890"
    },
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/billing",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "etag": "-4242348048554929329",
      "objectType": "CustomerBillingProfile"
    }
  },
  "relationshipToPartner": "reseller",
  "allowDelegatedAccess": true,
  "customDomains": [
    "abcdefgh1234.ccsctp.net"
  ],
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Customer"
  }
}
```
