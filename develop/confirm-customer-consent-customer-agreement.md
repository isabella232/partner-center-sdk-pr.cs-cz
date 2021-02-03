---
title: Potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Přečtěte si, jak potvrdit přijetí zákaznických smluv Microsoftu pomocí rozhraní API partnerského centra.
ms.date: 02/04/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 239ca43c70fb8aa7f0d06e564e6c0726b235ffbe
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767109"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="697b7-103">Potvrzení souhlasu zákazníka se zákaznickou smlouvou Microsoftu pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="697b7-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="697b7-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="697b7-104">**Applies to:**</span></span>

- <span data-ttu-id="697b7-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="697b7-105">Partner Center</span></span>

<span data-ttu-id="697b7-106">Partnerské centrum v současné době podporuje potvrzení souhlasu zákazníka s zákaznickou smlouvou Microsoftu pouze ve *veřejném cloudu Microsoftu*.</span><span class="sxs-lookup"><span data-stu-id="697b7-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="697b7-107">Tato funkce se v současnosti nevztahuje na:</span><span class="sxs-lookup"><span data-stu-id="697b7-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="697b7-108">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="697b7-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="697b7-109">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="697b7-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="697b7-110">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="697b7-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="697b7-111">Tento článek popisuje, jak ověřit nebo znovu potvrdit přijetí smlouvy o zákaznících Microsoftu v rámci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="697b7-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="697b7-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="697b7-112">Prerequisites</span></span>

- <span data-ttu-id="697b7-113">Pokud používáte sadu SDK partnerského centra .NET, verze 1,14 nebo novější je povinná.</span><span class="sxs-lookup"><span data-stu-id="697b7-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="697b7-114">Přihlašovací údaje popsané v [partnerském centru ověřování](./partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="697b7-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="697b7-115">*Tento scénář podporuje jenom ověřování aplikací a uživatelů.*</span><span class="sxs-lookup"><span data-stu-id="697b7-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="697b7-116">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="697b7-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="697b7-117">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="697b7-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="697b7-118">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="697b7-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="697b7-119">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="697b7-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="697b7-120">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="697b7-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="697b7-121">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="697b7-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="697b7-122">Datum (**dateAgreed**), kdy zákazník přijal smlouvu o zákaznících Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="697b7-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="697b7-123">Informace o uživateli od organizace zákazníka, která přijala zákaznickou smlouvu od Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="697b7-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="697b7-124">Sem patří:</span><span class="sxs-lookup"><span data-stu-id="697b7-124">This includes:</span></span>
  - <span data-ttu-id="697b7-125">Jméno</span><span class="sxs-lookup"><span data-stu-id="697b7-125">First name</span></span>
  - <span data-ttu-id="697b7-126">Příjmení</span><span class="sxs-lookup"><span data-stu-id="697b7-126">Last name</span></span>
  - <span data-ttu-id="697b7-127">E-mailová adresa</span><span class="sxs-lookup"><span data-stu-id="697b7-127">Email address</span></span>
  - <span data-ttu-id="697b7-128">Telefonní číslo (volitelné)</span><span class="sxs-lookup"><span data-stu-id="697b7-128">Phone number (optional)</span></span>

## <a name="net"></a><span data-ttu-id="697b7-129">.NET</span><span class="sxs-lookup"><span data-stu-id="697b7-129">.NET</span></span>

