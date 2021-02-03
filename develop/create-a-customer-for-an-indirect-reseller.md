---
title: Vytvoření zákazníka pro nepřímého prodejce
description: Zjistěte, jak může nepřímý poskytovatel použít rozhraní API partnerského centra k vytvoření zákazníka pro nepřímý prodejce.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e2386f1963a5bb3ea4269bcbf4327c75987f3b91
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767140"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="a538b-103">Vytvoření zákazníka pro nepřímý prodejce pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="a538b-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="a538b-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="a538b-104">**Applies to:**</span></span>

- <span data-ttu-id="a538b-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="a538b-105">Partner Center</span></span>

<span data-ttu-id="a538b-106">Nepřímý poskytovatel může vytvořit zákazníka pro nepřímý prodejce.</span><span class="sxs-lookup"><span data-stu-id="a538b-106">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a538b-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a538b-107">Prerequisites</span></span>

- <span data-ttu-id="a538b-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a538b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a538b-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="a538b-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="a538b-110">Identifikátor tenanta nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="a538b-110">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="a538b-111">Nepřímý prodejce musí mít partnerství s nepřímým zprostředkovatelem.</span><span class="sxs-lookup"><span data-stu-id="a538b-111">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="a538b-112">C\#</span><span class="sxs-lookup"><span data-stu-id="a538b-112">C\#</span></span>

<span data-ttu-id="a538b-113">Přidání nového zákazníka pro nepřímý prodejce:</span><span class="sxs-lookup"><span data-stu-id="a538b-113">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="a538b-114">Vytvořte instanci nového objektu [**zákazníka**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) a potom vytvořte instanci a naplňte [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="a538b-114">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="a538b-115">Nezapomeňte přiřadit ID nepřímého prodejce k vlastnosti [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) .</span><span class="sxs-lookup"><span data-stu-id="a538b-115">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="a538b-116">K získání rozhraní pro operace shromažďování zákazníka použijte vlastnost [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) .</span><span class="sxs-lookup"><span data-stu-id="a538b-116">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="a538b-117">Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) vytvořte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a538b-117">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="a538b-118">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="a538b-118">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

<span data-ttu-id="a538b-119">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a538b-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a538b-120">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateCustomerforIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="a538b-120">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a538b-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="a538b-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a538b-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="a538b-122">Request syntax</span></span>

| <span data-ttu-id="a538b-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="a538b-123">Method</span></span>   | <span data-ttu-id="a538b-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a538b-124">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="a538b-125">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="a538b-125">**POST**</span></span> | <span data-ttu-id="a538b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a538b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a538b-127">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a538b-127">Request headers</span></span>

<span data-ttu-id="a538b-128">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a538b-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a538b-129">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a538b-129">Request body</span></span>

<span data-ttu-id="a538b-130">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="a538b-130">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="a538b-131">Název</span><span class="sxs-lookup"><span data-stu-id="a538b-131">Name</span></span>                                          | <span data-ttu-id="a538b-132">Typ</span><span class="sxs-lookup"><span data-stu-id="a538b-132">Type</span></span>   | <span data-ttu-id="a538b-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a538b-133">Required</span></span> | <span data-ttu-id="a538b-134">Popis</span><span class="sxs-lookup"><span data-stu-id="a538b-134">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="a538b-135">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="a538b-135">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="a538b-136">object</span><span class="sxs-lookup"><span data-stu-id="a538b-136">object</span></span> | <span data-ttu-id="a538b-137">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-137">Yes</span></span>      | <span data-ttu-id="a538b-138">Informace o fakturačním profilu zákazníka</span><span class="sxs-lookup"><span data-stu-id="a538b-138">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="a538b-139">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="a538b-139">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="a538b-140">object</span><span class="sxs-lookup"><span data-stu-id="a538b-140">object</span></span> | <span data-ttu-id="a538b-141">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-141">Yes</span></span>      | <span data-ttu-id="a538b-142">Informace o profilu společnosti zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a538b-142">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="a538b-143">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="a538b-143">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="a538b-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-144">string</span></span> | <span data-ttu-id="a538b-145">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-145">Yes</span></span>      | <span data-ttu-id="a538b-146">ID nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="a538b-146">The indirect reseller ID.</span></span> <span data-ttu-id="a538b-147">Nepřímý prodejce, který je uveden zde, musí mít partnerství s nepřímým zprostředkovatelem nebo se požadavek nezdaří.</span><span class="sxs-lookup"><span data-stu-id="a538b-147">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="a538b-148">Všimněte si také, že pokud není zadána hodnota AssociatedPartnerId, zákazník je vytvořen jako přímý zákazník nepřímého poskytovatele, nikoli jako nepřímý prodejce.</span><span class="sxs-lookup"><span data-stu-id="a538b-148">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="a538b-149">Doména</span><span class="sxs-lookup"><span data-stu-id="a538b-149">Domain</span></span>| <span data-ttu-id="a538b-150">Řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-150">String</span></span>| <span data-ttu-id="a538b-151">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-151">Yes</span></span>|<span data-ttu-id="a538b-152">Název domény zákazníka, například contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="a538b-152">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="a538b-153">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="a538b-153">organizationRegistrationNumber</span></span>|    <span data-ttu-id="a538b-154">řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-154">string</span></span>|<span data-ttu-id="a538b-155">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-155">Yes</span></span>|     <span data-ttu-id="a538b-156">Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích).</span><span class="sxs-lookup"><span data-stu-id="a538b-156">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="a538b-157">Požadované jenom pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích.</span><span class="sxs-lookup"><span data-stu-id="a538b-157">Only required for customer’s company/organization located in the following countries.</span></span> <span data-ttu-id="a538b-158">Arménie (AM), Ázerbájdžán (AZ), Bělorusko (BY), Maďarsko (HU), Kazachstán (KZ), Kyrgyzstán (KG), Moldavsko (MD), Rusko (RU), Tádžikistán (TJ), Uzbekistán (UZ), Ukrajina (UA).</span><span class="sxs-lookup"><span data-stu-id="a538b-158">Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA).</span></span> <span data-ttu-id="a538b-159">Pro společnost nebo organizaci zákazníka nacházející se v jiných zemích by neměl být určen.</span><span class="sxs-lookup"><span data-stu-id="a538b-159">For customer’s company/organization located in other countries this should not be specified.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="a538b-160">Fakturační profil</span><span class="sxs-lookup"><span data-stu-id="a538b-160">Billing profile</span></span>

