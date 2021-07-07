---
title: Ověření adresy
description: Jak ověřit adresu pomocí rozhraní API pro ověření adresy.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14d45977f3af6e8bba1b7cb7f969aa7c5bb671da
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529881"
---
# <a name="validate-an-address"></a><span data-ttu-id="9d7d3-103">Ověření adresy</span><span class="sxs-lookup"><span data-stu-id="9d7d3-103">Validate an address</span></span>

<span data-ttu-id="9d7d3-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9d7d3-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9d7d3-105">Jak ověřit adresu pomocí rozhraní API pro ověření adresy.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="9d7d3-106">Rozhraní API pro ověření adresy by se mělo používat jenom pro předběžné ověření aktualizací profilu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="9d7d3-107">Použijte ho s porozuměním, že pokud je země USA, Kanada, Čína nebo Mexiko, pole State se ověří podle seznamu platných stavů pro příslušnou zemi.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="9d7d3-108">Ve všech ostatních zemích tento test neproběhne a rozhraní API kontroluje, zda je stav platný řetězec.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d7d3-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9d7d3-109">Prerequisites</span></span>

<span data-ttu-id="9d7d3-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9d7d3-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9d7d3-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="9d7d3-112">C\#</span><span class="sxs-lookup"><span data-stu-id="9d7d3-112">C\#</span></span>

<span data-ttu-id="9d7d3-113">Chcete-li ověřit adresu, nejprve vytvořte instanci nového objektu **adresy** a naplňte ji na adresu, kterou chcete ověřit.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="9d7d3-114">Pak načtěte rozhraní k operacím **ověřování** z vlastnosti **IAggregatePartner. valids** a zavolejte metodu **IsAddressValid** s objektem adresy.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

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

## <a name="java"></a><span data-ttu-id="9d7d3-115">Java</span><span class="sxs-lookup"><span data-stu-id="9d7d3-115">Java</span></span>

<span data-ttu-id="9d7d3-116">Chcete-li ověřit adresu, nejprve vytvořte instanci nového objektu **adresy** a naplňte ji na adresu, kterou chcete ověřit.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-116">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="9d7d3-117">Pak načtěte rozhraní k operacím **ověřování** z funkce **IAggregatePartner. getvalids** a zavolejte metodu **isAddressValid** s objektem adresy.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-117">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="9d7d3-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d7d3-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="9d7d3-119">Chcete-li ověřit adresu, spusťte [**test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) s naplněnými parametry adresy.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-119">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="9d7d3-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="9d7d3-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9d7d3-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="9d7d3-121">Request syntax</span></span>

| <span data-ttu-id="9d7d3-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="9d7d3-122">Method</span></span>   | <span data-ttu-id="9d7d3-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9d7d3-123">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="9d7d3-124">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="9d7d3-124">**POST**</span></span> | <span data-ttu-id="9d7d3-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/Address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9d7d3-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9d7d3-126">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9d7d3-126">Request headers</span></span>

<span data-ttu-id="9d7d3-127">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9d7d3-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9d7d3-128">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9d7d3-128">Request body</span></span>

