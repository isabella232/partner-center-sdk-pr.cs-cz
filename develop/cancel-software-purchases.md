---
title: Zrušení nákupů předplatného
description: Možnost samostatného poskytování softwaru pro zrušení předplatných softwaru a trvalého nákupu softwaru pomocí rozhraní API partnerského centra.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 877702ac930919ff72c6cc45a3c0e8ecc7e1b5f4
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974229"
---
# <a name="cancel-software-purchases"></a><span data-ttu-id="b4874-103">Zrušení nákupů předplatného</span><span class="sxs-lookup"><span data-stu-id="b4874-103">Cancel software purchases</span></span>

<span data-ttu-id="b4874-104">Pomocí rozhraní API partnerského centra můžete zrušit odběry softwaru a trvalé nákupy softwaru (Pokud se tyto nákupy uskutečnily v okně zrušení od data nákupu).</span><span class="sxs-lookup"><span data-stu-id="b4874-104">You can use the Partner Center APIs to cancel software subscriptions and perpetual software purchases (as long as those purchases were made within the cancellation window from the purchase date).</span></span> <span data-ttu-id="b4874-105">K provedení těchto zrušení nemusíte vytvářet lístek podpory a můžete místo toho použít následující samoobslužné metody.</span><span class="sxs-lookup"><span data-stu-id="b4874-105">You don't need to create a support ticket to make such cancellations, and can use the following self-service methods instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4874-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b4874-106">Prerequisites</span></span>

- <span data-ttu-id="b4874-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b4874-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b4874-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="b4874-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="b4874-109">C\#</span><span class="sxs-lookup"><span data-stu-id="b4874-109">C\#</span></span>

<span data-ttu-id="b4874-110">Postup při zrušení pořadí softwaru</span><span class="sxs-lookup"><span data-stu-id="b4874-110">To cancel a software order,</span></span>

1. <span data-ttu-id="b4874-111">Předejte přihlašovací údaje účtu do metody [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) , abyste získali rozhraní [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) pro získání partnerských operací.</span><span class="sxs-lookup"><span data-stu-id="b4874-111">Pass your account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

