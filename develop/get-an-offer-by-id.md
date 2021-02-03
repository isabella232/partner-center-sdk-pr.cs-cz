---
title: Získání nabídky podle ID
description: Získá prostředek nabídky, který odpovídá ID nabídky.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: 9448276e817affb823eddabbcab8757c79615fbd
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767054"
---
# <a name="get-an-offer-by-id"></a>Získání nabídky podle ID

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Získá prostředek **nabídky** , který odpovídá ID nabídky.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID nabídky

## <a name="c"></a>C\#

Chcete-li najít konkrétní nabídku podle ID, použijte svou kolekci **IAggregatePartner.** offers, vytvořte zemi se voláním **ByCountry ()** a poté zavolejte metodu [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) . Pak zavolejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) nebo [**Get Async ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) .

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample **Třída**: GetOffer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Chcete-li najít konkrétní nabídku podle ID, použijte funkci **IAggregatePartner. res** , stanovte zemi voláním funkce **byCountry ()** a potom zavolejte funkci **byID ()** . Pak zavolejte funkci **Get ()** .

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Chcete-li najít konkrétní nabídku podle ID, spusťte příkaz [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) a zadejte parametry **CountryCode** a **hodnotami OfferId** .

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{Offer-ID}? Country = {Country-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

| Název           | Typ       | Vyžadováno | Popis                           |
|----------------|------------|----------|---------------------------------------|
| **ID nabídky**   | **guid**   | Y        | Identifikátor GUID, který odpovídá této nabídce |
| **ID země** | **řetezce** | Y        | ID země nebo oblasti                |

### <a name="request-headers"></a>Hlavičky požadavku

- Je vyžadováno **ID národního prostředí** naformátovaného jako řetězec.
Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v těle odpovědi prostředek **nabídky** .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Mon, 23 Nov 2015 23:13:01 GMT

{
    "id": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "name": "Office 365 Business Premium",
    "description": "For businesses with 1 to 300 users that need the latest desktop version of Office,
                    plus anywhere access to email, filesharing, and online conferencing.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "rank": 56,
    "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/031C9E47-4802-4248-838E-778FB1D2CC05",
    "locale": "en-us",
    "country": "US",
    "category": {
        "id": "SmallBusiness_Key",
        "name": "Small Business",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    "prerequisiteOffers": [],
    "isAddOn": false,
    "isAvailableForPurchase": true,
    "billing": "license",
    "isAutoRenewable": true,
    "product": {
        "id": "f245ecc8-75af-4f8e-b61f-27d8114de5f3",
        "name": "Office 365 Business Premium",
        "unit": "Licenses"
    },
    "unitType": "Licenses",
    "links": {
        "learnMore": {
            "uri": "http: //g.microsoftonline.com/0BXPS00en/909",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Offer"
    }
}
```
