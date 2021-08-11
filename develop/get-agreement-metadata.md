---
title: Získání metadat smluv pro Smlouvu o službách Microsoft Cloud
description: Tento článek vysvětluje, jak získat metadata smlouvy pro Smlouva o službách Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 55a09752844f74caaf878f1e2dcfe3d8a70a283c5e0e9daefba89c558405690a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994111"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Získání metadat smluv pro Smlouvu o službách Microsoft Cloud

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **AgreementMetaData** aktuálně podporuje Partnerské centrum ve veřejném cloudu Microsoftu.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.9 nebo novější.

- Pokud používáte sadu Java SDK Partnerské centrum, vyžaduje se verze 1.8 nebo novější.

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md) Tento scénář podporuje ověřování aplikací a uživatelů.

## <a name="net-version-114-or-newer"></a>.NET (verze 1.14 nebo novější)

Načtení metadat smlouvy pro Smlouva o službách Microsoft Cloud:

1. Nejprve načtěte **kolekci IAggregatePartner.AgreementDetails.**

2. Voláním **metody ByAgreementType** vyfiltrujte kolekci, Smlouva o službách Microsoft Cloud.

3. Nakonec zavolejte **metodu Get** **nebo GetAsync.**

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Úplnou ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [konzolové testovací aplikace.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="net-version-19---113"></a>.NET (verze 1.9 – 1.13)

Načtení metadat smlouvy pro Smlouva o službách Microsoft Cloud:

Nejprve načtěte **kolekci IAggregatePartner.AgreementDetails** a potom zavolejte **metody Get** nebo **GetAsync.** Pak vyhledejte položku v kolekci , která odpovídá Smlouva o službách Microsoft Cloud:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Načtení metadat smlouvy pro Smlouva o službách Microsoft Cloud:

Nejprve **zavolejte funkci IAggregatePartner.getAgreementDetails** a potom zavolejte **funkci get.** Pak vyhledejte položku v kolekci , která odpovídá Smlouva o službách Microsoft Cloud:

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

Úplnou ukázku najdete ve třídě [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) z projektu [konzolové testovací aplikace.](https://github.com/Microsoft/Partner-Center-Java-Samples)

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Načtení metadat smlouvy pro Smlouva o službách Microsoft Cloud:

Použijte příkaz [**Get-PartnerAgreementDetail.**](/powershell/module/partnercenter/get-partneragreementdetail) Pak vyhledejte položku v kolekci , která odpovídá Smlouva o službách Microsoft Cloud:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>Požadavek REST

Pokud chcete načíst metadata smlouvy Smlouva o službách Microsoft Cloud, nejprve vytvořte požadavek REST pro načtení kolekce **AgreementMetaData.** Pak vyhledejte položku v kolekci, která odpovídá Smlouva o službách Microsoft Cloud.

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v textu odpovědi kolekci prostředků **AgreementMetaData.**

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

Pokud chcete v odpovědi identifikovat prostředek, který odpovídá Smlouva o službách Microsoft Cloud, vyhledejte prostředek, jehož vlastnost **agreementType** má hodnotu MicrosoftCloudAgreement.
