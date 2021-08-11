---
title: Aktualizace kvalifikace zákazníka
description: Asynchronně aktualizuje kvalifikace zákazníka, včetně adresy přidružené k profilu.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 6d46d6a170e4ebcd441e678c482469c4041b2435bf7ee946dc91db554ec4932a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997953"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Asynchronní aktualizace kvalifikace zákazníka

Aktualizuje kvalifikace zákazníka asynchronně.

Partner může asynchronně aktualizovat kvalifikace zákazníka tak, aby byla "Vzdělávání" nebo "GovernmentCommunityCloud". Ostatní hodnoty None (Žádný) a Nonprofit (Neziskové organizace) nelze nastavit.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Pokud chcete vytvořit kvalifikaci zákazníka pro "Vzdělávání", nejprve vytvořte objekt představující typ kvalifikace. Potom zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka. Potom pomocí [**vlastnosti Kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Nakonec zavolejte `CreateQualifications()` nebo `CreateQualificationsAsync()` s objektem typu kvalifikace jako vstupním parametrem.

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Ukázka:** [Konzolová ukázková aplikace](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples **– třída:** CreateCustomerQualification.cs

Pokud chcete aktualizovat kvalifikace zákazníka na **GovernmentCommunityCloud** u stávajícího zákazníka bez kvalifikace, musí partner také zahrnout ověřovací kód [**zákazníka.**](utility-resources.md#validationcode) Nejprve vytvořte objekt představující typ kvalifikace. Potom zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka. Potom pomocí [**vlastnosti Kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Nakonec zavolejte metodu nebo s objektem typu kvalifikace a `CreateQualifications()` `CreateQualificationsAsync()` ověřovacím kódem jako vstupními parametry.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Ukázka:** [Konzolová ukázková aplikace](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples **– třída:** CreateCustomerQualificationWithGCC.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K aktualizaci kvalifikace použijte následující parametr dotazu.

| Název                   | Typ | Vyžadováno | Popis                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | Identifikátor GUID | Yes      | Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci. |
| **validationCode (kód ověření)**     | int  | No       | Je potřeba jenom pro Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje objekt kvalifikace v textu požadavku.

Vlastnost | Typ | Vyžadováno | Popis
-------- | ---- | -------- | -----------
Qualification | řetězec | Yes | Řetězcová hodnota z [**výčtu CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v textu odpovědi objekt kvalifikace. Níže je příklad volání **POST** na zákazníka (s předchozí **kvalifikaceí None**) s **kvalifikaceí Education.**

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a>Související články

- [Získání kvalifikace zákazníka](./get-customer-qualification-asynchronous.md)
- [Získání ověřovacích kódů partnera](get-a-partner-s-validation-codes.md)
