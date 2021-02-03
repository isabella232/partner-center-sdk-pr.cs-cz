---
title: Získání cen pro Microsoft Azure
description: Jak získat kartu Azure Rate s cenami v reálném čase pro nabídku Azure. Ceny Azure jsou poměrně dynamické a často se mění.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0716f0428b13604105b435a2ce8287a8b4609fea
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/19/2020
ms.locfileid: "97767669"
---
# <a name="get-prices-for-microsoft-azure"></a>Získání cen pro Microsoft Azure

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak získat [kartu Azure Rate](azure-rate-card-resources.md) s cenami v reálném čase pro nabídku Azure. Ceny Azure jsou poměrně dynamické a často se mění.

Pokud chcete sledovat využití a předpovídat měsíční fakturaci a faktury pro jednotlivé zákazníky, můžete tento dotaz na kartu Azure Rate kombinovat a získat tak ceny Microsoft Azure s žádostí o [získání záznamů o využití zákazníka pro Azure](get-a-customer-s-utilization-record-for-azure.md).

Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění. Ve výchozím nastavení používá rozhraní API nastavení partnerského profilu v partnerském centru a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná. Povědomí o poloze je obzvláště důležité, pokud spravujete prodej na více trzích z jedné centrálně centralizované kanceláře. Další informace najdete v tématu [parametry identifikátoru URI](#uri-parameters).

## <a name="c"></a>C\#

Pokud chcete získat kartu Azure Rate, zavolejte metodu [**IAzureRateCard. Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) , která vrátí prostředek [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) , který obsahuje ceny Azure.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetAzureRateCard.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pokud chcete získat kartu Azure Rate, zavolejte funkci **IAzureRateCard. Get** , která vrátí podrobnosti o sazbách, které obsahují ceny Azure.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pokud chcete získat kartu Azure, spusťte příkaz [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) , který vrátí podrobnosti o ceníku, který obsahuje ceny Azure.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                        |
|---------|--------------------------------------------------------------------|
| **Čtěte** | *{baseURL}*/v1/ratecards/Azure? Currency = {currency} &oblast = {region} |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Název     | Typ   | Vyžadováno | Popis                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | řetězec | No       | Volitelná tři písmena ISO kódu pro měnu, ve které se budou poskytovat sazby za prostředky (například `EUR` ). Výchozí formát je `USD`. |
| oblast   | řetězec | No       | Volitelné dvoumístné číslo země/oblasti ISO, které označuje uvedení na trh, na který byla nabídka koupena (například `FR` ). Výchozí formát je `US`.        |

Do žádosti můžete zahrnout volitelné [záhlaví](headers.md#rest-request-headers) X-locale. Pokud nezadáte hlavičku X-locale, použije se výchozí hodnota ("en-US").

- Pokud v žádosti zadáte parametry měny a oblasti, použije se k určení jazyka odpovědi hodnota X-locale.

- Pokud v požadavku neposkytnete parametry region a Currency, použije se k určení oblasti, měny a jazyka odpovědi hodnota X-locale.

### <a name="request-header"></a>Hlavička požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
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
    "locale": "en",
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
