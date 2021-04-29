---
title: Zrušení objednávky z integrace izolovaného prostoru
description: Naučte se používat rozhraní API partnerského centra ke zrušení různých typů objednávek předplatného z účtů izolovaného prostoru integrace.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3bf862c62804a56e6f73dd3ec36d2e9eb65f997
ms.sourcegitcommit: f59a9311c8a37d45695caf74794ec1697426acc9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2021
ms.locfileid: "108210015"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="00b46-103">Zrušení objednávky z izolovaného prostoru integrace pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="00b46-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="00b46-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="00b46-104">**Applies to:**</span></span>

- <span data-ttu-id="00b46-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="00b46-105">Partner Center</span></span>
- <span data-ttu-id="00b46-106">Partnerské centrum provozované společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="00b46-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="00b46-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="00b46-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="00b46-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="00b46-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="00b46-109">Tento článek popisuje, jak pomocí rozhraní API partnerského centra zrušit různé typy objednávek předplatného z účtů karantény integrace.</span><span class="sxs-lookup"><span data-stu-id="00b46-109">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="00b46-110">Takové objednávky můžou zahrnovat rezervované instance, software a komerční objednávky předplatného SaaS (software jako služba) na webu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="00b46-110">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

>[!NOTE] 
><span data-ttu-id="00b46-111">Pamatujte na to, že zrušení rezervovaných instancí nebo komerčních předplatných SaaS na webu Marketplace je možné pouze z účtů karantény integrace.</span><span class="sxs-lookup"><span data-stu-id="00b46-111">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span> <span data-ttu-id="00b46-112">Jakékoli objednávky izolovaného prostoru (sandbox), které jsou starší než 60 dní, nelze zrušit z partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="00b46-112">Any sandbox orders which are older than 60 days cannot be cancelled from Partner Center.</span></span> <span data-ttu-id="00b46-113">Pokud potřebujete pomoc, můžete se obrátit na podporu partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="00b46-113">If you need assistance, reach out to Partner Center Support.</span></span> 

<span data-ttu-id="00b46-114">Pokud chcete zrušit výrobní zakázky softwaru prostřednictvím rozhraní API, použijte [Zrušit – software – nákupy](cancel-software-purchases.md).</span><span class="sxs-lookup"><span data-stu-id="00b46-114">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="00b46-115">Pomocí [zrušit nákup](/partner-center/csp-software-subscriptions)můžete také zrušit výrobní zakázky softwaru prostřednictvím řídicího panelu.</span><span class="sxs-lookup"><span data-stu-id="00b46-115">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00b46-116">Požadavky</span><span class="sxs-lookup"><span data-stu-id="00b46-116">Prerequisites</span></span>

- <span data-ttu-id="00b46-117">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="00b46-117">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="00b46-118">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="00b46-118">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="00b46-119">Partnerský účet integrace izolovaného prostoru (sandbox) se zákazníkem s aktivní rezervovanou instancí/softwarem nebo SaaS předplatnými třetích stran.</span><span class="sxs-lookup"><span data-stu-id="00b46-119">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="00b46-120">C\#</span><span class="sxs-lookup"><span data-stu-id="00b46-120">C\#</span></span>

<span data-ttu-id="00b46-121">Pokud chcete objednávku zrušit z karantény integrace Integration, předejte přihlašovací údaje účtu do [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metody, abyste získali [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) rozhraní pro získání partnerských operací.</span><span class="sxs-lookup"><span data-stu-id="00b46-121">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="00b46-122">Chcete-li vybrat konkrétní [objednávku](order-resources.md#order), použijte operace partnera a [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metodu volání s identifikátorem zákazníka a určete tak zákazníka, následovaný **`Orders.ById()`** identifikátorem objednávky a určete tak objednávku a nakonec **`Get`** nebo **`GetAsync`** metodu, kterou chcete načíst.</span><span class="sxs-lookup"><span data-stu-id="00b46-122">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="00b46-123">Nastavte [**`Order.Status`**](order-resources.md#order) vlastnost na `cancelled` a použijte **`Patch()`** metodu pro aktualizaci pořadí.</span><span class="sxs-lookup"><span data-stu-id="00b46-123">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="00b46-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="00b46-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="00b46-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="00b46-125">Request syntax</span></span>

| <span data-ttu-id="00b46-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="00b46-126">Method</span></span>     | <span data-ttu-id="00b46-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="00b46-127">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="00b46-128">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="00b46-128">**PATCH**</span></span> | <span data-ttu-id="00b46-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="00b46-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="00b46-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="00b46-130">URI parameter</span></span>

<span data-ttu-id="00b46-131">K odstranění zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="00b46-131">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="00b46-132">Název</span><span class="sxs-lookup"><span data-stu-id="00b46-132">Name</span></span>                   | <span data-ttu-id="00b46-133">Typ</span><span class="sxs-lookup"><span data-stu-id="00b46-133">Type</span></span>     | <span data-ttu-id="00b46-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="00b46-134">Required</span></span> | <span data-ttu-id="00b46-135">Popis</span><span class="sxs-lookup"><span data-stu-id="00b46-135">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00b46-136">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="00b46-136">**customer-tenant-id**</span></span> | <span data-ttu-id="00b46-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="00b46-137">**guid**</span></span> | <span data-ttu-id="00b46-138">Y</span><span class="sxs-lookup"><span data-stu-id="00b46-138">Y</span></span>        | <span data-ttu-id="00b46-139">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="00b46-139">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="00b46-140">**ID objednávky**</span><span class="sxs-lookup"><span data-stu-id="00b46-140">**order-id**</span></span> | <span data-ttu-id="00b46-141">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="00b46-141">**string**</span></span> | <span data-ttu-id="00b46-142">Y</span><span class="sxs-lookup"><span data-stu-id="00b46-142">Y</span></span>        | <span data-ttu-id="00b46-143">Hodnota je řetězec, který označuje ID objednávek, které je třeba zrušit.</span><span class="sxs-lookup"><span data-stu-id="00b46-143">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="00b46-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="00b46-144">Request headers</span></span>

<span data-ttu-id="00b46-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="00b46-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="00b46-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="00b46-146">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="00b46-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="00b46-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="00b46-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="00b46-148">REST response</span></span>

<span data-ttu-id="00b46-149">V případě úspěchu vrátí tato metoda objednávku Canceled.</span><span class="sxs-lookup"><span data-stu-id="00b46-149">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="00b46-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="00b46-150">Response success and error codes</span></span>

<span data-ttu-id="00b46-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="00b46-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="00b46-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="00b46-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="00b46-153">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="00b46-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="00b46-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="00b46-154">Response example</span></span>

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
