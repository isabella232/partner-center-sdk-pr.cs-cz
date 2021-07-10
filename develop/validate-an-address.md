---
title: Ověření adresy
description: Jak ověřit adresu pomocí rozhraní API pro ověřování adres
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2eeca91b0e5a507dac6df4ecf61a56aed2d2d921
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572076"
---
# <a name="validate-an-address"></a>Ověření adresy

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Jak ověřit adresu pomocí rozhraní API pro ověřování adres

Rozhraní API pro ověřování adres by se mělo používat jenom pro předběžné ověření aktualizací profilů zákazníků. Použijte ho s pochopením, že pokud je země USA, Kanada, Čína nebo Mexiko, pole státu se ověří na seznamu platných států pro příslušnou zemi. Ve všech ostatních zemích k tomuto testu nedochází a rozhraní API kontroluje pouze to, že stav je platný řetězec.

## <a name="prerequisites"></a>Požadavky

Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

## <a name="c"></a>C\#

Pokud chcete ověřit adresu, nejprve vytvořte instanci nového objektu **Address** a naplňte ji adresou, která se má ověřit. Pak z vlastnosti  **IAggregatePartner.Validations** načtěte rozhraní pro operace Ověření a zavolejte metodu **IsAddressValid** s objektem address.

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

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                 |
|----------|-----------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu požadavku.

| Název         | Typ   | Vyžadováno | Popis                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | řetězec | Y        | První řádek adresy.                             |
| addressline2 | řetězec | N        | Druhý řádek adresy. Tato vlastnost je nepovinná. |
| city         | řetězec | Y        | Město.                                                  |
| state        | řetězec | Y        | Stav                                                 |
| Postalcode   | řetězec | Y        | PSČ                                           |
| country      | řetězec | Y        | Dvoupísový kód země iso alpha-2.                |

### <a name="response-details"></a>Podrobnosti odpovědi

Odpověď vrátí jednu z následujících stavových zpráv:

| Status     | Popis |    Počet vrácených navrhovaných adres |
|-------|---------------|-------------------|
|Ověřená expedice | Adresa je ověřená a je možné ji poslat na adresu . | Jednoduché |
|Ověřené | Adresa je ověřená. | Jednoduché |
|Vyžaduje se interakce | Navrhovaná adresa se výrazně změnila a vyžaduje potvrzení uživatele. | Jednoduché |
|Částečná ulice | Ulice v adrese je částečná a potřebuje další informace. | Více – maximálně tři |
|Částečně místní | Dané prostory (číslo budovy, číslo sady a další) jsou částečné a potřebují další informace. | Více – maximálně tři |
|Několik | V adrese je několik polí, která jsou částečná (potenciálně také částečná ulice a částečná část místně). | Více – maximálně tři |
|Žádná | Adresa je nesprávná. | Žádná |
|Není ověřeno. | Adresu nebylo možné odeslat prostřednictvím procesu ověřování. | Žádná |

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

V případě úspěchu vrátí metoda v textu odpovědi objekt **AddressValidationResponse** se stavový **kódem HTTP 200.** Příklad najdete níže.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
