---
title: Potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Přečtěte si, jak potvrdit přijetí zákaznických smluv Microsoftu pomocí rozhraní API partnerského centra.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62a6cebd5d6d093377dd5940dcff6204b7095c70
ms.sourcegitcommit: ebb36208d6e2dea705f62b7d60d471f10c55132e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/09/2021
ms.locfileid: "100006062"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Potvrzení souhlasu zákazníka se zákaznickou smlouvou Microsoftu pomocí rozhraní API partnerského centra

**Platí pro:**

- Partnerské centrum

Partnerské centrum v současné době podporuje potvrzení souhlasu zákazníka s zákaznickou smlouvou Microsoftu pouze ve *veřejném cloudu Microsoftu*. Tato funkce se v současnosti nevztahuje na:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak ověřit nebo znovu potvrdit přijetí smlouvy o zákaznících Microsoftu v rámci zákazníka.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu SDK partnerského centra .NET, verze 1,14 nebo novější je povinná.

- Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md). *Tento scénář podporuje jenom ověřování aplikací a uživatelů.*

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Datum (**dateAgreed**), kdy zákazník přijal smlouvu o zákaznících Microsoftu.

- Informace o uživateli od organizace zákazníka, která přijala zákaznickou smlouvu od Microsoftu. Sem patří:
  - Jméno
  - Příjmení
  - E-mailová adresa
  - Telefonní číslo (volitelné)
- Pokud se u zákazníka změní následující hodnoty, Partnerské centrum umožní vytvoření jiné smlouvy pro daného zákazníka: křestní jméno příjmení jméno e-mailové adresy. v opačném případě získají partneři následující kód chyby, protože se vytvořil duplicitní zákazník.


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a>.NET

Potvrzení nebo opětovné potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky:

1. Načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu. Musíte získat **TemplateID** smlouvy o zákaznících Microsoftu. Další podrobnosti najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Vytvořte nový objekt **smlouvy** obsahující podrobnosti o potvrzení.

3. Použijte kolekci **IAgreggatePartner. Customers** a zavolejte metodu **ById** se zadaným **identifikátorem Customer-tenant-ID**.

4. Použijte vlastnost **smlouvy** a potom zavoláním metody **Create** nebo **CreateAsync**.

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

Kompletní ukázku najdete ve třídě [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Žádost REST

Potvrzení nebo opětovné potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky:

1. Načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu. Musíte získat **TemplateID** smlouvy o zákaznících Microsoftu. Další podrobnosti najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](get-customer-agreement-metadata.md).

2. Vytvořte nový prostředek [ **smlouvy**](agreement-resources.md) , abyste si ověřili, že zákazník přijal zákaznickou smlouvu Microsoftu. Použijte následující [syntaxi žádosti REST](#request-syntax).

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Použijte následující parametr dotazu k určení zákazníka, kterého si potvrzujete.

| Název               | Typ | Vyžadováno | Popis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| Customer-tenant-ID | Identifikátor GUID | Ano | Hodnota je **číslo zákazníka**, který je ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v těle žádosti REST.

| Název      | Typ   | Description                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Smlouva | object | Podrobnosti poskytované partnerem k potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky. |

#### <a name="agreement"></a>Smlouva

Tato tabulka popisuje minimální požadovaná pole pro vytvoření [prostředku **smlouvy**](agreement-resources.md).

| Vlastnost       | Typ   | Description                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Kontakt](./utility-resources.md#contact) | Informace o uživateli od organizace zákazníka, která přijala smlouvu o zákaznících Microsoftu, včetně:  **FirstName**, **LastName**, **e-mail** a **phoneNumber** (volitelné) |
| dateAgreed     | řetězec ve formátu data a času UTC |Datum, kdy zákazník smlouvu přijal. |
| templateId     | řetězec | Jedinečný identifikátor typu smlouvy přijatého zákazníkem **TemplateID** pro smlouvu o zákaznících Microsoftu můžete získat tak, že načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu. Podrobnosti najdete v článku [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](./get-customer-agreement-metadata.md) . |
| typ           | řetězec | Typ smlouvy, kterou zákazník přijal. Pokud zákazník přijal zákaznickou smlouvu Microsoftu, použijte "MicrosoftCustomerAgreement". |

#### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda prostředek [ **smlouvy**](./agreement-resources.md).

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.

Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

#### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
