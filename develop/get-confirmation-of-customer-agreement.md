---
title: Získání potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Tento článek vysvětluje, jak získat potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766897"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="ec1f5-103">Získání potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka</span><span class="sxs-lookup"><span data-stu-id="ec1f5-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="ec1f5-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="ec1f5-104">**Applies to:**</span></span>

- <span data-ttu-id="ec1f5-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="ec1f5-105">Partner Center</span></span>

<span data-ttu-id="ec1f5-106">V současné době je prostředek **smlouvy** podporován partnerským centrem pouze ve *veřejném cloudu Microsoftu*.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-106">The **Agreement** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="ec1f5-107">Tento prostředek se nevztahuje na:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-107">This resource doesn't apply to:</span></span>

- <span data-ttu-id="ec1f5-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="ec1f5-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ec1f5-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="ec1f5-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ec1f5-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ec1f5-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ec1f5-111">Tento článek vysvětluje, jak můžete získat potvrzení přijetí smlouvy o zákaznících Microsoftu u zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-111">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec1f5-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ec1f5-112">Prerequisites</span></span>

- <span data-ttu-id="ec1f5-113">Pokud používáte sadu SDK partnerského centra .NET, verze 1,14 nebo novější je povinná.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="ec1f5-114">Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="ec1f5-115">Tento scénář podporuje jenom ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-115">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="ec1f5-116">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ec1f5-117">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ec1f5-118">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ec1f5-119">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ec1f5-120">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="ec1f5-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ec1f5-121">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="ec1f5-122">.NET</span><span class="sxs-lookup"><span data-stu-id="ec1f5-122">.NET</span></span>

<span data-ttu-id="ec1f5-123">Chcete-li získat potvrzení o přijetí od zákazníka, které bylo dříve poskytnuto:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="ec1f5-124">Použijte kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById** se zadaným identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="ec1f5-125">Načtěte vlastnost **smluvs** a Filtrujte výsledky do smlouvy na zákazníky Microsoftu voláním metody **ByAgreementType** .</span><span class="sxs-lookup"><span data-stu-id="ec1f5-125">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="ec1f5-126">Volejte metodu **Get** nebo **GetAsync** .</span><span class="sxs-lookup"><span data-stu-id="ec1f5-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="ec1f5-127">Kompletní ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="ec1f5-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ec1f5-128">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ec1f5-128">REST request</span></span>

<span data-ttu-id="ec1f5-129">Chcete-li získat potvrzení přijetí od zákazníka, které bylo dříve poskytnuto:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-129">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="ec1f5-130">Vytvořte žádost REST, aby se načetla kolekce [smluv](./agreement-resources.md) pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-130">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="ec1f5-131">Použijte parametr dotazu **agreemtntype** k určení oboru výsledků jenom na zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-131">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ec1f5-132">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ec1f5-132">Request syntax</span></span>

<span data-ttu-id="ec1f5-133">Použijte následující syntaxi žádosti:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-133">Use the following request syntax:</span></span>

| <span data-ttu-id="ec1f5-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="ec1f5-134">Method</span></span> | <span data-ttu-id="ec1f5-135">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ec1f5-135">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec1f5-136">GET</span><span class="sxs-lookup"><span data-stu-id="ec1f5-136">GET</span></span>    | <span data-ttu-id="ec1f5-137">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements? agreemtntype = {smlouva-Type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ec1f5-137">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="ec1f5-138">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="ec1f5-138">URI parameters</span></span>

<span data-ttu-id="ec1f5-139">S vaším požadavkem můžete použít následující parametry identifikátoru URI:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-139">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="ec1f5-140">Název</span><span class="sxs-lookup"><span data-stu-id="ec1f5-140">Name</span></span>             | <span data-ttu-id="ec1f5-141">Typ</span><span class="sxs-lookup"><span data-stu-id="ec1f5-141">Type</span></span> | <span data-ttu-id="ec1f5-142">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ec1f5-142">Required</span></span> | <span data-ttu-id="ec1f5-143">Popis</span><span class="sxs-lookup"><span data-stu-id="ec1f5-143">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec1f5-144">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="ec1f5-144">customer-tenant-id</span></span> | <span data-ttu-id="ec1f5-145">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="ec1f5-145">GUID</span></span> | <span data-ttu-id="ec1f5-146">Yes</span><span class="sxs-lookup"><span data-stu-id="ec1f5-146">Yes</span></span> | <span data-ttu-id="ec1f5-147">Hodnota je **CustomerTenantId** ve formátu GUID, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-147">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="ec1f5-148">typ smlouvy</span><span class="sxs-lookup"><span data-stu-id="ec1f5-148">agreement-type</span></span> | <span data-ttu-id="ec1f5-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="ec1f5-149">string</span></span> | <span data-ttu-id="ec1f5-150">No</span><span class="sxs-lookup"><span data-stu-id="ec1f5-150">No</span></span> | <span data-ttu-id="ec1f5-151">Tento parametr vrátí všechna metadata smlouvy.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-151">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="ec1f5-152">Tento parametr slouží k určení rozsahu odpovědi dotazu na konkrétní typ smlouvy.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-152">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="ec1f5-153">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-153">The supported values are:</span></span> <br/><br/> <span data-ttu-id="ec1f5-154">**MicrosoftCloudAgreement** , která zahrnuje pouze metadata smlouvy typu *MicrosoftCloudAgreement*.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-154">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="ec1f5-155">**MicrosoftCustomerAgreement** , která zahrnuje pouze metadata smlouvy typu *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-155">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="ec1f5-156">**\*** který vrátí všechna metadata smlouvy.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-156">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="ec1f5-157">(Nepoužívejte **\*** , pokud váš kód nemá potřebnou logiku pro zpracování neočekávaných typů smluv.)</span><span class="sxs-lookup"><span data-stu-id="ec1f5-157">(Don't use **\*** unless your code has the necessary logic to handle unexpected agreement types.)</span></span><br/><br/> <span data-ttu-id="ec1f5-158">**Poznámka:** Pokud není zadán parametr URI, výchozí dotaz se **MicrosoftCloudAgreement** na zpětnou kompatibilitu.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-158">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="ec1f5-159">Společnost Microsoft může v každé chvíli zavést metadata smlouvy s novými typy smluv.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-159">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="ec1f5-160">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ec1f5-160">Request headers</span></span>

<span data-ttu-id="ec1f5-161">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ec1f5-162">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ec1f5-162">Request body</span></span>

<span data-ttu-id="ec1f5-163">Žádné</span><span class="sxs-lookup"><span data-stu-id="ec1f5-163">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ec1f5-164">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ec1f5-164">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="ec1f5-165">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ec1f5-165">REST response</span></span>

<span data-ttu-id="ec1f5-166">V případě úspěchu tato metoda vrátí kolekci prostředků **smlouvy** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-166">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ec1f5-167">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ec1f5-167">Response success and error codes</span></span>

<span data-ttu-id="ec1f5-168">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-168">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="ec1f5-169">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-169">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ec1f5-170">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-170">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ec1f5-171">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ec1f5-171">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
