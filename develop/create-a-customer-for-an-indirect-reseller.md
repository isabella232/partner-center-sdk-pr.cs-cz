---
title: Vytvoření zákazníka pro nepřímého prodejce
description: Zjistěte, jak může nepřímý poskytovatel Partnerské centrum rozhraní API k vytvoření zákazníka pro nepřímého prodejce.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9a6218aeb61f3775c89d34b4d57a17741e3a1e93
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973736"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="af222-103">Vytvoření zákazníka pro nepřímého prodejce pomocí Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="af222-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="af222-104">Nepřímý poskytovatel může vytvořit zákazníka pro nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="af222-104">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af222-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="af222-105">Prerequisites</span></span>

- <span data-ttu-id="af222-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="af222-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="af222-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="af222-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="af222-108">Identifikátor tenanta nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="af222-108">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="af222-109">Nepřímý prodejce musí mít partnerství s nepřímým poskytovatelem.</span><span class="sxs-lookup"><span data-stu-id="af222-109">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="af222-110">C\#</span><span class="sxs-lookup"><span data-stu-id="af222-110">C\#</span></span>

<span data-ttu-id="af222-111">Přidání nového zákazníka pro nepřímého prodejce:</span><span class="sxs-lookup"><span data-stu-id="af222-111">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="af222-112">Vytvořte instanci nového [**objektu Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) a pak vytvořte instanci a naplňte profily [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)</span><span class="sxs-lookup"><span data-stu-id="af222-112">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="af222-113">Nezapomeňte přiřadit ID nepřímého prodejce k vlastnosti [**AssociatedPartnerID.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)</span><span class="sxs-lookup"><span data-stu-id="af222-113">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="af222-114">Pomocí vlastnosti [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) získejte rozhraní pro operace shromažďování zákazníků.</span><span class="sxs-lookup"><span data-stu-id="af222-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="af222-115">Pokud chcete [**vytvořit zákazníka,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) zavolejte metodu Create nebo [**CreateAsync.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)</span><span class="sxs-lookup"><span data-stu-id="af222-115">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="af222-116">Příklad \# jazyka C</span><span class="sxs-lookup"><span data-stu-id="af222-116">C\# example</span></span>

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

<span data-ttu-id="af222-117">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="af222-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="af222-118">**Project:** SDK pro Partnerské centrum Samples **Class:** CreateCustomerforIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="af222-118">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="af222-119">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="af222-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="af222-120">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="af222-120">Request syntax</span></span>

| <span data-ttu-id="af222-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="af222-121">Method</span></span>   | <span data-ttu-id="af222-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="af222-122">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="af222-123">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="af222-123">**POST**</span></span> | <span data-ttu-id="af222-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="af222-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="af222-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="af222-125">Request headers</span></span>

<span data-ttu-id="af222-126">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="af222-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="af222-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="af222-127">Request body</span></span>

