---
title: Získání cen pro partnerské sdílené služby Microsoft Azure
description: jak získat kartu Azure Rate s cenami za Microsoft Azure sdílené služby partnerských služeb
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 33ee82bb966dee459cdeef6691c5e86eb7369fc7f76117f9360ac51d6cb3da22
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995811"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a>Získání cen pro partnerské sdílené služby Microsoft Azure

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

jak získat [kartu Azure Rate](azure-rate-card-resources.md) s cenami za Microsoft Azure sdílené služby partnerských služeb

Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění. Ve výchozím nastavení používá rozhraní API nastavení partnerského profilu v partnerském centru a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná. Povědomí o poloze je obzvláště důležité, pokud spravujete prodej na více trzích z jedné centrálně centralizované kanceláře.

## <a name="example-code"></a>Příklad kódu

## <a name="c"></a>C\#

Pokud chcete získat kartu Azure Rate, zavolejte metodu [**IAzureRateCard. Getshared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) , která vrátí prostředek [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) , který obsahuje ceny Azure.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pokud chcete získat kartu Azure Rate, zavolejte funkci **IAzureRateCard. Getshared** , která vrátí podrobnosti o sazbách, které obsahují ceny Azure.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pokud chcete získat kartu Azure, spusťte příkaz [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) a zadejte parametr **SharedServices** , který vrátí podrobnosti o sazbách, které obsahují ceny Azure.

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                               |
|---------|---------------------------------------------------------------------------|
| **Čtěte** | *{baseURL}*/v1/ratecards/Azure-Shared? Currency = {currency} &oblast = {region} |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Název     | Typ   | Vyžadováno | Popis                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | řetězec | No       | Volitelná tři písmena ISO kódu pro měnu, ve které se budou poskytovat sazby za prostředky (například `EUR` ). Výchozí hodnota je měna přidružená k trhu v partnerském profilu. |
| oblast   | řetězec | No       | Volitelné dvoumístné číslo země/oblasti ISO, které označuje uvedení na trh, na který byla nabídka koupena (například `FR` ). Výchozím nastavením je kód země nebo oblasti nastavený v partnerském profilu.        |

Pokud je v požadavku zahrnutá volitelná hlavička X-locale, její hodnota určuje jazyk použitý pro podrobnosti v odpovědi.

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

Pokud je požadavek úspěšný, vrátí prostředek [Azure Rate karta](azure-rate-card-resources.md) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en-US",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
