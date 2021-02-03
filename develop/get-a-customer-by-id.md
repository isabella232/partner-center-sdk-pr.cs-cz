---
title: Získání zákazníka podle ID
description: Získá zdroj zákazníka, který odpovídá ID zákazníka.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: dd4301dbb6f749b675fe624daf7f63751806f856
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766877"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="6c5b4-103">Získání zákazníka podle ID</span><span class="sxs-lookup"><span data-stu-id="6c5b4-103">Get a customer by ID</span></span>

<span data-ttu-id="6c5b4-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="6c5b4-104">**Applies To**</span></span>

- <span data-ttu-id="6c5b4-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="6c5b4-105">Partner Center</span></span>
- <span data-ttu-id="6c5b4-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="6c5b4-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="6c5b4-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="6c5b4-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6c5b4-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6c5b4-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6c5b4-109">Získá zdroj **zákazníka** , který odpovídá ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-109">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c5b4-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6c5b4-110">Prerequisites</span></span>

- <span data-ttu-id="6c5b4-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6c5b4-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6c5b4-112">Tento scénář podporuje přihlašovací údaje aplikace + uživatele nebo ověřování jen pro aplikace.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-112">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="6c5b4-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6c5b4-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6c5b4-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6c5b4-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6c5b4-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6c5b4-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="6c5b4-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6c5b4-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6c5b4-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6c5b4-119">C\#</span><span class="sxs-lookup"><span data-stu-id="6c5b4-119">C\#</span></span>

<span data-ttu-id="6c5b4-120">Chcete-li získat zákazníka podle ID, použijte svou kolekci [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) a potom zavolejte metody [**Get (**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) ) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) .</span><span class="sxs-lookup"><span data-stu-id="6c5b4-120">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="6c5b4-121">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6c5b4-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6c5b4-122">**Projekt**: PartnerSDK. FeatureSamples **Třída**: CustomerInformation.cs</span><span class="sxs-lookup"><span data-stu-id="6c5b4-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="6c5b4-123">Java</span><span class="sxs-lookup"><span data-stu-id="6c5b4-123">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="6c5b4-124">Chcete-li získat zákazníka podle ID, použijte funkci **IAggregatePartner. GetCustomers** , zavolejte funkci **byId ()** a zavolejte funkci **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="6c5b4-124">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="6c5b4-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c5b4-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="6c5b4-126">Chcete-li získat zákazníka podle ID, spusťte příkaz [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) a zadejte parametr **CustomerID** .</span><span class="sxs-lookup"><span data-stu-id="6c5b4-126">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="6c5b4-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="6c5b4-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6c5b4-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="6c5b4-128">Request syntax</span></span>

| <span data-ttu-id="6c5b4-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="6c5b4-129">Method</span></span>  | <span data-ttu-id="6c5b4-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="6c5b4-130">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="6c5b4-131">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="6c5b4-131">**GET**</span></span> | <span data-ttu-id="6c5b4-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6c5b4-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6c5b4-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="6c5b4-133">URI parameter</span></span>

<span data-ttu-id="6c5b4-134">Pro konkrétního zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-134">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="6c5b4-135">Název</span><span class="sxs-lookup"><span data-stu-id="6c5b4-135">Name</span></span>                   | <span data-ttu-id="6c5b4-136">Typ</span><span class="sxs-lookup"><span data-stu-id="6c5b4-136">Type</span></span>     | <span data-ttu-id="6c5b4-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="6c5b4-137">Required</span></span> | <span data-ttu-id="6c5b4-138">Popis</span><span class="sxs-lookup"><span data-stu-id="6c5b4-138">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6c5b4-139">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="6c5b4-139">**customer-tenant-id**</span></span> | <span data-ttu-id="6c5b4-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="6c5b4-140">**guid**</span></span> | <span data-ttu-id="6c5b4-141">Y</span><span class="sxs-lookup"><span data-stu-id="6c5b4-141">Y</span></span>        | <span data-ttu-id="6c5b4-142">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-142">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6c5b4-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="6c5b4-143">Request headers</span></span>

<span data-ttu-id="6c5b4-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6c5b4-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6c5b4-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="6c5b4-145">Request body</span></span>

<span data-ttu-id="6c5b4-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="6c5b4-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6c5b4-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="6c5b4-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="6c5b4-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="6c5b4-148">REST response</span></span>

<span data-ttu-id="6c5b4-149">V případě úspěchu tato metoda vrátí prostředek [zákazníka](customer-resources.md#customer) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-149">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6c5b4-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="6c5b4-150">Response success and error codes</span></span>

<span data-ttu-id="6c5b4-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6c5b4-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="6c5b4-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6c5b4-153">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6c5b4-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6c5b4-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="6c5b4-154">Response example</span></span>

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