<span data-ttu-id="af222-128">Tato tabulka popisuje požadované vlastnosti v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="af222-128">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="af222-129">Název</span><span class="sxs-lookup"><span data-stu-id="af222-129">Name</span></span>                                          | <span data-ttu-id="af222-130">Typ</span><span class="sxs-lookup"><span data-stu-id="af222-130">Type</span></span>   | <span data-ttu-id="af222-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="af222-131">Required</span></span> | <span data-ttu-id="af222-132">Popis</span><span class="sxs-lookup"><span data-stu-id="af222-132">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="af222-133">Profil fakturace</span><span class="sxs-lookup"><span data-stu-id="af222-133">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="af222-134">object</span><span class="sxs-lookup"><span data-stu-id="af222-134">object</span></span> | <span data-ttu-id="af222-135">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-135">Yes</span></span>      | <span data-ttu-id="af222-136">Informace o fakturačním profilu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="af222-136">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="af222-137">Profil společnosti</span><span class="sxs-lookup"><span data-stu-id="af222-137">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="af222-138">object</span><span class="sxs-lookup"><span data-stu-id="af222-138">object</span></span> | <span data-ttu-id="af222-139">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-139">Yes</span></span>      | <span data-ttu-id="af222-140">Informace o profilu společnosti zákazníka.</span><span class="sxs-lookup"><span data-stu-id="af222-140">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="af222-141">AssociatedPartnerId (ID přidruženéhopartneru)</span><span class="sxs-lookup"><span data-stu-id="af222-141">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="af222-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-142">string</span></span> | <span data-ttu-id="af222-143">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-143">Yes</span></span>      | <span data-ttu-id="af222-144">ID nepřímého prodejce.</span><span class="sxs-lookup"><span data-stu-id="af222-144">The indirect reseller ID.</span></span> <span data-ttu-id="af222-145">Nepřímý prodejce uvedený zde uvedeným ID musí mít partnerství s nepřímým poskytovatelem, jinak se žádost nezdaří.</span><span class="sxs-lookup"><span data-stu-id="af222-145">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="af222-146">Všimněte si také, že pokud není zadaná hodnota AssociatedPartnerId, zákazník se místo nepřímého prodejce vytvoří jako přímý zákazník nepřímého poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="af222-146">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="af222-147">Doména</span><span class="sxs-lookup"><span data-stu-id="af222-147">Domain</span></span>| <span data-ttu-id="af222-148">Řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-148">String</span></span>| <span data-ttu-id="af222-149">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-149">Yes</span></span>|<span data-ttu-id="af222-150">Název domény zákazníka, například contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="af222-150">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="af222-151">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="af222-151">organizationRegistrationNumber</span></span>|    <span data-ttu-id="af222-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-152">string</span></span>|<span data-ttu-id="af222-153">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-153">Yes</span></span>|     <span data-ttu-id="af222-154">Registrační číslo organizace zákazníka (v určitých zemích se také označuje jako číslo INN).</span><span class="sxs-lookup"><span data-stu-id="af222-154">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="af222-155">Vyžaduje se pouze pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménie (AM), Narština (AM), Kaskádština (AZ), Kaskády (BY), Kaskády (HU), KZ (KZ), Sidean (KG), Nar (MD), Korea (RU), Tádžština (TJ), Zamíce (UZ), Indie, Brazílie, Jižní Afrika, Saúdská Arábie, Saúdská Arábie, Malajsie, Malajsie, Zamísťování, Zamísťování, Jižní Asie a Malajsie.</span><span class="sxs-lookup"><span data-stu-id="af222-155">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="af222-156">Pro společnost nebo organizaci zákazníka v jiných zemích se jedná o volitelné pole.</span><span class="sxs-lookup"><span data-stu-id="af222-156">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="af222-157">Fakturační profil</span><span class="sxs-lookup"><span data-stu-id="af222-157">Billing profile</span></span>

