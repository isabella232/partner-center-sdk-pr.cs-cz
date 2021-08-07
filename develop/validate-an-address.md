---
title: Ověření adresy
description: Jak ověřit adresu pomocí rozhraní API pro ověření adresy.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0d3c27a763887e89e1116dbaf605db349369036c38378011dcca3fa07732a738
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989233"
---
# <a name="validate-an-address"></a>Ověření adresy

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Jak ověřit adresu pomocí rozhraní API pro ověření adresy.

Rozhraní API pro ověření adresy by se mělo používat jenom pro předběžné ověření aktualizací profilu zákazníka. Použijte ho s porozuměním, že pokud je země USA, Kanada, Čína nebo Mexiko, pole State se ověří podle seznamu platných stavů pro příslušnou zemi. Ve všech ostatních zemích tento test neproběhne a rozhraní API kontroluje, zda je stav platný řetězec.

## <a name="prerequisites"></a>Požadavky

Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

## <a name="c"></a>C\#

Chcete-li ověřit adresu, nejprve vytvořte instanci nového objektu **adresy** a naplňte ji na adresu, kterou chcete ověřit. Pak načtěte rozhraní k operacím **ověřování** z vlastnosti **IAggregatePartner. valids** a zavolejte metodu **IsAddressValid** s objektem adresy.

```csharp
IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",
    Country = "US"
};

// Validate the address.
AddressValidationResponse result = partnerOperations.Validations.IsAddressValid(address);

// If the request completes successfully, you can inspect the response object.

// See the status of the validation.
Console.WriteLine($"Status: {addressValidationResult.Status}");

// See the validation message returned.
Console.WriteLine($"Validation Message Returned: {addressValidationResult.ValidationMessage ?? "No message returned."}");

// See the original address submitted for validation.
Console.WriteLine($"Original Address:\n{this.DisplayAddress(addressValidationResult.OriginalAddress)}");

// See the suggested addresses returned by the API, if any exist.
Console.WriteLine($"Suggested Addresses Returned: {addressValidationResult.SuggestedAddresses?.Count ?? "None."}");

if (addressValidationResult.SuggestedAddresses != null && addressValidationResult.SuggestedAddresses.Any())
{
    addressValidationResult.SuggestedAddresses.ForEach(a => Console.WriteLine(this.DisplayAddress(a)));
}

// Helper method to pretty-print an Address object.
private string DisplayAddress(Address address)
{
    StringBuilder sb = new StringBuilder();

    foreach (var property in address.GetType().GetProperties())
    {
        sb.AppendLine($"{property.Name}: {property.GetValue(address) ?? "None to Display."}");
    }

    return sb.ToString();
}
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                 |
|----------|-----------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/validations/Address HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu žádosti.

| Název         | Typ   | Vyžadováno | Popis                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | řetězec | Y        | První řádek adresy                             |
| addressline2 | řetězec | N        | Druhý řádek adresy. Tato vlastnost je nepovinná. |
| city         | řetězec | Y        | Město.                                                  |
| state        | řetězec | Y        | Stav                                                 |
| ovládacím   | řetězec | Y        | Poštovní směrovací číslo.                                           |
| country      | řetězec | Y        | Kód země ISO alfa-2 se dvěma znaky.                |

### <a name="response-details"></a>Podrobnosti odpovědi

Odpověď vrátí jednu z následujících stavových zpráv:

| Status     | Popis |    Počet vrácených navrhovaných adres |
|-------|---------------|-------------------|
|Ověřené pro přepravce | Adresa je ověřena a může být expedována. | Jednoduché |
|Ověřují | Adresa je ověřena. | Jednoduché |
|Je vyžadována interakce | Navrhovaná adresa se významně změnila a potřebuje potvrzení uživatele. | Jednoduché |
|Částečně ulice | Daná ulice v adrese je částečně a potřebuje další informace. | Více – maximálně tři |
|Částečně místní | Dané prostory (stavební číslo, číslo sady a další) jsou částečné a vyžadují další informace. | Více – maximálně tři |
|Několik | Adresa obsahuje několik polí, která jsou v této adrese částečně (případně i částečně a částečně v ulici). | Více – maximálně tři |
|Žádná | Adresa je nesprávná. | Žádná |
|Není ověřeno. | Adresu nelze odeslat prostřednictvím procesu ověřování. | Žádná |

### <a name="request-example"></a>Příklad požadavku

```http
# "VerifiedShippable" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
Host: api.partnercenter.microsoft.com
Content-Length: 137
X-Locale: en-US

{
    "AddressLine1": "1 Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}

# "StreetPartial" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
Host: api.partnercenter.microsoft.com
Content-Length: 135
X-Locale: en-US

{
    "AddressLine1": "Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu metoda vrátí objekt **AddressValidationResponse** v těle odpovědi se stavovým kódem **http 200** . Příklad najdete níže.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
# "VerifiedShippable" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:19:19 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-8300"
        }
    ],
    "status": "VerifiedShippable"
}

# "StreetPartial" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:34:08 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-6399"
        }
    ],
    "status": "StreetPartial",
    "validationMessage": "Address field invalid for property: 'Region', 'PostalCode', 'City'"
}
```
