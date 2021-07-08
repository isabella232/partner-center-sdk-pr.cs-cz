---
title: Získání cen pro partnerské sdílené služby Microsoft Azure
description: Jak získat ceníkovou kartu Azure s cenami pro Microsoft Azure partnerskými sdílenými službami
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0008d7474f7e57bbbd765afdf2487ee279848ac3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548800"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a><span data-ttu-id="a0c99-103">Získání cen pro partnerské sdílené služby Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a0c99-103">Get prices for Microsoft Azure Partner Shared Services</span></span>

<span data-ttu-id="a0c99-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a0c99-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a0c99-105">Jak získat [ceníkovou](azure-rate-card-resources.md) kartu Azure s cenami pro Microsoft Azure partnerských služeb.</span><span class="sxs-lookup"><span data-stu-id="a0c99-105">How to get an [Azure Rate Card](azure-rate-card-resources.md) with prices for Microsoft Azure Partner Shared Services.</span></span>

<span data-ttu-id="a0c99-106">Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění.</span><span class="sxs-lookup"><span data-stu-id="a0c99-106">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="a0c99-107">Ve výchozím nastavení rozhraní API používá nastavení profilu partnera v Partnerské centrum a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná.</span><span class="sxs-lookup"><span data-stu-id="a0c99-107">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="a0c99-108">Povědomí o umístění je zvlášť důležité, pokud spravujete prodeje na několika trzích z jedné centralizované kanceláře.</span><span class="sxs-lookup"><span data-stu-id="a0c99-108">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span>

## <a name="example-code"></a><span data-ttu-id="a0c99-109">Příklad kódu</span><span class="sxs-lookup"><span data-stu-id="a0c99-109">Example Code</span></span>

## <a name="c"></a><span data-ttu-id="a0c99-110">C\#</span><span class="sxs-lookup"><span data-stu-id="a0c99-110">C\#</span></span>

<span data-ttu-id="a0c99-111">Pokud chcete získat kartu sazeb Azure, zavolejte metodu [**IAzureRateCard.GetShared,**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) která vrátí prostředek [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) obsahující ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c99-111">To obtain the Azure Rate Card, call the [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a><span data-ttu-id="a0c99-112">Java</span><span class="sxs-lookup"><span data-stu-id="a0c99-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="a0c99-113">Pokud chcete získat kartu sazeb Azure, zavolejte **funkci IAzureRateCard.getShared,** která vrátí podrobnosti o ceníkové kartě, která obsahuje ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c99-113">To obtain the Azure Rate Card, call the **IAzureRateCard.getShared** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a><span data-ttu-id="a0c99-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0c99-114">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a0c99-115">Pokud chcete získat kartu Azure, spusťte příkaz [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) a zadáním parametru **SharedServices** vraťte podrobnosti o kartě sazby, která obsahuje ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c99-115">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command and specify the **SharedServices** parameter to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a><span data-ttu-id="a0c99-116">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="a0c99-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a0c99-117">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="a0c99-117">Request syntax</span></span>

| <span data-ttu-id="a0c99-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="a0c99-118">Method</span></span>  | <span data-ttu-id="a0c99-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a0c99-119">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="a0c99-120">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="a0c99-120">**GET**</span></span> | <span data-ttu-id="a0c99-121">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span><span class="sxs-lookup"><span data-stu-id="a0c99-121">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="a0c99-122">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="a0c99-122">URI parameters</span></span>

| <span data-ttu-id="a0c99-123">Název</span><span class="sxs-lookup"><span data-stu-id="a0c99-123">Name</span></span>     | <span data-ttu-id="a0c99-124">Typ</span><span class="sxs-lookup"><span data-stu-id="a0c99-124">Type</span></span>   | <span data-ttu-id="a0c99-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a0c99-125">Required</span></span> | <span data-ttu-id="a0c99-126">Popis</span><span class="sxs-lookup"><span data-stu-id="a0c99-126">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a0c99-127">currency</span><span class="sxs-lookup"><span data-stu-id="a0c99-127">currency</span></span> | <span data-ttu-id="a0c99-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0c99-128">string</span></span> | <span data-ttu-id="a0c99-129">No</span><span class="sxs-lookup"><span data-stu-id="a0c99-129">No</span></span>       | <span data-ttu-id="a0c99-130">Volitelný třípísmenný kód ISO pro měnu, ve které budou uvedeny sazby prostředků (například `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="a0c99-130">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="a0c99-131">Výchozí hodnota je měna přidružená k trhu v profilu partnera.</span><span class="sxs-lookup"><span data-stu-id="a0c99-131">The default is the currency associated with the market in the partner profile.</span></span> |
| <span data-ttu-id="a0c99-132">oblast</span><span class="sxs-lookup"><span data-stu-id="a0c99-132">region</span></span>   | <span data-ttu-id="a0c99-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="a0c99-133">string</span></span> | <span data-ttu-id="a0c99-134">No</span><span class="sxs-lookup"><span data-stu-id="a0c99-134">No</span></span>       | <span data-ttu-id="a0c99-135">Volitelný dvoupísmenný kód ISO země/oblasti, který označuje trh, na kterém je nabídka zakoupená (například `FR` ).</span><span class="sxs-lookup"><span data-stu-id="a0c99-135">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="a0c99-136">Výchozí hodnota je kód země/oblasti nastavený v profilu partnera.</span><span class="sxs-lookup"><span data-stu-id="a0c99-136">The default is the country/region code set in the partner profile.</span></span>        |

<span data-ttu-id="a0c99-137">Pokud je v požadavku zahrnutá volitelná hlavička X-Locale, jeho hodnota určuje jazyk použitý pro podrobnosti v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="a0c99-137">If the optional X-Locale header is included in the request, its value determines the language used for the details in the response.</span></span>

### <a name="request-headers"></a><span data-ttu-id="a0c99-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a0c99-138">Request headers</span></span>

<span data-ttu-id="a0c99-139">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a0c99-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a0c99-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a0c99-140">Request body</span></span>

<span data-ttu-id="a0c99-141">Žádné</span><span class="sxs-lookup"><span data-stu-id="a0c99-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a0c99-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a0c99-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a0c99-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a0c99-143">REST response</span></span>

<span data-ttu-id="a0c99-144">Pokud je požadavek úspěšný, vrátí prostředek [Azure Rate Card.](azure-rate-card-resources.md)</span><span class="sxs-lookup"><span data-stu-id="a0c99-144">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a0c99-145">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="a0c99-145">Response success and error codes</span></span>

<span data-ttu-id="a0c99-146">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a0c99-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a0c99-147">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="a0c99-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a0c99-148">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a0c99-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a0c99-149">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a0c99-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en-US",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
