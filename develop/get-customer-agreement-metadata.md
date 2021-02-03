---
title: Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu
description: Tento článek vysvětluje, jak získat metadata smlouvy pro zákaznickou smlouvu Microsoftu.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766895"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu

**Platí pro:**

- Partnerské centrum

Metadata smlouvy pro zákaznickou smlouvu Microsoft jsou aktuálně podporována partnerským centrem pouze ve *veřejném cloudu společnosti Microsoft*. Neplatí pro:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Metadata smlouvy pro zákaznickou smlouvu od Microsoftu musíte načíst, abyste mohli:

- [Potvrzení souhlasu zákazníka s zákaznickou smlouvou Microsoftu](./confirm-customer-consent-customer-agreement.md)
- [Načtení odkazu ke stažení pro šablonu zákaznické smlouvy Microsoft](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu SDK partnerského centra .NET, verze 1,14 nebo novější je povinná.

- Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md). Tento scénář podporuje jenom ověřování uživatelů a aplikací.

## <a name="net-version-114-or-newer"></a>.NET (verze 1,14 nebo novější)

Načtení metadat smlouvy pro zákaznickou smlouvu Microsoftu:

1. Nejdřív načtěte kolekci **IAggregatePartner. AgreementDetails** .

2. Zavolejte metodu **ByAgreementType** , která filtruje kolekci na zákaznickou smlouvu Microsoftu.

3. Nakonec volejte metodu **Get** nebo **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Kompletní ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Žádost REST

Načtení metadat smlouvy pro zákaznickou smlouvu Microsoftu:

1. Vytvořte žádost REST pro načtení kolekce [AgreementMetaData](./agreement-metadata-resources.md) .

2. Použijte parametr dotazu **agreemtntype** k určení oboru výsledků jenom pro zákaznickou smlouvu Microsoftu.

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Agreements? agreemtntype = {smlouva-Type} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Název                   | Typ     | Vyžadováno | Popis                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| typ smlouvy | řetězec | No | Tento parametr slouží k určení rozsahu odpovědi dotazu na konkrétní typ smlouvy. Podporované hodnoty jsou: <br/><br/>**MicrosoftCloudAgreement** , která zahrnuje metadata smlouvy pouze typu *MicrosoftCloudAgreement*<br/><br/>**MicrosoftCustomerAgreement** , která zahrnuje metadata smlouvy pouze typu *MicrosoftCustomerAgreement*.<br/><br/>**\*** který vrátí všechna metadata smlouvy. (Nepoužívejte **\*** , pokud váš kód nemá nezbytnou běhovou logiku pro zpracování neznámých typů smluv, protože společnost Microsoft může zavést metadata smlouvy s novými typy smluv kdykoli.)<br/><br/> **Poznámka:** Pokud není zadán parametr URI, výchozí dotaz se **MicrosoftCloudAgreement** na zpětnou kompatibilitu.  |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí kolekci [prostředků **AgreementMetaData**](./agreement-metadata-resources.md) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.

Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
