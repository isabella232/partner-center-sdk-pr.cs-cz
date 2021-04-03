---
title: Vytvoření zákazníka pro nepřímého prodejce
description: Zjistěte, jak může nepřímý poskytovatel použít rozhraní API partnerského centra k vytvoření zákazníka pro nepřímý prodejce.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 13cd1b051abb536d397dcd4000228f67fe3206b8
ms.sourcegitcommit: 204e518e794b6b076a17488ee9ca1aaaa4beaaec
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2021
ms.locfileid: "106103942"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="05edd-103">Vytvoření zákazníka pro nepřímý prodejce pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="05edd-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="05edd-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="05edd-104">**Applies to:**</span></span>

- <span data-ttu-id="05edd-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="05edd-105">Partner Center</span></span>

<span data-ttu-id="05edd-106">Nepřímý poskytovatel může vytvořit zákazníka pro nepřímý prodejce.</span><span class="sxs-lookup"><span data-stu-id="05edd-106">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05edd-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="05edd-107">Prerequisites</span></span>

- <span data-ttu-id="05edd-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="05edd-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="05edd-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="05edd-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="05edd-110">Identifikátor tenanta nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="05edd-110">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="05edd-111">Nepřímý prodejce musí mít partnerství s nepřímým zprostředkovatelem.</span><span class="sxs-lookup"><span data-stu-id="05edd-111">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="05edd-112">C\#</span><span class="sxs-lookup"><span data-stu-id="05edd-112">C\#</span></span>

<span data-ttu-id="05edd-113">Přidání nového zákazníka pro nepřímý prodejce:</span><span class="sxs-lookup"><span data-stu-id="05edd-113">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="05edd-114">Vytvořte instanci nového objektu [**zákazníka**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) a potom vytvořte instanci a naplňte [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="05edd-114">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="05edd-115">Nezapomeňte přiřadit ID nepřímého prodejce k vlastnosti [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) .</span><span class="sxs-lookup"><span data-stu-id="05edd-115">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="05edd-116">K získání rozhraní pro operace shromažďování zákazníka použijte vlastnost [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) .</span><span class="sxs-lookup"><span data-stu-id="05edd-116">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="05edd-117">Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) vytvořte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05edd-117">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="05edd-118">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="05edd-118">C\# example</span></span>

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

<span data-ttu-id="05edd-119">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="05edd-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="05edd-120">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateCustomerforIndirectReseller. cs</span><span class="sxs-lookup"><span data-stu-id="05edd-120">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="05edd-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="05edd-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="05edd-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="05edd-122">Request syntax</span></span>

| <span data-ttu-id="05edd-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="05edd-123">Method</span></span>   | <span data-ttu-id="05edd-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="05edd-124">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="05edd-125">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="05edd-125">**POST**</span></span> | <span data-ttu-id="05edd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="05edd-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="05edd-127">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="05edd-127">Request headers</span></span>

<span data-ttu-id="05edd-128">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="05edd-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="05edd-129">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="05edd-129">Request body</span></span>

