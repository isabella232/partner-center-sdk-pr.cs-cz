---
title: Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu
description: Tento článek vysvětluje, jak získat metadata smlouvy pro zákaznickou smlouvu Microsoftu.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 384fa227a103ed10dc2fd055afa7688d3b2a418504360eb4a5025615cf2a4f67
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989351"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu

**Platí pro**: partnerské Centrum

Nevztahuje **se na**: partnerské Centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Metadata smlouvy pro zákaznickou smlouvu Microsoft jsou aktuálně podporována partnerským centrem pouze ve veřejném cloudu společnosti Microsoft.

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
| typ smlouvy | řetězec | No | Tento parametr slouží k určení rozsahu odpovědi dotazu na konkrétní typ smlouvy. Podporované hodnoty jsou: <br/><br/>**MicrosoftCloudAgreement** , která zahrnuje metadata smlouvy pouze typu *MicrosoftCloudAgreement*<br/><br/>**MicrosoftCustomerAgreement** , která zahrnuje metadata smlouvy pouze typu *MicrosoftCustomerAgreement*.<br/><br/>**\**_, který vrátí všechna metadata smlouvy. (Nepoužívat _* \* *_ Pokud váš kód nemá nezbytnou běhovou logiku pro zpracování neznámých typů smluv, protože společnost Microsoft může v každém okamžiku zavést metadata smlouvy s novými typy smluv.) <br/> <br/> _* Poznámka:** Pokud není ZADÁN parametr URI, je výchozí hodnota dotazu **MicrosoftCloudAgreement** na zpětnou kompatibilitu.  |

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
