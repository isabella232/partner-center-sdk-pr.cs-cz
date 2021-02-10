---
title: Potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Přečtěte si, jak potvrdit přijetí zákaznických smluv Microsoftu pomocí rozhraní API partnerského centra.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62a6cebd5d6d093377dd5940dcff6204b7095c70
ms.sourcegitcommit: ebb36208d6e2dea705f62b7d60d471f10c55132e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/09/2021
ms.locfileid: "100006062"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="0a463-103">Potvrzení souhlasu zákazníka se zákaznickou smlouvou Microsoftu pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="0a463-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="0a463-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="0a463-104">**Applies to:**</span></span>

- <span data-ttu-id="0a463-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0a463-105">Partner Center</span></span>

<span data-ttu-id="0a463-106">Partnerské centrum v současné době podporuje potvrzení souhlasu zákazníka s zákaznickou smlouvou Microsoftu pouze ve *veřejném cloudu Microsoftu*.</span><span class="sxs-lookup"><span data-stu-id="0a463-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="0a463-107">Tato funkce se v současnosti nevztahuje na:</span><span class="sxs-lookup"><span data-stu-id="0a463-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="0a463-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="0a463-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0a463-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="0a463-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0a463-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0a463-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0a463-111">Tento článek popisuje, jak ověřit nebo znovu potvrdit přijetí smlouvy o zákaznících Microsoftu v rámci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0a463-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a463-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0a463-112">Prerequisites</span></span>

- <span data-ttu-id="0a463-113">Pokud používáte sadu SDK partnerského centra .NET, verze 1,14 nebo novější je povinná.</span><span class="sxs-lookup"><span data-stu-id="0a463-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="0a463-114">Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0a463-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="0a463-115">*Tento scénář podporuje jenom ověřování aplikací a uživatelů.*</span><span class="sxs-lookup"><span data-stu-id="0a463-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="0a463-116">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0a463-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0a463-117">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0a463-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0a463-118">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="0a463-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0a463-119">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="0a463-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0a463-120">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="0a463-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0a463-121">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0a463-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0a463-122">Datum (**dateAgreed**), kdy zákazník přijal smlouvu o zákaznících Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0a463-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="0a463-123">Informace o uživateli od organizace zákazníka, která přijala zákaznickou smlouvu od Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0a463-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="0a463-124">Sem patří:</span><span class="sxs-lookup"><span data-stu-id="0a463-124">This includes:</span></span>
  - <span data-ttu-id="0a463-125">Jméno</span><span class="sxs-lookup"><span data-stu-id="0a463-125">First name</span></span>
  - <span data-ttu-id="0a463-126">Příjmení</span><span class="sxs-lookup"><span data-stu-id="0a463-126">Last name</span></span>
  - <span data-ttu-id="0a463-127">E-mailová adresa</span><span class="sxs-lookup"><span data-stu-id="0a463-127">Email address</span></span>
  - <span data-ttu-id="0a463-128">Telefonní číslo (volitelné)</span><span class="sxs-lookup"><span data-stu-id="0a463-128">Phone number (optional)</span></span>
- <span data-ttu-id="0a463-129">Pokud se u zákazníka změní následující hodnoty, Partnerské centrum umožní vytvoření jiné smlouvy pro daného zákazníka: křestní jméno příjmení jméno e-mailové adresy. v opačném případě získají partneři následující kód chyby, protože se vytvořil duplicitní zákazník.</span><span class="sxs-lookup"><span data-stu-id="0a463-129">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a><span data-ttu-id="0a463-130">.NET</span><span class="sxs-lookup"><span data-stu-id="0a463-130">.NET</span></span>

<span data-ttu-id="0a463-131">Potvrzení nebo opětovné potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky:</span><span class="sxs-lookup"><span data-stu-id="0a463-131">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="0a463-132">Načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0a463-132">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="0a463-133">Musíte získat **TemplateID** smlouvy o zákaznících Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0a463-133">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="0a463-134">Další podrobnosti najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="0a463-134">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="0a463-135">Vytvořte nový objekt **smlouvy** obsahující podrobnosti o potvrzení.</span><span class="sxs-lookup"><span data-stu-id="0a463-135">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="0a463-136">Použijte kolekci **IAgreggatePartner. Customers** a zavolejte metodu **ById** se zadaným **identifikátorem Customer-tenant-ID**.</span><span class="sxs-lookup"><span data-stu-id="0a463-136">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="0a463-137">Použijte vlastnost **smlouvy** a potom zavoláním metody **Create** nebo **CreateAsync**.</span><span class="sxs-lookup"><span data-stu-id="0a463-137">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

