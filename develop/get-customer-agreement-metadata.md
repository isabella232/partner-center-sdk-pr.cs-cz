---
title: Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu
description: Tento článek vysvětluje, jak získat metadata smlouvy pro zákaznickou smlouvu Microsoftu.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766895"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="61502-103">Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu</span><span class="sxs-lookup"><span data-stu-id="61502-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="61502-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="61502-104">**Applies to:**</span></span>

- <span data-ttu-id="61502-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="61502-105">Partner Center</span></span>

<span data-ttu-id="61502-106">Metadata smlouvy pro zákaznickou smlouvu Microsoft jsou aktuálně podporována partnerským centrem pouze ve *veřejném cloudu společnosti Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="61502-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="61502-107">Neplatí pro:</span><span class="sxs-lookup"><span data-stu-id="61502-107">It doesn't apply to:</span></span>

- <span data-ttu-id="61502-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="61502-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="61502-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="61502-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="61502-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="61502-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="61502-111">Metadata smlouvy pro zákaznickou smlouvu od Microsoftu musíte načíst, abyste mohli:</span><span class="sxs-lookup"><span data-stu-id="61502-111">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="61502-112">Potvrzení souhlasu zákazníka s zákaznickou smlouvou Microsoftu</span><span class="sxs-lookup"><span data-stu-id="61502-112">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="61502-113">Načtení odkazu ke stažení pro šablonu zákaznické smlouvy Microsoft</span><span class="sxs-lookup"><span data-stu-id="61502-113">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="61502-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="61502-114">Prerequisites</span></span>

- <span data-ttu-id="61502-115">Pokud používáte sadu SDK partnerského centra .NET, verze 1,14 nebo novější je povinná.</span><span class="sxs-lookup"><span data-stu-id="61502-115">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="61502-116">Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="61502-116">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="61502-117">Tento scénář podporuje jenom ověřování uživatelů a aplikací.</span><span class="sxs-lookup"><span data-stu-id="61502-117">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="61502-118">.NET (verze 1,14 nebo novější)</span><span class="sxs-lookup"><span data-stu-id="61502-118">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="61502-119">Načtení metadat smlouvy pro zákaznickou smlouvu Microsoftu:</span><span class="sxs-lookup"><span data-stu-id="61502-119">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="61502-120">Nejdřív načtěte kolekci **IAggregatePartner. AgreementDetails** .</span><span class="sxs-lookup"><span data-stu-id="61502-120">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="61502-121">Zavolejte metodu **ByAgreementType** , která filtruje kolekci na zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="61502-121">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="61502-122">Nakonec volejte metodu **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="61502-122">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="61502-123">Kompletní ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="61502-123">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="61502-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="61502-124">REST request</span></span>

<span data-ttu-id="61502-125">Načtení metadat smlouvy pro zákaznickou smlouvu Microsoftu:</span><span class="sxs-lookup"><span data-stu-id="61502-125">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="61502-126">Vytvořte žádost REST pro načtení kolekce [AgreementMetaData](./agreement-metadata-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="61502-126">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="61502-127">Použijte parametr dotazu **agreemtntype** k určení oboru výsledků jenom pro zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="61502-127">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="61502-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="61502-128">Request syntax</span></span>

| <span data-ttu-id="61502-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="61502-129">Method</span></span> | <span data-ttu-id="61502-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="61502-130">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="61502-131">GET</span><span class="sxs-lookup"><span data-stu-id="61502-131">GET</span></span>    | <span data-ttu-id="61502-132">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Agreements? agreemtntype = {smlouva-Type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="61502-132">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="61502-133">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="61502-133">URI parameters</span></span>

| <span data-ttu-id="61502-134">Název</span><span class="sxs-lookup"><span data-stu-id="61502-134">Name</span></span>                   | <span data-ttu-id="61502-135">Typ</span><span class="sxs-lookup"><span data-stu-id="61502-135">Type</span></span>     | <span data-ttu-id="61502-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="61502-136">Required</span></span> | <span data-ttu-id="61502-137">Popis</span><span class="sxs-lookup"><span data-stu-id="61502-137">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="61502-138">typ smlouvy</span><span class="sxs-lookup"><span data-stu-id="61502-138">agreement-type</span></span> | <span data-ttu-id="61502-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="61502-139">string</span></span> | <span data-ttu-id="61502-140">No</span><span class="sxs-lookup"><span data-stu-id="61502-140">No</span></span> | <span data-ttu-id="61502-141">Tento parametr slouží k určení rozsahu odpovědi dotazu na konkrétní typ smlouvy.</span><span class="sxs-lookup"><span data-stu-id="61502-141">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="61502-142">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="61502-142">The supported values are:</span></span> <br/><br/><span data-ttu-id="61502-143">**MicrosoftCloudAgreement** , která zahrnuje metadata smlouvy pouze typu *MicrosoftCloudAgreement*</span><span class="sxs-lookup"><span data-stu-id="61502-143">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="61502-144">**MicrosoftCustomerAgreement** , která zahrnuje metadata smlouvy pouze typu *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="61502-144">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="61502-145">**\*** který vrátí všechna metadata smlouvy.</span><span class="sxs-lookup"><span data-stu-id="61502-145">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="61502-146">(Nepoužívejte **\*** , pokud váš kód nemá nezbytnou běhovou logiku pro zpracování neznámých typů smluv, protože společnost Microsoft může zavést metadata smlouvy s novými typy smluv kdykoli.)</span><span class="sxs-lookup"><span data-stu-id="61502-146">(Don't use **\*** unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)</span></span><br/><br/> <span data-ttu-id="61502-147">**Poznámka:** Pokud není zadán parametr URI, výchozí dotaz se **MicrosoftCloudAgreement** na zpětnou kompatibilitu.</span><span class="sxs-lookup"><span data-stu-id="61502-147">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="61502-148">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="61502-148">Request headers</span></span>

<span data-ttu-id="61502-149">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="61502-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="61502-150">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="61502-150">Request body</span></span>

<span data-ttu-id="61502-151">Žádné</span><span class="sxs-lookup"><span data-stu-id="61502-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="61502-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="61502-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="61502-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="61502-153">REST response</span></span>

<span data-ttu-id="61502-154">V případě úspěchu tato metoda vrátí kolekci [prostředků **AgreementMetaData**](./agreement-metadata-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="61502-154">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="61502-155">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="61502-155">Response success and error codes</span></span>

<span data-ttu-id="61502-156">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="61502-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="61502-157">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="61502-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="61502-158">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="61502-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="61502-159">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="61502-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
