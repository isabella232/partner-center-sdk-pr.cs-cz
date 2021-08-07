---
title: Vytvoření zákazníka
description: Zjistěte, jak Cloud Solution Provider (CSP) může pomocí Partnerské centrum API vytvořit nového zákazníka. Článek popisuje požadavky a další kroky.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 49df47441276c7e79074e1bf7f8d50cd72054b42acd93938de088046b68b6d98
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991765"
---
# <a name="create-a-customer-using-partner-center-apis"></a>Vytvoření zákazníka pomocí Partnerské centrum API

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government

Tento článek vysvětluje, jak vytvořit nového zákazníka.

> [!IMPORTANT]
> Pokud jste nepřímý poskytovatel a chcete vytvořit zákazníka pro nepřímého prodejce, přečtěte si prosím informace v tématu Vytvoření zákazníka [pro nepřímého prodejce.](create-a-customer-for-an-indirect-reseller.md)

Jako partner CSP (Cloud Solution Provider) můžete při vytváření zákazníka za zákazníka zasaťovat objednávky. Při vytváření zákazníka také vytvoříte:

- Objekt tenanta Azure Active Directory (AD) zákazníka.

- Vztah mezi prodejcem a zákazníkem, který se používá pro delegovaná oprávnění správce.

- Uživatelské jméno a heslo pro přihlášení jako správce zákazníka.

Po vytvoření zákazníka nezapomeňte uložit ID zákazníka a podrobnosti o Službě Azure AD pro budoucí použití s SDK pro Partnerské centrum (například správu účtů).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

> [!IMPORTANT]
> Pokud chcete vytvořit tenanta zákazníka, musíte během procesu vytváření zadat platnou fyzickou adresu. Adresu je možné ověřit podle kroků uvedených ve [scénáři Ověření](validate-an-address.md) adresy. Pokud vytvoříte zákazníka pomocí neplatné adresy v prostředí sandboxu, nebudete moct tohoto tenanta zákazníka odstranit.

## <a name="c"></a>C\#

Přidání zákazníka:

1. Vytvořte instanci nového [**objektu Customer.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) Nezapomeňte vyplnit [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)

2. Přidejte nového zákazníka do kolekce [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) voláním [**metody Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)

### <a name="c-example"></a>Příklad \# jazyka C

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

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class**: CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Vytvoření nového zákazníka:

1. Vytvořte novou instanci objektů **CustomerBillingProfile** a **CustomerCompanyProfile.** Nezapomeňte vyplnit požadovaná pole.

2. Vytvořte zákazníka zavolám funkci **IAggregatePartner.getCustomers().create.**

### <a name="java-example"></a>Příklad v Javě

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

Pokud chcete vytvořit zákazníka, spusťte [**příkaz New-PartnerCustomer.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                       |
|----------|-------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

- Toto rozhraní API je idempotentní (pokud ho zavoláte vícekrát, nepřidá jiný výsledek).

- Vyžaduje se ID požadavku a ID korelace.

- Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu požadavku.

| Název                              | Typ   | Description                                 |
|-----------------------------------|--------|---------------------------------------------|
| [Profil fakturace](#billing-profile) | object | Informace o fakturačním profilu zákazníka. |
| [Profil společnosti](#company-profile) | object | Informace o profilu společnosti zákazníka. |

#### <a name="billing-profile"></a>Fakturační profil

Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) potřebná k vytvoření nového zákazníka.

| Název             | Typ                                     | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-mail            | řetězec                                   | E-mailová adresa zákazníka                                                                                                                                                                                   |
| jazyková verze          | řetězec                                   | Jejich preferovaná kultura komunikace a měny, například en-US. Podporované [Partnerské centrum v tématu Podporované jazyky](partner-center-supported-languages-and-locales.md) a národní prostředí. |
| language         | řetězec                                   | Výchozí jazyk. Podporují se dva kódy znakových `en` jazyků (například `fr` nebo ).                                                                                                                                |
| název \_ společnosti    | řetězec                                   | Název registrované společnosti nebo organizace.                                                                                                                                                                       |
| výchozí \_ adresa | [Adresa](utility-resources.md#address) | Registrovaná adresa společnosti nebo organizace zákazníka. Informace o [omezeních](utility-resources.md#address) délky najdete v tématu Prostředek adresy.                                             |

#### <a name="company-profile"></a>Profil společnosti

Tato tabulka popisuje minimální povinná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) potřebná k vytvoření nového zákazníka.

| Název   | Typ   | Description                                                  |
|--------|--------|--------------------------------------------------------------|
| doména | řetězec | Název domény zákazníka, například contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Řetězec|Registrační číslo organizace zákazníka (v určitých zemích se také označuje jako číslo INN). Vyžaduje se pouze pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménie (AM), Kaskádština (AM), Kaskádština (AZ), Kaskády (BY), Indu (HU), KZ (KZ), Korea, Jižní Afrika, Japonsko, Spojené arabské emiráty, Saúdská Arábie, Brazílie, Vietnam, Zamísťování, Jarda a Jarda. Pro společnost nebo organizaci zákazníka v jiných zemích se jedná o volitelné pole.|

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

V případě úspěchu vrátí toto rozhraní API [pro](customer-resources.md#customer) nového zákazníka prostředek zákazníka. Uložte si ID zákazníka a podrobnosti o Azure AD pro budoucí použití s SDK pro Partnerské centrum. Budete je například potřebovat ke správě účtů.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Odpovědi mají stavový kód HTTP, který označuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

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
