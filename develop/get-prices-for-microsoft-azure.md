---
title: Získání cen pro Microsoft Azure
description: Jak získat kartu Azure Rate s cenami v reálném čase pro nabídku Azure. Ceny Azure jsou poměrně dynamické a často se mění.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0716f0428b13604105b435a2ce8287a8b4609fea
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/19/2020
ms.locfileid: "97767669"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="322c2-104">Získání cen pro Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="322c2-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="322c2-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="322c2-105">**Applies To**</span></span>

- <span data-ttu-id="322c2-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="322c2-106">Partner Center</span></span>
- <span data-ttu-id="322c2-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="322c2-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="322c2-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="322c2-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="322c2-109">Jak získat [kartu Azure Rate](azure-rate-card-resources.md) s cenami v reálném čase pro nabídku Azure.</span><span class="sxs-lookup"><span data-stu-id="322c2-109">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="322c2-110">Ceny Azure jsou poměrně dynamické a často se mění.</span><span class="sxs-lookup"><span data-stu-id="322c2-110">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="322c2-111">Pokud chcete sledovat využití a předpovídat měsíční fakturaci a faktury pro jednotlivé zákazníky, můžete tento dotaz na kartu Azure Rate kombinovat a získat tak ceny Microsoft Azure s žádostí o [získání záznamů o využití zákazníka pro Azure](get-a-customer-s-utilization-record-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="322c2-111">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="322c2-112">Ceny se liší podle trhu a měny a toto rozhraní API bere v úvahu umístění.</span><span class="sxs-lookup"><span data-stu-id="322c2-112">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="322c2-113">Ve výchozím nastavení používá rozhraní API nastavení partnerského profilu v partnerském centru a v jazyce prohlížeče a tato nastavení jsou přizpůsobitelná.</span><span class="sxs-lookup"><span data-stu-id="322c2-113">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="322c2-114">Povědomí o poloze je obzvláště důležité, pokud spravujete prodej na více trzích z jedné centrálně centralizované kanceláře.</span><span class="sxs-lookup"><span data-stu-id="322c2-114">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="322c2-115">Další informace najdete v tématu [parametry identifikátoru URI](#uri-parameters).</span><span class="sxs-lookup"><span data-stu-id="322c2-115">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="322c2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="322c2-116">C\#</span></span>

<span data-ttu-id="322c2-117">Pokud chcete získat kartu Azure Rate, zavolejte metodu [**IAzureRateCard. Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) , která vrátí prostředek [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) , který obsahuje ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="322c2-117">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="322c2-118">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="322c2-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="322c2-119">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetAzureRateCard.cs</span><span class="sxs-lookup"><span data-stu-id="322c2-119">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="322c2-120">Java</span><span class="sxs-lookup"><span data-stu-id="322c2-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="322c2-121">Pokud chcete získat kartu Azure Rate, zavolejte funkci **IAzureRateCard. Get** , která vrátí podrobnosti o sazbách, které obsahují ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="322c2-121">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="322c2-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="322c2-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="322c2-123">Pokud chcete získat kartu Azure, spusťte příkaz [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) , který vrátí podrobnosti o ceníku, který obsahuje ceny Azure.</span><span class="sxs-lookup"><span data-stu-id="322c2-123">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="322c2-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="322c2-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="322c2-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="322c2-125">Request syntax</span></span>

| <span data-ttu-id="322c2-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="322c2-126">Method</span></span>  | <span data-ttu-id="322c2-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="322c2-127">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="322c2-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="322c2-128">**GET**</span></span> | <span data-ttu-id="322c2-129">*{baseURL}*/v1/ratecards/Azure? Currency = {currency} &oblast = {region}</span><span class="sxs-lookup"><span data-stu-id="322c2-129">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="322c2-130">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="322c2-130">URI parameters</span></span>

| <span data-ttu-id="322c2-131">Název</span><span class="sxs-lookup"><span data-stu-id="322c2-131">Name</span></span>     | <span data-ttu-id="322c2-132">Typ</span><span class="sxs-lookup"><span data-stu-id="322c2-132">Type</span></span>   | <span data-ttu-id="322c2-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="322c2-133">Required</span></span> | <span data-ttu-id="322c2-134">Popis</span><span class="sxs-lookup"><span data-stu-id="322c2-134">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="322c2-135">currency</span><span class="sxs-lookup"><span data-stu-id="322c2-135">currency</span></span> | <span data-ttu-id="322c2-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="322c2-136">string</span></span> | <span data-ttu-id="322c2-137">No</span><span class="sxs-lookup"><span data-stu-id="322c2-137">No</span></span>       | <span data-ttu-id="322c2-138">Volitelná tři písmena ISO kódu pro měnu, ve které se budou poskytovat sazby za prostředky (například `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="322c2-138">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="322c2-139">Výchozí formát je `USD`.</span><span class="sxs-lookup"><span data-stu-id="322c2-139">The default is `USD`.</span></span> |
| <span data-ttu-id="322c2-140">oblast</span><span class="sxs-lookup"><span data-stu-id="322c2-140">region</span></span>   | <span data-ttu-id="322c2-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="322c2-141">string</span></span> | <span data-ttu-id="322c2-142">No</span><span class="sxs-lookup"><span data-stu-id="322c2-142">No</span></span>       | <span data-ttu-id="322c2-143">Volitelné dvoumístné číslo země/oblasti ISO, které označuje uvedení na trh, na který byla nabídka koupena (například `FR` ).</span><span class="sxs-lookup"><span data-stu-id="322c2-143">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="322c2-144">Výchozí formát je `US`.</span><span class="sxs-lookup"><span data-stu-id="322c2-144">The default is `US`.</span></span>        |

<span data-ttu-id="322c2-145">Do žádosti můžete zahrnout volitelné [záhlaví](headers.md#rest-request-headers) X-locale.</span><span class="sxs-lookup"><span data-stu-id="322c2-145">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="322c2-146">Pokud nezadáte hlavičku X-locale, použije se výchozí hodnota ("en-US").</span><span class="sxs-lookup"><span data-stu-id="322c2-146">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="322c2-147">Pokud v žádosti zadáte parametry měny a oblasti, použije se k určení jazyka odpovědi hodnota X-locale.</span><span class="sxs-lookup"><span data-stu-id="322c2-147">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="322c2-148">Pokud v požadavku neposkytnete parametry region a Currency, použije se k určení oblasti, měny a jazyka odpovědi hodnota X-locale.</span><span class="sxs-lookup"><span data-stu-id="322c2-148">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="322c2-149">Hlavička požadavku</span><span class="sxs-lookup"><span data-stu-id="322c2-149">Request header</span></span>

<span data-ttu-id="322c2-150">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="322c2-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="322c2-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="322c2-151">Request body</span></span>

<span data-ttu-id="322c2-152">Žádné</span><span class="sxs-lookup"><span data-stu-id="322c2-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="322c2-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="322c2-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="322c2-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="322c2-154">REST response</span></span>

<span data-ttu-id="322c2-155">Pokud je požadavek úspěšný, vrátí prostředek [Azure Rate karta](azure-rate-card-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="322c2-155">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="322c2-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="322c2-156">Response success and error codes</span></span>

<span data-ttu-id="322c2-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="322c2-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="322c2-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="322c2-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="322c2-159">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="322c2-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="322c2-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="322c2-160">Response example</span></span>

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
