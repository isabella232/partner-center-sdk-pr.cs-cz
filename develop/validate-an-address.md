---
title: Ověření adresy
description: Jak ověřit adresu pomocí rozhraní API pro ověření adresy.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 22d5faec2fdab4907067bb01cb74e110032dea9a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766728"
---
# <a name="validate-an-address"></a>Ověření adresy

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak ověřit adresu pomocí rozhraní API pro ověření adresy.

Rozhraní API pro ověření adresy by se mělo používat jenom pro předběžné ověření aktualizací profilu zákazníka. Použijte ho s porozuměním, že pokud je země USA, Kanada, Čína nebo Mexiko, pole State se ověří podle seznamu platných stavů pro příslušnou zemi. Ve všech ostatních zemích tento test neproběhne a rozhraní API kontroluje, zda je stav platný řetězec.

## <a name="prerequisites"></a>Požadavky

Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

## <a name="c"></a>C\#

Chcete-li ověřit adresu, nejprve vytvořte instanci nového objektu **adresy** a naplňte ji na adresu, kterou chcete ověřit. Pak načtěte rozhraní k operacím **ověřování** z vlastnosti **IAggregatePartner. valids** a zavolejte metodu **IsAddressValid** s objektem adresy.

```csharp
// IAggregatePartner partnerOperations;

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
bool result = partnerOperations.Validations.IsAddressValid(address);

// If the address is valid, the result should equal true.
Console.WriteLine("Result: " + result.ToString());

// The following is an example that causes address validation to fail.
try
{
    // Change to an invalid postal code for this address.
    address.PostalCode = "98007";

    // Validate the address.
    result = partnerOperations.Validations.IsAddressValid(address);

    Console.WriteLine("ERROR: The code should have thrown an exception - BadRequest(400).");
}
catch (PartnerException exception)
{
    if (exception.ErrorCategory == PartnerErrorCategory.BadInput)
    {
        Console.WriteLine(exception.ErrorCategory.ToString());
        Console.WriteLine("Exception:");
        Console.WriteLine("Message: {0}", exception.Message);
    }
    else
    {
        throw;
    }
}
```

## <a name="java"></a>Java

Chcete-li ověřit adresu, nejprve vytvořte instanci nového objektu **adresy** a naplňte ji na adresu, kterou chcete ověřit. Pak načtěte rozhraní k operacím **ověřování** z funkce **IAggregatePartner. getvalids** a zavolejte metodu **isAddressValid** s objektem adresy.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address();

address.setAddressLine1("One Microsoft Way");
address.setCity("Redmond");
address.setState("WA");
address.setCountry("US");
address.setPostalCode("98052");

try
{
    // Validate the address
    Boolean validationResult = partnerOperations.getValidations().isAddressValid(address);

    System.out.println(validationResult ? "The address is valid." : "Invalid address");
}
catch (Exception exception)
{
    System.out.println("Address is invalid");

    if (! StringHelper.isNullOrWhiteSpace(exception.getMessage()))
    {
        System.out.println(exception.getMessage());
    }
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Chcete-li ověřit adresu, spusťte [**test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) s naplněnými parametry adresy.

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
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

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 129

{
    "AddressLine1": "One Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí metoda stavový kód 200, jak je znázorněno v příkladu úspěšného ověření odpovědi níže.

Pokud požadavek neproběhne úspěšně, vrátí metoda stavový kód 400, jak je znázorněno v následujícím příkladu, který se nezdařil při ověřování odpovědi. Tělo odpovědi obsahuje datovou část JSON s dalšími informacemi o chybě.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response---validation-succeeded-example"></a>Odpověď – Příklad úspěšného ověření

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a>Odpověď – příklad neúspěšného ověření

```http
HTTP/1.1 400 Bad Request
Content-Length: 418
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: pdlItMyvtkmGHDWt.0
MS-ServerId: 101112012
Date: Tue, 14 Mar 2017 01:57:55 GMT

{
    "code": 2007,
    "description": "{\"code\":\"60071\",\"reason\":\"ZipCityInvalid - Details: Field - &#39;City&#39; is corrected from OldValue: &#39;Redmond&#39; to NewValue: &#39;BELLEVUE&#39;.\",\"corrected_address\":{\"country\":\"US\",\"region\":\"WA\",\"city\":\"BELLEVUE\",\"address_line1\":\"One Microsoft Way\",\"postal_code\":\"98007\"},\"object_type\":\"AddressValidation\",\"resource_status\":\"Active\"}",
    "data": [],
    "source": "PartnerFD"
}
```
