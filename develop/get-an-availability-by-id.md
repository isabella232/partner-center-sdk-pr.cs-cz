---
title: Získat dostupnost podle ID
description: Získá dostupnost pro zadaný produkt a SKU pomocí ID dostupnosti.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766671"
---
# <a name="get-the-availability-by-id"></a>Získat dostupnost podle ID

**Platí pro**

- Partnerské centrum

Získá dostupnost pro zadaný produkt a SKU pomocí ID dostupnosti.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID produktu.

- ID SKU.

- ID dostupnosti.

## <a name="c"></a>C\#

Pokud chcete získat podrobnosti o konkrétní [dostupnosti](product-resources.md#availability), začněte pomocí kroků v části [získání skladové položky podle ID](get-a-sku-by-id.md) , abyste získali rozhraní pro konkrétní [skladové](product-resources.md#sku) operace. Ve výsledném rozhraní vyberte vlastnost **Nákup** a získejte rozhraní s dostupnými operacemi pro nákup dostupnosti. Potom předejte ID dostupnosti metodě **ById ()** , abyste získali operace pro konkrétní dostupnost a pak volali **Get ()** nebo **GetAsync ()** pro načtení podrobností o dostupnosti.

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

Pokud chcete získat podrobnosti o konkrétní [dostupnosti](product-resources.md#availability), začněte pomocí kroků v části [získání skladové položky podle ID](get-a-sku-by-id.md) , abyste získali rozhraní pro konkrétní [skladové](product-resources.md#sku) operace. Z výsledného rozhraní vyberte funkci **getAvailabilities** , abyste získali rozhraní s dostupnými operacemi pro nákup dostupnosti. Potom předejte ID dostupnosti funkci **byId ()** , abyste získali operace pro konkrétní dostupnost a pak zavolali funkci **Get ()** pro načtení podrobností o dostupnosti.

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

Chcete-li získat podrobnosti o [konkrétní dostupnosti](product-resources.md#availability), spusťte příkaz [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) a zadejte parametry **AvailabilityId**, **CountryCode**, **ProductID** a **SkuId** pro načtení podrobností o dostupnosti.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/skus/{SKU-ID}/availabilities/{Availability-ID}? Country = {Country-Code} HTTP/1.1         |

### <a name="uri-parameter"></a>Parametr URI

K získání konkrétní dostupnosti pomocí ID dostupnosti použijte následující cestu a parametry dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ID produktu             | řetězec   | Yes      | Řetězec ve formátu GUID, který identifikuje produkt.            |
| SKU – ID                 | řetězec   | Yes      | Řetězec ve formátu GUID, který identifikuje SKU.                |
| ID dostupnosti        | řetězec   | Yes      | Řetězec ve formátu GUID, který identifikuje dostupnost.       |
| kód země           | řetězec   | Yes      | ID země nebo oblasti.                                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu obsahuje tělo odpovědi prostředek [dostupnosti](product-resources.md#availability) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

Tato metoda vrací následující kódy chyb:

| Stavový kód HTTP     | Kód chyby   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Produkt nebyl nalezen.                                                                                    |
| 404                  | 400018       | SKU se nepovedlo najít.                                                                                        |
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
