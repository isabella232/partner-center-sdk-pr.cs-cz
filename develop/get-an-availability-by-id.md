---
title: Získání dostupnosti podle ID
description: Získá dostupnost pro zadaný produkt a SKU pomocí ID dostupnosti.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: fccd566e83dab8994280fdee072c0d6f27b690d5292ed3973427088f46b30d6b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993550"
---
# <a name="get-the-availability-by-id"></a>Získání dostupnosti podle ID

Získá dostupnost pro zadaný produkt a SKU pomocí ID dostupnosti.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID produktu.

- ID SKU.

- ID dostupnosti.

## <a name="c"></a>C\#

Pokud chcete získat podrobnosti o konkrétní [dostupnosti,](product-resources.md#availability)začněte postupem v tématu Získání [SKU podle ID](get-a-sku-by-id.md) a získejte rozhraní pro operace [konkrétní SKU.](product-resources.md#sku) Ve výsledném rozhraní vyberte vlastnost **Availabilities** a získejte rozhraní s dostupnými operacemi pro dostupnost. Potom předejte ID dostupnosti metodě **ById(),** abyste získali operace pro tuto konkrétní dostupnost, a potom zavoláte **Get()** nebo **GetAsync()** a načtete podrobnosti o dostupnosti.

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pokud chcete získat podrobnosti o konkrétní [dostupnosti,](product-resources.md#availability)začněte postupem v tématu Získání [SKU podle ID](get-a-sku-by-id.md) a získejte rozhraní pro operace [konkrétní SKU.](product-resources.md#sku) Ve výsledném rozhraní vyberte funkci **getAvailabilities** a získejte rozhraní s dostupnými operacemi pro dostupnost. Potom předejte ID dostupnosti do funkce **byId(),** abyste získali operace pro tuto konkrétní dostupnost, a potom zavoláte funkci **get(),** která načte podrobnosti o dostupnosti.

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pokud chcete získat podrobnosti o konkrétní [dostupnosti,](product-resources.md#availability)spusťte [**get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) a zadáním parametrů **AvailabilityId**, **CountryCode**, **ProductId** a **SkuId** načtěte podrobnosti o dostupnosti.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{ID_produktu}/skus/{ID_SKU}/availabilities/{ID_dostupnosti}?country={kód_země} HTTP/1.1         |

### <a name="uri-parameter"></a>Parametr URI

Pomocí následující cesty a parametrů dotazu získejte konkrétní dostupnost pomocí ID dostupnosti.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| id produktu             | řetězec   | Yes      | Řetězec formátovaný identifikátorem GUID, který identifikuje produkt.            |
| sku-id                 | řetězec   | Yes      | Řetězec formátovaný identifikátorem GUID, který identifikuje SKU.                |
| ID dostupnosti        | řetězec   | Yes      | Řetězec formátovaný identifikátorem GUID, který identifikuje dostupnost.       |
| kód země           | řetězec   | Yes      | ID země nebo oblasti.                                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu bude tělo odpovědi obsahovat [prostředek](product-resources.md#availability) dostupnosti.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

Tato metoda vrátí následující kódy chyb:

| Stavový kód HTTP     | Kód chyby   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Produkt se nenašel.                                                                                    |
| 404                  | 400018       | SKU se nenašla.                                                                                        |
| 404                  | 400019       | Dostupnost se nenašla.                                                                                   |

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": false,
    "terms": [{
        "duration": "P1Y",
        "description": "1 Year Prepaid"
    }],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
