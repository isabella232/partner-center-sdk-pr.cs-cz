---
title: Vytvoření zákazníka
description: Přečtěte si, jak může partner Cloud Solution Provider (CSP) použít rozhraní API partnerského centra k vytvoření nového zákazníka. Článek popisuje požadavky a další akce.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bc8e9d38353511e747ba4da99b11be40d08781e3
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274593"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="fbd5c-104">Vytvoření zákazníka pomocí rozhraní API partnerského centra</span><span class="sxs-lookup"><span data-stu-id="fbd5c-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="fbd5c-105">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="fbd5c-105">**Applies to:**</span></span>

- <span data-ttu-id="fbd5c-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="fbd5c-106">Partner Center</span></span>
- <span data-ttu-id="fbd5c-107">Partnerské centrum provozované společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="fbd5c-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="fbd5c-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fbd5c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fbd5c-109">Tento článek vysvětluje, jak vytvořit nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-109">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbd5c-110">Pokud jste nepřímý poskytovatel a chcete vytvořit zákazníka pro nepřímý prodejce, přečtěte si téma [Vytvoření zákazníka pro nepřímý prodejce](create-a-customer-for-an-indirect-reseller.md).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-110">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="fbd5c-111">Jako partner poskytovatele Cloud Solution Provider (CSP) můžete při vytváření zákazníka umístit objednávky jménem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-111">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="fbd5c-112">Při vytváření zákazníka vytvoříte také:</span><span class="sxs-lookup"><span data-stu-id="fbd5c-112">When you create a customer, you also create:</span></span>

- <span data-ttu-id="fbd5c-113">Objekt tenanta Azure Active Directory (AD) pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-113">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="fbd5c-114">Vztah mezi prodejcem a zákazníkem, který se používá pro delegovaná oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-114">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="fbd5c-115">Uživatelské jméno a heslo pro přihlášení jako správce pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-115">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="fbd5c-116">Po vytvoření zákazníka nezapomeňte uložit ID zákazníka a podrobnosti služby Azure AD pro budoucí použití se sadou SDK partnerského centra (například Správa účtů).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-116">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbd5c-117">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fbd5c-117">Prerequisites</span></span>

- <span data-ttu-id="fbd5c-118">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-118">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fbd5c-119">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-119">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbd5c-120">Chcete-li vytvořit tenanta zákazníka, je nutné během procesu vytváření zadat platnou fyzickou adresu.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-120">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="fbd5c-121">Adresu lze ověřit podle kroků uvedených v rámci scénáře [ověření adresy](validate-an-address.md) .</span><span class="sxs-lookup"><span data-stu-id="fbd5c-121">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="fbd5c-122">Pokud vytvoříte zákazníka pomocí neplatné adresy v prostředí izolovaného prostoru (sandbox), nebudete moci odstranit tohoto tenanta zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-122">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="fbd5c-123">C\#</span><span class="sxs-lookup"><span data-stu-id="fbd5c-123">C\#</span></span>

<span data-ttu-id="fbd5c-124">Postup přidání zákazníka:</span><span class="sxs-lookup"><span data-stu-id="fbd5c-124">To add a customer:</span></span>