<span data-ttu-id="a538b-161">Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) , který je potřeba k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a538b-161">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="a538b-162">Název</span><span class="sxs-lookup"><span data-stu-id="a538b-162">Name</span></span>             | <span data-ttu-id="a538b-163">Typ</span><span class="sxs-lookup"><span data-stu-id="a538b-163">Type</span></span>                                     | <span data-ttu-id="a538b-164">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a538b-164">Required</span></span> | <span data-ttu-id="a538b-165">Popis</span><span class="sxs-lookup"><span data-stu-id="a538b-165">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a538b-166">e-mail</span><span class="sxs-lookup"><span data-stu-id="a538b-166">email</span></span>            | <span data-ttu-id="a538b-167">řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-167">string</span></span>                                   | <span data-ttu-id="a538b-168">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-168">Yes</span></span>      | <span data-ttu-id="a538b-169">E-mailová adresa zákazníka</span><span class="sxs-lookup"><span data-stu-id="a538b-169">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="a538b-170">jazyková verze</span><span class="sxs-lookup"><span data-stu-id="a538b-170">culture</span></span>          | <span data-ttu-id="a538b-171">řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-171">string</span></span>                                   | <span data-ttu-id="a538b-172">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-172">Yes</span></span>      | <span data-ttu-id="a538b-173">Upřednostňovaná jazyková verze pro komunikaci a měnu, jako je "en-US".</span><span class="sxs-lookup"><span data-stu-id="a538b-173">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="a538b-174">Podporované jazykové verze najdete v tématu [podporované jazyky a národní prostředí partnerského centra](partner-center-supported-languages-and-locales.md) .</span><span class="sxs-lookup"><span data-stu-id="a538b-174">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="a538b-175">language</span><span class="sxs-lookup"><span data-stu-id="a538b-175">language</span></span>         | <span data-ttu-id="a538b-176">řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-176">string</span></span>                                   | <span data-ttu-id="a538b-177">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-177">Yes</span></span>      | <span data-ttu-id="a538b-178">Výchozí jazyk.</span><span class="sxs-lookup"><span data-stu-id="a538b-178">The default language.</span></span> <span data-ttu-id="a538b-179">Jsou podporovány dva znakové kódy jazyka (například `en` nebo `fr` ).</span><span class="sxs-lookup"><span data-stu-id="a538b-179">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="a538b-180">\_název společnosti</span><span class="sxs-lookup"><span data-stu-id="a538b-180">company\_name</span></span>    | <span data-ttu-id="a538b-181">řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-181">string</span></span>                                   | <span data-ttu-id="a538b-182">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-182">Yes</span></span>      | <span data-ttu-id="a538b-183">Registrovaný název společnosti nebo organizace.</span><span class="sxs-lookup"><span data-stu-id="a538b-183">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="a538b-184">výchozí \_ adresa</span><span class="sxs-lookup"><span data-stu-id="a538b-184">default\_address</span></span> | [<span data-ttu-id="a538b-185">Adresa</span><span class="sxs-lookup"><span data-stu-id="a538b-185">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="a538b-186">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-186">Yes</span></span>      | <span data-ttu-id="a538b-187">Registrovaná adresa společnosti nebo organizace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a538b-187">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="a538b-188">Informace o omezeních délky najdete v tématu [adresa](utility-resources.md#address) prostředku.</span><span class="sxs-lookup"><span data-stu-id="a538b-188">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="a538b-189">Profil společnosti</span><span class="sxs-lookup"><span data-stu-id="a538b-189">Company profile</span></span>