2. <span data-ttu-id="b4874-112">Vyberte konkrétní [objednávku](order-resources.md#order) , kterou chcete zrušit.</span><span class="sxs-lookup"><span data-stu-id="b4874-112">Select a particular [Order](order-resources.md#order) you wish to cancel.</span></span> <span data-ttu-id="b4874-113">Zavolejte metodu [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka, za nímž následuje **Order. ById ()** s identifikátorem objednávky.</span><span class="sxs-lookup"><span data-stu-id="b4874-113">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier, followed by **Orders.ById()** with order identifier.</span></span>

3. <span data-ttu-id="b4874-114">Pro načtení objednávky zavolejte metodu **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="b4874-114">Call the **Get** or **GetAsync** method to retrieve the order.</span></span>

4. <span data-ttu-id="b4874-115">Nastavte vlastnost [**Order. status**](order-resources.md#order) na `cancelled` .</span><span class="sxs-lookup"><span data-stu-id="b4874-115">Set the [**Order.Status**](order-resources.md#order) property to `cancelled`.</span></span>

5. <span data-ttu-id="b4874-116">Volitelné Chcete-li zadat určité položky řádku pro zrušení, nastavte [**Order. položky řádku**](order-resources.md#order) na seznam položek řádků, které chcete zrušit.</span><span class="sxs-lookup"><span data-stu-id="b4874-116">(Optional) If you want to specify certain line items for cancellation, set the [**Order.LineItems**](order-resources.md#order) to list of line items that you want to cancel.</span></span>

6. <span data-ttu-id="b4874-117">K aktualizaci objednávky použijte metodu **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="b4874-117">Use the **Patch()** method to update the order.</span></span>

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="b4874-118">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b4874-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b4874-119">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b4874-119">Request syntax</span></span>

| <span data-ttu-id="b4874-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="b4874-120">Method</span></span>     | <span data-ttu-id="b4874-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b4874-121">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="b4874-122">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="b4874-122">**PATCH**</span></span> | <span data-ttu-id="b4874-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b4874-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b4874-124">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="b4874-124">URI parameters</span></span>

<span data-ttu-id="b4874-125">K odstranění zákazníka použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="b4874-125">Use the following query parameters to delete a customer.</span></span>

| <span data-ttu-id="b4874-126">Název</span><span class="sxs-lookup"><span data-stu-id="b4874-126">Name</span></span>                   | <span data-ttu-id="b4874-127">Typ</span><span class="sxs-lookup"><span data-stu-id="b4874-127">Type</span></span>     | <span data-ttu-id="b4874-128">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b4874-128">Required</span></span> | <span data-ttu-id="b4874-129">Popis</span><span class="sxs-lookup"><span data-stu-id="b4874-129">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b4874-130">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="b4874-130">**customer-tenant-id**</span></span> | <span data-ttu-id="b4874-131">**guid**</span><span class="sxs-lookup"><span data-stu-id="b4874-131">**guid**</span></span> | <span data-ttu-id="b4874-132">Y</span><span class="sxs-lookup"><span data-stu-id="b4874-132">Y</span></span>        | <span data-ttu-id="b4874-133">Hodnota je identifikátor zákazníka s formátovaným identifikátorem GUID, který umožňuje prodejci filtrovat výsledky pro konkrétního zákazníka, který patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="b4874-133">The value is a GUID formatted customer tenant identifier that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="b4874-134">**ID objednávky**</span><span class="sxs-lookup"><span data-stu-id="b4874-134">**order-id**</span></span> | <span data-ttu-id="b4874-135">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="b4874-135">**string**</span></span> | <span data-ttu-id="b4874-136">Y</span><span class="sxs-lookup"><span data-stu-id="b4874-136">Y</span></span>        | <span data-ttu-id="b4874-137">Hodnota je řetězec, který označuje identifikátor objednávky, kterou chcete zrušit.</span><span class="sxs-lookup"><span data-stu-id="b4874-137">The value is a string that denotes the identifier of the order that you want to cancel.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b4874-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b4874-138">Request headers</span></span>

<span data-ttu-id="b4874-139">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b4874-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b4874-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b4874-140">Request body</span></span>

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a><span data-ttu-id="b4874-141">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b4874-141">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="b4874-142">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b4874-142">REST response</span></span>

<span data-ttu-id="b4874-143">V případě úspěchu vrátí tato metoda pořadí s stornovanými položkami řádků.</span><span class="sxs-lookup"><span data-stu-id="b4874-143">If successful, this method returns the order with canceled line items.</span></span>

<span data-ttu-id="b4874-144">Stav objednávky bude označen jako **zrušený** , pokud jsou všechny položky řádku v objednávce zrušeny nebo **dokončeny** , pokud nejsou všechny položky řádku v objednávce zrušeny.</span><span class="sxs-lookup"><span data-stu-id="b4874-144">The order status will be marked as either **cancelled** if all the line items in the order are canceled, or **completed** if not all line items in the order are canceled.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b4874-145">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b4874-145">Response success and error codes</span></span>

<span data-ttu-id="b4874-146">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b4874-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b4874-147">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b4874-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b4874-148">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b4874-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b4874-149">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b4874-149">Response example</span></span>

<span data-ttu-id="b4874-150">V následujícím příkladu odpovědi vidíte, že množství položky řádku s identifikátorem nabídky se **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** změní na nula (0).</span><span class="sxs-lookup"><span data-stu-id="b4874-150">In the following example response, you can see that the quantity of line item with the offer identifier **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** has become zero (0).</span></span> <span data-ttu-id="b4874-151">Tato změna znamená, že položka řádku, která byla označena pro zrušení, byla úspěšně zrušena.</span><span class="sxs-lookup"><span data-stu-id="b4874-151">This change means that the line item that was marked for cancellation has been canceled successfully.</span></span> <span data-ttu-id="b4874-152">Příklad pořadí obsahuje další položky řádku, které nebyly zrušeny, což znamená, že stav celkového pořadí bude označen jako **dokončený**, nikoli **zrušený**.</span><span class="sxs-lookup"><span data-stu-id="b4874-152">The example order contains other line items that weren't canceled, which means that the status of the overall order will be marked as **completed**, not **cancelled**.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
