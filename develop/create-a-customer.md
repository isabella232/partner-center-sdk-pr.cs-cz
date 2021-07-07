---
title: Vytvoření zákazníka
description: Zjistěte, jak Cloud Solution Provider (CSP) může pomocí Partnerské centrum API vytvořit nového zákazníka. Článek popisuje požadavky a další kroky.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6232ca77d057f2f5168b73d81ec551669d540246
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973719"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="5c0cc-104">Vytvoření zákazníka pomocí Partnerské centrum API</span><span class="sxs-lookup"><span data-stu-id="5c0cc-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="5c0cc-105">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5c0cc-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5c0cc-106">Tento článek vysvětluje, jak vytvořit nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-106">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c0cc-107">Pokud jste nepřímý poskytovatel a chcete vytvořit zákazníka pro nepřímého prodejce, přečtěte si prosím informace v tématu Vytvoření zákazníka [pro nepřímého prodejce.](create-a-customer-for-an-indirect-reseller.md)</span><span class="sxs-lookup"><span data-stu-id="5c0cc-107">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="5c0cc-108">Jako partner CSP (Cloud Solution Provider) můžete při vytváření zákazníka za zákazníka zasaťovat objednávky.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-108">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="5c0cc-109">Při vytváření zákazníka také vytvoříte:</span><span class="sxs-lookup"><span data-stu-id="5c0cc-109">When you create a customer, you also create:</span></span>

- <span data-ttu-id="5c0cc-110">Objekt tenanta Azure Active Directory (AD) zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-110">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="5c0cc-111">Vztah mezi prodejcem a zákazníkem, který se používá pro delegovaná oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-111">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="5c0cc-112">Uživatelské jméno a heslo pro přihlášení jako správce zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-112">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="5c0cc-113">Po vytvoření zákazníka nezapomeňte uložit ID zákazníka a podrobnosti o Službě Azure AD pro budoucí použití s SDK pro Partnerské centrum (například správu účtů).</span><span class="sxs-lookup"><span data-stu-id="5c0cc-113">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c0cc-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5c0cc-114">Prerequisites</span></span>

- <span data-ttu-id="5c0cc-115">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5c0cc-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5c0cc-116">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c0cc-117">Pokud chcete vytvořit tenanta zákazníka, musíte během procesu vytváření zadat platnou fyzickou adresu.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-117">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="5c0cc-118">Adresu je možné ověřit podle kroků uvedených ve [scénáři Ověření](validate-an-address.md) adresy.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-118">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="5c0cc-119">Pokud vytvoříte zákazníka pomocí neplatné adresy v prostředí sandboxu, nebudete moct tohoto tenanta zákazníka odstranit.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-119">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="5c0cc-120">C\#</span><span class="sxs-lookup"><span data-stu-id="5c0cc-120">C\#</span></span>

<span data-ttu-id="5c0cc-121">Přidání zákazníka:</span><span class="sxs-lookup"><span data-stu-id="5c0cc-121">To add a customer:</span></span>

1. <span data-ttu-id="5c0cc-122">Vytvořte instanci nového [**objektu Customer.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer)</span><span class="sxs-lookup"><span data-stu-id="5c0cc-122">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="5c0cc-123">Nezapomeňte vyplnit [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)</span><span class="sxs-lookup"><span data-stu-id="5c0cc-123">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="5c0cc-124">Přidejte nového zákazníka do kolekce [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) voláním [**metody Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)</span><span class="sxs-lookup"><span data-stu-id="5c0cc-124">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="5c0cc-125">Příklad \# jazyka C</span><span class="sxs-lookup"><span data-stu-id="5c0cc-125">C\# example</span></span>

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

<span data-ttu-id="5c0cc-126">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5c0cc-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5c0cc-127">**Project:** SDK pro Partnerské centrum Samples **Class**: CreateCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="5c0cc-127">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="5c0cc-128">Java</span><span class="sxs-lookup"><span data-stu-id="5c0cc-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="5c0cc-129">Vytvoření nového zákazníka:</span><span class="sxs-lookup"><span data-stu-id="5c0cc-129">To create a new customer:</span></span>