<span data-ttu-id="05edd-130">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="05edd-130">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="05edd-131">Název</span><span class="sxs-lookup"><span data-stu-id="05edd-131">Name</span></span>                                          | <span data-ttu-id="05edd-132">Typ</span><span class="sxs-lookup"><span data-stu-id="05edd-132">Type</span></span>   | <span data-ttu-id="05edd-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="05edd-133">Required</span></span> | <span data-ttu-id="05edd-134">Popis</span><span class="sxs-lookup"><span data-stu-id="05edd-134">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="05edd-135">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="05edd-135">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="05edd-136">object</span><span class="sxs-lookup"><span data-stu-id="05edd-136">object</span></span> | <span data-ttu-id="05edd-137">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-137">Yes</span></span>      | <span data-ttu-id="05edd-138">Informace o fakturačním profilu zákazníka</span><span class="sxs-lookup"><span data-stu-id="05edd-138">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="05edd-139">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="05edd-139">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="05edd-140">object</span><span class="sxs-lookup"><span data-stu-id="05edd-140">object</span></span> | <span data-ttu-id="05edd-141">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-141">Yes</span></span>      | <span data-ttu-id="05edd-142">Informace o profilu společnosti zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05edd-142">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="05edd-143">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="05edd-143">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="05edd-144">řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-144">string</span></span> | <span data-ttu-id="05edd-145">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-145">Yes</span></span>      | <span data-ttu-id="05edd-146">ID nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="05edd-146">The indirect reseller ID.</span></span> <span data-ttu-id="05edd-147">Nepřímý prodejce, který je uveden zde, musí mít partnerství s nepřímým zprostředkovatelem nebo se požadavek nezdaří.</span><span class="sxs-lookup"><span data-stu-id="05edd-147">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="05edd-148">Všimněte si také, že pokud není zadána hodnota AssociatedPartnerId, zákazník je vytvořen jako přímý zákazník nepřímého poskytovatele, nikoli jako nepřímý prodejce.</span><span class="sxs-lookup"><span data-stu-id="05edd-148">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="05edd-149">Doména</span><span class="sxs-lookup"><span data-stu-id="05edd-149">Domain</span></span>| <span data-ttu-id="05edd-150">Řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-150">String</span></span>| <span data-ttu-id="05edd-151">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-151">Yes</span></span>|<span data-ttu-id="05edd-152">Název domény zákazníka, například contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="05edd-152">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="05edd-153">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="05edd-153">organizationRegistrationNumber</span></span>|    <span data-ttu-id="05edd-154">řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-154">string</span></span>|<span data-ttu-id="05edd-155">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-155">Yes</span></span>|     <span data-ttu-id="05edd-156">Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích).</span><span class="sxs-lookup"><span data-stu-id="05edd-156">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="05edd-157">Požadované jenom pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménská (AM), Ázerbájdžán (AZ), Bělorusko (BY), Maďarsko (HU), Kazachstán (KZ), Kyrgyzstán (KG), Moldavsko (MD), Rusko (RU), Tádžikistán (TJ), Uzbekistán (UZ), Ukrajina (UA), Indie, Brazílie, Jižní Afrika, Polsko, Spojené arabské emiráty, Saúdská Arábie, Turecko, Thajsko, Vietnam, Maďarsko, Jižní Súdán a Venezuela.</span><span class="sxs-lookup"><span data-stu-id="05edd-157">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan and Venezuela.</span></span> <span data-ttu-id="05edd-158">Pro společnost nebo organizaci zákazníka nacházející se v jiných zemích je to volitelné pole.</span><span class="sxs-lookup"><span data-stu-id="05edd-158">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="05edd-159">Fakturační profil</span><span class="sxs-lookup"><span data-stu-id="05edd-159">Billing profile</span></span>