<span data-ttu-id="a538b-190">Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) , který je potřeba k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a538b-190">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="a538b-191">Název</span><span class="sxs-lookup"><span data-stu-id="a538b-191">Name</span></span>   | <span data-ttu-id="a538b-192">Typ</span><span class="sxs-lookup"><span data-stu-id="a538b-192">Type</span></span>   | <span data-ttu-id="a538b-193">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a538b-193">Required</span></span> | <span data-ttu-id="a538b-194">Popis</span><span class="sxs-lookup"><span data-stu-id="a538b-194">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="a538b-195">doména</span><span class="sxs-lookup"><span data-stu-id="a538b-195">domain</span></span> | <span data-ttu-id="a538b-196">řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-196">string</span></span> | <span data-ttu-id="a538b-197">Yes</span><span class="sxs-lookup"><span data-stu-id="a538b-197">Yes</span></span>     | <span data-ttu-id="a538b-198">Název domény zákazníka, například contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="a538b-198">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="a538b-199">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="a538b-199">organizationRegistrationNumber</span></span> | <span data-ttu-id="a538b-200">řetězec</span><span class="sxs-lookup"><span data-stu-id="a538b-200">string</span></span> | <span data-ttu-id="a538b-201">Závisí na podmínce</span><span class="sxs-lookup"><span data-stu-id="a538b-201">Depends on condition</span></span> | <span data-ttu-id="a538b-202">Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích).</span><span class="sxs-lookup"><span data-stu-id="a538b-202">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="a538b-203">Toto pole se vyžaduje jenom v případě, že se společnost nebo organizace zákazníka nacházejí v následujících zemích:</span><span class="sxs-lookup"><span data-stu-id="a538b-203">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="a538b-204">– Arménská (AM)</span><span class="sxs-lookup"><span data-stu-id="a538b-204">- Armenia (AM)</span></span> <br/><span data-ttu-id="a538b-205">-Ázerbájdžán (AZ)</span><span class="sxs-lookup"><span data-stu-id="a538b-205">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="a538b-206">-Bělorusko (do)</span><span class="sxs-lookup"><span data-stu-id="a538b-206">- Belarus (BY)</span></span><br/><span data-ttu-id="a538b-207">-Maďarsko (HU)</span><span class="sxs-lookup"><span data-stu-id="a538b-207">- Hungary (HU)</span></span><br/><span data-ttu-id="a538b-208">-Kazachstán (KZ)</span><span class="sxs-lookup"><span data-stu-id="a538b-208">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="a538b-209">-Kyrgyzstán (KG)</span><span class="sxs-lookup"><span data-stu-id="a538b-209">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="a538b-210">-Moldávie (MD)</span><span class="sxs-lookup"><span data-stu-id="a538b-210">- Moldova (MD)</span></span><br/><span data-ttu-id="a538b-211">– Rusko (RU)</span><span class="sxs-lookup"><span data-stu-id="a538b-211">- Russia (RU)</span></span><br/><span data-ttu-id="a538b-212">-Tádžikistán (TJ)</span><span class="sxs-lookup"><span data-stu-id="a538b-212">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="a538b-213">-Uzbekistán (UZ)</span><span class="sxs-lookup"><span data-stu-id="a538b-213">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="a538b-214">– Ukrajina (UA)</span><span class="sxs-lookup"><span data-stu-id="a538b-214">- Ukraine (UA)</span></span><br/><br/><span data-ttu-id="a538b-215">Toto pole není vyžadováno, pokud se společnost nebo organizace zákazníka nacházejí v jiných zemích, než je zde zobrazená.</span><span class="sxs-lookup"><span data-stu-id="a538b-215">This field is not required if the customer’s company/organization is located in other countries beyond those shown here.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="a538b-216">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a538b-216">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="a538b-217">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a538b-217">REST response</span></span>

<span data-ttu-id="a538b-218">V případě úspěchu bude odpověď obsahovat [zákaznický](customer-resources.md#customer) prostředek pro nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a538b-218">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a538b-219">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="a538b-219">Response success and error codes</span></span>

<span data-ttu-id="a538b-220">Odpovědi se dodávají se stavovým kódem HTTP, který označuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a538b-220">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a538b-221">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="a538b-221">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a538b-222">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a538b-222">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a538b-223">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a538b-223">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```