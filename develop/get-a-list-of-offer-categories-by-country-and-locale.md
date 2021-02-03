---
title: Získání seznamu kategorií nabídek podle trhu
description: Jak získat kolekci, která obsahuje všechny kategorie nabídek v dané zemi nebo oblasti a národním prostředí.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 22c46ed03a8579c53ee18c14cbca9a1e19ddb82a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766932"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>Získání seznamu kategorií nabídek podle trhu

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak získat kolekci, která obsahuje všechny kategorie nabídek v dané zemi nebo oblasti a národním prostředí.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

## <a name="c"></a>C\#

Postup získání seznamu kategorií nabídek v dané zemi nebo oblasti a národním prostředí:

1. K volání metody [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) v daném kontextu použijte kolekci [**IAggregatePartner. Operations.**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner)

2. Zkontrolujte vlastnost [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) výsledného objektu.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

Příklad naleznete v následujících tématech:

- Ukázka: [aplikace testů konzoly](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSample**
- Třída: **PartnerSDK. FeatureSample**

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories? Country = {Country-ID} HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání kategorií nabídek.

| Název           | Typ       | Vyžadováno | Popis            |
|----------------|------------|----------|------------------------|
| **ID země** | **řetezce** | Y        | ID země nebo oblasti |

### <a name="request-headers"></a>Hlavičky požadavku

Je vyžadováno **ID národního prostředí** naformátovaného jako řetězec.

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí kolekci prostředků **OfferCategory** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
