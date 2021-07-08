---
title: Získání metadat smluv pro Smlouvu o službách Microsoft Cloud
description: Tento článek vysvětluje, jak získat metadata smlouvy pro Microsoft Cloud smlouvu.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 2588327e72a13de75eb9e02675edbd535491adc4
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760789"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Získání metadat smluv pro Smlouvu o službách Microsoft Cloud

**Platí pro**: partnerské Centrum

Nevztahuje **se na**: partnerské Centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **AgreementMetaData** je aktuálně podporovaný partnerským centrem jenom ve veřejném cloudu Microsoftu.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu SDK partnerského centra .NET, verze 1,9 nebo novější je povinná.

- Pokud používáte sadu SDK pro partnerský Center Java, verze 1,8 nebo novější je povinná.

- Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md). Tento scénář podporuje ověřování aplikací a uživatelů.

## <a name="net-version-114-or-newer"></a>.NET (verze 1,14 nebo novější)

Načtení metadat smlouvy pro Microsoft Cloud smlouvu:

1. Nejdřív načtěte kolekci **IAggregatePartner. AgreementDetails** .

2. Zavolejte metodu **ByAgreementType** pro filtrování kolekce do smlouvy Microsoft Cloud.

3. Nakonec volejte metodu **Get** nebo **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Kompletní ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="net-version-19---113"></a>.NET (verze 1,9 – 1,13)

Postup načtení metadat smlouvy pro Microsoft Cloud smlouvu:

Nejprve načtěte kolekci **IAggregatePartner. AgreementDetails** a poté zavolejte metody **Get** nebo **GetAsync** . Pak vyhledejte položku v kolekci, která odpovídá Microsoft Cloud smlouvě:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Postup načtení metadat smlouvy pro Microsoft Cloud smlouvu:

Nejprve zavolejte funkci **IAggregatePartner. getAgreementDetails** a poté zavolejte funkci **Get** . Pak vyhledejte položku v kolekci, která odpovídá Microsoft Cloud smlouvě:

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

Kompletní ukázku najdete ve třídě [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) z projektu [testovací aplikace konzoly](https://github.com/Microsoft/Partner-Center-Java-Samples) .

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Postup načtení metadat smlouvy pro Microsoft Cloud smlouvu:

Použijte příkaz [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) . Pak vyhledejte položku v kolekci, která odpovídá Microsoft Cloud smlouvě:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>Žádost REST

Pokud chcete načíst metadata smlouvy pro Microsoft Cloud smlouvu, nejdřív vytvořte žádost REST pro načtení kolekce **AgreementMetaData** . Pak vyhledejte položku v kolekci, která odpovídá Microsoft Cloud smlouvě.

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Agreements HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu tato metoda vrátí kolekci prostředků **AgreementMetaData** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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

Pro identifikaci prostředku v odpovědi, která odpovídá Microsoft Cloud smlouvě, vyhledejte prostředek, jehož vlastnost **agreemtntype** má hodnotu "MicrosoftCloudAgreement".
