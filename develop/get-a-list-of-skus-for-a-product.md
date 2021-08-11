---
title: Získání seznamu skladových položek pro produkt (podle země)
description: Kolekci SKU pro produkt můžete získat a filtrovat podle země pomocí Partnerské centrum API.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1f15ecaa7d84f4c68c6221e459d9977a79cffd9fa19d32ccbd7e6bec6444a93c
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995437"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a>Získání seznamu skladových položek pro produkt (podle země)

Kolekci SKU dostupných v zemi pro konkrétní produkt můžete získat pomocí Partnerské centrum API.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- Identifikátor produktu.

## <a name="c"></a>C\#

Získání seznamu skladových položek pro produkt:

1. Rozhraní pro operace konkrétního produktu získáte podle kroků v části [Získání produktu podle ID](get-a-product-by-id.md).

2. V rozhraní vyberte vlastnost **Skus** a získejte rozhraní s dostupnými operacemi pro skladové položky.

3. Voláním **metody Get()** nebo **GetAsync()** načtěte kolekci dostupných SKU pro produkt.

4. (Volitelné) Vyberte rozsah rezervace pomocí metody **ByReservationScope().**

5. (Volitelné) Před voláním metody **Get()** nebo **GetAsync()** použijte metodu **ByTargetSegment()** k filtrování skladových měr podle cílového segmentu.

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Získání seznamu skladových položek pro produkt:

1. Rozhraní pro operace konkrétního produktu získáte podle kroků v části [Získání produktu podle ID](get-a-product-by-id.md).

2. V rozhraní vyberte funkci **getSkus** a získejte rozhraní s dostupnými operacemi pro skladové položky.

3. Voláním **funkce get()** načtete kolekci dostupných skladových cen pro produkt.

4. (Volitelné) Před voláním funkce **get()** použijte funkci **byTargetSegment()** k filtrování skladových měr podle cílového segmentu.

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Získání seznamu skladových položek pro produkt:

1. Spusťte příkaz [**Get-PartnerProductSku.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md)

2. (Volitelné) Zadáním **parametru Segment** můžete skladové hodnoty filtrovat podle cílového segmentu.

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{id_produktu}/skus?country={kód_země}&targetSegment={target-segment} HTTP/1.1  |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K získání seznamu skladových položek pro produkt použijte následující cestu a parametry dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| id produktu             | řetězec   | Yes      | Řetězec, který identifikuje produkt.                           |
| kód země           | řetězec   | Yes      | ID země nebo oblasti.                                            |
| target-segment         | řetězec   | No       | Řetězec, který identifikuje cílový segment použitý k filtrování. |
| reservationScope | řetězec   | No | Při dotazování na seznam skladových položek pro produkt rezervace Azure zadejte , abyste získali seznam skladových položek `reservationScope=AzurePlan` použitelných pro AzurePlan. Tento parametr vyloučíte, pokud chcete získat seznam skladových položek pro produkty rezervací Azure, které se vztahují k předplatným Microsoft Azure (MS-AZR-0145P).  |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-examples"></a>Příklady požadavků

Získání seznamu skladových položek pro daný produkt:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Získejte seznam skladových položek pro produkt Azure Reservation. Zahrnovat pouze skladové prostředky, které se vztahují k plánům Azure, Microsoft Azure předplatná MS-AZR-0145P:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Získejte seznam skladových položek pro produkt Azure Reservation. Zahrnovat pouze SKU, které se vztahují na předplatná Microsoft Azure (MS-AZR-0145P), a ne na plány Azure:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu bude text odpovědi obsahovat kolekci prostředků [SKU.](product-resources.md#sku)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

Tato metoda vrátí následující kódy chyb:

| Stavový kód HTTP     | Kód chyby   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Přístup k požadovanému targetSegment není povolený.                                                     |
| 404                  | 400013       | Nadřazený produkt se nenašel.                                                                         |

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
            "minimumQuantity": 1,
            "maximumQuantity": 999999999,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "AzureSubscriptionRegistration",
                "InventoryCheck"
            ],
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
            "minimumQuantity": 1,
            "maximumQuantity": 999999999,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "AzureSubscriptionRegistration",
                "InventoryCheck"
            ],
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
