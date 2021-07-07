---
title: Získání souhrnu využití pro partnera
description: Pomocí prostředku PartnerUsageSummary můžete získat přehled o využití partnerů pro všechny zákazníky, kteří během aktuálního fakturačního období zakoupili určitou službu nebo prostředek Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: f003980f1b521ad0ac26dbfd0d4821b9096fdd27
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873900"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="26abd-103">Získání souhrnu využití pro partnera</span><span class="sxs-lookup"><span data-stu-id="26abd-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="26abd-104">**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="26abd-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="26abd-105">Pomocí prostředku **PartnerUsageSummary** můžete získat přehled o využití partnerů pro všechny zákazníky, kteří během aktuálního fakturačního období zakoupili určitou službu nebo prostředek Azure.</span><span class="sxs-lookup"><span data-stu-id="26abd-105">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="26abd-106">*Celkový počet vrácený tímto rozhraním API nebude vracet spotřebu pro zákazníky, kteří mají plán Azure.*</span><span class="sxs-lookup"><span data-stu-id="26abd-106">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="26abd-107">Plánováno pro zastaralost v budoucnu.</span><span class="sxs-lookup"><span data-stu-id="26abd-107">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26abd-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="26abd-108">Prerequisites</span></span>

- <span data-ttu-id="26abd-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="26abd-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="26abd-110">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="26abd-110">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="26abd-111">C\#</span><span class="sxs-lookup"><span data-stu-id="26abd-111">C\#</span></span>

<span data-ttu-id="26abd-112">Pokud chcete získat shrnutí využití pro všechny zákazníky, kteří během aktuálního fakturačního období zakoupili určitou službu nebo prostředek Azure:</span><span class="sxs-lookup"><span data-stu-id="26abd-112">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="26abd-113">Použijte své **IAggregatePartner**.</span><span class="sxs-lookup"><span data-stu-id="26abd-113">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="26abd-114">Zavolejte vlastnost **UsageSummary** , za kterou následují metody **Get ()** nebo **GetAsync ()** :</span><span class="sxs-lookup"><span data-stu-id="26abd-114">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="26abd-115">Příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="26abd-115">For an example, see the following:</span></span>

- <span data-ttu-id="26abd-116">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="26abd-116">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="26abd-117">Project: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="26abd-117">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="26abd-118">Třída: **GetPartnerUsageSummary. cs**</span><span class="sxs-lookup"><span data-stu-id="26abd-118">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="26abd-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="26abd-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="26abd-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="26abd-120">Request syntax</span></span>

| <span data-ttu-id="26abd-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="26abd-121">Method</span></span>  | <span data-ttu-id="26abd-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="26abd-122">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="26abd-123">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="26abd-123">**GET**</span></span> | <span data-ttu-id="26abd-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="26abd-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="26abd-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="26abd-125">Request headers</span></span>

<span data-ttu-id="26abd-126">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="26abd-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="26abd-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="26abd-127">Request body</span></span>

<span data-ttu-id="26abd-128">Žádné</span><span class="sxs-lookup"><span data-stu-id="26abd-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="26abd-129">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="26abd-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="26abd-130">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="26abd-130">REST response</span></span>

<span data-ttu-id="26abd-131">V případě úspěchu tato metoda vrátí prostředek **PartnerUsageSummary** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="26abd-131">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="26abd-132">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="26abd-132">Response success and error codes</span></span>

<span data-ttu-id="26abd-133">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="26abd-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="26abd-134">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="26abd-134">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="26abd-135">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="26abd-135">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="26abd-136">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="26abd-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "customersOverBudget": 1,
    "customersTrendingOver": 0,
    "customersWithUsageBasedSubscription": 11,
    "resourceId": "11111111-4574-4539-bc42-0e539b9684c0",
    "id": "11111111-4574-4539-bc42-0e539b9684c0",
    "resourceName": "PLAMUATT2NETNEW",
    "name": "PLAMUATT2NETNEW",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerUsageSummary"
    }
}
```
