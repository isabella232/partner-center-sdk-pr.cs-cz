---
title: Vytvoření zákazníka pro nepřímého prodejce
description: Zjistěte, jak může nepřímý poskytovatel použít rozhraní API partnerského centra k vytvoření zákazníka pro nepřímý prodejce.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 0de40d08e9fc2b9cf87b7c3c41214fdd34ad26f3
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274576"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Vytvoření zákazníka pro nepřímý prodejce pomocí rozhraní API partnerského centra

**Platí pro:**

- Partnerské centrum

Nepřímý poskytovatel může vytvořit zákazníka pro nepřímý prodejce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- Identifikátor tenanta nepřímého prodejce.

- Nepřímý prodejce musí mít partnerství s nepřímým zprostředkovatelem.

## <a name="c"></a>C\#

Přidání nového zákazníka pro nepřímý prodejce:

1. Vytvořte instanci nového objektu [**zákazníka**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) a potom vytvořte instanci a naplňte [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) a [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile). Nezapomeňte přiřadit ID nepřímého prodejce k vlastnosti [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) .

2. K získání rozhraní pro operace shromažďování zákazníka použijte vlastnost [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) .

3. Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) vytvořte zákazníka.

### <a name="c-example"></a>\#Příklad C

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

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateCustomerforIndirectReseller. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                       |
|----------|-------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu žádosti.

| Název                                          | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | object | Yes      | Informace o fakturačním profilu zákazníka                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | object | Yes      | Informace o profilu společnosti zákazníka.                                                               
| [AssociatedPartnerId](customer-resources.md#customer) | řetězec | Yes      | ID nepřímého prodejce. Nepřímý prodejce, který je uveden zde, musí mít partnerství s nepřímým zprostředkovatelem nebo se požadavek nezdaří. Všimněte si také, že pokud není zadána hodnota AssociatedPartnerId, zákazník je vytvořen jako přímý zákazník nepřímého poskytovatele, nikoli jako nepřímý prodejce. |
|Doména| Řetězec| Yes|Název domény zákazníka, například contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    řetězec|Yes|     Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích). Požadované jenom pro společnost nebo organizaci zákazníka, která se nachází v následujících zemích: Arménská (AM), Ázerbájdžán (AZ), Bělorusko (BY), Maďarsko (HU), Kazachstán (KZ), Kyrgyzstán (KG), Moldavsko (MD), Rusko (RU), Tádžikistán (TJ), Uzbekistán (UZ), Ukrajina (UA), Indie, Brazílie, Jižní Afrika, Polsko, Spojené arabské emiráty, Saúdská Arábie, Turecko, Thajsko, Vietnam, Maďarsko, Jižní Súdán a Venezuela. Pro společnost nebo organizaci zákazníka nacházející se v jiných zemích je to volitelné pole.|



#### <a name="billing-profile"></a>Fakturační profil

Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerBillingProfile](customer-resources.md#customerbillingprofile) , který je potřeba k vytvoření nového zákazníka.

| Název             | Typ                                     | Vyžadováno | Popis                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-mail            | řetězec                                   | Yes      | E-mailová adresa zákazníka                                                                                                                                                                                   |
| jazyková verze          | řetězec                                   | Yes      | Upřednostňovaná jazyková verze pro komunikaci a měnu, jako je "en-US". Podporované jazykové verze najdete v tématu [podporované jazyky a národní prostředí partnerského centra](partner-center-supported-languages-and-locales.md) . |
| language         | řetězec                                   | Yes      | Výchozí jazyk. Jsou podporovány dva znakové kódy jazyka (například `en` nebo `fr` ).                                                                                                                                |
| \_název společnosti    | řetězec                                   | Yes      | Registrovaný název společnosti nebo organizace.                                                                                                                                                                       |
| výchozí \_ adresa | [Adresa](utility-resources.md#address) | Yes      | Registrovaná adresa společnosti nebo organizace zákazníka. Informace o omezeních délky najdete v tématu [adresa](utility-resources.md#address) prostředku.                                             |

#### <a name="company-profile"></a>Profil společnosti

Tato tabulka popisuje minimální požadovaná pole z prostředku [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) , který je potřeba k vytvoření nového zákazníka.

| Název   | Typ   | Vyžadováno | Popis                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| doména | řetězec | Yes     | Název domény zákazníka, například contoso.onmicrosoft.com. |
| organizationRegistrationNumber | řetězec | Závisí na podmínce | Registrační číslo organizace zákazníka (také označované jako DIČ v určitých zemích). <br/><br/>Toto pole se vyžaduje jenom v případě, že se společnost nebo organizace zákazníka nacházejí v následujících zemích: <br/><br/>– Arménská (AM) <br/>-Ázerbájdžán (AZ)<br/>-Bělorusko (do)<br/>-Maďarsko (HU)<br/>-Kazachstán (KZ)<br/>-Kyrgyzstán (KG)<br/>-Moldávie (MD)<br/>– Rusko (RU)<br/>-Tádžikistán (TJ)<br/>-Uzbekistán (UZ)<br/>– Ukrajina (UA)<br/>– Indie <br/>– Brazílie <br/>– Jižní Afrika <br/>– Polsko <br/>– Spojené arabské emiráty <br/>– Saúdská Arábie <br/>– Turecko <br/>– Thajsko <br/>– Vietnam <br/>– Myanmar <br/>– Irák <br/>– Jižní Súdán <br/>– Venezuela<br/> <br/>Pro společnost nebo organizaci zákazníka nacházející se v jiných zemích je to volitelné pole.  |

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

V případě úspěchu bude odpověď obsahovat [zákaznický](customer-resources.md#customer) prostředek pro nového zákazníka.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Odpovědi se dodávají se stavovým kódem HTTP, který označuje úspěch nebo neúspěch a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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