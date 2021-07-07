---
title: Získání všech záznamů o měsíčním využití pro předplatné
description: Pomocí kolekce prostředků AzureResourceMonthlyUsageRecord můžete získat seznam služeb v rámci předplatného zákazníka a informace o jejich přidruženém hodnocení využití.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ee4bd413eec7d5a2dddbe3803df8839589ab7504
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760279"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="2d7db-103">Získání všech záznamů o měsíčním využití pro předplatné</span><span class="sxs-lookup"><span data-stu-id="2d7db-103">Get all monthly usage records for a subscription</span></span>

<span data-ttu-id="2d7db-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2d7db-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2d7db-105">Pomocí kolekce prostředků [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) můžete získat seznam služeb v rámci předplatného zákazníka a informace o jejich přidruženém hodnocení využití.</span><span class="sxs-lookup"><span data-stu-id="2d7db-105">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d7db-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2d7db-106">Prerequisites</span></span>

- <span data-ttu-id="2d7db-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2d7db-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2d7db-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="2d7db-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2d7db-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2d7db-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2d7db-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2d7db-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2d7db-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="2d7db-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2d7db-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="2d7db-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2d7db-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d7db-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2d7db-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2d7db-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2d7db-115">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="2d7db-115">A subscription identifier.</span></span>

<span data-ttu-id="2d7db-116">*Toto rozhraní API podporuje Microsoft Azure předplatná MS-AZR-0145P. Pokud používáte plán Azure, podívejte se místo toho na získání dat o využití [pro předplatné podle měřiče.](get-a-customer-subscription-meter-usage-records.md)*</span><span class="sxs-lookup"><span data-stu-id="2d7db-116">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="2d7db-117">C\#</span><span class="sxs-lookup"><span data-stu-id="2d7db-117">C\#</span></span>

<span data-ttu-id="2d7db-118">Získání informací o využití prostředků předplatného:</span><span class="sxs-lookup"><span data-stu-id="2d7db-118">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="2d7db-119">K volání metody **ById()** použijte kolekci **IAggregatePartner.Customers.**</span><span class="sxs-lookup"><span data-stu-id="2d7db-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="2d7db-120">Zavolejte **vlastnost Subscriptions** a **UsageRecords** a pak **vlastnost Resources.**</span><span class="sxs-lookup"><span data-stu-id="2d7db-120">Call the **Subscriptions** property, and **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="2d7db-121">Volejte **metody Get()** nebo **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="2d7db-121">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="2d7db-122">Příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="2d7db-122">For an example, see the following:</span></span>

- <span data-ttu-id="2d7db-123">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2d7db-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="2d7db-124">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="2d7db-124">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="2d7db-125">Třída: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="2d7db-125">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="2d7db-126">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="2d7db-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2d7db-127">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="2d7db-127">Request syntax</span></span>

| <span data-ttu-id="2d7db-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="2d7db-128">Method</span></span>  | <span data-ttu-id="2d7db-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2d7db-129">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2d7db-130">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="2d7db-130">**GET**</span></span> | <span data-ttu-id="2d7db-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{id-pro-předplatné}/usagerecords/resources HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2d7db-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2d7db-132">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="2d7db-132">URI parameters</span></span>

<span data-ttu-id="2d7db-133">Tato tabulka obsahuje seznam požadovaných parametrů dotazu k získání informací o hodnocení využití.</span><span class="sxs-lookup"><span data-stu-id="2d7db-133">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="2d7db-134">Název</span><span class="sxs-lookup"><span data-stu-id="2d7db-134">Name</span></span>                    | <span data-ttu-id="2d7db-135">Typ</span><span class="sxs-lookup"><span data-stu-id="2d7db-135">Type</span></span>     | <span data-ttu-id="2d7db-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="2d7db-136">Required</span></span> | <span data-ttu-id="2d7db-137">Popis</span><span class="sxs-lookup"><span data-stu-id="2d7db-137">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="2d7db-138">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="2d7db-138">**customer-tenant-id**</span></span>  | <span data-ttu-id="2d7db-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="2d7db-139">**guid**</span></span> | <span data-ttu-id="2d7db-140">Y</span><span class="sxs-lookup"><span data-stu-id="2d7db-140">Y</span></span>        | <span data-ttu-id="2d7db-141">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="2d7db-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="2d7db-142">**id předplatného**</span><span class="sxs-lookup"><span data-stu-id="2d7db-142">**subscription-id**</span></span> | <span data-ttu-id="2d7db-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="2d7db-143">**guid**</span></span> | <span data-ttu-id="2d7db-144">Y</span><span class="sxs-lookup"><span data-stu-id="2d7db-144">Y</span></span>        | <span data-ttu-id="2d7db-145">Identifikátor GUID odpovídající předplatnému.</span><span class="sxs-lookup"><span data-stu-id="2d7db-145">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2d7db-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2d7db-146">Request headers</span></span>

<span data-ttu-id="2d7db-147">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2d7db-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2d7db-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2d7db-148">Request body</span></span>

<span data-ttu-id="2d7db-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="2d7db-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2d7db-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="2d7db-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="2d7db-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2d7db-151">REST response</span></span>

<span data-ttu-id="2d7db-152">V případě úspěchu vrátí tato metoda v textu odpovědi kolekci prostředků **AzureResourceMonthlyUsageRecord.**</span><span class="sxs-lookup"><span data-stu-id="2d7db-152">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2d7db-153">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="2d7db-153">Response success and error codes</span></span>

<span data-ttu-id="2d7db-154">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2d7db-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2d7db-155">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="2d7db-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2d7db-156">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2d7db-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2d7db-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="2d7db-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
