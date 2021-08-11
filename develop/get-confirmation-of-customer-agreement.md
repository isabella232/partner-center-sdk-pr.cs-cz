---
title: Získání potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Tento článek vysvětluje, jak získat potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f5e71f2660c6db638193deec02e9ba4f25a35be6aabdc1c4219f63b1f3295908
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993499"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Získání potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **smlouvy** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu.

Tento článek vysvětluje, jak můžete načíst potvrzení souhlasu zákazníka s přijetím Smlouva se zákazníkem Microsoftu.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.14 nebo novější.

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md) Tento scénář podporuje pouze ověřování aplikací a uživatelů.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="net"></a>.NET

Získání potvrzení přijetí zákazníkem, která byla dříve poskytnuta:

- Použijte kolekci **IAggregatePartner.Customers** a zavolejte **metodu ById** se zadaným identifikátorem zákazníka.

- **Načítá vlastnost Agreements** a filtruje výsledky, Smlouva se zákazníkem Microsoftu voláním **metody ByAgreementType.**

- Volejte **metodu Get** **nebo GetAsync.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Úplnou ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [konzolové testovací](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) aplikace.

## <a name="rest-request"></a>Požadavek REST

Získání dříve poskytnutého potvrzení přijetí zákazníkem:

1. Vytvořte požadavek REST pro načtení kolekce [Smluv](./agreement-resources.md) pro zákazníka.

2. Parametr dotazu **agreementType** použijte k nastavení rozsahu výsledků pouze na Smlouva se zákazníkem Microsoftu.

### <a name="request-syntax"></a>Syntaxe požadavku

Použijte následující syntaxi požadavku:

| Metoda | Identifikátor URI žádosti                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{id_tenanta_zákazníka}/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

S požadavkem můžete použít následující parametry identifikátoru URI:

| Název             | Typ | Vyžadováno | Popis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | Identifikátor GUID | Yes | Hodnota je identifikátor GUID naformátovaný **jako CustomerTenantId,** který umožňuje zadat zákazníka. |
| agreement-type | řetězec | No | Tento parametr vrátí všechna metadata smlouvy. Tento parametr použijte k nastavení rozsahu odpovědi na dotaz na konkrétní typ smlouvy. Podporované hodnoty jsou: <br/><br/> **MicrosoftCloudAgreement,** který obsahuje jenom metadata smlouvy typu *MicrosoftCloudAgreement*.<br/><br/> **MicrosoftCustomerAgreement,** který obsahuje jenom metadata smlouvy typu *MicrosoftCustomerAgreement*.<br/><br/> **\**– vrátí všechna metadata smlouvy. (Nepoužívejte _* \* *_ pokud váš kód nemá potřebnou logiku pro zpracování neočekávaných typů smlouvy.) <br/> <br/> _* Poznámka:** Pokud není zadaný parametr URI, výchozí hodnota dotazu je **MicrosoftCloudAgreement** pro zpětnou kompatibilitu. Microsoft může kdykoli zavést metadata smlouvy s novými typy smlouvy.  |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu vrátí tato  metoda v textu odpovědi kolekci prostředků smlouvy.

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
