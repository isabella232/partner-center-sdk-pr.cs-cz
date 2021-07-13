---
title: Ověření adresy
description: Jak ověřit adresu pomocí rozhraní API pro ověření adresy.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30f5cd526ab038dce400e79822d89b8086ba3799
ms.sourcegitcommit: 41bf9dca55f4c96d382b327a75b2d2418edfc9bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/13/2021
ms.locfileid: "113655621"
---
# <a name="validate-an-address"></a><span data-ttu-id="4a33f-103">Ověření adresy</span><span class="sxs-lookup"><span data-stu-id="4a33f-103">Validate an address</span></span>

<span data-ttu-id="4a33f-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4a33f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4a33f-105">Jak ověřit adresu pomocí rozhraní API pro ověření adresy.</span><span class="sxs-lookup"><span data-stu-id="4a33f-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="4a33f-106">Rozhraní API pro ověření adresy by se mělo používat jenom pro předběžné ověření aktualizací profilu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="4a33f-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="4a33f-107">Použijte ho s porozuměním, že pokud je země USA, Kanada, Čína nebo Mexiko, pole State se ověří podle seznamu platných stavů pro příslušnou zemi.</span><span class="sxs-lookup"><span data-stu-id="4a33f-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="4a33f-108">Ve všech ostatních zemích tento test neproběhne a rozhraní API kontroluje, zda je stav platný řetězec.</span><span class="sxs-lookup"><span data-stu-id="4a33f-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a33f-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4a33f-109">Prerequisites</span></span>

<span data-ttu-id="4a33f-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4a33f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4a33f-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="4a33f-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="4a33f-112">C\#</span><span class="sxs-lookup"><span data-stu-id="4a33f-112">C\#</span></span>

<span data-ttu-id="4a33f-113">Chcete-li ověřit adresu, nejprve vytvořte instanci nového objektu **adresy** a naplňte ji na adresu, kterou chcete ověřit.</span><span class="sxs-lookup"><span data-stu-id="4a33f-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="4a33f-114">Pak načtěte rozhraní k operacím **ověřování** z vlastnosti **IAggregatePartner. valids** a zavolejte metodu **IsAddressValid** s objektem adresy.</span><span class="sxs-lookup"><span data-stu-id="4a33f-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="4a33f-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="4a33f-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4a33f-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="4a33f-116">Request syntax</span></span>

| <span data-ttu-id="4a33f-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="4a33f-117">Method</span></span>   | <span data-ttu-id="4a33f-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="4a33f-118">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="4a33f-119">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="4a33f-119">**POST**</span></span> | <span data-ttu-id="4a33f-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/Address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4a33f-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4a33f-121">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="4a33f-121">Request headers</span></span>

<span data-ttu-id="4a33f-122">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4a33f-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4a33f-123">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="4a33f-123">Request body</span></span>

