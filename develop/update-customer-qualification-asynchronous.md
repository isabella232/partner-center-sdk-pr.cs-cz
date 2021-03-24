---
title: Aktualizace kvalifikace zákazníka
description: Provede asynchronní aktualizace kvalifikací zákazníka, včetně adresy přidružené k profilu.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 7606eeaac4df158ec0fad6ffd4e565bb250f448e
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030602"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Asynchronní aktualizace kvalifikací zákazníka

Asynchronně aktualizuje kvalifikace zákazníka.

Partner může provést asynchronní aktualizaci kvalifikací zákazníka, pokud jde o "vzdělávání" nebo "GovernmentCommunityCloud". Další hodnoty, "none" a "neziskové" nelze nastavit.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Chcete-li vytvořit kvalifikaci zákazníka pro "vzdělávání", nejprve vytvořte objekt reprezentující typ kvalifikace. Pak zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka. Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) . Nakonec zavolejte `CreateQualifications()` nebo `CreateQualificationsAsync()` s typem kvalifikace Object jako vstupní parametr.

``` csharp
var qualificationType = { Qualification = "education" };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Ukázka**: [ukázková aplikace konzoly](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: **Třída** SdkSamples: CreateCustomerQualification. cs

Pokud chcete aktualizovat kvalifikaci zákazníka tak, aby se **GovernmentCommunityCloud** na stávajícího zákazníkovi bez kvalifikace, partner taky musí zahrnovat [**ValidationCode**](utility-resources.md#validationcode)zákazníka. Nejprve vytvořte objekt reprezentující typ kvalifikace. Pak zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka. Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) . Nakonec volejte `CreateQualifications()` nebo `CreateQualificationsAsync()` s objektem typu kvalifikace a ověřovacím kódem jako vstupní parametry.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Ukázka**: [ukázková aplikace konzoly](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: **Třída** SdkSamples: CreateCustomerQualificationWithGCC. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer_ID}/Qualifications? kód = {VALIDATIONCODE} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K aktualizaci kvalifikace použijte následující parametr dotazu.

| Název                   | Typ | Vyžadováno | Popis                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | Identifikátor GUID | Yes      | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci. |
| **validationCode**     | int  | No       | Je potřeba jenom pro cloudovou komunitu státní správy.                                                                                                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje objekt kvalifikace v textu požadavku.

Vlastnost | Typ | Vyžadováno | Popis
-------- | ---- | -------- | -----------
Qualification | řetězec | Yes | Hodnota řetězce z výčtu [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .

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

V případě úspěchu tato metoda vrátí objekt kvalifikace v těle odpovědi. Níže je uveden příklad volání **post** na zákazníka (s předchozí kvalifikací **none**) s kvalifikací **vzdělávání** .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

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
