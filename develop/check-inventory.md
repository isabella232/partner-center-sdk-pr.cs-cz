---
title: Kontrolovat inventář
description: Naučte se používat rozhraní API partnerského centra ke kontrole inventáře konkrétní sady položek katalogu. To můžete provést k identifikaci produktů nebo SKU zákazníka.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b982dbd7e5e10d454ef87a1e750546ea50eb8438
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974076"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a><span data-ttu-id="e11d6-104">Podívejte se na inventář položek katalogu pomocí rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e11d6-104">Check the inventory of catalog items using Partner Center APIs</span></span>

<span data-ttu-id="e11d6-105">Jak kontrolovat inventář konkrétní sady položek katalogu</span><span class="sxs-lookup"><span data-stu-id="e11d6-105">How to check the inventory for a specific set of catalog items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e11d6-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e11d6-106">Prerequisites</span></span>

- <span data-ttu-id="e11d6-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e11d6-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e11d6-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e11d6-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e11d6-109">Jedno nebo více ID produktu.</span><span class="sxs-lookup"><span data-stu-id="e11d6-109">One or more product IDs.</span></span> <span data-ttu-id="e11d6-110">Volitelně lze také zadat ID SKU.</span><span class="sxs-lookup"><span data-stu-id="e11d6-110">Optionally, SKU IDs can also be specified.</span></span>

- <span data-ttu-id="e11d6-111">Jakýkoliv další kontext potřebný pro ověření inventáře SKU, na který odkazuje poskytnutá ID produktu nebo SKU.</span><span class="sxs-lookup"><span data-stu-id="e11d6-111">Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU ID(s).</span></span> <span data-ttu-id="e11d6-112">Tyto požadavky se mohou lišit podle typu produktu/SKU a lze je určit z vlastnosti [](product-resources.md#sku) **InventoryVariables** SKU.</span><span class="sxs-lookup"><span data-stu-id="e11d6-112">These requirements may vary by type of product/SKU and can be determined from the [SKU's](product-resources.md#sku) **InventoryVariables** property.</span></span>

## <a name="c"></a><span data-ttu-id="e11d6-113">C\#</span><span class="sxs-lookup"><span data-stu-id="e11d6-113">C\#</span></span>

<span data-ttu-id="e11d6-114">Chcete-li zkontrolovat inventář, Sestavte objekt [InventoryCheckRequest](product-resources.md#inventorycheckrequest) pomocí objektu [InventoryItem](product-resources.md#inventoryitem) pro každou položku, kterou chcete zkontrolovat.</span><span class="sxs-lookup"><span data-stu-id="e11d6-114">To check the inventory, build an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) object using an [InventoryItem](product-resources.md#inventoryitem) object for each item to be checked.</span></span> <span data-ttu-id="e11d6-115">Pak použijte přistupující objekt **IAggregatePartner. Extensions** , určete jeho rozsah až na **produkt** a pak vyberte zemi pomocí metody **ByCountry ()** .</span><span class="sxs-lookup"><span data-stu-id="e11d6-115">Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method.</span></span> <span data-ttu-id="e11d6-116">Nakonec zavolejte metodu **CheckInventory ()** s vaším objektem **InventoryCheckRequest** .</span><span class="sxs-lookup"><span data-stu-id="e11d6-116">Finally, call the **CheckInventory()** method with your **InventoryCheckRequest** object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a><span data-ttu-id="e11d6-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e11d6-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e11d6-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e11d6-118">Request syntax</span></span>

| <span data-ttu-id="e11d6-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="e11d6-119">Method</span></span>   | <span data-ttu-id="e11d6-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e11d6-120">Request URI</span></span>                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e11d6-121">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="e11d6-121">**POST**</span></span> | <span data-ttu-id="e11d6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Extensions/Product/checkInventory? Country = {Country-Code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e11d6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="e11d6-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e11d6-123">URI parameter</span></span>

<span data-ttu-id="e11d6-124">K kontrole inventáře použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="e11d6-124">Use the following query parameter to check the inventory.</span></span>

| <span data-ttu-id="e11d6-125">Název</span><span class="sxs-lookup"><span data-stu-id="e11d6-125">Name</span></span>                   | <span data-ttu-id="e11d6-126">Typ</span><span class="sxs-lookup"><span data-stu-id="e11d6-126">Type</span></span>     | <span data-ttu-id="e11d6-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e11d6-127">Required</span></span> | <span data-ttu-id="e11d6-128">Popis</span><span class="sxs-lookup"><span data-stu-id="e11d6-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="e11d6-129">kód země</span><span class="sxs-lookup"><span data-stu-id="e11d6-129">country-code</span></span>           | <span data-ttu-id="e11d6-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="e11d6-130">string</span></span>   | <span data-ttu-id="e11d6-131">Yes</span><span class="sxs-lookup"><span data-stu-id="e11d6-131">Yes</span></span>      | <span data-ttu-id="e11d6-132">ID země nebo oblasti.</span><span class="sxs-lookup"><span data-stu-id="e11d6-132">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="e11d6-133">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e11d6-133">Request headers</span></span>

<span data-ttu-id="e11d6-134">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e11d6-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e11d6-135">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e11d6-135">Request body</span></span>

<span data-ttu-id="e11d6-136">Podrobnosti o požadavku inventáře, které se skládají z prostředku [InventoryCheckRequest](product-resources.md#inventorycheckrequest) , který obsahuje jeden nebo více prostředků [InventoryItem](product-resources.md#inventoryitem) .</span><span class="sxs-lookup"><span data-stu-id="e11d6-136">The inventory request details, consisting of an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) resource containing one or more [InventoryItem](product-resources.md#inventoryitem) resources.</span></span>

### <a name="request-example"></a><span data-ttu-id="e11d6-137">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e11d6-137">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a><span data-ttu-id="e11d6-138">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e11d6-138">REST response</span></span>

<span data-ttu-id="e11d6-139">V případě úspěchu tělo odpovědi obsahuje kolekci objektů [InventoryItem](product-resources.md#inventoryitem) , které jsou vyplněny s podrobnostmi o omezení, pokud jsou použity.</span><span class="sxs-lookup"><span data-stu-id="e11d6-139">If successful, the response body contains a collection of [InventoryItem](product-resources.md#inventoryitem) objects populated with the restriction details, if any apply.</span></span>

>[!NOTE]
><span data-ttu-id="e11d6-140">Pokud vstupní InventoryItem představuje položku, která nebyla nalezena v katalogu, nebude součástí výstupní kolekce.</span><span class="sxs-lookup"><span data-stu-id="e11d6-140">If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e11d6-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e11d6-141">Response success and error codes</span></span>

<span data-ttu-id="e11d6-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e11d6-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e11d6-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e11d6-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e11d6-144">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e11d6-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e11d6-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e11d6-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
