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
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a>Podívejte se na inventář položek katalogu pomocí rozhraní API partnerského centra.

Jak kontrolovat inventář konkrétní sady položek katalogu

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- Jedno nebo více ID produktu. Volitelně lze také zadat ID SKU.

- Jakýkoliv další kontext potřebný pro ověření inventáře SKU, na který odkazuje poskytnutá ID produktu nebo SKU. Tyto požadavky se mohou lišit podle typu produktu/SKU a lze je určit z vlastnosti [](product-resources.md#sku) **InventoryVariables** SKU.

## <a name="c"></a>C\#

Chcete-li zkontrolovat inventář, Sestavte objekt [InventoryCheckRequest](product-resources.md#inventorycheckrequest) pomocí objektu [InventoryItem](product-resources.md#inventoryitem) pro každou položku, kterou chcete zkontrolovat. Pak použijte přistupující objekt **IAggregatePartner. Extensions** , určete jeho rozsah až na **produkt** a pak vyberte zemi pomocí metody **ByCountry ()** . Nakonec zavolejte metodu **CheckInventory ()** s vaším objektem **InventoryCheckRequest** .

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

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Extensions/Product/checkInventory? Country = {Country-Code} HTTP/1.1                        |

### <a name="uri-parameter"></a>Parametr URI

K kontrole inventáře použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| kód země           | řetězec   | Yes      | ID země nebo oblasti.                                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Podrobnosti o požadavku inventáře, které se skládají z prostředku [InventoryCheckRequest](product-resources.md#inventorycheckrequest) , který obsahuje jeden nebo více prostředků [InventoryItem](product-resources.md#inventoryitem) .

### <a name="request-example"></a>Příklad požadavku

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

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tělo odpovědi obsahuje kolekci objektů [InventoryItem](product-resources.md#inventoryitem) , které jsou vyplněny s podrobnostmi o omezení, pokud jsou použity.

>[!NOTE]
>Pokud vstupní InventoryItem představuje položku, která nebyla nalezena v katalogu, nebude součástí výstupní kolekce.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

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
