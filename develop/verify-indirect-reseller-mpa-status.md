---
title: Ověření stavu podepisování Smlouva s partnerem Microsoftu prodejce
description: Pomocí rozhraní AGREEMENTStatus API můžete ověřit, jestli nepřímý prodejce smlouvu Smlouva s partnerem Microsoftu.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f83acc61624a72354c390905b1250bc021dd39aa
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529830"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Ověření stavu podepisování Smlouva s partnerem Microsoftu prodejce

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud for US Government

Pomocí ID tenanta (Microsoft ID) Microsoft Partner Network (PGA/PLA) nebo CLOUD SOLUTION PROVIDER (CSP) můžete ověřit, jestli nepřímý prodejce smlouvu Smlouva s partnerem Microsoftu podepsal. Pomocí jednoho z těchto identifikátorů můžete zkontrolovat stav podepisování Smlouva s partnerem Microsoftu pomocí rozhraní **AgreementStatus** API.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID MPN (PGA/PLA) nebo ID tenanta CSP (Microsoft ID) nepřímého prodejce. *Musíte použít jeden z těchto dvou identifikátorů.*

## <a name="c"></a>C\#

Získání stavu Smlouva s partnerem Microsoftu podpisu nepřímého prodejce:

1. Pomocí kolekce **IAggregatePartner.Compliance** zavolejte vlastnost **AgreementSignatureStatus.**

2. Volejte [**metodu Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Ukázka: **[Konzolová testovací aplikace](console-test-app.md)**
- Project: **PartnerCenterSDK.FeaturesSamples**
- Třída: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda | Identifikátor URI žádosti |
| ------ | ----------- |
| **Dostat** | *[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{Název Programu}/agreementstatus?mpnId={MpnId}&tenantId={ID tenanta} |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci partnera musíte zadat jeden z následujících dvou parametrů dotazu. Pokud jeden z těchto dvou parametrů dotazu nezadáte, zobrazí se **chyba 400 (Chybný** požadavek).

| Název | Typ | Vyžadováno | Popis |
| ---- | ---- | -------- | ----------- |
| **ID mpn** | int | No | ID Microsoft Partner Network (PGA/PLA), které identifikuje nepřímého prodejce. |
| **ID tenanta** | Identifikátor GUID | No | Id Microsoftu, které identifikuje účet CSP nepřímého prodejce. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [Partnerské centrum REST.](headers.md)

### <a name="request-examples"></a>Příklady požadavků

#### <a name="request-using-mpn-id-pgapla"></a>Žádost s využitím ID MPN (PGA/PLA)

Následující příklad požadavku získá stav podepisování Smlouva s partnerem Microsoftu nepřímého prodejce s použitím ID Microsoft Partner Network prodejce.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>Žádost s využitím ID tenanta CSP

Následující příklad požadavku získá stav podepisování Smlouva s partnerem Microsoftu nepřímého prodejce pomocí ID tenanta CSP nepřímého prodejce (Microsoft ID).

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v Partnerské centrum [REST.](error-codes.md)

### <a name="response-example-success"></a>Příklad odpovědi (úspěch)

Následující příklad odpovědi úspěšně vrátí, jestli nepřímý prodejce smlouvu Smlouva s partnerem Microsoftu.

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a>Příklady odpovědí (selhání)

Odpovědi podobné následujícím příkladům můžete dostávat v případě, že stav podepisování nepřímého prodejce Smlouva s partnerem Microsoftu nelze vrátit.

#### <a name="non-guid-formatted-csp-tenant-id"></a>ID tenanta CSP, který není formátovaný guid

Následující příklad odpovědi se vrátí, když ID tenanta CSP, které jste předáli rozhraní API, není identifikátor GUID.

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a>Necílové ID MPN

Následující příklad odpovědi se vrátí, když ID MPN (PGA/PLA), které jste předali rozhraní API, není číselné.

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a>Žádné ID MPN nebo ID tenanta CSP

Následující příklad odpovědi se vrátí, když do rozhraní API předáte ID MPN (PGA/PLA) nebo ID tenanta CSP. Rozhraní API musíte předat jeden ze dvou typů ID.

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Předané ID tenanta MPN i ID tenanta CSP

Následující příklad odpovědi se vrátí, když do rozhraní API předáte ID MPN (PGA/PLA) i ID tenanta CSP. Rozhraní API *musíte předat* pouze jeden ze dvou typů identifikátorů.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>CSP Indirect Reseller ID MPN (PGA/PLA) je neplatné nebo se nemigruje z Partner Membership Center na Partnerské centrum

Následující příklad odpovědi se vrátí, když je předané ID MPN nepřímého prodejce (PGA nebo PLA) neplatné nebo se nemigruje z Partner Membership Center na Partnerské centrum. [Další informace](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>CSP Indirect Provider oblasti CSP Indirect Reseller oblasti se neshodují.

Následující příklad odpovědi se vrátí, když se oblast ID MPN nepřímého prodejce (PGA/PLA) neshoduje s oblastí nepřímého poskytovatele. [Přečtěte si další](/partner-center/mpa-indirect-provider-faq) informace o oblastech CSP.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>CSP Indirect Reseller účet existuje v Partnerské centrum, ale ještě nepodepsal MPA.

Následující příklad odpovědi se vrátí, CSP Indirect Reseller účet v Partnerské centrum ještě podepsání MPA. [Další informace](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>K CSP Indirect Reseller ID MPN není přidružený žádný účet.

Následující příklad odpovědi se vrátí, když Partnerské centrum rozpozná ID MPN (PGA/PLA) předané v požadavku, ale k danému ID MPN (PGA/PLA) není přidružená žádná registrace CSP. [Další informace](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a>Neplatné ID tenanta

Následující příklad odpovědi se vrátí, Partnerské centrum nenajde žádný účet přidružený k ID tenanta předané v požadavku.

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>S daným ID tenanta se nenašlo žádné MPA

Následující příklad odpovědi se vrátí, Partnerské centrum nemůže najít žádný podpis MPA s daným ID tenanta. [Další informace](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```