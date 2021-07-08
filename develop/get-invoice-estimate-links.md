---
title: Získání odkazů na odhad faktury
description: Můžete získat kolekci odkazů odhadu na podrobnosti o položce řádku odsouhlasení dotazů.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.assetid: ''
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 719becd3fac5605c4ad48ab86d483ba7903d65d8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549140"
---
# <a name="get-invoice-estimate-links"></a><span data-ttu-id="08fb3-103">Získání odkazů na odhad faktury</span><span class="sxs-lookup"><span data-stu-id="08fb3-103">Get invoice estimate links</span></span>

<span data-ttu-id="08fb3-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="08fb3-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="08fb3-105">Můžete získat odkazy na odhady, které vám pomůžou s podrobnostmi dotazu na nefakturovatelné položky řádku odsouhlasení.</span><span class="sxs-lookup"><span data-stu-id="08fb3-105">You can get estimate links to help query details for unbilled reconciliation line items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08fb3-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="08fb3-106">Prerequisites</span></span>

- <span data-ttu-id="08fb3-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="08fb3-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="08fb3-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="08fb3-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="08fb3-109">Identifikátor faktury</span><span class="sxs-lookup"><span data-stu-id="08fb3-109">An invoice identifier.</span></span> <span data-ttu-id="08fb3-110">Určuje fakturu, pro kterou se mají načíst položky řádku.</span><span class="sxs-lookup"><span data-stu-id="08fb3-110">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="08fb3-111">C\#</span><span class="sxs-lookup"><span data-stu-id="08fb3-111">C\#</span></span>

<span data-ttu-id="08fb3-112">Následující příklad kódu ukazuje, jak můžete získat odkazy odhadu na dotazování nefakturovaných položek na řádku pro danou měnu.</span><span class="sxs-lookup"><span data-stu-id="08fb3-112">The following example code shows how you can get the estimate links to query unbilled line items for a given currency.</span></span> <span data-ttu-id="08fb3-113">Odpověď obsahuje odkazy odhadu pro jednotlivé období (například aktuální a předchozí měsíc).</span><span class="sxs-lookup"><span data-stu-id="08fb3-113">The response contains the estimate links for each period (for example, the current and previous month).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();
```

<span data-ttu-id="08fb3-114">Podobný příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="08fb3-114">For a similar example, see the following:</span></span>

- <span data-ttu-id="08fb3-115">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="08fb3-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="08fb3-116">Project: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="08fb3-116">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="08fb3-117">Třída: **GetEstimatesLinks. cs**</span><span class="sxs-lookup"><span data-stu-id="08fb3-117">Class: **GetEstimatesLinks.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="08fb3-118">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="08fb3-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="08fb3-119">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="08fb3-119">Request syntax</span></span>

| <span data-ttu-id="08fb3-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="08fb3-120">Method</span></span>  | <span data-ttu-id="08fb3-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="08fb3-121">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="08fb3-122">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="08fb3-122">**GET**</span></span> | <span data-ttu-id="08fb3-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/Estimates/Links? CurrencyCode = {CURRENCYCODE} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="08fb3-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="08fb3-124">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="08fb3-124">URI parameters</span></span>

<span data-ttu-id="08fb3-125">Při vytváření žádosti použijte následující identifikátor URI a parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="08fb3-125">Use the following URI and query parameter when creating the request.</span></span>

| <span data-ttu-id="08fb3-126">Název</span><span class="sxs-lookup"><span data-stu-id="08fb3-126">Name</span></span>                   | <span data-ttu-id="08fb3-127">Typ</span><span class="sxs-lookup"><span data-stu-id="08fb3-127">Type</span></span>   | <span data-ttu-id="08fb3-128">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="08fb3-128">Required</span></span> | <span data-ttu-id="08fb3-129">Popis</span><span class="sxs-lookup"><span data-stu-id="08fb3-129">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="08fb3-130">currencyCode</span><span class="sxs-lookup"><span data-stu-id="08fb3-130">currencyCode</span></span>           | <span data-ttu-id="08fb3-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="08fb3-131">string</span></span> | <span data-ttu-id="08fb3-132">Yes</span><span class="sxs-lookup"><span data-stu-id="08fb3-132">Yes</span></span>      | <span data-ttu-id="08fb3-133">Kód měny pro nefakturovatelné položky řádku</span><span class="sxs-lookup"><span data-stu-id="08fb3-133">The currency code for the unbilled line items.</span></span>                    |

### <a name="request-headers"></a><span data-ttu-id="08fb3-134">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="08fb3-134">Request headers</span></span>

<span data-ttu-id="08fb3-135">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="08fb3-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="08fb3-136">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="08fb3-136">Request body</span></span>

<span data-ttu-id="08fb3-137">Žádné</span><span class="sxs-lookup"><span data-stu-id="08fb3-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="08fb3-138">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="08fb3-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/estimates/links?currencycode=usd HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="08fb3-139">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="08fb3-139">REST response</span></span>

<span data-ttu-id="08fb3-140">V případě úspěchu obsahuje odpověď odkazy na načtení nefakturovaných odhadů.</span><span class="sxs-lookup"><span data-stu-id="08fb3-140">If successful, the response contains the links to retrieve unbilled estimates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="08fb3-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="08fb3-141">Response success and error codes</span></span>

<span data-ttu-id="08fb3-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="08fb3-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="08fb3-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="08fb3-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="08fb3-144">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="08fb3-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="08fb3-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="08fb3-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 80EAA055-B5D3-4D88-BFE8-924A3F706462
MS-RequestId: 1b18689e-3fe3-4fdb-d09e-39d13941390b
X-Locale: en-US
X-SourceFiles: =?UTF-8?B?RDpcU291cmNlc1xSUEUuUGFydG5lci5TZXJ2aWNlLkJpbGxpbmdTZXJ2aWNlXHYxLjFcV2ViQXBpc1xCaWxsaW5nU2VydmljZS5WMi5XZWJcdjFcaW52b2ljZXNcZXN0aW1hdGVzXGxpbmtz?=
X-Powered-By: ASP.NET
Date: Thu, 14 Mar 2019 18:15:06 GMT
Content-Length: 1857

{
  "totalCount": 4,
  "items": [
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    }
  ],
  "attributes": {
    "objectType": "Collection"
 }
}
```
