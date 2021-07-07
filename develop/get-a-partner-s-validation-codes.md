---
title: získání ověřovacích kódů Government Community Cloud partnera
description: jak získat ověřovací kódy Government Community Cloud partnera.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 04bccf587628337004a5825b534048945f791839
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873866"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="55e48-103">Získání ověřovacích kódů partnera</span><span class="sxs-lookup"><span data-stu-id="55e48-103">Get a partner's validation codes</span></span>

<span data-ttu-id="55e48-104">tento článek popisuje, jak získat kolekci ověřovacích kódů Government Community Cloud partnerů.</span><span class="sxs-lookup"><span data-stu-id="55e48-104">This article describes how to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="55e48-105">Ověřovací kód je nutný k vytvoření zákazníka v cloudu pro státní správu komunity.</span><span class="sxs-lookup"><span data-stu-id="55e48-105">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="55e48-106">pokud vás zajímá, že vaše organizace nebo organizace zákazníka jsou schválené pro Office 365 Government GCC pro csp, přečtěte si téma [Office 365 Government GCC pro poskytovatele csp a kritéria nároku na zákazníky](/partner-center/csp-gcc-validate).</span><span class="sxs-lookup"><span data-stu-id="55e48-106">If you are interested in having your organization or your customer's organization approved for Office 365 Government GCC for CSP, see [Office 365 Government GCC for CSP Partner and Customer eligibility criteria](/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55e48-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="55e48-107">Prerequisites</span></span>

- <span data-ttu-id="55e48-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="55e48-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="55e48-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="55e48-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="55e48-110">Potvrzení ověření po [vyplnění formuláře.](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner)</span><span class="sxs-lookup"><span data-stu-id="55e48-110">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="55e48-111">Zákazník bez kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="55e48-111">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="55e48-112">C\#</span><span class="sxs-lookup"><span data-stu-id="55e48-112">C\#</span></span>

<span data-ttu-id="55e48-113">Pokud chcete získat seznam všech ověřovacích kódů partnera, zavolejte na **GetValidationCodes**.</span><span class="sxs-lookup"><span data-stu-id="55e48-113">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="55e48-114">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="55e48-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="55e48-115">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="55e48-115">Request syntax</span></span>

| <span data-ttu-id="55e48-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="55e48-116">Method</span></span>  | <span data-ttu-id="55e48-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="55e48-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="55e48-118">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="55e48-118">**GET**</span></span> | <span data-ttu-id="55e48-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/All/validations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="55e48-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="55e48-120">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="55e48-120">Request headers</span></span>

<span data-ttu-id="55e48-121">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="55e48-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="55e48-122">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="55e48-122">Request body</span></span>

<span data-ttu-id="55e48-123">Žádné</span><span class="sxs-lookup"><span data-stu-id="55e48-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="55e48-124">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="55e48-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="55e48-125">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="55e48-125">REST response</span></span>

<span data-ttu-id="55e48-126">V případě úspěchu tato metoda vrátí seznam prostředků [**ValidationCode**](utility-resources.md#validationcode) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="55e48-126">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="55e48-127">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="55e48-127">Response success and error codes</span></span>

<span data-ttu-id="55e48-128">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="55e48-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="55e48-129">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="55e48-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="55e48-130">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="55e48-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="55e48-131">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="55e48-131">Response example</span></span>

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