<span data-ttu-id="05edd-160">Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) , který je potřeba k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05edd-160">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="05edd-161">Název</span><span class="sxs-lookup"><span data-stu-id="05edd-161">Name</span></span>             | <span data-ttu-id="05edd-162">Typ</span><span class="sxs-lookup"><span data-stu-id="05edd-162">Type</span></span>                                     | <span data-ttu-id="05edd-163">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="05edd-163">Required</span></span> | <span data-ttu-id="05edd-164">Popis</span><span class="sxs-lookup"><span data-stu-id="05edd-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="05edd-165">e-mail</span><span class="sxs-lookup"><span data-stu-id="05edd-165">email</span></span>            | <span data-ttu-id="05edd-166">řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-166">string</span></span>                                   | <span data-ttu-id="05edd-167">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-167">Yes</span></span>      | <span data-ttu-id="05edd-168">E-mailová adresa zákazníka</span><span class="sxs-lookup"><span data-stu-id="05edd-168">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="05edd-169">jazyková verze</span><span class="sxs-lookup"><span data-stu-id="05edd-169">culture</span></span>          | <span data-ttu-id="05edd-170">řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-170">string</span></span>                                   | <span data-ttu-id="05edd-171">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-171">Yes</span></span>      | <span data-ttu-id="05edd-172">Upřednostňovaná jazyková verze pro komunikaci a měnu, jako je "en-US".</span><span class="sxs-lookup"><span data-stu-id="05edd-172">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="05edd-173">Podporované jazykové verze najdete v tématu [podporované jazyky a národní prostředí partnerského centra](partner-center-supported-languages-and-locales.md) .</span><span class="sxs-lookup"><span data-stu-id="05edd-173">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="05edd-174">language</span><span class="sxs-lookup"><span data-stu-id="05edd-174">language</span></span>         | <span data-ttu-id="05edd-175">řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-175">string</span></span>                                   | <span data-ttu-id="05edd-176">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-176">Yes</span></span>      | <span data-ttu-id="05edd-177">Výchozí jazyk.</span><span class="sxs-lookup"><span data-stu-id="05edd-177">The default language.</span></span> <span data-ttu-id="05edd-178">Jsou podporovány dva znakové kódy jazyka (například `en` nebo `fr` ).</span><span class="sxs-lookup"><span data-stu-id="05edd-178">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="05edd-179">\_název společnosti</span><span class="sxs-lookup"><span data-stu-id="05edd-179">company\_name</span></span>    | <span data-ttu-id="05edd-180">řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-180">string</span></span>                                   | <span data-ttu-id="05edd-181">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-181">Yes</span></span>      | <span data-ttu-id="05edd-182">Registrovaný název společnosti nebo organizace.</span><span class="sxs-lookup"><span data-stu-id="05edd-182">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="05edd-183">výchozí \_ adresa</span><span class="sxs-lookup"><span data-stu-id="05edd-183">default\_address</span></span> | [<span data-ttu-id="05edd-184">Adresa</span><span class="sxs-lookup"><span data-stu-id="05edd-184">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="05edd-185">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-185">Yes</span></span>      | <span data-ttu-id="05edd-186">Registrovaná adresa společnosti nebo organizace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05edd-186">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="05edd-187">Informace o omezeních délky najdete v tématu [adresa](utility-resources.md#address) prostředku.</span><span class="sxs-lookup"><span data-stu-id="05edd-187">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="05edd-188">Profil společnosti</span><span class="sxs-lookup"><span data-stu-id="05edd-188">Company profile</span></span>

<span data-ttu-id="05edd-189">Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) , který je potřeba k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05edd-189">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="05edd-190">Název</span><span class="sxs-lookup"><span data-stu-id="05edd-190">Name</span></span>   | <span data-ttu-id="05edd-191">Typ</span><span class="sxs-lookup"><span data-stu-id="05edd-191">Type</span></span>   | <span data-ttu-id="05edd-192">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="05edd-192">Required</span></span> | <span data-ttu-id="05edd-193">Popis</span><span class="sxs-lookup"><span data-stu-id="05edd-193">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="05edd-194">doména</span><span class="sxs-lookup"><span data-stu-id="05edd-194">domain</span></span> | <span data-ttu-id="05edd-195">řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-195">string</span></span> | <span data-ttu-id="05edd-196">Yes</span><span class="sxs-lookup"><span data-stu-id="05edd-196">Yes</span></span>     | <span data-ttu-id="05edd-197">Název domény zákazníka, například contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="05edd-197">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="05edd-198">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="05edd-198">organizationRegistrationNumber</span></span> | <span data-ttu-id="05edd-199">řetězec</span><span class="sxs-lookup"><span data-stu-id="05edd-199">string</span></span> | <span data-ttu-id="05edd-200">Závisí na podmínce</span><span class="sxs-lookup"><span data-stu-id="05edd-200">Depends on condition</span></span> | <span data-ttu-id="05edd-201">Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích).</span><span class="sxs-lookup"><span data-stu-id="05edd-201">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="05edd-202">Toto pole se vyžaduje jenom v případě, že se společnost nebo organizace zákazníka nacházejí v následujících zemích:</span><span class="sxs-lookup"><span data-stu-id="05edd-202">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="05edd-203">– Arménská (AM)</span><span class="sxs-lookup"><span data-stu-id="05edd-203">- Armenia (AM)</span></span> <br/><span data-ttu-id="05edd-204">-Ázerbájdžán (AZ)</span><span class="sxs-lookup"><span data-stu-id="05edd-204">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="05edd-205">-Bělorusko (do)</span><span class="sxs-lookup"><span data-stu-id="05edd-205">- Belarus (BY)</span></span><br/><span data-ttu-id="05edd-206">-Maďarsko (HU)</span><span class="sxs-lookup"><span data-stu-id="05edd-206">- Hungary (HU)</span></span><br/><span data-ttu-id="05edd-207">-Kazachstán (KZ)</span><span class="sxs-lookup"><span data-stu-id="05edd-207">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="05edd-208">-Kyrgyzstán (KG)</span><span class="sxs-lookup"><span data-stu-id="05edd-208">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="05edd-209">-Moldávie (MD)</span><span class="sxs-lookup"><span data-stu-id="05edd-209">- Moldova (MD)</span></span><br/><span data-ttu-id="05edd-210">– Rusko (RU)</span><span class="sxs-lookup"><span data-stu-id="05edd-210">- Russia (RU)</span></span><br/><span data-ttu-id="05edd-211">-Tádžikistán (TJ)</span><span class="sxs-lookup"><span data-stu-id="05edd-211">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="05edd-212">-Uzbekistán (UZ)</span><span class="sxs-lookup"><span data-stu-id="05edd-212">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="05edd-213">– Ukrajina (UA)</span><span class="sxs-lookup"><span data-stu-id="05edd-213">- Ukraine (UA)</span></span><br/><br/><span data-ttu-id="05edd-214">Toto pole není vyžadováno, pokud se společnost nebo organizace zákazníka nacházejí v jiných zemích, než je zde zobrazená.</span><span class="sxs-lookup"><span data-stu-id="05edd-214">This field is not required if the customer’s company/organization is located in other countries beyond those shown here.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="05edd-215">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="05edd-215">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="05edd-216">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="05edd-216">REST response</span></span>

<span data-ttu-id="05edd-217">V případě úspěchu bude odpověď obsahovat [zákaznický](customer-resources.md#customer) prostředek pro nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05edd-217">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="05edd-218">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="05edd-218">Response success and error codes</span></span>

<span data-ttu-id="05edd-219">Odpovědi se dodávají se stavovým kódem HTTP, který označuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="05edd-219">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="05edd-220">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="05edd-220">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="05edd-221">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="05edd-221">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="05edd-222">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="05edd-222">Response example</span></span>

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