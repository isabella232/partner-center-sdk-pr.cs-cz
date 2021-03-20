---
title: Aktualizace kvalifikace zákazníka
description: Naučte se aktualizovat kvalifikace zákazníka prostřednictvím synchronního screeningu nebo dozvíte ČSFD, včetně adresy přidružené k profilu.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c202d95beab771241a9665243be5f08ab6f82fd5
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711963"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a>Aktualizace kvalifikace zákazníka prostřednictvím synchronního ověřování

**Platí pro**

- Partnerské centrum

Naučte se synchronně aktualizovat kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra. Informace o tom, jak to provést asynchronně, najdete v tématu [aktualizace kvalifikace zákazníka prostřednictvím asynchronního ověřování](update-customer-qualification-asynchronous.md).

Partner může aktualizovat kvalifikaci zákazníka na "vzdělávání" nebo "GovernmentCommunityCloud". Další hodnoty, "none" a "neziskové" nelze nastavit.

## <a name="prerequisites"></a>Předpoklady

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Pokud chcete aktualizovat kvalifikaci zákazníka na "vzdělávání", zavolejte **[Update/dotnet/API/Microsoft. Store. partnercenter. kvalifikaci. icustomerqualification. Update)** na stávajícím  [**zákazníkovi**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: PartnerSDK. FeatureSamples **Třída**: CustomerQualificationOperations. cs

Aktualizace kvalifikace zákazníka tak, aby se **GovernmentCommunityCloud** na stávajícího zákazníkovi bez kvalifikace.  Partner je taky nutný k zahrnutí [**ValidationCode**](utility-resources.md#validationcode)zákazníka.

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer_ID}/Qualification? kód = {VALIDATIONCODE} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K aktualizaci kvalifikace použijte následující parametr dotazu.

| Název                   | Typ | Vyžadováno | Popis                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | Identifikátor GUID | Yes      | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci. |
| **validationCode**     | int  | No       | Je potřeba jenom pro cloudovou komunitu státní správy.                                                                                                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Celočíselná hodnota z výčtu [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .

### <a name="request-example"></a>Příklad požadavku

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí aktualizovanou vlastnost [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

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