---
title: Aktualizace rozpočtu útraty využívání zákazníka
description: Aktualizuje rozpočet útraty přidělený pro využití zákazníka.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 839305fb8fad3ce2442ab93e1d8a4a170b4d41c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767004"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="56af7-103">Aktualizace rozpočtu útraty využívání zákazníka</span><span class="sxs-lookup"><span data-stu-id="56af7-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="56af7-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="56af7-104">**Applies To**</span></span>

- <span data-ttu-id="56af7-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="56af7-105">Partner Center</span></span>
- <span data-ttu-id="56af7-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="56af7-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="56af7-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="56af7-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="56af7-108">Aktualizuje [rozpočet útraty](customer-usage-resources.md#customerusagesummary) přidělený pro využití zákazníka.</span><span class="sxs-lookup"><span data-stu-id="56af7-108">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56af7-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="56af7-109">Prerequisites</span></span>

- <span data-ttu-id="56af7-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="56af7-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="56af7-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="56af7-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="56af7-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="56af7-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="56af7-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="56af7-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="56af7-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="56af7-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="56af7-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="56af7-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="56af7-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="56af7-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="56af7-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="56af7-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="56af7-118">C\#</span><span class="sxs-lookup"><span data-stu-id="56af7-118">C\#</span></span>

<span data-ttu-id="56af7-119">Pokud chcete aktualizovat rozpočet výdajů na využívání zákazníka, nejprve vytvořte nový objekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) s aktualizovanou velikostí.</span><span class="sxs-lookup"><span data-stu-id="56af7-119">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="56af7-120">Pak použijte kolekci [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="56af7-120">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="56af7-121">Pak přejděte do vlastnosti [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) a předejte aktualizované rozpočty využití do metody [**patch ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) nebo [**PatchAsync ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) .</span><span class="sxs-lookup"><span data-stu-id="56af7-121">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
```

## <a name="rest-request"></a><span data-ttu-id="56af7-122">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="56af7-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="56af7-123">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="56af7-123">Request syntax</span></span>

| <span data-ttu-id="56af7-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="56af7-124">Method</span></span>    | <span data-ttu-id="56af7-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="56af7-125">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="56af7-126">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="56af7-126">**PATCH**</span></span> | <span data-ttu-id="56af7-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="56af7-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="56af7-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="56af7-128">URI parameter</span></span>

<span data-ttu-id="56af7-129">Pro aktualizaci fakturačního profilu použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="56af7-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="56af7-130">Název</span><span class="sxs-lookup"><span data-stu-id="56af7-130">Name</span></span>                   | <span data-ttu-id="56af7-131">Typ</span><span class="sxs-lookup"><span data-stu-id="56af7-131">Type</span></span>     | <span data-ttu-id="56af7-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="56af7-132">Required</span></span> | <span data-ttu-id="56af7-133">Popis</span><span class="sxs-lookup"><span data-stu-id="56af7-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="56af7-134">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="56af7-134">**customer-tenant-id**</span></span> | <span data-ttu-id="56af7-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="56af7-135">**guid**</span></span> | <span data-ttu-id="56af7-136">Y</span><span class="sxs-lookup"><span data-stu-id="56af7-136">Y</span></span>        | <span data-ttu-id="56af7-137">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="56af7-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="56af7-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="56af7-138">Request headers</span></span>

<span data-ttu-id="56af7-139">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="56af7-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="56af7-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="56af7-140">Request body</span></span>

<span data-ttu-id="56af7-141">Úplný prostředek.</span><span class="sxs-lookup"><span data-stu-id="56af7-141">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="56af7-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="56af7-142">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
     "Amount": 100,
     "Attributes": {
          "ObjectType": "SpendingBudget"
     }
}
```

## <a name="rest-response"></a><span data-ttu-id="56af7-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="56af7-143">REST response</span></span>

<span data-ttu-id="56af7-144">V případě úspěchu tato metoda vrátí rozpočet útraty uživatele s aktualizovanou velikostí.</span><span class="sxs-lookup"><span data-stu-id="56af7-144">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="56af7-145">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="56af7-145">Response success and error codes</span></span>

<span data-ttu-id="56af7-146">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="56af7-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="56af7-147">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="56af7-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="56af7-148">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="56af7-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="56af7-149">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="56af7-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

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
            "method":"PATCH",
            "headers":[]
        }
    }
}
```
