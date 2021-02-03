---
title: Získání potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Tento článek vysvětluje, jak získat potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766897"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Získání potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka

**Platí pro:**

- Partnerské centrum

V současné době je prostředek **smlouvy** podporován partnerským centrem pouze ve *veřejném cloudu Microsoftu*. Tento prostředek se nevztahuje na:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek vysvětluje, jak můžete získat potvrzení přijetí smlouvy o zákaznících Microsoftu u zákazníka.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu SDK partnerského centra .NET, verze 1,14 nebo novější je povinná.

- Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md). Tento scénář podporuje jenom ověřování aplikací a uživatelů.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="net"></a>.NET

Chcete-li získat potvrzení o přijetí od zákazníka, které bylo dříve poskytnuto:

- Použijte kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById** se zadaným identifikátorem zákazníka.

- Načtěte vlastnost **smluvs** a Filtrujte výsledky do smlouvy na zákazníky Microsoftu voláním metody **ByAgreementType** .

- Volejte metodu **Get** nebo **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Kompletní ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Žádost REST

Chcete-li získat potvrzení přijetí od zákazníka, které bylo dříve poskytnuto:

1. Vytvořte žádost REST, aby se načetla kolekce [smluv](./agreement-resources.md) pro zákazníka.

2. Použijte parametr dotazu **agreemtntype** k určení oboru výsledků jenom na zákaznickou smlouvu Microsoftu.

### <a name="request-syntax"></a>Syntaxe žádosti

Použijte následující syntaxi žádosti:

| Metoda | Identifikátor URI žádosti                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements? agreemtntype = {smlouva-Type} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

S vaším požadavkem můžete použít následující parametry identifikátoru URI:

| Název             | Typ | Vyžadováno | Popis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| Customer-tenant-ID | Identifikátor GUID | Yes | Hodnota je **CustomerTenantId** ve formátu GUID, který umožňuje zadat zákazníka. |
| typ smlouvy | řetězec | No | Tento parametr vrátí všechna metadata smlouvy. Tento parametr slouží k určení rozsahu odpovědi dotazu na konkrétní typ smlouvy. Podporované hodnoty jsou: <br/><br/> **MicrosoftCloudAgreement** , která zahrnuje pouze metadata smlouvy typu *MicrosoftCloudAgreement*.<br/><br/> **MicrosoftCustomerAgreement** , která zahrnuje pouze metadata smlouvy typu *MicrosoftCustomerAgreement*.<br/><br/> **\*** který vrátí všechna metadata smlouvy. (Nepoužívejte **\*** , pokud váš kód nemá potřebnou logiku pro zpracování neočekávaných typů smluv.)<br/><br/> **Poznámka:** Pokud není zadán parametr URI, výchozí dotaz se **MicrosoftCloudAgreement** na zpětnou kompatibilitu. Společnost Microsoft může v každé chvíli zavést metadata smlouvy s novými typy smluv.  |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí kolekci prostředků **smlouvy** v těle odpovědi.

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
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