1. <span data-ttu-id="fbd5c-125">Vytvoří instanci nového objektu [**zákazníka**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) .</span><span class="sxs-lookup"><span data-stu-id="fbd5c-125">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="fbd5c-126">Nezapomeňte vyplnit [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-126">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="fbd5c-127">Přidejte nového zákazníka do kolekce [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , a to voláním [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-127">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="fbd5c-128">\#Příklad C</span><span class="sxs-lookup"><span data-stu-id="fbd5c-128">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix),
        //// OrganizationRegistrationNumber = "123456" // Please add if in specific country that requires
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            MiddleName = "MiddleName",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

<span data-ttu-id="fbd5c-129">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fbd5c-130">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateCustomer. cs</span><span class="sxs-lookup"><span data-stu-id="fbd5c-130">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="fbd5c-131">Java</span><span class="sxs-lookup"><span data-stu-id="fbd5c-131">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="fbd5c-132">Vytvoření nového zákazníka:</span><span class="sxs-lookup"><span data-stu-id="fbd5c-132">To create a new customer:</span></span>

1. <span data-ttu-id="fbd5c-133">Vytvoří novou instanci třídy **CustomerBillingProfile** a objektů **CustomerCompanyProfile** .</span><span class="sxs-lookup"><span data-stu-id="fbd5c-133">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="fbd5c-134">Nezapomeňte vyplnit požadovaná pole.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-134">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="fbd5c-135">Vytvořte zákazníka voláním funkce **IAggregatePartner. GetCustomers (). Create** .</span><span class="sxs-lookup"><span data-stu-id="fbd5c-135">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="fbd5c-136">Příklad Java</span><span class="sxs-lookup"><span data-stu-id="fbd5c-136">Java example</span></span>

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a><span data-ttu-id="fbd5c-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbd5c-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="fbd5c-138">Pokud chcete vytvořit zákazníka, spusťte příkaz [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) .</span><span class="sxs-lookup"><span data-stu-id="fbd5c-138">To create a customer execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="fbd5c-139">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fbd5c-139">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fbd5c-140">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fbd5c-140">Request syntax</span></span>

| <span data-ttu-id="fbd5c-141">Metoda</span><span class="sxs-lookup"><span data-stu-id="fbd5c-141">Method</span></span>   | <span data-ttu-id="fbd5c-142">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fbd5c-142">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="fbd5c-143">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="fbd5c-143">**POST**</span></span> | <span data-ttu-id="fbd5c-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fbd5c-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fbd5c-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fbd5c-145">Request headers</span></span>

- <span data-ttu-id="fbd5c-146">Toto rozhraní API se idempotentní (nepřinese se mu jiný výsledek, pokud ho zavoláte víckrát).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-146">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="fbd5c-147">Vyžaduje se ID žádosti a ID korelace.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-147">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="fbd5c-148">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fbd5c-149">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fbd5c-149">Request body</span></span>

<span data-ttu-id="fbd5c-150">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-150">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="fbd5c-151">Název</span><span class="sxs-lookup"><span data-stu-id="fbd5c-151">Name</span></span>                              | <span data-ttu-id="fbd5c-152">Typ</span><span class="sxs-lookup"><span data-stu-id="fbd5c-152">Type</span></span>   | <span data-ttu-id="fbd5c-153">Description</span><span class="sxs-lookup"><span data-stu-id="fbd5c-153">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="fbd5c-154">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="fbd5c-154">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="fbd5c-155">object</span><span class="sxs-lookup"><span data-stu-id="fbd5c-155">object</span></span> | <span data-ttu-id="fbd5c-156">Informace o fakturačním profilu zákazníka</span><span class="sxs-lookup"><span data-stu-id="fbd5c-156">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="fbd5c-157">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="fbd5c-157">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="fbd5c-158">object</span><span class="sxs-lookup"><span data-stu-id="fbd5c-158">object</span></span> | <span data-ttu-id="fbd5c-159">Informace o profilu společnosti zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-159">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="fbd5c-160">Fakturační profil</span><span class="sxs-lookup"><span data-stu-id="fbd5c-160">Billing profile</span></span>

<span data-ttu-id="fbd5c-161">Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) , který je potřeba k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-161">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="fbd5c-162">Název</span><span class="sxs-lookup"><span data-stu-id="fbd5c-162">Name</span></span>             | <span data-ttu-id="fbd5c-163">Typ</span><span class="sxs-lookup"><span data-stu-id="fbd5c-163">Type</span></span>                                     | <span data-ttu-id="fbd5c-164">Description</span><span class="sxs-lookup"><span data-stu-id="fbd5c-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fbd5c-165">e-mail</span><span class="sxs-lookup"><span data-stu-id="fbd5c-165">email</span></span>            | <span data-ttu-id="fbd5c-166">řetězec</span><span class="sxs-lookup"><span data-stu-id="fbd5c-166">string</span></span>                                   | <span data-ttu-id="fbd5c-167">E-mailová adresa zákazníka</span><span class="sxs-lookup"><span data-stu-id="fbd5c-167">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="fbd5c-168">jazyková verze</span><span class="sxs-lookup"><span data-stu-id="fbd5c-168">culture</span></span>          | <span data-ttu-id="fbd5c-169">řetězec</span><span class="sxs-lookup"><span data-stu-id="fbd5c-169">string</span></span>                                   | <span data-ttu-id="fbd5c-170">Upřednostňovaná jazyková verze pro komunikaci a měnu, jako je "en-US".</span><span class="sxs-lookup"><span data-stu-id="fbd5c-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="fbd5c-171">Podporované jazykové verze najdete v tématu [podporované jazyky a národní prostředí partnerského centra](partner-center-supported-languages-and-locales.md) .</span><span class="sxs-lookup"><span data-stu-id="fbd5c-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="fbd5c-172">language</span><span class="sxs-lookup"><span data-stu-id="fbd5c-172">language</span></span>         | <span data-ttu-id="fbd5c-173">řetězec</span><span class="sxs-lookup"><span data-stu-id="fbd5c-173">string</span></span>                                   | <span data-ttu-id="fbd5c-174">Výchozí jazyk.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-174">The default language.</span></span> <span data-ttu-id="fbd5c-175">Jsou podporovány dva znakové kódy jazyka (například `en` nebo `fr` ).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-175">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="fbd5c-176">\_název společnosti</span><span class="sxs-lookup"><span data-stu-id="fbd5c-176">company\_name</span></span>    | <span data-ttu-id="fbd5c-177">řetězec</span><span class="sxs-lookup"><span data-stu-id="fbd5c-177">string</span></span>                                   | <span data-ttu-id="fbd5c-178">Registrovaný název společnosti nebo organizace.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-178">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="fbd5c-179">výchozí \_ adresa</span><span class="sxs-lookup"><span data-stu-id="fbd5c-179">default\_address</span></span> | [<span data-ttu-id="fbd5c-180">Adresa</span><span class="sxs-lookup"><span data-stu-id="fbd5c-180">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="fbd5c-181">Registrovaná adresa společnosti nebo organizace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-181">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="fbd5c-182">Informace o omezeních délky najdete v tématu [adresa](utility-resources.md#address) prostředku.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-182">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="fbd5c-183">Profil společnosti</span><span class="sxs-lookup"><span data-stu-id="fbd5c-183">Company profile</span></span>

<span data-ttu-id="fbd5c-184">Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) , který je potřeba k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-184">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="fbd5c-185">Název</span><span class="sxs-lookup"><span data-stu-id="fbd5c-185">Name</span></span>   | <span data-ttu-id="fbd5c-186">Typ</span><span class="sxs-lookup"><span data-stu-id="fbd5c-186">Type</span></span>   | <span data-ttu-id="fbd5c-187">Description</span><span class="sxs-lookup"><span data-stu-id="fbd5c-187">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="fbd5c-188">doména</span><span class="sxs-lookup"><span data-stu-id="fbd5c-188">domain</span></span> | <span data-ttu-id="fbd5c-189">řetězec</span><span class="sxs-lookup"><span data-stu-id="fbd5c-189">string</span></span> | <span data-ttu-id="fbd5c-190">Název domény zákazníka, například contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-190">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="fbd5c-191">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="fbd5c-191">organizationRegistrationNumber</span></span>|<span data-ttu-id="fbd5c-192">Řetězec</span><span class="sxs-lookup"><span data-stu-id="fbd5c-192">String</span></span>|<span data-ttu-id="fbd5c-193">Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-193">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="fbd5c-194">Požadováno jenom pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménská (AM), Ázerbájdžán (AZ), Bělorusko (BY), Maďarsko (HU), Kazachstán (KZ), Kyrgyzstán (KG), Moldavsko (MD), Rusko (RU), Tádžikistán (TJ), Uzbekistán (UZ), Ukrajina (UA), Brazílie (BR), Indie, Jižní Afrika, Polsko, Spojené arabské emiráty, Saúdská Arábie, Turecko, Thajsko, Vietnam, Myanmar, Irák, Jižní Súdán a Venezuela.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-194">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), Brazil(BR), India, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan and Venezuela.</span></span> <span data-ttu-id="fbd5c-195">Pro společnost nebo organizaci zákazníka nacházející se v jiných zemích je to volitelné pole.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-195">For customer’s company/organization located in other countries this is an optional field.</span></span>|

### <a name="request-example"></a><span data-ttu-id="fbd5c-196">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fbd5c-196">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="fbd5c-197">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fbd5c-197">REST response</span></span>

<span data-ttu-id="fbd5c-198">V případě úspěchu toto rozhraní API vrátí [zákaznický](customer-resources.md#customer) prostředek pro nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-198">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="fbd5c-199">Uložte si podrobnosti o ID zákazníka a Azure AD pro budoucí použití se sadou partner Center SDK.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-199">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="fbd5c-200">Budete je potřebovat pro použití se správou účtů, například.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-200">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fbd5c-201">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fbd5c-201">Response success and error codes</span></span>

<span data-ttu-id="fbd5c-202">Odpovědi se dodávají se stavovým kódem HTTP, který označuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-202">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fbd5c-203">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fbd5c-203">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fbd5c-204">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fbd5c-204">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fbd5c-205">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fbd5c-205">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