<span data-ttu-id="4a33f-124">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="4a33f-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="4a33f-125">Název</span><span class="sxs-lookup"><span data-stu-id="4a33f-125">Name</span></span>         | <span data-ttu-id="4a33f-126">Typ</span><span class="sxs-lookup"><span data-stu-id="4a33f-126">Type</span></span>   | <span data-ttu-id="4a33f-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="4a33f-127">Required</span></span> | <span data-ttu-id="4a33f-128">Popis</span><span class="sxs-lookup"><span data-stu-id="4a33f-128">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="4a33f-129">addressline1</span><span class="sxs-lookup"><span data-stu-id="4a33f-129">addressline1</span></span> | <span data-ttu-id="4a33f-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="4a33f-130">string</span></span> | <span data-ttu-id="4a33f-131">Y</span><span class="sxs-lookup"><span data-stu-id="4a33f-131">Y</span></span>        | <span data-ttu-id="4a33f-132">První řádek adresy</span><span class="sxs-lookup"><span data-stu-id="4a33f-132">The first line of the address.</span></span>                             |
| <span data-ttu-id="4a33f-133">addressline2</span><span class="sxs-lookup"><span data-stu-id="4a33f-133">addressline2</span></span> | <span data-ttu-id="4a33f-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="4a33f-134">string</span></span> | <span data-ttu-id="4a33f-135">N</span><span class="sxs-lookup"><span data-stu-id="4a33f-135">N</span></span>        | <span data-ttu-id="4a33f-136">Druhý řádek adresy.</span><span class="sxs-lookup"><span data-stu-id="4a33f-136">The second line of the address.</span></span> <span data-ttu-id="4a33f-137">Tato vlastnost je nepovinná.</span><span class="sxs-lookup"><span data-stu-id="4a33f-137">This property is optional.</span></span> |
| <span data-ttu-id="4a33f-138">city</span><span class="sxs-lookup"><span data-stu-id="4a33f-138">city</span></span>         | <span data-ttu-id="4a33f-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="4a33f-139">string</span></span> | <span data-ttu-id="4a33f-140">Y</span><span class="sxs-lookup"><span data-stu-id="4a33f-140">Y</span></span>        | <span data-ttu-id="4a33f-141">Město.</span><span class="sxs-lookup"><span data-stu-id="4a33f-141">The city.</span></span>                                                  |
| <span data-ttu-id="4a33f-142">state</span><span class="sxs-lookup"><span data-stu-id="4a33f-142">state</span></span>        | <span data-ttu-id="4a33f-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="4a33f-143">string</span></span> | <span data-ttu-id="4a33f-144">Y</span><span class="sxs-lookup"><span data-stu-id="4a33f-144">Y</span></span>        | <span data-ttu-id="4a33f-145">Stav</span><span class="sxs-lookup"><span data-stu-id="4a33f-145">The state.</span></span>                                                 |
| <span data-ttu-id="4a33f-146">ovládacím</span><span class="sxs-lookup"><span data-stu-id="4a33f-146">postalcode</span></span>   | <span data-ttu-id="4a33f-147">řetězec</span><span class="sxs-lookup"><span data-stu-id="4a33f-147">string</span></span> | <span data-ttu-id="4a33f-148">Y</span><span class="sxs-lookup"><span data-stu-id="4a33f-148">Y</span></span>        | <span data-ttu-id="4a33f-149">Poštovní směrovací číslo.</span><span class="sxs-lookup"><span data-stu-id="4a33f-149">The postal code.</span></span>                                           |
| <span data-ttu-id="4a33f-150">country</span><span class="sxs-lookup"><span data-stu-id="4a33f-150">country</span></span>      | <span data-ttu-id="4a33f-151">řetězec</span><span class="sxs-lookup"><span data-stu-id="4a33f-151">string</span></span> | <span data-ttu-id="4a33f-152">Y</span><span class="sxs-lookup"><span data-stu-id="4a33f-152">Y</span></span>        | <span data-ttu-id="4a33f-153">Kód země ISO alfa-2 se dvěma znaky.</span><span class="sxs-lookup"><span data-stu-id="4a33f-153">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="response-details"></a><span data-ttu-id="4a33f-154">Podrobnosti odpovědi</span><span class="sxs-lookup"><span data-stu-id="4a33f-154">Response details</span></span>

<span data-ttu-id="4a33f-155">Odpověď vrátí jednu z následujících stavových zpráv:</span><span class="sxs-lookup"><span data-stu-id="4a33f-155">The response will return one of the following status messages:</span></span>

