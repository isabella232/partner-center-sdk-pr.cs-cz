---
title: Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu
description: Tento článek vysvětluje, jak získat metadata smlouvy pro Smlouva se zákazníkem Microsoftu.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 5c20b317edf16b159050884070683880cf7e45bb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025713"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="b4add-103">Získání metadat smluv pro Smlouvu se zákazníkem Microsoftu</span><span class="sxs-lookup"><span data-stu-id="b4add-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="b4add-104">**Platí pro:** Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b4add-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="b4add-105">**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b4add-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b4add-106">Metadata smlouvy pro Smlouva se zákazníkem Microsoftu se v současné době Partnerské centrum jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="b4add-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="b4add-107">Než budete moci Smlouva se zákazníkem Microsoftu:</span><span class="sxs-lookup"><span data-stu-id="b4add-107">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="b4add-108">Potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu</span><span class="sxs-lookup"><span data-stu-id="b4add-108">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="b4add-109">Načtení odkazu ke stažení Smlouva se zákazníkem Microsoftu šablony</span><span class="sxs-lookup"><span data-stu-id="b4add-109">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="b4add-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b4add-110">Prerequisites</span></span>

- <span data-ttu-id="b4add-111">Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.14 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="b4add-111">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="b4add-112">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b4add-112">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="b4add-113">Tento scénář podporuje pouze ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="b4add-113">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="b4add-114">.NET (verze 1.14 nebo novější)</span><span class="sxs-lookup"><span data-stu-id="b4add-114">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="b4add-115">Načtení metadat smlouvy pro Smlouva se zákazníkem Microsoftu:</span><span class="sxs-lookup"><span data-stu-id="b4add-115">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="b4add-116">Nejprve načtěte **kolekci IAggregatePartner.AgreementDetails.**</span><span class="sxs-lookup"><span data-stu-id="b4add-116">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="b4add-117">Voláním **metody ByAgreementType** vyfiltrujte kolekci, Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="b4add-117">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="b4add-118">Nakonec zavolejte **metodu Get** **nebo GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="b4add-118">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="b4add-119">Úplnou ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [konzolové testovací aplikace.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="b4add-119">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b4add-120">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="b4add-120">REST request</span></span>

<span data-ttu-id="b4add-121">Načtení metadat smlouvy pro Smlouva se zákazníkem Microsoftu:</span><span class="sxs-lookup"><span data-stu-id="b4add-121">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="b4add-122">Vytvořte požadavek REST pro načtení [kolekce AgreementMetaData.](./agreement-metadata-resources.md)</span><span class="sxs-lookup"><span data-stu-id="b4add-122">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="b4add-123">Parametr dotazu **agreementType** použijte k nastavení rozsahu výsledku pouze na Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="b4add-123">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b4add-124">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="b4add-124">Request syntax</span></span>

| <span data-ttu-id="b4add-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="b4add-125">Method</span></span> | <span data-ttu-id="b4add-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b4add-126">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="b4add-127">GET</span><span class="sxs-lookup"><span data-stu-id="b4add-127">GET</span></span>    | <span data-ttu-id="b4add-128">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b4add-128">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b4add-129">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="b4add-129">URI parameters</span></span>

| <span data-ttu-id="b4add-130">Název</span><span class="sxs-lookup"><span data-stu-id="b4add-130">Name</span></span>                   | <span data-ttu-id="b4add-131">Typ</span><span class="sxs-lookup"><span data-stu-id="b4add-131">Type</span></span>     | <span data-ttu-id="b4add-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b4add-132">Required</span></span> | <span data-ttu-id="b4add-133">Popis</span><span class="sxs-lookup"><span data-stu-id="b4add-133">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="b4add-134">agreement-type</span><span class="sxs-lookup"><span data-stu-id="b4add-134">agreement-type</span></span> | <span data-ttu-id="b4add-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="b4add-135">string</span></span> | <span data-ttu-id="b4add-136">No</span><span class="sxs-lookup"><span data-stu-id="b4add-136">No</span></span> | <span data-ttu-id="b4add-137">Tento parametr použijte k nastavení rozsahu odpovědi na dotaz na konkrétní typ smlouvy.</span><span class="sxs-lookup"><span data-stu-id="b4add-137">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="b4add-138">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="b4add-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="b4add-139">**MicrosoftCloudAgreement,** který zahrnuje jenom metadata smlouvy typu *MicrosoftCloudAgreement*</span><span class="sxs-lookup"><span data-stu-id="b4add-139">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="b4add-140">**MicrosoftCustomerAgreement,** který obsahuje metadata smlouvy pouze typu *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="b4add-140">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="b4add-141">**\**– vrátí všechna metadata smlouvy. (Nepoužívejte _\* \* _ pokud váš kód nemá potřebnou logiku modulu runtime pro zpracování neznámých typů smlouvy, protože Microsoft může kdykoli zavést metadata smlouvy s novými *typy smlouvy.) <br/> <br/> _* Poznámka:*\* Pokud není zadaný parametr URI, výchozí hodnota dotazu je **MicrosoftCloudAgreement** pro zpětnou kompatibilitu.</span><span class="sxs-lookup"><span data-stu-id="b4add-141">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="b4add-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b4add-142">Request headers</span></span>

<span data-ttu-id="b4add-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b4add-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b4add-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b4add-144">Request body</span></span>

<span data-ttu-id="b4add-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="b4add-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b4add-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b4add-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="b4add-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b4add-147">REST response</span></span>

<span data-ttu-id="b4add-148">V případě úspěchu vrátí tato metoda v textu odpovědi kolekci prostředků [ **AgreementMetaData.**](./agreement-metadata-resources.md)</span><span class="sxs-lookup"><span data-stu-id="b4add-148">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b4add-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="b4add-149">Response success and error codes</span></span>

<span data-ttu-id="b4add-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b4add-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="b4add-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="b4add-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b4add-152">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b4add-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b4add-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b4add-153">Response example</span></span>

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
