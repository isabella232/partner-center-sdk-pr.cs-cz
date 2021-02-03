---
title: Získá všechny měsíční záznamy o využití pro předplatné.
description: Pomocí kolekce prostředků AzureResourceMonthlyUsageRecord můžete získat seznam služeb v rámci předplatného zákazníka a jejich přidružených informací o využití.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1dd09d4976c9626e088cda02ce36669dd7121a99
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766996"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="b240d-103">Získá všechny měsíční záznamy o využití pro předplatné.</span><span class="sxs-lookup"><span data-stu-id="b240d-103">Get all monthly usage records for a subscription.</span></span>

<span data-ttu-id="b240d-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="b240d-104">**Applies to:**</span></span>

- <span data-ttu-id="b240d-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b240d-105">Partner Center</span></span>
- <span data-ttu-id="b240d-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="b240d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b240d-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b240d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b240d-108">Pomocí kolekce prostředků [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) můžete získat seznam služeb v rámci předplatného zákazníka a jejich přidružených informací o využití.</span><span class="sxs-lookup"><span data-stu-id="b240d-108">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b240d-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b240d-109">Prerequisites</span></span>

- <span data-ttu-id="b240d-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b240d-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b240d-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="b240d-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b240d-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b240d-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b240d-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b240d-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b240d-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b240d-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b240d-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b240d-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b240d-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b240d-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b240d-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b240d-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b240d-118">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="b240d-118">A subscription identifier.</span></span>

<span data-ttu-id="b240d-119">*Toto rozhraní API podporuje jenom odběry Microsoft Azure (MS-AZR-0145P). Pokud používáte plán Azure, přečtěte si místo toho část [získat data o využití pro předplatné podle měřičů](get-a-customer-subscription-meter-usage-records.md) .*</span><span class="sxs-lookup"><span data-stu-id="b240d-119">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="b240d-120">C\#</span><span class="sxs-lookup"><span data-stu-id="b240d-120">C\#</span></span>

<span data-ttu-id="b240d-121">Získání informací o využití prostředků u předplatného:</span><span class="sxs-lookup"><span data-stu-id="b240d-121">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="b240d-122">Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="b240d-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="b240d-123">Zavolejte vlastnost **Subscriptions** a také **UsageRecords** a pak vlastnost **Resources (prostředky** ).</span><span class="sxs-lookup"><span data-stu-id="b240d-123">Call the **Subscriptions** property, as well as **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="b240d-124">Zavolejte metody **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="b240d-124">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="b240d-125">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="b240d-125">For an example, see the following:</span></span>

- <span data-ttu-id="b240d-126">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="b240d-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="b240d-127">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="b240d-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="b240d-128">Třída: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="b240d-128">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="b240d-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b240d-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b240d-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b240d-130">Request syntax</span></span>

| <span data-ttu-id="b240d-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="b240d-131">Method</span></span>  | <span data-ttu-id="b240d-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b240d-132">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b240d-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b240d-133">**GET**</span></span> | <span data-ttu-id="b240d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription}/usagerecords/Resources HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b240d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b240d-135">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="b240d-135">URI parameters</span></span>

<span data-ttu-id="b240d-136">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o hodnocení využití.</span><span class="sxs-lookup"><span data-stu-id="b240d-136">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="b240d-137">Název</span><span class="sxs-lookup"><span data-stu-id="b240d-137">Name</span></span>                    | <span data-ttu-id="b240d-138">Typ</span><span class="sxs-lookup"><span data-stu-id="b240d-138">Type</span></span>     | <span data-ttu-id="b240d-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b240d-139">Required</span></span> | <span data-ttu-id="b240d-140">Popis</span><span class="sxs-lookup"><span data-stu-id="b240d-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="b240d-141">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="b240d-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="b240d-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="b240d-142">**guid**</span></span> | <span data-ttu-id="b240d-143">Y</span><span class="sxs-lookup"><span data-stu-id="b240d-143">Y</span></span>        | <span data-ttu-id="b240d-144">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="b240d-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="b240d-145">**ID předplatného**</span><span class="sxs-lookup"><span data-stu-id="b240d-145">**subscription-id**</span></span> | <span data-ttu-id="b240d-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="b240d-146">**guid**</span></span> | <span data-ttu-id="b240d-147">Y</span><span class="sxs-lookup"><span data-stu-id="b240d-147">Y</span></span>        | <span data-ttu-id="b240d-148">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="b240d-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b240d-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b240d-149">Request headers</span></span>

<span data-ttu-id="b240d-150">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b240d-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b240d-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b240d-151">Request body</span></span>

<span data-ttu-id="b240d-152">Žádné</span><span class="sxs-lookup"><span data-stu-id="b240d-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b240d-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b240d-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="b240d-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b240d-154">REST response</span></span>

<span data-ttu-id="b240d-155">V případě úspěchu tato metoda vrátí kolekci prostředků **AzureResourceMonthlyUsageRecord** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b240d-155">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b240d-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b240d-156">Response success and error codes</span></span>

<span data-ttu-id="b240d-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b240d-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b240d-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b240d-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b240d-159">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b240d-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b240d-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b240d-160">Response example</span></span>

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
