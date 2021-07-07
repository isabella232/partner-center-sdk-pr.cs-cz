---
title: Aktualizace rozpočtu útraty využívání zákazníka
description: Aktualizuje rozpočet útraty přidělený pro využití zákazníka.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 043bd442266d081105e5e8767b6d597e89fc9e8b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529711"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="7cfa9-103">Aktualizace rozpočtu útraty využívání zákazníka</span><span class="sxs-lookup"><span data-stu-id="7cfa9-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="7cfa9-104">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7cfa9-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7cfa9-105">Aktualizuje [rozpočet útraty](customer-usage-resources.md#customerusagesummary) přidělený pro využití zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-105">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cfa9-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7cfa9-106">Prerequisites</span></span>

- <span data-ttu-id="7cfa9-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7cfa9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7cfa9-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7cfa9-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7cfa9-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7cfa9-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7cfa9-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7cfa9-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7cfa9-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="7cfa9-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7cfa9-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7cfa9-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7cfa9-115">C\#</span><span class="sxs-lookup"><span data-stu-id="7cfa9-115">C\#</span></span>

<span data-ttu-id="7cfa9-116">Pokud chcete aktualizovat rozpočet výdajů na využívání zákazníka, nejprve vytvořte nový objekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) s aktualizovanou velikostí.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-116">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="7cfa9-117">Pak použijte kolekci [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-117">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="7cfa9-118">Pak přejděte do vlastnosti [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) a předejte aktualizované rozpočty využití do metody [**patch ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) nebo [**PatchAsync ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) .</span><span class="sxs-lookup"><span data-stu-id="7cfa9-118">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="7cfa9-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="7cfa9-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7cfa9-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="7cfa9-120">Request syntax</span></span>

| <span data-ttu-id="7cfa9-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="7cfa9-121">Method</span></span>    | <span data-ttu-id="7cfa9-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="7cfa9-122">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7cfa9-123">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="7cfa9-123">**PATCH**</span></span> | <span data-ttu-id="7cfa9-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7cfa9-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7cfa9-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="7cfa9-125">URI parameter</span></span>

<span data-ttu-id="7cfa9-126">Pro aktualizaci fakturačního profilu použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-126">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="7cfa9-127">Název</span><span class="sxs-lookup"><span data-stu-id="7cfa9-127">Name</span></span>                   | <span data-ttu-id="7cfa9-128">Typ</span><span class="sxs-lookup"><span data-stu-id="7cfa9-128">Type</span></span>     | <span data-ttu-id="7cfa9-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="7cfa9-129">Required</span></span> | <span data-ttu-id="7cfa9-130">Popis</span><span class="sxs-lookup"><span data-stu-id="7cfa9-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7cfa9-131">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="7cfa9-131">**customer-tenant-id**</span></span> | <span data-ttu-id="7cfa9-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="7cfa9-132">**guid**</span></span> | <span data-ttu-id="7cfa9-133">Y</span><span class="sxs-lookup"><span data-stu-id="7cfa9-133">Y</span></span>        | <span data-ttu-id="7cfa9-134">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7cfa9-135">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="7cfa9-135">Request headers</span></span>

<span data-ttu-id="7cfa9-136">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7cfa9-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7cfa9-137">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="7cfa9-137">Request body</span></span>

<span data-ttu-id="7cfa9-138">Úplný prostředek.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-138">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="7cfa9-139">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="7cfa9-139">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="7cfa9-140">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="7cfa9-140">REST response</span></span>

<span data-ttu-id="7cfa9-141">V případě úspěchu tato metoda vrátí rozpočet útraty uživatele s aktualizovanou velikostí.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-141">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7cfa9-142">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="7cfa9-142">Response success and error codes</span></span>

<span data-ttu-id="7cfa9-143">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7cfa9-144">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="7cfa9-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7cfa9-145">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7cfa9-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7cfa9-146">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="7cfa9-146">Response example</span></span>

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
