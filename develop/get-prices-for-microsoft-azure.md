---
title: Získání cen pro Microsoft Azure
description: Jak získat ceníkovou kartu Azure s cenami v reálném čase pro nabídku Azure Ceny Azure jsou poměrně dynamické a často se mění.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4f66ab19ef3723fbaa27acff941cf48683a7c25c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548783"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="61713-104">Získání cen pro Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="61713-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="61713-105">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="61713-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="61713-106">Jak získat [ceníkovou kartu Azure](azure-rate-card-resources.md) s cenami v reálném čase pro nabídku Azure</span><span class="sxs-lookup"><span data-stu-id="61713-106">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="61713-107">Ceny Azure jsou poměrně dynamické a často se mění.</span><span class="sxs-lookup"><span data-stu-id="61713-107">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="61713-108">Pokud chcete sledovat využití a pomoct s předpovídáním měsíčních faktur a faktur pro jednotlivé zákazníky, můžete zkombinovat tento dotaz na kartu sazeb Azure a získat ceny za Microsoft Azure s žádostí o získání záznamů o využití azure [zákazníkem.](get-a-customer-s-utilization-record-for-azure.md)</span><span class="sxs-lookup"><span data-stu-id="61713-108">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="61713-109">Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění.</span><span class="sxs-lookup"><span data-stu-id="61713-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="61713-110">Ve výchozím nastavení rozhraní API používá nastavení profilu partnera v Partnerské centrum a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná.</span><span class="sxs-lookup"><span data-stu-id="61713-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="61713-111">Povědomí o umístění je zvlášť důležité, pokud spravujete prodeje na několika trzích z jedné centralizované kanceláře.</span><span class="sxs-lookup"><span data-stu-id="61713-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="61713-112">Další informace najdete v tématu Parametry [identifikátoru URI.](#uri-parameters)</span><span class="sxs-lookup"><span data-stu-id="61713-112">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="61713-113">C\#</span><span class="sxs-lookup"><span data-stu-id="61713-113">C\#</span></span>

<span data-ttu-id="61713-114">Pokud chcete získat kartu sazeb Azure, zavolejte metodu [**IAzureRateCard.Get,**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) která vrátí prostředek [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) obsahující ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="61713-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="61713-115">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="61713-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="61713-116">**Project:** SDK pro Partnerské centrum Samples **Class**: GetAzureRateCard.cs</span><span class="sxs-lookup"><span data-stu-id="61713-116">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="61713-117">Java</span><span class="sxs-lookup"><span data-stu-id="61713-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="61713-118">Pokud chcete získat kartu sazeb Azure, zavolejte **funkci IAzureRateCard.get,** která vrátí podrobnosti o kartě sazeb, která obsahuje ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="61713-118">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="61713-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="61713-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="61713-120">Pokud chcete získat kartu Azure, spusťte příkaz [**Get-PartnerAzureRateCard,**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) který vrátí podrobnosti o kartě sazeb, která obsahuje ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="61713-120">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="61713-121">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="61713-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="61713-122">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="61713-122">Request syntax</span></span>

| <span data-ttu-id="61713-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="61713-123">Method</span></span>  | <span data-ttu-id="61713-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="61713-124">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="61713-125">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="61713-125">**GET**</span></span> | <span data-ttu-id="61713-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span><span class="sxs-lookup"><span data-stu-id="61713-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="61713-127">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="61713-127">URI parameters</span></span>

| <span data-ttu-id="61713-128">Název</span><span class="sxs-lookup"><span data-stu-id="61713-128">Name</span></span>     | <span data-ttu-id="61713-129">Typ</span><span class="sxs-lookup"><span data-stu-id="61713-129">Type</span></span>   | <span data-ttu-id="61713-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="61713-130">Required</span></span> | <span data-ttu-id="61713-131">Popis</span><span class="sxs-lookup"><span data-stu-id="61713-131">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="61713-132">currency</span><span class="sxs-lookup"><span data-stu-id="61713-132">currency</span></span> | <span data-ttu-id="61713-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="61713-133">string</span></span> | <span data-ttu-id="61713-134">No</span><span class="sxs-lookup"><span data-stu-id="61713-134">No</span></span>       | <span data-ttu-id="61713-135">Volitelný třípísmenný kód ISO pro měnu, ve které budou uvedeny sazby prostředků (například `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="61713-135">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="61713-136">Výchozí formát je `USD`.</span><span class="sxs-lookup"><span data-stu-id="61713-136">The default is `USD`.</span></span> |
| <span data-ttu-id="61713-137">oblast</span><span class="sxs-lookup"><span data-stu-id="61713-137">region</span></span>   | <span data-ttu-id="61713-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="61713-138">string</span></span> | <span data-ttu-id="61713-139">No</span><span class="sxs-lookup"><span data-stu-id="61713-139">No</span></span>       | <span data-ttu-id="61713-140">Volitelný dvoupísmenný kód ISO země/oblasti, který označuje trh, na kterém je nabídka zakoupená (například `FR` ).</span><span class="sxs-lookup"><span data-stu-id="61713-140">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="61713-141">Výchozí formát je `US`.</span><span class="sxs-lookup"><span data-stu-id="61713-141">The default is `US`.</span></span>        |

<span data-ttu-id="61713-142">Do požadavku můžete zahrnout volitelnou [hlavičku](headers.md#rest-request-headers) X-Locale.</span><span class="sxs-lookup"><span data-stu-id="61713-142">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="61713-143">Pokud hlavičku X-Locale nezadáte, použije se výchozí hodnota (en-US).</span><span class="sxs-lookup"><span data-stu-id="61713-143">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="61713-144">Pokud v požadavku zadáte parametry měny a oblasti, hodnota X-národního prostředí se použije k určení jazyka odpovědi.</span><span class="sxs-lookup"><span data-stu-id="61713-144">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="61713-145">Pokud v požadavku nezadáte parametry oblasti a měny, hodnota X-národního prostředí se použije k určení oblasti, měny a jazyka odpovědi.</span><span class="sxs-lookup"><span data-stu-id="61713-145">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="61713-146">Hlavička požadavku</span><span class="sxs-lookup"><span data-stu-id="61713-146">Request header</span></span>

<span data-ttu-id="61713-147">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="61713-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="61713-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="61713-148">Request body</span></span>

<span data-ttu-id="61713-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="61713-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="61713-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="61713-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="61713-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="61713-151">REST response</span></span>

<span data-ttu-id="61713-152">Pokud je požadavek úspěšný, vrátí prostředek [Azure Rate Card.](azure-rate-card-resources.md)</span><span class="sxs-lookup"><span data-stu-id="61713-152">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="61713-153">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="61713-153">Response success and error codes</span></span>

<span data-ttu-id="61713-154">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="61713-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="61713-155">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="61713-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="61713-156">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="61713-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="61713-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="61713-157">Response example</span></span>

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
    "locale": "en",
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
