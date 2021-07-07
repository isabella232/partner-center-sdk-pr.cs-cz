---
title: Potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Zjistěte, jak potvrdit přijetí služby zákazníkem Smlouva se zákazníkem Microsoftu pomocí Partnerské centrum API.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 002508109191ede53cd06f25efc38286647fd67c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974008"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu pomocí Partnerské centrum API

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Partnerské centrum v současné době podporuje potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu pouze ve veřejném cloudu Microsoftu.

Tento článek popisuje, jak potvrdit nebo znovu potvrdit souhlas zákazníka s Smlouva se zákazníkem Microsoftu.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.14 nebo novější.

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md) *Tento scénář podporuje pouze ověřování aplikací a uživatelů.*

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Datum **(dateAgreed),** kdy zákazník přijal Smlouva se zákazníkem Microsoftu.

- Informace o uživateli z organizace zákazníka, který přijal Smlouva se zákazníkem Microsoftu. Sem patří:
  - Jméno
  - Příjmení
  - E-mailová adresa
  - Telefon číslo (volitelné)
- Pokud se pro zákazníka změní následující hodnoty, umožní Partnerské centrum vytvořit pro tohoto zákazníka jinou smlouvu: Jméno Příjmení E-mailová adresa Telefon číslo V opačném případě partneři obdrží následující kód chyby kvůli vytvoření duplicitního zákazníka.


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

Potvrzení nebo potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu:

1. Načtěte metadata smlouvy pro Smlouva se zákazníkem Microsoftu. Je nutné získat **templateId** Smlouva se zákazníkem Microsoftu. Další informace najdete v tématu [Získání metadat smlouvy pro Smlouva se zákazníkem Microsoftu](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Vytvořte nový objekt **Agreement** obsahující podrobnosti o potvrzení.

3. Použijte kolekci **IAgreggatePartner.Customers** a zavolejte metodu **ById** se zadaným **ID tenanta zákazníka**.

4. Použijte vlastnost **Agreements** a pak zavoláte **Create** nebo **CreateAsync.**

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

Úplnou ukázku najdete ve třídě [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) z projektu [konzolové testovací](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) aplikace.

## <a name="rest-request"></a>Požadavek REST

Potvrzení nebo potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu:

1. Načtěte metadata smlouvy pro Smlouva se zákazníkem Microsoftu. Je nutné získat **templateId** Smlouva se zákazníkem Microsoftu. Další informace najdete v tématu [Získání metadat smlouvy pro Smlouva se zákazníkem Microsoftu](get-customer-agreement-metadata.md).

2. Vytvořte nový prostředek [ **smlouvy,** abyste](agreement-resources.md) potvrdili, že zákazník přijal Smlouva se zákazníkem Microsoftu. Použijte následující [syntaxi požadavku REST.](#request-syntax)

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/smlouvy HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Pomocí následujícího parametru dotazu zadejte zákazníka, který potvrzujete.

| Název               | Typ | Vyžadováno | Popis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | Identifikátor GUID | Yes | Hodnota je id tenanta zákazníka ve **formátu** GUID, což je identifikátor, který umožňuje zadat zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu požadavku REST.

| Název      | Typ   | Description                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Smlouva | object | Podrobnosti poskytnuté partnerem pro potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu. |

#### <a name="agreement"></a>Smlouva

Tato tabulka popisuje minimální požadovaná pole pro vytvoření [ **prostředku** smlouvy.](agreement-resources.md)

| Vlastnost       | Typ   | Description                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Kontakt](./utility-resources.md#contact) | Informace o uživateli z organizace zákazníka, který přijal Smlouva se zákazníkem Microsoftu, včetně:  **jméno,** **příjmení,** **e-mail** a **telefonní číslo** (volitelné) |
| datum odgreed     | řetězec ve formátu data a času UTC |Datum, kdy zákazník smlouvu přijal. |
| ID šablony     | řetězec | Jedinečný identifikátor typu smlouvy přijatého zákazníkem Můžete získat **templateId pro** Smlouva se zákazníkem Microsoftu načtením metadat smlouvy pro Smlouva se zákazníkem Microsoftu. Podrobnosti [najdete v tématu Smlouva se zákazníkem Microsoftu](./get-customer-agreement-metadata.md) smlouvy. |
| typ           | řetězec | Typ smlouvy přijatý zákazníkem. Pokud zákazník přijal Smlouva se zákazníkem Microsoftu. |

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

V případě úspěchu vrátí tato metoda [ **prostředek smlouvy**](./agreement-resources.md).

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.

K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
