---
title: Potvrzení přijetí Smlouvy se zákazníkem Microsoftu ze strany zákazníka
description: Zjistěte, jak potvrdit přijetí služby zákazníkem Smlouva se zákazníkem Microsoftu pomocí Partnerské centrum API.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 002508109191ede53cd06f25efc38286647fd67c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974008"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="8cf7a-103">Potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu pomocí Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="8cf7a-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="8cf7a-104">**Platí pro:** Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="8cf7a-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="8cf7a-105">**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8cf7a-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8cf7a-106">Partnerské centrum v současné době podporuje potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu pouze ve veřejném cloudu Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the Microsoft public cloud.</span></span>

<span data-ttu-id="8cf7a-107">Tento článek popisuje, jak potvrdit nebo znovu potvrdit souhlas zákazníka s Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-107">This article describes how to confirm or reconfirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cf7a-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8cf7a-108">Prerequisites</span></span>

- <span data-ttu-id="8cf7a-109">Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.14 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="8cf7a-110">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8cf7a-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="8cf7a-111">*Tento scénář podporuje pouze ověřování aplikací a uživatelů.*</span><span class="sxs-lookup"><span data-stu-id="8cf7a-111">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="8cf7a-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8cf7a-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8cf7a-113">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8cf7a-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8cf7a-114">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="8cf7a-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8cf7a-115">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="8cf7a-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8cf7a-116">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8cf7a-117">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8cf7a-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8cf7a-118">Datum **(dateAgreed),** kdy zákazník přijal Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-118">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="8cf7a-119">Informace o uživateli z organizace zákazníka, který přijal Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-119">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="8cf7a-120">Sem patří:</span><span class="sxs-lookup"><span data-stu-id="8cf7a-120">This includes:</span></span>
  - <span data-ttu-id="8cf7a-121">Jméno</span><span class="sxs-lookup"><span data-stu-id="8cf7a-121">First name</span></span>
  - <span data-ttu-id="8cf7a-122">Příjmení</span><span class="sxs-lookup"><span data-stu-id="8cf7a-122">Last name</span></span>
  - <span data-ttu-id="8cf7a-123">E-mailová adresa</span><span class="sxs-lookup"><span data-stu-id="8cf7a-123">Email address</span></span>
  - <span data-ttu-id="8cf7a-124">Telefon číslo (volitelné)</span><span class="sxs-lookup"><span data-stu-id="8cf7a-124">Phone number (optional)</span></span>
- <span data-ttu-id="8cf7a-125">Pokud se pro zákazníka změní následující hodnoty, umožní Partnerské centrum vytvořit pro tohoto zákazníka jinou smlouvu: Jméno Příjmení E-mailová adresa Telefon číslo V opačném případě partneři obdrží následující kód chyby kvůli vytvoření duplicitního zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-125">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


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

## <a name="net"></a><span data-ttu-id="8cf7a-126">.NET</span><span class="sxs-lookup"><span data-stu-id="8cf7a-126">.NET</span></span>

