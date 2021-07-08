---
title: Získání rozpočtu na útratu za využití zákazníka
description: Rozpočet útraty (objekt SpendingBudget) můžete použít k aktualizaci souhrnu využití zákazníka (prostředek CustomerUsageSummary).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b55f59fff7e5d7865811ecab3e901848126d31f7
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874869"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="965af-103">Získání rozpočtu na útratu za využití zákazníka</span><span class="sxs-lookup"><span data-stu-id="965af-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="965af-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="965af-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="965af-105">Rozpočet útraty (objekt **SpendingBudget)** můžete aktualizovat v souhrnu využití zákazníka [(prostředek **CustomerUsageSummary).**](customer-usage-resources.md#customerusagesummary)</span><span class="sxs-lookup"><span data-stu-id="965af-105">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="965af-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="965af-106">Prerequisites</span></span>

- <span data-ttu-id="965af-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="965af-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="965af-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="965af-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="965af-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="965af-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="965af-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="965af-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="965af-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="965af-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="965af-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="965af-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="965af-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="965af-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="965af-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="965af-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="965af-115">C\#</span><span class="sxs-lookup"><span data-stu-id="965af-115">C\#</span></span>

<span data-ttu-id="965af-116">Aktualizace rozpočtu útraty za využití zákazníka:</span><span class="sxs-lookup"><span data-stu-id="965af-116">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="965af-117">Vytvořte nový objekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) s aktualizovanou částkou.</span><span class="sxs-lookup"><span data-stu-id="965af-117">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="965af-118">Kolekci [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) použijte k volání metody [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="965af-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="965af-119">Voláním [**metody Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) získejte rozpočet využití zákazníka.</span><span class="sxs-lookup"><span data-stu-id="965af-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="965af-120">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="965af-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="965af-121">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="965af-121">Request syntax</span></span>

| <span data-ttu-id="965af-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="965af-122">Method</span></span>    | <span data-ttu-id="965af-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="965af-123">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="965af-124">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="965af-124">**GET**</span></span> | <span data-ttu-id="965af-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="965af-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="965af-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="965af-126">URI parameter</span></span>

<span data-ttu-id="965af-127">K aktualizaci fakturačního profilu použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="965af-127">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="965af-128">Název</span><span class="sxs-lookup"><span data-stu-id="965af-128">Name</span></span>                   | <span data-ttu-id="965af-129">Typ</span><span class="sxs-lookup"><span data-stu-id="965af-129">Type</span></span>     | <span data-ttu-id="965af-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="965af-130">Required</span></span> | <span data-ttu-id="965af-131">Popis</span><span class="sxs-lookup"><span data-stu-id="965af-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="965af-132">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="965af-132">**customer-tenant-id**</span></span> | <span data-ttu-id="965af-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="965af-133">**guid**</span></span> | <span data-ttu-id="965af-134">Y</span><span class="sxs-lookup"><span data-stu-id="965af-134">Y</span></span>        | <span data-ttu-id="965af-135">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="965af-135">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="965af-136">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="965af-136">Request headers</span></span>

<span data-ttu-id="965af-137">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="965af-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="965af-138">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="965af-138">Request body</span></span>

<span data-ttu-id="965af-139">Úplný prostředek.</span><span class="sxs-lookup"><span data-stu-id="965af-139">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="965af-140">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="965af-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="965af-141">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="965af-141">REST response</span></span>

<span data-ttu-id="965af-142">V případě úspěchu tato metoda vrátí rozpočet útraty uživatele s aktualizovanou částkou.</span><span class="sxs-lookup"><span data-stu-id="965af-142">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="965af-143">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="965af-143">Response success and error codes</span></span>

<span data-ttu-id="965af-144">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="965af-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="965af-145">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="965af-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="965af-146">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="965af-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="965af-147">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="965af-147">Response example</span></span>

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