<span data-ttu-id="697b7-130">Potvrzení nebo opětovné potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky:</span><span class="sxs-lookup"><span data-stu-id="697b7-130">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="697b7-131">Načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="697b7-131">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="697b7-132">Musíte získat **TemplateID** smlouvy o zákaznících Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="697b7-132">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="697b7-133">Další podrobnosti najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="697b7-133">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="697b7-134">Vytvořte nový objekt **smlouvy** obsahující podrobnosti o potvrzení.</span><span class="sxs-lookup"><span data-stu-id="697b7-134">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="697b7-135">Použijte kolekci **IAgreggatePartner. Customers** a zavolejte metodu **ById** se zadaným **identifikátorem Customer-tenant-ID**.</span><span class="sxs-lookup"><span data-stu-id="697b7-135">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="697b7-136">Použijte vlastnost **smlouvy** a potom zavoláním metody **Create** nebo **CreateAsync**.</span><span class="sxs-lookup"><span data-stu-id="697b7-136">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="697b7-137">Kompletní ukázku najdete ve třídě [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) z projektu [testovací aplikace konzoly](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .</span><span class="sxs-lookup"><span data-stu-id="697b7-137">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="697b7-138">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="697b7-138">REST request</span></span>

<span data-ttu-id="697b7-139">Potvrzení nebo opětovné potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky:</span><span class="sxs-lookup"><span data-stu-id="697b7-139">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="697b7-140">Načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="697b7-140">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="697b7-141">Musíte získat **TemplateID** smlouvy o zákaznících Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="697b7-141">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="697b7-142">Další podrobnosti najdete v tématu [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="697b7-142">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="697b7-143">Vytvořte nový prostředek [ **smlouvy**](agreement-resources.md) , abyste si ověřili, že zákazník přijal zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="697b7-143">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="697b7-144">Použijte následující [syntaxi žádosti REST](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="697b7-144">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="697b7-145">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="697b7-145">Request syntax</span></span>

| <span data-ttu-id="697b7-146">Metoda</span><span class="sxs-lookup"><span data-stu-id="697b7-146">Method</span></span> | <span data-ttu-id="697b7-147">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="697b7-147">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="697b7-148">POST</span><span class="sxs-lookup"><span data-stu-id="697b7-148">POST</span></span>   | <span data-ttu-id="697b7-149">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="697b7-149">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="697b7-150">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="697b7-150">URI parameter</span></span>

<span data-ttu-id="697b7-151">Použijte následující parametr dotazu k určení zákazníka, kterého si potvrzujete.</span><span class="sxs-lookup"><span data-stu-id="697b7-151">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="697b7-152">Název</span><span class="sxs-lookup"><span data-stu-id="697b7-152">Name</span></span>               | <span data-ttu-id="697b7-153">Typ</span><span class="sxs-lookup"><span data-stu-id="697b7-153">Type</span></span> | <span data-ttu-id="697b7-154">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="697b7-154">Required</span></span> | <span data-ttu-id="697b7-155">Popis</span><span class="sxs-lookup"><span data-stu-id="697b7-155">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="697b7-156">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="697b7-156">customer-tenant-id</span></span> | <span data-ttu-id="697b7-157">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="697b7-157">GUID</span></span> | <span data-ttu-id="697b7-158">Yes</span><span class="sxs-lookup"><span data-stu-id="697b7-158">Yes</span></span> | <span data-ttu-id="697b7-159">Hodnota je **číslo zákazníka**, který je ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="697b7-159">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="697b7-160">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="697b7-160">Request headers</span></span>

<span data-ttu-id="697b7-161">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="697b7-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="697b7-162">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="697b7-162">Request body</span></span>

<span data-ttu-id="697b7-163">Tato tabulka popisuje požadované vlastnosti v těle žádosti REST.</span><span class="sxs-lookup"><span data-stu-id="697b7-163">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="697b7-164">Název</span><span class="sxs-lookup"><span data-stu-id="697b7-164">Name</span></span>      | <span data-ttu-id="697b7-165">Typ</span><span class="sxs-lookup"><span data-stu-id="697b7-165">Type</span></span>   | <span data-ttu-id="697b7-166">Description</span><span class="sxs-lookup"><span data-stu-id="697b7-166">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="697b7-167">Smlouva</span><span class="sxs-lookup"><span data-stu-id="697b7-167">Agreement</span></span> | <span data-ttu-id="697b7-168">object</span><span class="sxs-lookup"><span data-stu-id="697b7-168">object</span></span> | <span data-ttu-id="697b7-169">Podrobnosti poskytované partnerem k potvrzení přijetí smlouvy o zákaznících Microsoftu pro zákazníky.</span><span class="sxs-lookup"><span data-stu-id="697b7-169">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="697b7-170">Smlouva</span><span class="sxs-lookup"><span data-stu-id="697b7-170">Agreement</span></span>

<span data-ttu-id="697b7-171">Tato tabulka popisuje minimální požadovaná pole pro vytvoření [prostředku **smlouvy**](agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="697b7-171">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="697b7-172">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="697b7-172">Property</span></span>       | <span data-ttu-id="697b7-173">Typ</span><span class="sxs-lookup"><span data-stu-id="697b7-173">Type</span></span>   | <span data-ttu-id="697b7-174">Description</span><span class="sxs-lookup"><span data-stu-id="697b7-174">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="697b7-175">primaryContact</span><span class="sxs-lookup"><span data-stu-id="697b7-175">primaryContact</span></span> | [<span data-ttu-id="697b7-176">Kontakt</span><span class="sxs-lookup"><span data-stu-id="697b7-176">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="697b7-177">Informace o uživateli od organizace zákazníka, která přijala smlouvu o zákaznících Microsoftu, včetně:  **FirstName**, **LastName**, **e-mail** a **phoneNumber** (volitelné)</span><span class="sxs-lookup"><span data-stu-id="697b7-177">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="697b7-178">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="697b7-178">dateAgreed</span></span>     | <span data-ttu-id="697b7-179">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="697b7-179">string in UTC date time format</span></span> |<span data-ttu-id="697b7-180">Datum, kdy zákazník smlouvu přijal.</span><span class="sxs-lookup"><span data-stu-id="697b7-180">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="697b7-181">templateId</span><span class="sxs-lookup"><span data-stu-id="697b7-181">templateId</span></span>     | <span data-ttu-id="697b7-182">řetězec</span><span class="sxs-lookup"><span data-stu-id="697b7-182">string</span></span> | <span data-ttu-id="697b7-183">Jedinečný identifikátor typu smlouvy přijatého zákazníkem</span><span class="sxs-lookup"><span data-stu-id="697b7-183">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="697b7-184">**TemplateID** pro smlouvu o zákaznících Microsoftu můžete získat tak, že načtěte metadata smlouvy pro zákaznickou smlouvu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="697b7-184">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="697b7-185">Podrobnosti najdete v článku [získání metadat smlouvy pro zákaznickou smlouvu Microsoftu](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="697b7-185">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="697b7-186">typ</span><span class="sxs-lookup"><span data-stu-id="697b7-186">type</span></span>           | <span data-ttu-id="697b7-187">řetězec</span><span class="sxs-lookup"><span data-stu-id="697b7-187">string</span></span> | <span data-ttu-id="697b7-188">Typ smlouvy, kterou zákazník přijal.</span><span class="sxs-lookup"><span data-stu-id="697b7-188">Agreement type accepted by the customer.</span></span> <span data-ttu-id="697b7-189">Pokud zákazník přijal zákaznickou smlouvu Microsoftu, použijte "MicrosoftCustomerAgreement".</span><span class="sxs-lookup"><span data-stu-id="697b7-189">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="697b7-190">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="697b7-190">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="697b7-191">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="697b7-191">REST response</span></span>

<span data-ttu-id="697b7-192">V případě úspěchu vrátí tato metoda prostředek [ **smlouvy**](./agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="697b7-192">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="697b7-193">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="697b7-193">Response success and error codes</span></span>

<span data-ttu-id="697b7-194">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="697b7-194">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="697b7-195">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="697b7-195">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="697b7-196">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="697b7-196">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="697b7-197">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="697b7-197">Response example</span></span>

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
