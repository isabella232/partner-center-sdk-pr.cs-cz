---
title: Aktualizace kvalifikace zákazníka
description: Zjistěte, jak aktualizovat kvalifikace zákazníka prostřednictvím synchronního prověřování nebo prověřování, včetně adresy přidružené k profilu.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446645"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a>Aktualizace kvalifikace zákazníka prostřednictvím synchronního ověření

Zjistěte, jak synchronně aktualizovat kvalifikace zákazníka prostřednictvím Partnerské centrum API. Informace o tom, jak to provést asynchronně, najdete v tématu Aktualizace kvalifikace zákazníka [prostřednictvím asynchronního ověřování](update-customer-qualification-asynchronous.md).

Partner může aktualizovat kvalifikace zákazníka na "Vzdělávání" nebo "GovernmentCommunityCloud". Ostatní hodnoty None (Žádný) a Nonprofit (Neziskové organizace) nelze nastavit.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Pokud chcete aktualizovat kvalifikace zákazníka na "Vzdělávání", zavolejte **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** u stávajícího  [**zákazníka**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** PartnerSDK.FeatureSamples **– třída:** CustomerQualificationOperations.cs

Pokud chcete aktualizovat kvalifikace zákazníka na **GovernmentCommunityCloud** u stávajícího zákazníka bez kvalifikace, musí partner zahrnout ověřovací kód [**zákazníka.**](utility-resources.md#validationcode)

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K aktualizaci kvalifikace použijte následující parametr dotazu.

| Název                   | Typ | Vyžadováno | Popis                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | Identifikátor GUID | Yes      | Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci. |
| **validationCode (kód ověření)**     | int  | No       | Je potřeba jenom pro Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Celočíselná hodnota z [**výčtu CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)

### <a name="request-example"></a>Příklad požadavku

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v textu odpovědi [**aktualizovanou**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) vlastnost Kvalifikace.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a>Související články

- [Získání kvalifikace zákazníka](./get-customer-qualification-synchronous.md)
- [Získání ověřovacích kódů partnera](get-a-partner-s-validation-codes.md)
