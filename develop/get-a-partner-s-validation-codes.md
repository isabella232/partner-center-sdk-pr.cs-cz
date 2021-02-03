---
title: Získání kódů pro ověření cloudu komunity státní správy
description: Jak získat kódy pro ověření cloudového komunitního partnera pro státní správu.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: d84a3d3c69d835e42565c4e6f1edb06ab338340a
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766846"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="d8870-103">Získání ověřovacích kódů partnera</span><span class="sxs-lookup"><span data-stu-id="d8870-103">Get a partner's validation codes</span></span>

<span data-ttu-id="d8870-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="d8870-104">**Applies To**</span></span>

- <span data-ttu-id="d8870-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d8870-105">Partner Center</span></span>

<span data-ttu-id="d8870-106">Jak získat kolekci kódů pro ověření cloudu státní správy z partnerské komunity.</span><span class="sxs-lookup"><span data-stu-id="d8870-106">How to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="d8870-107">Ověřovací kód je nutný k vytvoření zákazníka v cloudu pro státní správu komunity.</span><span class="sxs-lookup"><span data-stu-id="d8870-107">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="d8870-108">Pokud vás zajímá, že máte vaši organizaci nebo organizaci schválenou pro Microsoft Office 365 pro poskytovatele CSP, přečtěte si téma [Office 365 vládní RSZ pro poskytovatele CSP a kritéria nároku na zákazníky/partner-Center/CSP-RSZ-Validate).</span><span class="sxs-lookup"><span data-stu-id="d8870-108">If you are interested in having your organization or your customers organization approved for Office 365 Government GCC for CSP, please see [Office 365 Government GCC for CSP Partner and Customer Eligibility Criteria/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8870-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d8870-109">Prerequisites</span></span>

- <span data-ttu-id="d8870-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d8870-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d8870-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="d8870-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d8870-112">Potvrzení ověření po [vyplnění formuláře.](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner)</span><span class="sxs-lookup"><span data-stu-id="d8870-112">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="d8870-113">Zákazník bez kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="d8870-113">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="d8870-114">C\#</span><span class="sxs-lookup"><span data-stu-id="d8870-114">C\#</span></span>

<span data-ttu-id="d8870-115">Pokud chcete získat seznam všech ověřovacích kódů partnera, zavolejte na **GetValidationCodes**.</span><span class="sxs-lookup"><span data-stu-id="d8870-115">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="d8870-116">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d8870-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d8870-117">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d8870-117">Request syntax</span></span>

| <span data-ttu-id="d8870-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="d8870-118">Method</span></span>  | <span data-ttu-id="d8870-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d8870-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d8870-120">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="d8870-120">**GET**</span></span> | <span data-ttu-id="d8870-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/All/validations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8870-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d8870-122">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d8870-122">Request headers</span></span>

<span data-ttu-id="d8870-123">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d8870-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d8870-124">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d8870-124">Request body</span></span>

<span data-ttu-id="d8870-125">Žádné</span><span class="sxs-lookup"><span data-stu-id="d8870-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d8870-126">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d8870-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="d8870-127">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d8870-127">REST response</span></span>

<span data-ttu-id="d8870-128">V případě úspěchu tato metoda vrátí seznam prostředků [**ValidationCode**](utility-resources.md#validationcode) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="d8870-128">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d8870-129">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d8870-129">Response success and error codes</span></span>

<span data-ttu-id="d8870-130">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d8870-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d8870-131">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d8870-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d8870-132">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d8870-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d8870-133">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d8870-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
