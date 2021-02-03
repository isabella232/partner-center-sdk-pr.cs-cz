---
title: Získání rozpočtu útraty využití zákazníka
description: Rozpočet útraty (objekt SpendingBudget) můžete použít k aktualizaci souhrnu využití zákazníků (prostředek CustomerUsageSummary).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8be9ceaab6b7546de8eacba1e52e8766719e5125
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766866"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="3fcf7-103">Získání rozpočtu útraty využití zákazníka</span><span class="sxs-lookup"><span data-stu-id="3fcf7-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="3fcf7-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="3fcf7-104">**Applies to:**</span></span>

- <span data-ttu-id="3fcf7-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="3fcf7-105">Partner Center</span></span>
- <span data-ttu-id="3fcf7-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="3fcf7-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3fcf7-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3fcf7-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3fcf7-108">Rozpočet útraty (objekt **SpendingBudget** ) můžete aktualizovat v [souhrnu využití zákazníků (prostředek **CustomerUsageSummary** )](customer-usage-resources.md#customerusagesummary).</span><span class="sxs-lookup"><span data-stu-id="3fcf7-108">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fcf7-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3fcf7-109">Prerequisites</span></span>

- <span data-ttu-id="3fcf7-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3fcf7-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3fcf7-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3fcf7-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3fcf7-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3fcf7-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3fcf7-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3fcf7-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3fcf7-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="3fcf7-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3fcf7-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3fcf7-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="3fcf7-118">C\#</span><span class="sxs-lookup"><span data-stu-id="3fcf7-118">C\#</span></span>

<span data-ttu-id="3fcf7-119">Aktualizace rozpočtu útraty využívání zákazníka:</span><span class="sxs-lookup"><span data-stu-id="3fcf7-119">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="3fcf7-120">Vytvoří nový objekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) s aktualizovanou velikostí.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-120">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="3fcf7-121">Pomocí kolekce [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) volejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) se zadaným identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-121">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="3fcf7-122">Zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) , abyste získali rozpočet využití zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest-request"></a><span data-ttu-id="3fcf7-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="3fcf7-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3fcf7-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="3fcf7-124">Request syntax</span></span>

| <span data-ttu-id="3fcf7-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="3fcf7-125">Method</span></span>    | <span data-ttu-id="3fcf7-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3fcf7-126">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3fcf7-127">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="3fcf7-127">**GET**</span></span> | <span data-ttu-id="3fcf7-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3fcf7-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3fcf7-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="3fcf7-129">URI parameter</span></span>

<span data-ttu-id="3fcf7-130">Pro aktualizaci fakturačního profilu použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-130">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="3fcf7-131">Název</span><span class="sxs-lookup"><span data-stu-id="3fcf7-131">Name</span></span>                   | <span data-ttu-id="3fcf7-132">Typ</span><span class="sxs-lookup"><span data-stu-id="3fcf7-132">Type</span></span>     | <span data-ttu-id="3fcf7-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3fcf7-133">Required</span></span> | <span data-ttu-id="3fcf7-134">Popis</span><span class="sxs-lookup"><span data-stu-id="3fcf7-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3fcf7-135">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="3fcf7-135">**customer-tenant-id**</span></span> | <span data-ttu-id="3fcf7-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="3fcf7-136">**guid**</span></span> | <span data-ttu-id="3fcf7-137">Y</span><span class="sxs-lookup"><span data-stu-id="3fcf7-137">Y</span></span>        | <span data-ttu-id="3fcf7-138">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3fcf7-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="3fcf7-139">Request headers</span></span>

<span data-ttu-id="3fcf7-140">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3fcf7-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3fcf7-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="3fcf7-141">Request body</span></span>

<span data-ttu-id="3fcf7-142">Úplný prostředek.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="3fcf7-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="3fcf7-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="3fcf7-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3fcf7-144">REST response</span></span>

<span data-ttu-id="3fcf7-145">V případě úspěchu tato metoda vrátí rozpočet útraty uživatele s aktualizovanou velikostí.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-145">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3fcf7-146">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="3fcf7-146">Response success and error codes</span></span>

<span data-ttu-id="3fcf7-147">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3fcf7-148">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="3fcf7-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3fcf7-149">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3fcf7-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3fcf7-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="3fcf7-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"GET",
            "headers":[]
        }
    }
}
```