<span data-ttu-id="8cf7a-127">Potvrzení nebo potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu:</span><span class="sxs-lookup"><span data-stu-id="8cf7a-127">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="8cf7a-128">Načtěte metadata smlouvy pro Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-128">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="8cf7a-129">Je nutné získat **templateId** Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-129">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="8cf7a-130">Další informace najdete v tématu [Získání metadat smlouvy pro Smlouva se zákazníkem Microsoftu](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="8cf7a-130">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="8cf7a-131">Vytvořte nový objekt **Agreement** obsahující podrobnosti o potvrzení.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-131">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="8cf7a-132">Použijte kolekci **IAgreggatePartner.Customers** a zavolejte metodu **ById** se zadaným **ID tenanta zákazníka**.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-132">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="8cf7a-133">Použijte vlastnost **Agreements** a pak zavoláte **Create** nebo **CreateAsync.**</span><span class="sxs-lookup"><span data-stu-id="8cf7a-133">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="8cf7a-134">Úplnou ukázku najdete ve třídě [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) z projektu [konzolové testovací](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) aplikace.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-134">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="8cf7a-135">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="8cf7a-135">REST request</span></span>

<span data-ttu-id="8cf7a-136">Potvrzení nebo potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu:</span><span class="sxs-lookup"><span data-stu-id="8cf7a-136">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="8cf7a-137">Načtěte metadata smlouvy pro Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-137">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="8cf7a-138">Je nutné získat **templateId** Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-138">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="8cf7a-139">Další informace najdete v tématu [Získání metadat smlouvy pro Smlouva se zákazníkem Microsoftu](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="8cf7a-139">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="8cf7a-140">Vytvořte nový prostředek [ **smlouvy,** abyste](agreement-resources.md) potvrdili, že zákazník přijal Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-140">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="8cf7a-141">Použijte následující [syntaxi požadavku REST.](#request-syntax)</span><span class="sxs-lookup"><span data-stu-id="8cf7a-141">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8cf7a-142">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="8cf7a-142">Request syntax</span></span>

| <span data-ttu-id="8cf7a-143">Metoda</span><span class="sxs-lookup"><span data-stu-id="8cf7a-143">Method</span></span> | <span data-ttu-id="8cf7a-144">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8cf7a-144">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8cf7a-145">POST</span><span class="sxs-lookup"><span data-stu-id="8cf7a-145">POST</span></span>   | <span data-ttu-id="8cf7a-146">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/smlouvy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8cf7a-146">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="8cf7a-147">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8cf7a-147">URI parameter</span></span>

<span data-ttu-id="8cf7a-148">Pomocí následujícího parametru dotazu zadejte zákazníka, který potvrzujete.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-148">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="8cf7a-149">Název</span><span class="sxs-lookup"><span data-stu-id="8cf7a-149">Name</span></span>               | <span data-ttu-id="8cf7a-150">Typ</span><span class="sxs-lookup"><span data-stu-id="8cf7a-150">Type</span></span> | <span data-ttu-id="8cf7a-151">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8cf7a-151">Required</span></span> | <span data-ttu-id="8cf7a-152">Popis</span><span class="sxs-lookup"><span data-stu-id="8cf7a-152">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="8cf7a-153">customer-tenant-id</span><span class="sxs-lookup"><span data-stu-id="8cf7a-153">customer-tenant-id</span></span> | <span data-ttu-id="8cf7a-154">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="8cf7a-154">GUID</span></span> | <span data-ttu-id="8cf7a-155">Yes</span><span class="sxs-lookup"><span data-stu-id="8cf7a-155">Yes</span></span> | <span data-ttu-id="8cf7a-156">Hodnota je id tenanta zákazníka ve **formátu** GUID, což je identifikátor, který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-156">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8cf7a-157">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8cf7a-157">Request headers</span></span>

<span data-ttu-id="8cf7a-158">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8cf7a-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8cf7a-159">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8cf7a-159">Request body</span></span>

<span data-ttu-id="8cf7a-160">Tato tabulka popisuje požadované vlastnosti v textu požadavku REST.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-160">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="8cf7a-161">Název</span><span class="sxs-lookup"><span data-stu-id="8cf7a-161">Name</span></span>      | <span data-ttu-id="8cf7a-162">Typ</span><span class="sxs-lookup"><span data-stu-id="8cf7a-162">Type</span></span>   | <span data-ttu-id="8cf7a-163">Description</span><span class="sxs-lookup"><span data-stu-id="8cf7a-163">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="8cf7a-164">Smlouva</span><span class="sxs-lookup"><span data-stu-id="8cf7a-164">Agreement</span></span> | <span data-ttu-id="8cf7a-165">object</span><span class="sxs-lookup"><span data-stu-id="8cf7a-165">object</span></span> | <span data-ttu-id="8cf7a-166">Podrobnosti poskytnuté partnerem pro potvrzení souhlasu zákazníka s Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-166">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="8cf7a-167">Smlouva</span><span class="sxs-lookup"><span data-stu-id="8cf7a-167">Agreement</span></span>

<span data-ttu-id="8cf7a-168">Tato tabulka popisuje minimální požadovaná pole pro vytvoření [ **prostředku** smlouvy.](agreement-resources.md)</span><span class="sxs-lookup"><span data-stu-id="8cf7a-168">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="8cf7a-169">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="8cf7a-169">Property</span></span>       | <span data-ttu-id="8cf7a-170">Typ</span><span class="sxs-lookup"><span data-stu-id="8cf7a-170">Type</span></span>   | <span data-ttu-id="8cf7a-171">Description</span><span class="sxs-lookup"><span data-stu-id="8cf7a-171">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="8cf7a-172">primaryContact</span><span class="sxs-lookup"><span data-stu-id="8cf7a-172">primaryContact</span></span> | [<span data-ttu-id="8cf7a-173">Kontakt</span><span class="sxs-lookup"><span data-stu-id="8cf7a-173">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="8cf7a-174">Informace o uživateli z organizace zákazníka, který přijal Smlouva se zákazníkem Microsoftu, včetně:  **jméno,** **příjmení,** **e-mail** a **telefonní číslo** (volitelné)</span><span class="sxs-lookup"><span data-stu-id="8cf7a-174">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="8cf7a-175">datum odgreed</span><span class="sxs-lookup"><span data-stu-id="8cf7a-175">dateAgreed</span></span>     | <span data-ttu-id="8cf7a-176">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="8cf7a-176">string in UTC date time format</span></span> |<span data-ttu-id="8cf7a-177">Datum, kdy zákazník smlouvu přijal.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-177">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="8cf7a-178">ID šablony</span><span class="sxs-lookup"><span data-stu-id="8cf7a-178">templateId</span></span>     | <span data-ttu-id="8cf7a-179">řetězec</span><span class="sxs-lookup"><span data-stu-id="8cf7a-179">string</span></span> | <span data-ttu-id="8cf7a-180">Jedinečný identifikátor typu smlouvy přijatého zákazníkem</span><span class="sxs-lookup"><span data-stu-id="8cf7a-180">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="8cf7a-181">Můžete získat **templateId pro** Smlouva se zákazníkem Microsoftu načtením metadat smlouvy pro Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-181">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="8cf7a-182">Podrobnosti [najdete v tématu Smlouva se zákazníkem Microsoftu](./get-customer-agreement-metadata.md) smlouvy.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-182">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="8cf7a-183">typ</span><span class="sxs-lookup"><span data-stu-id="8cf7a-183">type</span></span>           | <span data-ttu-id="8cf7a-184">řetězec</span><span class="sxs-lookup"><span data-stu-id="8cf7a-184">string</span></span> | <span data-ttu-id="8cf7a-185">Typ smlouvy přijatý zákazníkem.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-185">Agreement type accepted by the customer.</span></span> <span data-ttu-id="8cf7a-186">Pokud zákazník přijal Smlouva se zákazníkem Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-186">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="8cf7a-187">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8cf7a-187">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8cf7a-188">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8cf7a-188">REST response</span></span>

<span data-ttu-id="8cf7a-189">V případě úspěchu vrátí tato metoda [ **prostředek smlouvy**](./agreement-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8cf7a-189">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8cf7a-190">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="8cf7a-190">Response success and error codes</span></span>

<span data-ttu-id="8cf7a-191">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-191">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="8cf7a-192">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="8cf7a-192">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8cf7a-193">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8cf7a-193">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="8cf7a-194">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8cf7a-194">Response example</span></span>

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
