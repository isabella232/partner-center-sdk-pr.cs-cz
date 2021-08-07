---
title: Vytvoření zákazníka pro nepřímého prodejce
description: Zjistěte, jak může nepřímý poskytovatel Partnerské centrum rozhraní API k vytvoření zákazníka pro nepřímého prodejce.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e54e083dda758cc712c889916676007a389ba69c8009bb3d4907df343a436004
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991731"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Vytvoření zákazníka pro nepřímého prodejce pomocí Partnerské centrum API

Nepřímý poskytovatel může vytvořit zákazníka pro nepřímého prodejce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- Identifikátor tenanta nepřímého prodejce.

- Nepřímý prodejce musí mít partnerství s nepřímým poskytovatelem.

## <a name="c"></a>C\#

Přidání nového zákazníka pro nepřímého prodejce:

1. Vytvořte instanci nového [**objektu Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) a pak vytvořte instanci a naplňte profily [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile) Nezapomeňte přiřadit ID nepřímého prodejce k vlastnosti [**AssociatedPartnerID.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)

2. Pomocí vlastnosti [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) získejte rozhraní pro operace shromažďování zákazníků.

3. Pokud chcete [**vytvořit zákazníka,**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) zavolejte metodu Create nebo [**CreateAsync.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)

### <a name="c-example"></a>Příklad \# jazyka C

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

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                       |
|----------|-------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu požadavku.

| Název                                          | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Profil fakturace](#billing-profile)             | object | Yes      | Informace o fakturačním profilu zákazníka.                                                                                                                                                                                                                                                                                                           |
| [Profil společnosti](#company-profile)             | object | Yes      | Informace o profilu společnosti zákazníka.                                                               
| [AssociatedPartnerId (ID přidruženéhopartneru)](customer-resources.md#customer) | řetězec | Yes      | ID nepřímého prodejce. Nepřímý prodejce uvedený zde uvedeným ID musí mít partnerství s nepřímým poskytovatelem, jinak se žádost nezdaří. Všimněte si také, že pokud není zadaná hodnota AssociatedPartnerId, zákazník se místo nepřímého prodejce vytvoří jako přímý zákazník nepřímého poskytovatele. |
|Doména| Řetězec| Yes|Název domény zákazníka, například contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    řetězec|Yes|     Registrační číslo organizace zákazníka (v určitých zemích se také označuje jako číslo INN). Vyžaduje se pouze pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménie (AM), Narština (AM), Kaskádština (AZ), Kaskády (BY), Kaskády (HU), KZ (KZ), Sidean (KG), Nar (MD), Korea (RU), Tádžština (TJ), Zamíce (UZ), Indie, Brazílie, Jižní Afrika, Saúdská Arábie, Saúdská Arábie, Malajsie, Malajsie, Zamísťování, Zamísťování, Jižní Asie a Malajsie. Pro společnost nebo organizaci zákazníka v jiných zemích se jedná o volitelné pole.|



#### <a name="billing-profile"></a>Fakturační profil

Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) potřebná k vytvoření nového zákazníka.

| Název             | Typ                                     | Vyžadováno | Popis                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-mail            | řetězec                                   | Yes      | E-mailová adresa zákazníka                                                                                                                                                                                   |
| jazyková verze          | řetězec                                   | Yes      | Jejich preferovaná kultura komunikace a měny, například en-US. Podporované [Partnerské centrum v tématu Podporované jazyky](partner-center-supported-languages-and-locales.md) a národní prostředí. |
| language         | řetězec                                   | Yes      | Výchozí jazyk. Podporují se dva kódy znakových `en` jazyků (například `fr` nebo ).                                                                                                                                |
| název \_ společnosti    | řetězec                                   | Yes      | Název registrované společnosti nebo organizace.                                                                                                                                                                       |
| výchozí \_ adresa | [Adresa](utility-resources.md#address) | Yes      | Registrovaná adresa společnosti nebo organizace zákazníka. Informace o [omezeních](utility-resources.md#address) délky najdete v tématu Prostředek adresy.                                             |

#### <a name="company-profile"></a>Profil společnosti

Tato tabulka popisuje minimální povinná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) potřebná k vytvoření nového zákazníka.

| Název   | Typ   | Vyžadováno | Popis                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| doména | řetězec | Yes     | Název domény zákazníka, například contoso.onmicrosoft.com. |
| organizationRegistrationNumber | řetězec | Závisí na podměně. | Registrační číslo organizace zákazníka (v určitých zemích se také označuje jako číslo INN). <br/><br/>Vyplnění tohoto pole se vyžaduje pouze v případě, že se společnost nebo organizace zákazníka nachází v následujících zemích: <br/><br/>- Arménie (AM) <br/>– Az (Az)<br/>- Neschůdné (BY)<br/>– Šmídy (HU)<br/>– Šmídy (KZ)<br/>- Pohotový (KG)<br/>– Kaša (MD)<br/>– Rusko (RU)<br/>- Tádžovéstan (TJ)<br/>– Šmídy (UZ)<br/>– UA (Ka)<br/>– Indie <br/>– Brazílie <br/>– Jižní Afrika <br/>– Šátsko <br/>– United Kaskády <br/>– Saúdská Arábie <br/>– Kaša <br/>– Kaša <br/>– Vietnam <br/>- Selhot <br/>– Zamíscené <br/>– South Ára <br/>– Kaskády<br/> <br/>Pro společnost nebo organizaci zákazníka v jiných zemích se jedná o volitelné pole.  |

### <a name="request-example"></a>Příklad požadavku

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

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu odpověď obsahuje [prostředek zákazníka](customer-resources.md#customer) pro nového zákazníka.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Odpovědi mají stavový kód HTTP, který označuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

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