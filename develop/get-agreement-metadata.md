---
title: Získání metadat smluv pro Smlouvu o službách Microsoft Cloud
description: Tento článek vysvětluje, jak získat metadata smlouvy pro Microsoft Cloud smlouvu.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c6a404eb38c4c31d3e69bb598872b932d8985529
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766838"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a><span data-ttu-id="2047f-103">Získání metadat smluv pro Smlouvu o službách Microsoft Cloud</span><span class="sxs-lookup"><span data-stu-id="2047f-103">Get agreement metadata for Microsoft Cloud Agreement</span></span>

<span data-ttu-id="2047f-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="2047f-104">**Applies To**</span></span>

- <span data-ttu-id="2047f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="2047f-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="2047f-106">Prostředek **AgreementMetaData** je aktuálně podporovaný partnerským centrem jenom ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="2047f-106">The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="2047f-107">Neplatí pro:</span><span class="sxs-lookup"><span data-stu-id="2047f-107">It isn't applicable to:</span></span>
> - <span data-ttu-id="2047f-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="2047f-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="2047f-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="2047f-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="2047f-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2047f-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2047f-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2047f-111">Prerequisites</span></span>

- <span data-ttu-id="2047f-112">Pokud používáte sadu SDK partnerského centra .NET, verze 1,9 nebo novější je povinná.</span><span class="sxs-lookup"><span data-stu-id="2047f-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="2047f-113">Pokud používáte sadu SDK pro partnerský Center Java, verze 1,8 nebo novější je povinná.</span><span class="sxs-lookup"><span data-stu-id="2047f-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="2047f-114">Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2047f-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="2047f-115">Tento scénář podporuje ověřování aplikací a uživatelů..</span><span class="sxs-lookup"><span data-stu-id="2047f-115">This scenario supports app + user authentication..</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="2047f-116">.NET (verze 1,14 nebo novější)</span><span class="sxs-lookup"><span data-stu-id="2047f-116">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="2047f-117">Načtení metadat smlouvy pro Microsoft Cloud smlouvu:</span><span class="sxs-lookup"><span data-stu-id="2047f-117">To retrieve the agreement metadata for Microsoft Cloud Agreement:</span></span>

1. <span data-ttu-id="2047f-118">Nejdřív načtěte kolekci **IAggregatePartner. AgreementDetails** .</span><span class="sxs-lookup"><span data-stu-id="2047f-118">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="2047f-119">Zavolejte metodu **ByAgreementType** pro filtrování kolekce do smlouvy Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="2047f-119">Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.</span></span>

3. <span data-ttu-id="2047f-120">Nakonec volejte metodu **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="2047f-120">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="2047f-121">Kompletní ukázku najdete ve třídě [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="2047f-121">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="2047f-122">.NET (verze 1,9 – 1,13)</span><span class="sxs-lookup"><span data-stu-id="2047f-122">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="2047f-123">Postup načtení metadat smlouvy pro Microsoft Cloud smlouvu:</span><span class="sxs-lookup"><span data-stu-id="2047f-123">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="2047f-124">Nejprve načtěte kolekci **IAggregatePartner. AgreementDetails** a poté zavolejte metody **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="2047f-124">First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods.</span></span> <span data-ttu-id="2047f-125">Pak vyhledejte položku v kolekci, která odpovídá Microsoft Cloud smlouvě:</span><span class="sxs-lookup"><span data-stu-id="2047f-125">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a><span data-ttu-id="2047f-126">Java</span><span class="sxs-lookup"><span data-stu-id="2047f-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="2047f-127">Postup načtení metadat smlouvy pro Microsoft Cloud smlouvu:</span><span class="sxs-lookup"><span data-stu-id="2047f-127">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="2047f-128">Nejprve zavolejte funkci **IAggregatePartner. getAgreementDetails** a poté zavolejte funkci **Get** .</span><span class="sxs-lookup"><span data-stu-id="2047f-128">First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function.</span></span> <span data-ttu-id="2047f-129">Pak vyhledejte položku v kolekci, která odpovídá Microsoft Cloud smlouvě:</span><span class="sxs-lookup"><span data-stu-id="2047f-129">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

<span data-ttu-id="2047f-130">Kompletní ukázku najdete ve třídě [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) z projektu [testovací aplikace konzoly](https://github.com/Microsoft/Partner-Center-Java-Samples) .</span><span class="sxs-lookup"><span data-stu-id="2047f-130">A complete sample can be found in the [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="2047f-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2047f-131">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="2047f-132">Postup načtení metadat smlouvy pro Microsoft Cloud smlouvu:</span><span class="sxs-lookup"><span data-stu-id="2047f-132">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="2047f-133">Použijte příkaz [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) .</span><span class="sxs-lookup"><span data-stu-id="2047f-133">Use the [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) command.</span></span> <span data-ttu-id="2047f-134">Pak vyhledejte položku v kolekci, která odpovídá Microsoft Cloud smlouvě:</span><span class="sxs-lookup"><span data-stu-id="2047f-134">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a><span data-ttu-id="2047f-135">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="2047f-135">REST request</span></span>

<span data-ttu-id="2047f-136">Pokud chcete načíst metadata smlouvy pro Microsoft Cloud smlouvu, nejdřív vytvořte žádost REST pro načtení kolekce **AgreementMetaData** .</span><span class="sxs-lookup"><span data-stu-id="2047f-136">To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection.</span></span> <span data-ttu-id="2047f-137">Pak vyhledejte položku v kolekci, která odpovídá Microsoft Cloud smlouvě.</span><span class="sxs-lookup"><span data-stu-id="2047f-137">Then search for the item in the collection which corresponds to the Microsoft Cloud Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2047f-138">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="2047f-138">Request syntax</span></span>

| <span data-ttu-id="2047f-139">Metoda</span><span class="sxs-lookup"><span data-stu-id="2047f-139">Method</span></span> | <span data-ttu-id="2047f-140">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2047f-140">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="2047f-141">GET</span><span class="sxs-lookup"><span data-stu-id="2047f-141">GET</span></span>    | <span data-ttu-id="2047f-142">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2047f-142">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2047f-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2047f-143">Request headers</span></span>

<span data-ttu-id="2047f-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2047f-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2047f-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2047f-145">Request body</span></span>

<span data-ttu-id="2047f-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="2047f-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2047f-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="2047f-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="2047f-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2047f-148">REST response</span></span>

<span data-ttu-id="2047f-149">V případě úspěchu tato metoda vrátí kolekci prostředků **AgreementMetaData** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="2047f-149">If successful, this method returns a collection of **AgreementMetaData** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2047f-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="2047f-150">Response success and error codes</span></span>

<span data-ttu-id="2047f-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2047f-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2047f-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="2047f-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2047f-153">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2047f-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2047f-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="2047f-154">Response example</span></span>

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="2047f-155">K identifikaci prostředku v odpovědi, která odpovídá Microsoft Cloud smlouvě, vyhledejte prostředek, jehož vlastnost **agreemtntype** má hodnotu "MicrosoftCloudAgreement".</span><span class="sxs-lookup"><span data-stu-id="2047f-155">To identify the resource in the response which corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".</span></span>