| <span data-ttu-id="4a33f-156">Status</span><span class="sxs-lookup"><span data-stu-id="4a33f-156">Status</span></span>     | <span data-ttu-id="4a33f-157">Popis</span><span class="sxs-lookup"><span data-stu-id="4a33f-157">Description</span></span> |    <span data-ttu-id="4a33f-158">Počet vrácených navrhovaných adres</span><span class="sxs-lookup"><span data-stu-id="4a33f-158">Number of suggested addresses returned</span></span> |
|-------|---------------|-------------------|
|<span data-ttu-id="4a33f-159">Ověřené pro přepravce</span><span class="sxs-lookup"><span data-stu-id="4a33f-159">Verified shippable</span></span> | <span data-ttu-id="4a33f-160">Adresa je ověřena a může být expedována.</span><span class="sxs-lookup"><span data-stu-id="4a33f-160">Address is verified and can be shipped to.</span></span> | <span data-ttu-id="4a33f-161">Jednoduché</span><span class="sxs-lookup"><span data-stu-id="4a33f-161">Single</span></span> |
|<span data-ttu-id="4a33f-162">Ověřují</span><span class="sxs-lookup"><span data-stu-id="4a33f-162">Verified</span></span> | <span data-ttu-id="4a33f-163">Adresa je ověřena.</span><span class="sxs-lookup"><span data-stu-id="4a33f-163">Address is verified.</span></span> | <span data-ttu-id="4a33f-164">Jednoduché</span><span class="sxs-lookup"><span data-stu-id="4a33f-164">Single</span></span> |
|<span data-ttu-id="4a33f-165">Je vyžadována interakce</span><span class="sxs-lookup"><span data-stu-id="4a33f-165">Interaction required</span></span> | <span data-ttu-id="4a33f-166">Navrhovaná adresa se významně změnila a potřebuje potvrzení uživatele.</span><span class="sxs-lookup"><span data-stu-id="4a33f-166">Suggested address has been changed significantly and needs user confirmation.</span></span> | <span data-ttu-id="4a33f-167">Jednoduché</span><span class="sxs-lookup"><span data-stu-id="4a33f-167">Single</span></span> |
|<span data-ttu-id="4a33f-168">Částečně ulice</span><span class="sxs-lookup"><span data-stu-id="4a33f-168">Street partial</span></span> | <span data-ttu-id="4a33f-169">Daná ulice v adrese je částečně a potřebuje další informace.</span><span class="sxs-lookup"><span data-stu-id="4a33f-169">The given street in the address is partial and needs more info.</span></span> | <span data-ttu-id="4a33f-170">Více – maximálně tři</span><span class="sxs-lookup"><span data-stu-id="4a33f-170">Multiple—maximum of three</span></span> |
|<span data-ttu-id="4a33f-171">Částečně místní</span><span class="sxs-lookup"><span data-stu-id="4a33f-171">Premises partial</span></span> | <span data-ttu-id="4a33f-172">Dané prostory (stavební číslo, číslo sady a další) jsou částečné a vyžadují další informace.</span><span class="sxs-lookup"><span data-stu-id="4a33f-172">The given premises (building number, suite number, and others) are partial and need more info.</span></span> | <span data-ttu-id="4a33f-173">Více – maximálně tři</span><span class="sxs-lookup"><span data-stu-id="4a33f-173">Multiple—maximum of three</span></span> |
|<span data-ttu-id="4a33f-174">Několik</span><span class="sxs-lookup"><span data-stu-id="4a33f-174">Multiple</span></span> | <span data-ttu-id="4a33f-175">Adresa obsahuje několik polí, která jsou v této adrese částečně (případně i částečně a částečně v ulici).</span><span class="sxs-lookup"><span data-stu-id="4a33f-175">There are multiple fields that are partial in the address (potentially also including street partial and premises partial).</span></span> | <span data-ttu-id="4a33f-176">Více – maximálně tři</span><span class="sxs-lookup"><span data-stu-id="4a33f-176">Multiple—maximum of three</span></span> |
|<span data-ttu-id="4a33f-177">Žádná</span><span class="sxs-lookup"><span data-stu-id="4a33f-177">None</span></span> | <span data-ttu-id="4a33f-178">Adresa je nesprávná.</span><span class="sxs-lookup"><span data-stu-id="4a33f-178">Address is incorrect.</span></span> | <span data-ttu-id="4a33f-179">Žádná</span><span class="sxs-lookup"><span data-stu-id="4a33f-179">None</span></span> |
|<span data-ttu-id="4a33f-180">Není ověřeno.</span><span class="sxs-lookup"><span data-stu-id="4a33f-180">Not validated</span></span> | <span data-ttu-id="4a33f-181">Adresu nelze odeslat prostřednictvím procesu ověřování.</span><span class="sxs-lookup"><span data-stu-id="4a33f-181">Address was not able to be sent through the validation process.</span></span> | <span data-ttu-id="4a33f-182">Žádná</span><span class="sxs-lookup"><span data-stu-id="4a33f-182">None</span></span> |

### <a name="request-example"></a><span data-ttu-id="4a33f-183">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="4a33f-183">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4a33f-184">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="4a33f-184">REST response</span></span>

<span data-ttu-id="4a33f-185">V případě úspěchu metoda vrátí objekt **AddressValidationResponse** v těle odpovědi se stavovým kódem **http 200** .</span><span class="sxs-lookup"><span data-stu-id="4a33f-185">If successful, the method returns an **AddressValidationResponse** object in the response body, with a **HTTP 200** status code.</span></span> <span data-ttu-id="4a33f-186">Příklad najdete níže.</span><span class="sxs-lookup"><span data-stu-id="4a33f-186">An example is shown below.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4a33f-187">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="4a33f-187">Response success and error codes</span></span>

<span data-ttu-id="4a33f-188">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="4a33f-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4a33f-189">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="4a33f-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4a33f-190">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4a33f-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4a33f-191">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="4a33f-191">Response example</span></span>

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
