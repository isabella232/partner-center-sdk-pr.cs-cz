---
title: Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu
description: Tento článek vysvětluje, jak získat metadata smlouvy pro Smlouva se zákazníkem Microsoftu.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 5c20b317edf16b159050884070683880cf7e45bb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025713"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Metadata smlouvy pro Smlouva se zákazníkem Microsoftu se v současné době Partnerské centrum jenom ve veřejném cloudu Microsoftu.

Než budete moci Smlouva se zákazníkem Microsoftu:

- [Potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu](./confirm-customer-consent-customer-agreement.md)
- [Načtení odkazu ke stažení Smlouva se zákazníkem Microsoftu šablony](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.14 nebo novější.

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md) Tento scénář podporuje pouze ověřování aplikací a uživatelů.

## <a name="net-version-114-or-newer"></a>.NET (verze 1.14 nebo novější)

Načtení metadat smlouvy pro Smlouva se zákazníkem Microsoftu:

1. Nejprve načtěte **kolekci IAggregatePartner.AgreementDetails.**

2. Voláním **metody ByAgreementType** vyfiltrujte kolekci, Smlouva se zákazníkem Microsoftu.

3. Nakonec zavolejte **metodu Get** **nebo GetAsync.**

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Úplnou ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [konzolové testovací aplikace.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>Požadavek REST

Načtení metadat smlouvy pro Smlouva se zákazníkem Microsoftu:

1. Vytvořte požadavek REST pro načtení [kolekce AgreementMetaData.](./agreement-metadata-resources.md)

2. Parametr dotazu **agreementType** použijte k nastavení rozsahu výsledku pouze na Smlouva se zákazníkem Microsoftu.

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Název                   | Typ     | Vyžadováno | Popis                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| agreement-type | řetězec | No | Tento parametr použijte k nastavení rozsahu odpovědi na dotaz na konkrétní typ smlouvy. Podporované hodnoty jsou: <br/><br/>**MicrosoftCloudAgreement,** který zahrnuje jenom metadata smlouvy typu *MicrosoftCloudAgreement*<br/><br/>**MicrosoftCustomerAgreement,** který obsahuje metadata smlouvy pouze typu *MicrosoftCustomerAgreement*.<br/><br/>**\**– vrátí všechna metadata smlouvy. (Nepoužívejte _* \* _ pokud váš kód nemá potřebnou logiku modulu runtime pro zpracování neznámých typů smlouvy, protože Microsoft může kdykoli zavést metadata smlouvy s novými *typy smlouvy.) <br/> <br/> _* Poznámka:** Pokud není zadaný parametr URI, výchozí hodnota dotazu je **MicrosoftCloudAgreement** pro zpětnou kompatibilitu.  |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu vrátí tato metoda v textu odpovědi kolekci prostředků [ **AgreementMetaData.**](./agreement-metadata-resources.md)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.

K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
