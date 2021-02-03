---
title: Získat Souhrn využití všech předplatných zákazníka
description: Pomocí prostředku CustomerUsageSummary můžete získat od zákazníka používání konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c918434367a3514e6a6ad6034b4897c33f51025
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766794"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="4cdf4-103">Získat Souhrn využití všech předplatných zákazníka</span><span class="sxs-lookup"><span data-stu-id="4cdf4-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="4cdf4-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="4cdf4-104">**Applies to:**</span></span>

- <span data-ttu-id="4cdf4-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="4cdf4-105">Partner Center</span></span>
- <span data-ttu-id="4cdf4-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="4cdf4-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4cdf4-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4cdf4-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4cdf4-108">Pomocí prostředku **CustomerUsageSummary** můžete získat od zákazníka používání konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-108">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cdf4-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4cdf4-109">Prerequisites</span></span>

- <span data-ttu-id="4cdf4-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4cdf4-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4cdf4-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4cdf4-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4cdf4-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4cdf4-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4cdf4-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4cdf4-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4cdf4-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="4cdf4-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4cdf4-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4cdf4-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="4cdf4-118">C\#</span><span class="sxs-lookup"><span data-stu-id="4cdf4-118">C\#</span></span>

<span data-ttu-id="4cdf4-119">Získání souhrnu využití pro všechny předplatná zákazníka:</span><span class="sxs-lookup"><span data-stu-id="4cdf4-119">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="4cdf4-120">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="4cdf4-120">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="4cdf4-121">Zavolejte vlastnost **UsageSummary** , za kterou následují metody **Get ()** nebo **GetAsync ()** :</span><span class="sxs-lookup"><span data-stu-id="4cdf4-121">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="4cdf4-122">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="4cdf4-122">For an example, see the following:</span></span>

- <span data-ttu-id="4cdf4-123">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4cdf4-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="4cdf4-124">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="4cdf4-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="4cdf4-125">Třída: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="4cdf4-125">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="4cdf4-126">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="4cdf4-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4cdf4-127">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="4cdf4-127">Request syntax</span></span>

| <span data-ttu-id="4cdf4-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="4cdf4-128">Method</span></span>  | <span data-ttu-id="4cdf4-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="4cdf4-129">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4cdf4-130">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="4cdf4-130">**GET**</span></span> | <span data-ttu-id="4cdf4-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4cdf4-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="4cdf4-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="4cdf4-132">URI parameter</span></span>

<span data-ttu-id="4cdf4-133">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o využití ohodnocených zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="4cdf4-134">Název</span><span class="sxs-lookup"><span data-stu-id="4cdf4-134">Name</span></span>                   | <span data-ttu-id="4cdf4-135">Typ</span><span class="sxs-lookup"><span data-stu-id="4cdf4-135">Type</span></span>     | <span data-ttu-id="4cdf4-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="4cdf4-136">Required</span></span> | <span data-ttu-id="4cdf4-137">Popis</span><span class="sxs-lookup"><span data-stu-id="4cdf4-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="4cdf4-138">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="4cdf4-138">**customer-tenant-id**</span></span> | <span data-ttu-id="4cdf4-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="4cdf4-139">**guid**</span></span> | <span data-ttu-id="4cdf4-140">Y</span><span class="sxs-lookup"><span data-stu-id="4cdf4-140">Y</span></span>        | <span data-ttu-id="4cdf4-141">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4cdf4-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="4cdf4-142">Request headers</span></span>

<span data-ttu-id="4cdf4-143">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4cdf4-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4cdf4-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="4cdf4-144">Request body</span></span>

<span data-ttu-id="4cdf4-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="4cdf4-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4cdf4-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="4cdf4-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="4cdf4-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="4cdf4-147">REST response</span></span>

<span data-ttu-id="4cdf4-148">V případě úspěchu tato metoda vrátí prostředek **CustomerUsageSummary** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-148">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4cdf4-149">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="4cdf4-149">Response success and error codes</span></span>

<span data-ttu-id="4cdf4-150">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4cdf4-151">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="4cdf4-152">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4cdf4-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="4cdf4-153">Příklad odpovědi pro předplatné služby Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="4cdf4-153">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="4cdf4-154">V tomto příkladu si zákazník koupil nabídku **145P Azure PayG** .</span><span class="sxs-lookup"><span data-stu-id="4cdf4-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="4cdf4-155">*Pro zákazníky s předplatnými Microsoft Azure (MS-AZR-0145P) nedojde k žádné změně v odpovědi rozhraní API.*</span><span class="sxs-lookup"><span data-stu-id="4cdf4-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="4cdf4-156">Příklad odpovědi pro plán Azure</span><span class="sxs-lookup"><span data-stu-id="4cdf4-156">Response example for Azure plan</span></span>

<span data-ttu-id="4cdf4-157">V tomto příkladu si zákazník koupil plán Azure.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="4cdf4-158">*Pro zákazníky s plány Azure jsou v odpovědi rozhraní API tyto změny:*</span><span class="sxs-lookup"><span data-stu-id="4cdf4-158">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="4cdf4-159">**currencyLocale** se nahrazuje **currencyCode**</span><span class="sxs-lookup"><span data-stu-id="4cdf4-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="4cdf4-160">**usdTotalCost** je nové pole.</span><span class="sxs-lookup"><span data-stu-id="4cdf4-160">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