<span data-ttu-id="9d7d3-129">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-129">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="9d7d3-130">Název</span><span class="sxs-lookup"><span data-stu-id="9d7d3-130">Name</span></span>         | <span data-ttu-id="9d7d3-131">Typ</span><span class="sxs-lookup"><span data-stu-id="9d7d3-131">Type</span></span>   | <span data-ttu-id="9d7d3-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9d7d3-132">Required</span></span> | <span data-ttu-id="9d7d3-133">Popis</span><span class="sxs-lookup"><span data-stu-id="9d7d3-133">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="9d7d3-134">addressline1</span><span class="sxs-lookup"><span data-stu-id="9d7d3-134">addressline1</span></span> | <span data-ttu-id="9d7d3-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="9d7d3-135">string</span></span> | <span data-ttu-id="9d7d3-136">Y</span><span class="sxs-lookup"><span data-stu-id="9d7d3-136">Y</span></span>        | <span data-ttu-id="9d7d3-137">První řádek adresy</span><span class="sxs-lookup"><span data-stu-id="9d7d3-137">The first line of the address.</span></span>                             |
| <span data-ttu-id="9d7d3-138">addressline2</span><span class="sxs-lookup"><span data-stu-id="9d7d3-138">addressline2</span></span> | <span data-ttu-id="9d7d3-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="9d7d3-139">string</span></span> | <span data-ttu-id="9d7d3-140">N</span><span class="sxs-lookup"><span data-stu-id="9d7d3-140">N</span></span>        | <span data-ttu-id="9d7d3-141">Druhý řádek adresy.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-141">The second line of the address.</span></span> <span data-ttu-id="9d7d3-142">Tato vlastnost je nepovinná.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-142">This property is optional.</span></span> |
| <span data-ttu-id="9d7d3-143">city</span><span class="sxs-lookup"><span data-stu-id="9d7d3-143">city</span></span>         | <span data-ttu-id="9d7d3-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="9d7d3-144">string</span></span> | <span data-ttu-id="9d7d3-145">Y</span><span class="sxs-lookup"><span data-stu-id="9d7d3-145">Y</span></span>        | <span data-ttu-id="9d7d3-146">Město.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-146">The city.</span></span>                                                  |
| <span data-ttu-id="9d7d3-147">state</span><span class="sxs-lookup"><span data-stu-id="9d7d3-147">state</span></span>        | <span data-ttu-id="9d7d3-148">řetězec</span><span class="sxs-lookup"><span data-stu-id="9d7d3-148">string</span></span> | <span data-ttu-id="9d7d3-149">Y</span><span class="sxs-lookup"><span data-stu-id="9d7d3-149">Y</span></span>        | <span data-ttu-id="9d7d3-150">Stav</span><span class="sxs-lookup"><span data-stu-id="9d7d3-150">The state.</span></span>                                                 |
| <span data-ttu-id="9d7d3-151">ovládacím</span><span class="sxs-lookup"><span data-stu-id="9d7d3-151">postalcode</span></span>   | <span data-ttu-id="9d7d3-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="9d7d3-152">string</span></span> | <span data-ttu-id="9d7d3-153">Y</span><span class="sxs-lookup"><span data-stu-id="9d7d3-153">Y</span></span>        | <span data-ttu-id="9d7d3-154">Poštovní směrovací číslo.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-154">The postal code.</span></span>                                           |
| <span data-ttu-id="9d7d3-155">country</span><span class="sxs-lookup"><span data-stu-id="9d7d3-155">country</span></span>      | <span data-ttu-id="9d7d3-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="9d7d3-156">string</span></span> | <span data-ttu-id="9d7d3-157">Y</span><span class="sxs-lookup"><span data-stu-id="9d7d3-157">Y</span></span>        | <span data-ttu-id="9d7d3-158">Kód země ISO alfa-2 se dvěma znaky.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-158">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="9d7d3-159">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9d7d3-159">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9d7d3-160">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9d7d3-160">REST response</span></span>

<span data-ttu-id="9d7d3-161">V případě úspěchu vrátí metoda stavový kód 200, jak je znázorněno v příkladu úspěšného ověření odpovědi níže.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-161">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="9d7d3-162">Pokud požadavek neproběhne úspěšně, vrátí metoda stavový kód 400, jak je znázorněno v následujícím příkladu, který se nezdařil při ověřování odpovědi.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-162">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="9d7d3-163">Tělo odpovědi obsahuje datovou část JSON s dalšími informacemi o chybě.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-163">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9d7d3-164">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="9d7d3-164">Response success and error codes</span></span>

<span data-ttu-id="9d7d3-165">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9d7d3-166">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="9d7d3-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9d7d3-167">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9d7d3-167">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="9d7d3-168">Odpověď – Příklad úspěšného ověření</span><span class="sxs-lookup"><span data-stu-id="9d7d3-168">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="9d7d3-169">Odpověď – příklad neúspěšného ověření</span><span class="sxs-lookup"><span data-stu-id="9d7d3-169">Response - validation failed example</span></span>

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
