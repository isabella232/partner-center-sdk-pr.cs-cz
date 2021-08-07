---
title: Získání cen pro Microsoft Azure
description: Jak získat ceníkovou kartu Azure s cenami v reálném čase pro nabídku Azure Ceny Azure jsou poměrně dynamické a často se mění.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b69e9e3d8e6e4c4e447b308c890c4c054e6a1e5221bb523a5caca041d1ea115
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989087"
---
# <a name="get-prices-for-microsoft-azure"></a>Získání cen pro Microsoft Azure

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat [ceníkovou kartu Azure](azure-rate-card-resources.md) s cenami v reálném čase pro nabídku Azure Ceny Azure jsou poměrně dynamické a často se mění.

Pokud chcete sledovat využití a pomoct s předpovídáním měsíčních faktur a faktur pro jednotlivé zákazníky, můžete zkombinovat tento dotaz na kartu sazeb Azure a získat ceny za Microsoft Azure s žádostí o získání záznamů o využití azure [zákazníkem.](get-a-customer-s-utilization-record-for-azure.md)

Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění. Ve výchozím nastavení rozhraní API používá nastavení profilu partnera v Partnerské centrum a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná. Povědomí o umístění je zvlášť důležité, pokud spravujete prodeje na několika trzích z jedné centralizované kanceláře. Další informace najdete v tématu Parametry [identifikátoru URI.](#uri-parameters)

## <a name="c"></a>C\#

Pokud chcete získat kartu sazeb Azure, zavolejte metodu [**IAzureRateCard.Get,**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) která vrátí prostředek [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) obsahující ceny Azure.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class**: GetAzureRateCard.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pokud chcete získat kartu sazeb Azure, zavolejte **funkci IAzureRateCard.get,** která vrátí podrobnosti o kartě sazeb, která obsahuje ceny Azure.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pokud chcete získat kartu Azure, spusťte příkaz [**Get-PartnerAzureRateCard,**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) který vrátí podrobnosti o kartě sazeb, která obsahuje ceny Azure.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                        |
|---------|--------------------------------------------------------------------|
| **Dostat** | *{baseURL}*/v1/ratecards/azure?currency={currency}&region={region} |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Název     | Typ   | Vyžadováno | Popis                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | řetězec | No       | Volitelný třípísmenný kód ISO pro měnu, ve které budou uvedeny sazby prostředků (například `EUR` ). Výchozí formát je `USD`. |
| oblast   | řetězec | No       | Volitelný dvoupísmenný kód ISO země/oblasti, který označuje trh, na kterém je nabídka zakoupená (například `FR` ). Výchozí formát je `US`.        |

Do požadavku můžete zahrnout volitelnou [hlavičku](headers.md#rest-request-headers) X-Locale. Pokud hlavičku X-Locale nezadáte, použije se výchozí hodnota (en-US).

- Pokud v požadavku zadáte parametry měny a oblasti, hodnota X-národního prostředí se použije k určení jazyka odpovědi.

- Pokud v požadavku nezadáte parametry oblasti a měny, hodnota X-národního prostředí se použije k určení oblasti, měny a jazyka odpovědi.

### <a name="request-header"></a>Hlavička požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

Pokud je požadavek úspěšný, vrátí prostředek [Azure Rate Card.](azure-rate-card-resources.md)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
