---
title: Získání pravidel formátování adres podle trhu
description: Získejte očekávaný formát adresy na základě kódu ISO pro trh.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5233d059ea6e71c28df36b2242659c28c5dd857
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549038"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="27c0b-103">Získání pravidel formátování adres podle trhu</span><span class="sxs-lookup"><span data-stu-id="27c0b-103">Get address formatting rules by market</span></span>

<span data-ttu-id="27c0b-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="27c0b-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>


<span data-ttu-id="27c0b-105">Získejte očekávaný formát adresy na základě kódu ISO pro trh.</span><span class="sxs-lookup"><span data-stu-id="27c0b-105">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27c0b-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="27c0b-106">Prerequisites</span></span>

- <span data-ttu-id="27c0b-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="27c0b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="27c0b-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="27c0b-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="27c0b-109">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="27c0b-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="27c0b-110">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="27c0b-110">Request syntax</span></span>

| <span data-ttu-id="27c0b-111">Metoda</span><span class="sxs-lookup"><span data-stu-id="27c0b-111">Method</span></span>  | <span data-ttu-id="27c0b-112">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="27c0b-112">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="27c0b-113">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="27c0b-113">**GET**</span></span> | <span data-ttu-id="27c0b-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="27c0b-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="27c0b-115">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="27c0b-115">URI parameter</span></span>

| <span data-ttu-id="27c0b-116">Název</span><span class="sxs-lookup"><span data-stu-id="27c0b-116">Name</span></span>           | <span data-ttu-id="27c0b-117">Typ</span><span class="sxs-lookup"><span data-stu-id="27c0b-117">Type</span></span>       | <span data-ttu-id="27c0b-118">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="27c0b-118">Required</span></span> | <span data-ttu-id="27c0b-119">Popis</span><span class="sxs-lookup"><span data-stu-id="27c0b-119">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="27c0b-120">**isocode-id**</span><span class="sxs-lookup"><span data-stu-id="27c0b-120">**isocode-id**</span></span> | <span data-ttu-id="27c0b-121">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="27c0b-121">**string**</span></span> | <span data-ttu-id="27c0b-122">Y</span><span class="sxs-lookup"><span data-stu-id="27c0b-122">Y</span></span>        | <span data-ttu-id="27c0b-123">Dvoupísový kód ZEMĚ ISO.</span><span class="sxs-lookup"><span data-stu-id="27c0b-123">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="27c0b-124">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="27c0b-124">Request headers</span></span>

<span data-ttu-id="27c0b-125">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="27c0b-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="27c0b-126">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="27c0b-126">Request body</span></span>

<span data-ttu-id="27c0b-127">Žádné</span><span class="sxs-lookup"><span data-stu-id="27c0b-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="27c0b-128">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="27c0b-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="27c0b-129">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="27c0b-129">REST response</span></span>

<span data-ttu-id="27c0b-130">V případě úspěchu vrátí tato metoda v textu odpovědi objekt **CountryInformation.**</span><span class="sxs-lookup"><span data-stu-id="27c0b-130">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="27c0b-131">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="27c0b-131">Response success and error codes</span></span>

<span data-ttu-id="27c0b-132">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="27c0b-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="27c0b-133">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="27c0b-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="27c0b-134">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="27c0b-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="27c0b-135">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="27c0b-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1856
Content-Type: application/json
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
Date: Wed, 25 Nov 2015 06:36:47 GMT

{
    "iso2Code": "US",
    "defaultCulture": "en-US",
    "isStateRequired": true,
    "states": {
        "value": ["AK","AL","AR", "AZ","CA","CO","CT","DC","DE","FL","GA","HI","IA","ID","IL","IN",
        "KS","KY","LA","MA","MD","ME","MI","MN","MO","MS","MT","NC","ND","NE","NH","NJ","NM","NV",
        "NY","OH","OK","OR","PA","RI","SC","SD","TN","TX","UT","VA","VT","WA","WI","WV","WY"]
    },
    "supportedLanguages": {
        "value": ["en",
        "es"]
    },
    "supportedCultures": {
        "value": ["en-US",
        "es-US"]
    },
    "isPostalCodeRequired": true,
    "postalCodeRegex": "^\\d{
        5
    }(-\\d{
        4
    })?$",
    "isCityRequired": true,
    "isVatIdSupported": false,
    "taxIdFormat": "US######",
    "taxIdSample": "US999965",
    "phoneNumberRegex": "^(1[\\-\\/\\.]?)?(\((\\d{3})\)|(\\d{3}))[\\-\\/\\.]?(\\d{3})[\\-\\/\\.]?(\\d{4})$",
    "isRegistrationNumberSupported": false,
    "isTaxIdSupported": true,
    "resellerAgreementRegion": "AOC",
    "geographicRegion": "NorthAndLatinAmerica",
    "countryCallingCodes": {
        "value": ["1"]
    },
    "attributes": {
        "objectType": "CountryInformation"
    }
}
```
