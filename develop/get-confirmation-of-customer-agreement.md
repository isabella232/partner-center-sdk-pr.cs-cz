---
title: Získání potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Tento článek vysvětluje, jak získat potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3668a5e510effb533cade311f52513b9a81d40af
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760534"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="db48b-103">Získání potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka</span><span class="sxs-lookup"><span data-stu-id="db48b-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="db48b-104">**Platí pro:** Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="db48b-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="db48b-105">**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="db48b-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="db48b-106">Prostředek **smlouvy** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="db48b-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="db48b-107">Tento článek vysvětluje, jak můžete načíst potvrzení souhlasu zákazníka s přijetím Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="db48b-107">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db48b-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="db48b-108">Prerequisites</span></span>

- <span data-ttu-id="db48b-109">Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.14 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="db48b-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="db48b-110">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="db48b-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="db48b-111">Tento scénář podporuje pouze ověřování aplikací a uživatelů.</span><span class="sxs-lookup"><span data-stu-id="db48b-111">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="db48b-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="db48b-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="db48b-113">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="db48b-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="db48b-114">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="db48b-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="db48b-115">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="db48b-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="db48b-116">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="db48b-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="db48b-117">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="db48b-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="db48b-118">.NET</span><span class="sxs-lookup"><span data-stu-id="db48b-118">.NET</span></span>

<span data-ttu-id="db48b-119">Získání potvrzení přijetí zákazníkem, která byla dříve poskytnuta:</span><span class="sxs-lookup"><span data-stu-id="db48b-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="db48b-120">Použijte kolekci **IAggregatePartner.Customers** a zavolejte **metodu ById** se zadaným identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="db48b-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="db48b-121">**Načítá vlastnost Agreements** a filtruje výsledky, Smlouva se zákazníkem Microsoftu voláním **metody ByAgreementType.**</span><span class="sxs-lookup"><span data-stu-id="db48b-121">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="db48b-122">Volejte **metodu Get** **nebo GetAsync.**</span><span class="sxs-lookup"><span data-stu-id="db48b-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="db48b-123">Úplnou ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [konzolové testovací](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) aplikace.</span><span class="sxs-lookup"><span data-stu-id="db48b-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="db48b-124">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="db48b-124">REST request</span></span>

<span data-ttu-id="db48b-125">Získání dříve poskytnutého potvrzení přijetí zákazníkem:</span><span class="sxs-lookup"><span data-stu-id="db48b-125">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="db48b-126">Vytvořte požadavek REST pro načtení kolekce [Smluv](./agreement-resources.md) pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="db48b-126">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="db48b-127">Parametr dotazu **agreementType** použijte k nastavení rozsahu výsledků pouze na Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="db48b-127">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="db48b-128">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="db48b-128">Request syntax</span></span>

<span data-ttu-id="db48b-129">Použijte následující syntaxi požadavku:</span><span class="sxs-lookup"><span data-stu-id="db48b-129">Use the following request syntax:</span></span>

| <span data-ttu-id="db48b-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="db48b-130">Method</span></span> | <span data-ttu-id="db48b-131">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="db48b-131">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="db48b-132">GET</span><span class="sxs-lookup"><span data-stu-id="db48b-132">GET</span></span>    | <span data-ttu-id="db48b-133">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{id_tenanta_zákazníka}/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="db48b-133">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="db48b-134">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="db48b-134">URI parameters</span></span>

<span data-ttu-id="db48b-135">S požadavkem můžete použít následující parametry identifikátoru URI:</span><span class="sxs-lookup"><span data-stu-id="db48b-135">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="db48b-136">Název</span><span class="sxs-lookup"><span data-stu-id="db48b-136">Name</span></span>             | <span data-ttu-id="db48b-137">Typ</span><span class="sxs-lookup"><span data-stu-id="db48b-137">Type</span></span> | <span data-ttu-id="db48b-138">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="db48b-138">Required</span></span> | <span data-ttu-id="db48b-139">Popis</span><span class="sxs-lookup"><span data-stu-id="db48b-139">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="db48b-140">customer-tenant-id</span><span class="sxs-lookup"><span data-stu-id="db48b-140">customer-tenant-id</span></span> | <span data-ttu-id="db48b-141">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="db48b-141">GUID</span></span> | <span data-ttu-id="db48b-142">Yes</span><span class="sxs-lookup"><span data-stu-id="db48b-142">Yes</span></span> | <span data-ttu-id="db48b-143">Hodnota je identifikátor GUID naformátovaný **jako CustomerTenantId,** který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="db48b-143">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="db48b-144">agreement-type</span><span class="sxs-lookup"><span data-stu-id="db48b-144">agreement-type</span></span> | <span data-ttu-id="db48b-145">řetězec</span><span class="sxs-lookup"><span data-stu-id="db48b-145">string</span></span> | <span data-ttu-id="db48b-146">No</span><span class="sxs-lookup"><span data-stu-id="db48b-146">No</span></span> | <span data-ttu-id="db48b-147">Tento parametr vrátí všechna metadata smlouvy.</span><span class="sxs-lookup"><span data-stu-id="db48b-147">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="db48b-148">Tento parametr použijte k nastavení rozsahu odpovědi na dotaz na konkrétní typ smlouvy.</span><span class="sxs-lookup"><span data-stu-id="db48b-148">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="db48b-149">Podporované hodnoty jsou:</span><span class="sxs-lookup"><span data-stu-id="db48b-149">The supported values are:</span></span> <br/><br/> <span data-ttu-id="db48b-150">**MicrosoftCloudAgreement,** který obsahuje jenom metadata smlouvy typu *MicrosoftCloudAgreement*.</span><span class="sxs-lookup"><span data-stu-id="db48b-150">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="db48b-151">**MicrosoftCustomerAgreement,** který obsahuje jenom metadata smlouvy typu *MicrosoftCustomerAgreement*.</span><span class="sxs-lookup"><span data-stu-id="db48b-151">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="db48b-152">**\**– vrátí všechna metadata smlouvy. (Nepoužívejte _\* \* \*_ pokud váš kód nemá potřebnou logiku pro zpracování neočekávaných typů smlouvy.) <br/> <br/> _\* Poznámka:*\* Pokud není zadaný parametr URI, výchozí hodnota dotazu je **MicrosoftCloudAgreement** pro zpětnou kompatibilitu.</span><span class="sxs-lookup"><span data-stu-id="db48b-152">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary logic to handle unexpected agreement types.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="db48b-153">Microsoft může kdykoli zavést metadata smlouvy s novými typy smlouvy.</span><span class="sxs-lookup"><span data-stu-id="db48b-153">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="db48b-154">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="db48b-154">Request headers</span></span>

<span data-ttu-id="db48b-155">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="db48b-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="db48b-156">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="db48b-156">Request body</span></span>

<span data-ttu-id="db48b-157">Žádné</span><span class="sxs-lookup"><span data-stu-id="db48b-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="db48b-158">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="db48b-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="db48b-159">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="db48b-159">REST response</span></span>

<span data-ttu-id="db48b-160">V případě úspěchu vrátí tato  metoda v textu odpovědi kolekci prostředků smlouvy.</span><span class="sxs-lookup"><span data-stu-id="db48b-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="db48b-161">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="db48b-161">Response success and error codes</span></span>

<span data-ttu-id="db48b-162">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="db48b-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="db48b-163">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="db48b-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="db48b-164">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="db48b-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="db48b-165">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="db48b-165">Response example</span></span>

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