1. <span data-ttu-id="5c0cc-130">Vytvořte novou instanci objektů **CustomerBillingProfile** a **CustomerCompanyProfile.**</span><span class="sxs-lookup"><span data-stu-id="5c0cc-130">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="5c0cc-131">Nezapomeňte vyplnit požadovaná pole.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-131">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="5c0cc-132">Vytvořte zákazníka zavolám funkci **IAggregatePartner.getCustomers().create.**</span><span class="sxs-lookup"><span data-stu-id="5c0cc-132">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="5c0cc-133">Příklad v Javě</span><span class="sxs-lookup"><span data-stu-id="5c0cc-133">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="5c0cc-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c0cc-134">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="5c0cc-135">Pokud chcete vytvořit zákazníka, spusťte [**příkaz New-PartnerCustomer.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)</span><span class="sxs-lookup"><span data-stu-id="5c0cc-135">To create a customer, execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="5c0cc-136">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="5c0cc-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5c0cc-137">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="5c0cc-137">Request syntax</span></span>

| <span data-ttu-id="5c0cc-138">Metoda</span><span class="sxs-lookup"><span data-stu-id="5c0cc-138">Method</span></span>   | <span data-ttu-id="5c0cc-139">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5c0cc-139">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="5c0cc-140">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="5c0cc-140">**POST**</span></span> | <span data-ttu-id="5c0cc-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5c0cc-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5c0cc-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5c0cc-142">Request headers</span></span>

- <span data-ttu-id="5c0cc-143">Toto rozhraní API je idempotentní (pokud ho zavoláte vícekrát, nepřidá jiný výsledek).</span><span class="sxs-lookup"><span data-stu-id="5c0cc-143">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="5c0cc-144">Vyžaduje se ID požadavku a ID korelace.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-144">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="5c0cc-145">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5c0cc-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5c0cc-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="5c0cc-146">Request body</span></span>

<span data-ttu-id="5c0cc-147">Tato tabulka popisuje požadované vlastnosti v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="5c0cc-148">Název</span><span class="sxs-lookup"><span data-stu-id="5c0cc-148">Name</span></span>                              | <span data-ttu-id="5c0cc-149">Typ</span><span class="sxs-lookup"><span data-stu-id="5c0cc-149">Type</span></span>   | <span data-ttu-id="5c0cc-150">Description</span><span class="sxs-lookup"><span data-stu-id="5c0cc-150">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="5c0cc-151">Profil fakturace</span><span class="sxs-lookup"><span data-stu-id="5c0cc-151">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="5c0cc-152">object</span><span class="sxs-lookup"><span data-stu-id="5c0cc-152">object</span></span> | <span data-ttu-id="5c0cc-153">Informace o fakturačním profilu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-153">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="5c0cc-154">Profil společnosti</span><span class="sxs-lookup"><span data-stu-id="5c0cc-154">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="5c0cc-155">object</span><span class="sxs-lookup"><span data-stu-id="5c0cc-155">object</span></span> | <span data-ttu-id="5c0cc-156">Informace o profilu společnosti zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-156">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="5c0cc-157">Fakturační profil</span><span class="sxs-lookup"><span data-stu-id="5c0cc-157">Billing profile</span></span>

