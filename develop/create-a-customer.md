---
title: Vytvoření zákazníka
description: Přečtěte si, jak může partner Cloud Solution Provider (CSP) použít rozhraní API partnerského centra k vytvoření nového zákazníka. Článek popisuje požadavky a další akce.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 3bc8081c682bdf522bcb0ca218f16cafab7b3a99
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/08/2020
ms.locfileid: "97767153"
---
# <a name="create-a-customer-using-partner-center-apis"></a>Vytvoření zákazníka pomocí rozhraní API partnerského centra

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek vysvětluje, jak vytvořit nového zákazníka.

> [!IMPORTANT]
> Pokud jste nepřímý poskytovatel a chcete vytvořit zákazníka pro nepřímý prodejce, přečtěte si téma [Vytvoření zákazníka pro nepřímý prodejce](create-a-customer-for-an-indirect-reseller.md).

Jako partner poskytovatele Cloud Solution Provider (CSP) můžete při vytváření zákazníka umístit objednávky jménem zákazníka. Při vytváření zákazníka vytvoříte také:

- Objekt tenanta Azure Active Directory (AD) pro zákazníka.

- Vztah mezi prodejcem a zákazníkem, který se používá pro delegovaná oprávnění správce.

- Uživatelské jméno a heslo pro přihlášení jako správce pro zákazníka.

Po vytvoření zákazníka nezapomeňte uložit ID zákazníka a podrobnosti služby Azure AD pro budoucí použití se sadou SDK partnerského centra (například Správa účtů).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

> [!IMPORTANT]
> Chcete-li vytvořit tenanta zákazníka, je nutné během procesu vytváření zadat platnou fyzickou adresu. Adresu lze ověřit podle kroků uvedených v rámci scénáře [ověření adresy](validate-an-address.md) . Pokud vytvoříte zákazníka pomocí neplatné adresy v prostředí izolovaného prostoru (sandbox), nebudete moci odstranit tohoto tenanta zákazníka.

## <a name="c"></a>C\#

Postup přidání zákazníka:

1. Vytvoří instanci nového objektu [**zákazníka**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) . Nezapomeňte vyplnit [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).

2. Přidejte nového zákazníka do kolekce [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , a to voláním [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).

### <a name="c-example"></a>\#Příklad C

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

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Vytvoření nového zákazníka:

1. Vytvoří novou instanci třídy **CustomerBillingProfile** a objektů **CustomerCompanyProfile** . Nezapomeňte vyplnit požadovaná pole.

2. Vytvořte zákazníka voláním funkce **IAggregatePartner. GetCustomers (). Create** .

### <a name="java-example"></a>Příklad Java

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

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pokud chcete vytvořit zákazníka, spusťte příkaz [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) .

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                       |
|----------|-------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

- Toto rozhraní API se idempotentní (nepřinese se mu jiný výsledek, pokud ho zavoláte víckrát).

- Vyžaduje se ID žádosti a ID korelace.

- Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu žádosti.

| Název                              | Typ   | Description                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | object | Informace o fakturačním profilu zákazníka |
| [CompanyProfile](#company-profile) | object | Informace o profilu společnosti zákazníka. |

#### <a name="billing-profile"></a>Fakturační profil

Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) , který je potřeba k vytvoření nového zákazníka.

| Název             | Typ                                     | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-mail            | řetězec                                   | E-mailová adresa zákazníka                                                                                                                                                                                   |
| jazyková verze          | řetězec                                   | Upřednostňovaná jazyková verze pro komunikaci a měnu, jako je "en-US". Podporované jazykové verze najdete v tématu [podporované jazyky a národní prostředí partnerského centra](partner-center-supported-languages-and-locales.md) . |
| language         | řetězec                                   | Výchozí jazyk. Jsou podporovány dva znakové kódy jazyka (například `en` nebo `fr` ).                                                                                                                                |
| \_název společnosti    | řetězec                                   | Registrovaný název společnosti nebo organizace.                                                                                                                                                                       |
| výchozí \_ adresa | [Adresa](utility-resources.md#address) | Registrovaná adresa společnosti nebo organizace zákazníka. Informace o omezeních délky najdete v tématu [adresa](utility-resources.md#address) prostředku.                                             |

#### <a name="company-profile"></a>Profil společnosti

Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) , který je potřeba k vytvoření nového zákazníka.

| Název   | Typ   | Description                                                  |
|--------|--------|--------------------------------------------------------------|
| doména | řetězec | Název domény zákazníka, například contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Řetězec|Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích). Požadované jenom pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích. Arménie (AM), Ázerbájdžán (AZ), Bělorusko (BY), Maďarsko (HU), Kazachstán (KZ), Kyrgyzstán (KG), Moldavsko (MD), Rusko (RU), Tádžikistán (TJ), Uzbekistán (UZ), Ukrajina (UA). Pro společnost nebo organizaci zákazníka nacházející se v jiných zemích by neměl být určen.|


### <a name="request-example"></a>Příklad požadavku

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

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu toto rozhraní API vrátí [zákaznický](customer-resources.md#customer) prostředek pro nového zákazníka. Uložte si podrobnosti o ID zákazníka a Azure AD pro budoucí použití se sadou partner Center SDK. Budete je potřebovat pro použití se správou účtů, například.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Odpovědi se dodávají se stavovým kódem HTTP, který označuje úspěch nebo neúspěch a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

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
