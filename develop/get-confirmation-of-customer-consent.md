---
title: Získání potvrzení přijetí Smlouvy o službách Microsoft Cloud ze strany zákazníka
description: Tento článek vysvětluje, jak získat potvrzení souhlasu zákazníka s Smlouva o službách Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: 1b1a8cbacb667e579bcd218a29c3f553afce26c2
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549259"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>Získání potvrzení přijetí Smlouvy o službách Microsoft Cloud ze strany zákazníka

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **smlouvy** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu.

## <a name="prerequisites"></a>Požadavky

- Pokud používáte sadu .NET SDK Partnerské centrum, vyžaduje se verze 1.9 nebo novější.

- Pokud používáte sadu Java SDK Partnerské centrum, vyžaduje se verze 1.8 nebo novější.

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](./partner-center-authentication.md) Tento scénář podporuje pouze ověřování aplikací a uživatelů.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="net-version-14-or-newer"></a>.NET (verze 1.4 nebo novější)

Získání potvrzení přijetí zákazníkem, která byla dříve poskytnuta:

- Použijte kolekci **IAggregatePartner.Customers** a zavolejte **metodu ById** se zadaným identifikátorem zákazníka.

- **Načítá** vlastnost Agreements a filtruje výsledky, Smlouva o službách Microsoft Cloud voláním **metody ByAgreementType.**

- Volejte **metodu Get** **nebo GetAsync.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Úplnou ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [konzolové testovací](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) aplikace.

## <a name="net-version-19---113"></a>.NET (verze 1.9 – 1.13)

Pokud chcete načíst potvrzení o přijetí zákazníkem, které jste uvedli dříve:

Použijte kolekci **IAggregatePartner.Customers** a zavolejte metodu **ById** s identifikátorem zadaného zákazníka. Pak získejte vlastnost **Agreements** a potom voláním **metod Get** nebo **GetAsync.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pokud chcete načíst potvrzení o přijetí zákazníkem, které jste uvedli dříve:

Použijte funkci **IAggregatePartner.getCustomers** a zavolejte funkci **byId** s identifikátorem zadaného zákazníka. Pak získejte **funkci getAgreements** a potom zavoláte **funkci get.**

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

Úplnou ukázku najdete ve třídě [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) z projektu [konzolové testovací](https://github.com/Microsoft/Partner-Center-Java-Samples) aplikace.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pokud chcete načíst potvrzení o přijetí zákazníkem, které jste uvedli dříve:

Použijte příkaz [**Get-PartnerCustomerAgreement.**](/powershell/module/partnercenter/get-partnercustomeragreement)

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a>Požadavek REST

Pokud chcete získat potvrzení o přijetí zákazníkem, které jste uvedli dříve, přečtěte si následující pokyny.

Vytvořte nový prostředek **smlouvy** s příslušnými certifikačními informacemi.

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/smlouvy HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Pomocí následujícího parametru dotazu zadejte zákazníka, který potvrzujete.

| Název             | Typ | Vyžadováno | Popis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | Identifikátor GUID | Y        | Hodnota je identifikátor GUID naformátovaný **jako CustomerTenantId,** který umožňuje zadat zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato  metoda v textu odpovědi kolekci prostředků smlouvy.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