<span data-ttu-id="5c0cc-158">Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) potřebná k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="5c0cc-159">Název</span><span class="sxs-lookup"><span data-stu-id="5c0cc-159">Name</span></span>             | <span data-ttu-id="5c0cc-160">Typ</span><span class="sxs-lookup"><span data-stu-id="5c0cc-160">Type</span></span>                                     | <span data-ttu-id="5c0cc-161">Description</span><span class="sxs-lookup"><span data-stu-id="5c0cc-161">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5c0cc-162">e-mail</span><span class="sxs-lookup"><span data-stu-id="5c0cc-162">email</span></span>            | <span data-ttu-id="5c0cc-163">řetězec</span><span class="sxs-lookup"><span data-stu-id="5c0cc-163">string</span></span>                                   | <span data-ttu-id="5c0cc-164">E-mailová adresa zákazníka</span><span class="sxs-lookup"><span data-stu-id="5c0cc-164">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="5c0cc-165">jazyková verze</span><span class="sxs-lookup"><span data-stu-id="5c0cc-165">culture</span></span>          | <span data-ttu-id="5c0cc-166">řetězec</span><span class="sxs-lookup"><span data-stu-id="5c0cc-166">string</span></span>                                   | <span data-ttu-id="5c0cc-167">Jejich preferovaná kultura komunikace a měny, například en-US.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-167">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="5c0cc-168">Podporované [Partnerské centrum v tématu Podporované jazyky](partner-center-supported-languages-and-locales.md) a národní prostředí.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-168">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="5c0cc-169">language</span><span class="sxs-lookup"><span data-stu-id="5c0cc-169">language</span></span>         | <span data-ttu-id="5c0cc-170">řetězec</span><span class="sxs-lookup"><span data-stu-id="5c0cc-170">string</span></span>                                   | <span data-ttu-id="5c0cc-171">Výchozí jazyk.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-171">The default language.</span></span> <span data-ttu-id="5c0cc-172">Podporují se dva kódy znakových `en` jazyků (například `fr` nebo ).</span><span class="sxs-lookup"><span data-stu-id="5c0cc-172">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="5c0cc-173">název \_ společnosti</span><span class="sxs-lookup"><span data-stu-id="5c0cc-173">company\_name</span></span>    | <span data-ttu-id="5c0cc-174">řetězec</span><span class="sxs-lookup"><span data-stu-id="5c0cc-174">string</span></span>                                   | <span data-ttu-id="5c0cc-175">Název registrované společnosti nebo organizace.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-175">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="5c0cc-176">výchozí \_ adresa</span><span class="sxs-lookup"><span data-stu-id="5c0cc-176">default\_address</span></span> | [<span data-ttu-id="5c0cc-177">Adresa</span><span class="sxs-lookup"><span data-stu-id="5c0cc-177">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="5c0cc-178">Registrovaná adresa společnosti nebo organizace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-178">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="5c0cc-179">Informace o [omezeních](utility-resources.md#address) délky najdete v tématu Prostředek adresy.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-179">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="5c0cc-180">Profil společnosti</span><span class="sxs-lookup"><span data-stu-id="5c0cc-180">Company profile</span></span>

<span data-ttu-id="5c0cc-181">Tato tabulka popisuje minimální povinná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) potřebná k vytvoření nového zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-181">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="5c0cc-182">Název</span><span class="sxs-lookup"><span data-stu-id="5c0cc-182">Name</span></span>   | <span data-ttu-id="5c0cc-183">Typ</span><span class="sxs-lookup"><span data-stu-id="5c0cc-183">Type</span></span>   | <span data-ttu-id="5c0cc-184">Description</span><span class="sxs-lookup"><span data-stu-id="5c0cc-184">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="5c0cc-185">doména</span><span class="sxs-lookup"><span data-stu-id="5c0cc-185">domain</span></span> | <span data-ttu-id="5c0cc-186">řetězec</span><span class="sxs-lookup"><span data-stu-id="5c0cc-186">string</span></span> | <span data-ttu-id="5c0cc-187">Název domény zákazníka, například contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-187">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="5c0cc-188">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="5c0cc-188">organizationRegistrationNumber</span></span>|<span data-ttu-id="5c0cc-189">Řetězec</span><span class="sxs-lookup"><span data-stu-id="5c0cc-189">String</span></span>|<span data-ttu-id="5c0cc-190">Registrační číslo organizace zákazníka (v určitých zemích se také označuje jako číslo INN).</span><span class="sxs-lookup"><span data-stu-id="5c0cc-190">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="5c0cc-191">Vyžaduje se pouze pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménie (AM), Kaskádština (AM), Kaskádština (AZ), Kaskády (BY), Indu (HU), KZ (KZ), Korea, Jižní Afrika, Japonsko, Spojené arabské emiráty, Saúdská Arábie, Brazílie, Vietnam, Zamísťování, Jarda a Jarda.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-191">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), Brazil(BR), India, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="5c0cc-192">Pro společnost nebo organizaci zákazníka v jiných zemích se jedná o volitelné pole.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-192">For customer’s company/organization located in other countries, this is an optional field.</span></span>|

### <a name="request-example"></a><span data-ttu-id="5c0cc-193">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="5c0cc-193">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5c0cc-194">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5c0cc-194">REST response</span></span>

<span data-ttu-id="5c0cc-195">V případě úspěchu vrátí toto rozhraní API [pro](customer-resources.md#customer) nového zákazníka prostředek zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-195">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="5c0cc-196">Uložte si ID zákazníka a podrobnosti o Azure AD pro budoucí použití s SDK pro Partnerské centrum.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-196">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="5c0cc-197">Budete je například potřebovat ke správě účtů.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-197">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5c0cc-198">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="5c0cc-198">Response success and error codes</span></span>

<span data-ttu-id="5c0cc-199">Odpovědi mají stavový kód HTTP, který označuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-199">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5c0cc-200">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="5c0cc-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5c0cc-201">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5c0cc-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5c0cc-202">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="5c0cc-202">Response example</span></span>

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
