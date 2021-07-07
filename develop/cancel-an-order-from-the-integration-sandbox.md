---
title: Zrušení objednávky z integračního sandboxu
description: Zjistěte, jak pomocí Partnerské centrum API zrušit různé typy objednávek předplatných z účtů sandboxu integrace.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c4b658f406e420d8d3cd425688364fe3d440d3d
ms.sourcegitcommit: a3a78ec0f5078645b5a4f3b534165eef30f2c822
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2021
ms.locfileid: "113104967"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="9e17c-103">Zrušení objednávky z integračního sandboxu pomocí Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="9e17c-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="9e17c-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9e17c-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9e17c-105">Tento článek popisuje, jak pomocí Partnerské centrum API zrušit různé typy objednávek předplatného z účtů sandboxu integrace.</span><span class="sxs-lookup"><span data-stu-id="9e17c-105">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="9e17c-106">Tyto objednávky mohou zahrnovat rezervované instance, software a objednávky předplatného SaaS (Software jako služba) na komerčním marketplace.</span><span class="sxs-lookup"><span data-stu-id="9e17c-106">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

> [!NOTE] 
> <span data-ttu-id="9e17c-107">Upozorňujeme, že zrušení rezervovaných instancí nebo objednávek předplatného SaaS na komerčním marketplace je možné pouze z účtů sandboxu integrace.</span><span class="sxs-lookup"><span data-stu-id="9e17c-107">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span> <span data-ttu-id="9e17c-108">Všechny objednávky sandboxu, které jsou starší než 60 dnů, není možné zrušit z Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="9e17c-108">Any sandbox orders which are older than 60 days cannot be cancelled from Partner Center.</span></span>

<span data-ttu-id="9e17c-109">Pokud chcete zrušit produkční objednávky softwaru prostřednictvím rozhraní API, [použijte příkaz cancel-software-purchases](cancel-software-purchases.md).</span><span class="sxs-lookup"><span data-stu-id="9e17c-109">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="9e17c-110">Můžete také zrušit produkční objednávky softwaru prostřednictvím řídicího panelu pomocí [zrušení nákupu](/partner-center/csp-software-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="9e17c-110">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e17c-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9e17c-111">Prerequisites</span></span>

- <span data-ttu-id="9e17c-112">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9e17c-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e17c-113">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="9e17c-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9e17c-114">Partnerský účet sandboxu pro integraci se zákazníkem, který má aktivní rezervované instance, software nebo objednávky předplatného SaaS třetích stran.</span><span class="sxs-lookup"><span data-stu-id="9e17c-114">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="9e17c-115">C\#</span><span class="sxs-lookup"><span data-stu-id="9e17c-115">C\#</span></span>

<span data-ttu-id="9e17c-116">Pokud chcete zrušit objednávku z sandboxu integrace, předejte přihlašovací údaje svého účtu metodě , abyste získali rozhraní pro [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) získání partnerských operací.</span><span class="sxs-lookup"><span data-stu-id="9e17c-116">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="9e17c-117">Pokud chcete vybrat konkrétní [objednávku,](order-resources.md#order)pomocí operací partnera a volání metody s identifikátorem zákazníka určete zákazníka a pak s identifikátorem objednávky určete objednávku a nakonec metodu nebo metodu pro [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) **`Orders.ById()`** **`Get`** **`GetAsync`** načtení.</span><span class="sxs-lookup"><span data-stu-id="9e17c-117">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="9e17c-118">Nastavte [**`Order.Status`**](order-resources.md#order) vlastnost na a pomocí metody `cancelled` **`Patch()`** aktualizujte pořadí.</span><span class="sxs-lookup"><span data-stu-id="9e17c-118">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="9e17c-119">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="9e17c-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e17c-120">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="9e17c-120">Request syntax</span></span>

| <span data-ttu-id="9e17c-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="9e17c-121">Method</span></span>     | <span data-ttu-id="9e17c-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9e17c-122">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="9e17c-123">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="9e17c-123">**PATCH**</span></span> | <span data-ttu-id="9e17c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/orders/{ID_objednávky} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9e17c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9e17c-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9e17c-125">URI parameter</span></span>

<span data-ttu-id="9e17c-126">K odstranění zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="9e17c-126">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="9e17c-127">Název</span><span class="sxs-lookup"><span data-stu-id="9e17c-127">Name</span></span>                   | <span data-ttu-id="9e17c-128">Typ</span><span class="sxs-lookup"><span data-stu-id="9e17c-128">Type</span></span>     | <span data-ttu-id="9e17c-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9e17c-129">Required</span></span> | <span data-ttu-id="9e17c-130">Popis</span><span class="sxs-lookup"><span data-stu-id="9e17c-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9e17c-131">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="9e17c-131">**customer-tenant-id**</span></span> | <span data-ttu-id="9e17c-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="9e17c-132">**guid**</span></span> | <span data-ttu-id="9e17c-133">Y</span><span class="sxs-lookup"><span data-stu-id="9e17c-133">Y</span></span>        | <span data-ttu-id="9e17c-134">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="9e17c-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="9e17c-135">**ID objednávky**</span><span class="sxs-lookup"><span data-stu-id="9e17c-135">**order-id**</span></span> | <span data-ttu-id="9e17c-136">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="9e17c-136">**string**</span></span> | <span data-ttu-id="9e17c-137">Y</span><span class="sxs-lookup"><span data-stu-id="9e17c-137">Y</span></span>        | <span data-ttu-id="9e17c-138">Hodnota je řetězec označující ID objednávek, které je potřeba zrušit.</span><span class="sxs-lookup"><span data-stu-id="9e17c-138">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9e17c-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9e17c-139">Request headers</span></span>

<span data-ttu-id="9e17c-140">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9e17c-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9e17c-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9e17c-141">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="9e17c-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9e17c-142">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a><span data-ttu-id="9e17c-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9e17c-143">REST response</span></span>

<span data-ttu-id="9e17c-144">V případě úspěchu tato metoda vrátí zrušenou objednávku.</span><span class="sxs-lookup"><span data-stu-id="9e17c-144">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e17c-145">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="9e17c-145">Response success and error codes</span></span>

<span data-ttu-id="9e17c-146">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9e17c-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9e17c-147">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="9e17c-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e17c-148">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9e17c-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9e17c-149">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9e17c-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