<span data-ttu-id="0a463-138">Kompletní ukázku najdete ve třídě [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="0a463-138">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="0a463-139">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0a463-139">REST request</span></span>

<span data-ttu-id="0a463-140">Potvrzení nebo opětovné potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky:</span><span class="sxs-lookup"><span data-stu-id="0a463-140">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="0a463-141">Načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0a463-141">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="0a463-142">Musíte získat **TemplateID** smlouvy o zákaznících Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0a463-142">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="0a463-143">Další podrobnosti najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="0a463-143">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="0a463-144">Vytvořte nový prostředek [ **smlouvy**](agreement-resources.md) , abyste si ověřili, že zákazník přijal zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0a463-144">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="0a463-145">Použijte následující [syntaxi žádosti REST](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="0a463-145">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0a463-146">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0a463-146">Request syntax</span></span>

| <span data-ttu-id="0a463-147">Metoda</span><span class="sxs-lookup"><span data-stu-id="0a463-147">Method</span></span> | <span data-ttu-id="0a463-148">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0a463-148">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a463-149">POST</span><span class="sxs-lookup"><span data-stu-id="0a463-149">POST</span></span>   | <span data-ttu-id="0a463-150">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0a463-150">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="0a463-151">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0a463-151">URI parameter</span></span>

<span data-ttu-id="0a463-152">Použijte následující parametr dotazu k určení zákazníka, kterého si potvrzujete.</span><span class="sxs-lookup"><span data-stu-id="0a463-152">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="0a463-153">Název</span><span class="sxs-lookup"><span data-stu-id="0a463-153">Name</span></span>               | <span data-ttu-id="0a463-154">Typ</span><span class="sxs-lookup"><span data-stu-id="0a463-154">Type</span></span> | <span data-ttu-id="0a463-155">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0a463-155">Required</span></span> | <span data-ttu-id="0a463-156">Popis</span><span class="sxs-lookup"><span data-stu-id="0a463-156">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a463-157">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="0a463-157">customer-tenant-id</span></span> | <span data-ttu-id="0a463-158">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="0a463-158">GUID</span></span> | <span data-ttu-id="0a463-159">Ano</span><span class="sxs-lookup"><span data-stu-id="0a463-159">Yes</span></span> | <span data-ttu-id="0a463-160">Hodnota je **číslo zákazníka**, který je ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0a463-160">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0a463-161">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0a463-161">Request headers</span></span>

<span data-ttu-id="0a463-162">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0a463-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0a463-163">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0a463-163">Request body</span></span>

<span data-ttu-id="0a463-164">Tato tabulka popisuje požadované vlastnosti v těle žádosti REST.</span><span class="sxs-lookup"><span data-stu-id="0a463-164">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="0a463-165">Název</span><span class="sxs-lookup"><span data-stu-id="0a463-165">Name</span></span>      | <span data-ttu-id="0a463-166">Typ</span><span class="sxs-lookup"><span data-stu-id="0a463-166">Type</span></span>   | <span data-ttu-id="0a463-167">Description</span><span class="sxs-lookup"><span data-stu-id="0a463-167">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a463-168">Smlouva</span><span class="sxs-lookup"><span data-stu-id="0a463-168">Agreement</span></span> | <span data-ttu-id="0a463-169">object</span><span class="sxs-lookup"><span data-stu-id="0a463-169">object</span></span> | <span data-ttu-id="0a463-170">Podrobnosti poskytované partnerem k potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky.</span><span class="sxs-lookup"><span data-stu-id="0a463-170">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="0a463-171">Smlouva</span><span class="sxs-lookup"><span data-stu-id="0a463-171">Agreement</span></span>

<span data-ttu-id="0a463-172">Tato tabulka popisuje minimální požadovaná pole pro vytvoření [prostředku **smlouvy**](agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0a463-172">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="0a463-173">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="0a463-173">Property</span></span>       | <span data-ttu-id="0a463-174">Typ</span><span class="sxs-lookup"><span data-stu-id="0a463-174">Type</span></span>   | <span data-ttu-id="0a463-175">Description</span><span class="sxs-lookup"><span data-stu-id="0a463-175">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="0a463-176">primaryContact</span><span class="sxs-lookup"><span data-stu-id="0a463-176">primaryContact</span></span> | [<span data-ttu-id="0a463-177">Kontakt</span><span class="sxs-lookup"><span data-stu-id="0a463-177">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="0a463-178">Informace o uživateli od organizace zákazníka, která přijala smlouvu o zákaznících Microsoftu, včetně:  **FirstName**, **LastName**, **e-mail** a **phoneNumber** (volitelné)</span><span class="sxs-lookup"><span data-stu-id="0a463-178">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="0a463-179">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="0a463-179">dateAgreed</span></span>     | <span data-ttu-id="0a463-180">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="0a463-180">string in UTC date time format</span></span> |<span data-ttu-id="0a463-181">Datum, kdy zákazník smlouvu přijal.</span><span class="sxs-lookup"><span data-stu-id="0a463-181">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="0a463-182">templateId</span><span class="sxs-lookup"><span data-stu-id="0a463-182">templateId</span></span>     | <span data-ttu-id="0a463-183">řetězec</span><span class="sxs-lookup"><span data-stu-id="0a463-183">string</span></span> | <span data-ttu-id="0a463-184">Jedinečný identifikátor typu smlouvy přijatého zákazníkem</span><span class="sxs-lookup"><span data-stu-id="0a463-184">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="0a463-185">**TemplateID** pro smlouvu o zákaznících Microsoftu můžete získat tak, že načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="0a463-185">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="0a463-186">Podrobnosti najdete v článku [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="0a463-186">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="0a463-187">typ</span><span class="sxs-lookup"><span data-stu-id="0a463-187">type</span></span>           | <span data-ttu-id="0a463-188">řetězec</span><span class="sxs-lookup"><span data-stu-id="0a463-188">string</span></span> | <span data-ttu-id="0a463-189">Typ smlouvy, kterou zákazník přijal.</span><span class="sxs-lookup"><span data-stu-id="0a463-189">Agreement type accepted by the customer.</span></span> <span data-ttu-id="0a463-190">Pokud zákazník přijal zákaznickou smlouvu Microsoftu, použijte "MicrosoftCustomerAgreement".</span><span class="sxs-lookup"><span data-stu-id="0a463-190">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="0a463-191">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0a463-191">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a><span data-ttu-id="0a463-192">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0a463-192">REST response</span></span>

<span data-ttu-id="0a463-193">V případě úspěchu vrátí tato metoda prostředek [ **smlouvy**](./agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0a463-193">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0a463-194">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0a463-194">Response success and error codes</span></span>

<span data-ttu-id="0a463-195">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0a463-195">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="0a463-196">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0a463-196">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0a463-197">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0a463-197">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="0a463-198">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0a463-198">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