<span data-ttu-id="af222-158">Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) potřebná k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="af222-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="af222-159">Název</span><span class="sxs-lookup"><span data-stu-id="af222-159">Name</span></span>             | <span data-ttu-id="af222-160">Typ</span><span class="sxs-lookup"><span data-stu-id="af222-160">Type</span></span>                                     | <span data-ttu-id="af222-161">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="af222-161">Required</span></span> | <span data-ttu-id="af222-162">Popis</span><span class="sxs-lookup"><span data-stu-id="af222-162">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="af222-163">e-mail</span><span class="sxs-lookup"><span data-stu-id="af222-163">email</span></span>            | <span data-ttu-id="af222-164">řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-164">string</span></span>                                   | <span data-ttu-id="af222-165">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-165">Yes</span></span>      | <span data-ttu-id="af222-166">E-mailová adresa zákazníka</span><span class="sxs-lookup"><span data-stu-id="af222-166">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="af222-167">jazyková verze</span><span class="sxs-lookup"><span data-stu-id="af222-167">culture</span></span>          | <span data-ttu-id="af222-168">řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-168">string</span></span>                                   | <span data-ttu-id="af222-169">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-169">Yes</span></span>      | <span data-ttu-id="af222-170">Jejich preferovaná kultura komunikace a měny, například en-US.</span><span class="sxs-lookup"><span data-stu-id="af222-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="af222-171">Podporované [Partnerské centrum v tématu Podporované jazyky](partner-center-supported-languages-and-locales.md) a národní prostředí.</span><span class="sxs-lookup"><span data-stu-id="af222-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="af222-172">language</span><span class="sxs-lookup"><span data-stu-id="af222-172">language</span></span>         | <span data-ttu-id="af222-173">řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-173">string</span></span>                                   | <span data-ttu-id="af222-174">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-174">Yes</span></span>      | <span data-ttu-id="af222-175">Výchozí jazyk.</span><span class="sxs-lookup"><span data-stu-id="af222-175">The default language.</span></span> <span data-ttu-id="af222-176">Podporují se dva kódy znakových `en` jazyků (například `fr` nebo ).</span><span class="sxs-lookup"><span data-stu-id="af222-176">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="af222-177">název \_ společnosti</span><span class="sxs-lookup"><span data-stu-id="af222-177">company\_name</span></span>    | <span data-ttu-id="af222-178">řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-178">string</span></span>                                   | <span data-ttu-id="af222-179">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-179">Yes</span></span>      | <span data-ttu-id="af222-180">Název registrované společnosti nebo organizace.</span><span class="sxs-lookup"><span data-stu-id="af222-180">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="af222-181">výchozí \_ adresa</span><span class="sxs-lookup"><span data-stu-id="af222-181">default\_address</span></span> | [<span data-ttu-id="af222-182">Adresa</span><span class="sxs-lookup"><span data-stu-id="af222-182">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="af222-183">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-183">Yes</span></span>      | <span data-ttu-id="af222-184">Registrovaná adresa společnosti nebo organizace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="af222-184">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="af222-185">Informace o [omezeních](utility-resources.md#address) délky najdete v tématu Prostředek adresy.</span><span class="sxs-lookup"><span data-stu-id="af222-185">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="af222-186">Profil společnosti</span><span class="sxs-lookup"><span data-stu-id="af222-186">Company profile</span></span>

<span data-ttu-id="af222-187">Tato tabulka popisuje minimální povinná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) potřebná k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="af222-187">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="af222-188">Název</span><span class="sxs-lookup"><span data-stu-id="af222-188">Name</span></span>   | <span data-ttu-id="af222-189">Typ</span><span class="sxs-lookup"><span data-stu-id="af222-189">Type</span></span>   | <span data-ttu-id="af222-190">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="af222-190">Required</span></span> | <span data-ttu-id="af222-191">Popis</span><span class="sxs-lookup"><span data-stu-id="af222-191">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="af222-192">doména</span><span class="sxs-lookup"><span data-stu-id="af222-192">domain</span></span> | <span data-ttu-id="af222-193">řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-193">string</span></span> | <span data-ttu-id="af222-194">Yes</span><span class="sxs-lookup"><span data-stu-id="af222-194">Yes</span></span>     | <span data-ttu-id="af222-195">Název domény zákazníka, například contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="af222-195">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="af222-196">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="af222-196">organizationRegistrationNumber</span></span> | <span data-ttu-id="af222-197">řetězec</span><span class="sxs-lookup"><span data-stu-id="af222-197">string</span></span> | <span data-ttu-id="af222-198">Závisí na podměně.</span><span class="sxs-lookup"><span data-stu-id="af222-198">Depends on condition</span></span> | <span data-ttu-id="af222-199">Registrační číslo organizace zákazníka (v určitých zemích se také označuje jako číslo INN).</span><span class="sxs-lookup"><span data-stu-id="af222-199">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="af222-200">Vyplnění tohoto pole se vyžaduje pouze v případě, že se společnost nebo organizace zákazníka nachází v následujících zemích:</span><span class="sxs-lookup"><span data-stu-id="af222-200">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="af222-201">– Arménská (AM)</span><span class="sxs-lookup"><span data-stu-id="af222-201">- Armenia (AM)</span></span> <br/><span data-ttu-id="af222-202">-Ázerbájdžán (AZ)</span><span class="sxs-lookup"><span data-stu-id="af222-202">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="af222-203">-Bělorusko (do)</span><span class="sxs-lookup"><span data-stu-id="af222-203">- Belarus (BY)</span></span><br/><span data-ttu-id="af222-204">-Maďarsko (HU)</span><span class="sxs-lookup"><span data-stu-id="af222-204">- Hungary (HU)</span></span><br/><span data-ttu-id="af222-205">-Kazachstán (KZ)</span><span class="sxs-lookup"><span data-stu-id="af222-205">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="af222-206">-Kyrgyzstán (KG)</span><span class="sxs-lookup"><span data-stu-id="af222-206">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="af222-207">-Moldávie (MD)</span><span class="sxs-lookup"><span data-stu-id="af222-207">- Moldova (MD)</span></span><br/><span data-ttu-id="af222-208">– Rusko (RU)</span><span class="sxs-lookup"><span data-stu-id="af222-208">- Russia (RU)</span></span><br/><span data-ttu-id="af222-209">-Tádžikistán (TJ)</span><span class="sxs-lookup"><span data-stu-id="af222-209">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="af222-210">-Uzbekistán (UZ)</span><span class="sxs-lookup"><span data-stu-id="af222-210">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="af222-211">– Ukrajina (UA)</span><span class="sxs-lookup"><span data-stu-id="af222-211">- Ukraine (UA)</span></span><br/><span data-ttu-id="af222-212">– Indie</span><span class="sxs-lookup"><span data-stu-id="af222-212">- India</span></span> <br/><span data-ttu-id="af222-213">– Brazílie</span><span class="sxs-lookup"><span data-stu-id="af222-213">- Brazil</span></span> <br/><span data-ttu-id="af222-214">– Jižní Afrika</span><span class="sxs-lookup"><span data-stu-id="af222-214">- South Africa</span></span> <br/><span data-ttu-id="af222-215">– Polsko</span><span class="sxs-lookup"><span data-stu-id="af222-215">- Poland</span></span> <br/><span data-ttu-id="af222-216">– Spojené arabské emiráty</span><span class="sxs-lookup"><span data-stu-id="af222-216">- United Arab Emirates</span></span> <br/><span data-ttu-id="af222-217">– Saúdská Arábie</span><span class="sxs-lookup"><span data-stu-id="af222-217">- Saudi Arabia</span></span> <br/><span data-ttu-id="af222-218">– Turecko</span><span class="sxs-lookup"><span data-stu-id="af222-218">- Turkey</span></span> <br/><span data-ttu-id="af222-219">– Thajsko</span><span class="sxs-lookup"><span data-stu-id="af222-219">- Thailand</span></span> <br/><span data-ttu-id="af222-220">– Vietnam</span><span class="sxs-lookup"><span data-stu-id="af222-220">- Vietnam</span></span> <br/><span data-ttu-id="af222-221">– Myanmar</span><span class="sxs-lookup"><span data-stu-id="af222-221">- Myanmar</span></span> <br/><span data-ttu-id="af222-222">– Irák</span><span class="sxs-lookup"><span data-stu-id="af222-222">- Iraq</span></span> <br/><span data-ttu-id="af222-223">– Jižní Súdán</span><span class="sxs-lookup"><span data-stu-id="af222-223">- South Sudan</span></span> <br/><span data-ttu-id="af222-224">– Venezuela</span><span class="sxs-lookup"><span data-stu-id="af222-224">- Venezuela</span></span><br/> <br/><span data-ttu-id="af222-225">Pro společnost nebo organizaci zákazníka nacházející se v jiných zemích se jedná o volitelné pole.</span><span class="sxs-lookup"><span data-stu-id="af222-225">For customer’s company/organization located in other countries, this is an optional field.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="af222-226">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="af222-226">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="af222-227">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="af222-227">REST response</span></span>

<span data-ttu-id="af222-228">V případě úspěchu bude odpověď obsahovat [zákaznický](customer-resources.md#customer) prostředek pro nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="af222-228">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="af222-229">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="af222-229">Response success and error codes</span></span>

<span data-ttu-id="af222-230">Odpovědi se dodávají se stavovým kódem HTTP, který označuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="af222-230">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="af222-231">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="af222-231">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="af222-232">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="af222-232">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="af222-233">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="af222-233">Response example</span></span>

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