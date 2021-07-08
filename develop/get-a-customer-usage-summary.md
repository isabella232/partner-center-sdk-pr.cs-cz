---
title: Získání souhrnu využití pro všechna předplatná zákazníka
description: Prostředek CustomerUsageSummary můžete použít k získání využití konkrétní služby nebo prostředku Azure zákazníkem během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88c69637c94b9263ede6924cf2dd09513aa00f70
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874614"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="d56ce-103">Získání souhrnu využití pro všechna předplatná zákazníka</span><span class="sxs-lookup"><span data-stu-id="d56ce-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="d56ce-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d56ce-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d56ce-105">Prostředek **CustomerUsageSummary** můžete použít k získání využití konkrétní služby nebo prostředku Azure zákazníkem během aktuálního fakturačního období.</span><span class="sxs-lookup"><span data-stu-id="d56ce-105">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d56ce-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d56ce-106">Prerequisites</span></span>

- <span data-ttu-id="d56ce-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d56ce-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d56ce-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d56ce-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d56ce-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d56ce-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d56ce-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d56ce-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d56ce-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="d56ce-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d56ce-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="d56ce-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d56ce-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d56ce-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d56ce-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d56ce-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d56ce-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d56ce-115">C\#</span></span>

<span data-ttu-id="d56ce-116">Získání souhrnu využití pro všechna předplatná zákazníka:</span><span class="sxs-lookup"><span data-stu-id="d56ce-116">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="d56ce-117">K volání metody **ById()** použijte kolekci **IAggregatePartner.Customers.**</span><span class="sxs-lookup"><span data-stu-id="d56ce-117">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="d56ce-118">Zavolejte **vlastnost UsageSummary** následovanou metodami **Get()** nebo **GetAsync():**</span><span class="sxs-lookup"><span data-stu-id="d56ce-118">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="d56ce-119">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="d56ce-119">For an example, see the following:</span></span>

- <span data-ttu-id="d56ce-120">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d56ce-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d56ce-121">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="d56ce-121">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="d56ce-122">Třída: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="d56ce-122">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d56ce-123">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="d56ce-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d56ce-124">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="d56ce-124">Request syntax</span></span>

| <span data-ttu-id="d56ce-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="d56ce-125">Method</span></span>  | <span data-ttu-id="d56ce-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d56ce-126">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d56ce-127">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="d56ce-127">**GET**</span></span> | <span data-ttu-id="d56ce-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d56ce-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d56ce-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="d56ce-129">URI parameter</span></span>

<span data-ttu-id="d56ce-130">Tato tabulka uvádí požadovaný parametr dotazu k získání informací o hodnocených využitích zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d56ce-130">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="d56ce-131">Název</span><span class="sxs-lookup"><span data-stu-id="d56ce-131">Name</span></span>                   | <span data-ttu-id="d56ce-132">Typ</span><span class="sxs-lookup"><span data-stu-id="d56ce-132">Type</span></span>     | <span data-ttu-id="d56ce-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d56ce-133">Required</span></span> | <span data-ttu-id="d56ce-134">Popis</span><span class="sxs-lookup"><span data-stu-id="d56ce-134">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="d56ce-135">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="d56ce-135">**customer-tenant-id**</span></span> | <span data-ttu-id="d56ce-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="d56ce-136">**guid**</span></span> | <span data-ttu-id="d56ce-137">Y</span><span class="sxs-lookup"><span data-stu-id="d56ce-137">Y</span></span>        | <span data-ttu-id="d56ce-138">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="d56ce-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d56ce-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d56ce-139">Request headers</span></span>

<span data-ttu-id="d56ce-140">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d56ce-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d56ce-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d56ce-141">Request body</span></span>

<span data-ttu-id="d56ce-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="d56ce-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d56ce-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d56ce-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="d56ce-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d56ce-144">REST response</span></span>

<span data-ttu-id="d56ce-145">V případě úspěchu vrátí tato metoda v textu odpovědi prostředek **CustomerUsageSummary.**</span><span class="sxs-lookup"><span data-stu-id="d56ce-145">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d56ce-146">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="d56ce-146">Response success and error codes</span></span>

<span data-ttu-id="d56ce-147">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d56ce-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d56ce-148">Ke čtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="d56ce-148">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="d56ce-149">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d56ce-149">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="d56ce-150">Příklad odpovědi Microsoft Azure předplatného (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="d56ce-150">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="d56ce-151">V tomto příkladu zákazník zakoupil nabídku **azure payg 145P.**</span><span class="sxs-lookup"><span data-stu-id="d56ce-151">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="d56ce-152">*U zákazníků Microsoft Azure předplatných (MS-AZR-0145P) se v odpovědi rozhraní API nezmění.*</span><span class="sxs-lookup"><span data-stu-id="d56ce-152">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="d56ce-153">Příklad odpovědi pro plán Azure</span><span class="sxs-lookup"><span data-stu-id="d56ce-153">Response example for Azure plan</span></span>

<span data-ttu-id="d56ce-154">V tomto příkladu zákazník zakoupil plán Azure.</span><span class="sxs-lookup"><span data-stu-id="d56ce-154">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="d56ce-155">*U zákazníků s plány Azure došlo v odpovědi rozhraní API k následujícím změnám:*</span><span class="sxs-lookup"><span data-stu-id="d56ce-155">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="d56ce-156">**currencyLocale** se nahradí **kódem měny**</span><span class="sxs-lookup"><span data-stu-id="d56ce-156">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="d56ce-157">**usdTotalCost** je nové pole</span><span class="sxs-lookup"><span data-stu-id="d56ce-157">**usdTotalCost** is a new field</span></span>

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
