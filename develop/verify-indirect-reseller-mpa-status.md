---
title: Ověření stavu podepisování smlouvy Microsoft Partner pro nepřímý prodejce
description: Pomocí rozhraní AgreementStatus API můžete ověřit, jestli se nepřímý prodejce zaregistroval v rámci smlouvy o partnerovi Microsoftu.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9501f245a6c98fa90e77de7bc0caed8ca51fa4f2
ms.sourcegitcommit: 40baf4d825ce0ca6a254b5f368c308f025be7034
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/16/2021
ms.locfileid: "100537572"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Ověření stavu podepisování smlouvy Microsoft Partner pro nepřímý prodejce

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud for US Government

Můžete ověřit, jestli nepřímý prodejce podepsal smlouvu s partnerem Microsoftu pomocí svého Microsoft Partner Network (MPN) ID (PGA/PLA) nebo ID tenanta Cloud Solution Provider (Microsoft ID). Jeden z těchto identifikátorů můžete použít ke kontrole stavu podepisování smlouvy Microsoft Partner pomocí rozhraní **AgreementStatus** API.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID MPN (PGA/PLA) nebo ID tenanta CSP (Microsoft ID) nepřímého prodejce. *Je nutné použít jeden z těchto dvou identifikátorů.*

## <a name="c"></a>C\#

Postup získání stavu podpisu partnerské smlouvy Microsoftu pro nepřímý prodejce:

1. Pomocí kolekce **IAggregatePartner. dodržování předpisů** zavolejte vlastnost **AgreementSignatureStatus** .

2. Zavolejte metodu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) .

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Ukázka: **[aplikace testů konzoly](console-test-app.md)**
- Projekt: **PartnerCenterSDK. FeaturesSamples**
- Třída: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti |
| ------ | ----------- |
| **Čtěte** | *[{baseURL}](partner-center-rest-urls.md)*/v1/Compliance/{programname}/agreementstatus? mpnId = {mpnId} &tenantId = {tenantId} |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Chcete-li identifikovat partnera, je nutné zadat jeden z následujících dvou parametrů dotazu. Pokud neposkytnete jeden z těchto dvou parametrů dotazu, zobrazí se chyba **400 (chybná žádost)** .

| Název | Typ | Vyžadováno | Popis |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | Ne | ID Microsoft Partner Network (PGA/PLA), které identifikuje nepřímý prodejce. |
| **TenantId** | Identifikátor GUID | Ne | ID společnosti Microsoft, které identifikuje účet CSP nepřímého prodejce. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v [partnerském centru REST](headers.md).

### <a name="request-examples"></a>Příklady požadavků

#### <a name="request-using-mpn-id-pgapla"></a>Žádost s použitím ID MPN (PGA/PLA)

Následující příklad žádosti získá nepřímý prodejce na stav podepisování smlouvy o partnerovi Microsoftu pomocí Microsoft Partner Network ID nepřímého prodejce.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>Žádost o použití ID tenanta CSP

Následující příklad žádosti získá nepřímý prodejce na stav podepisování smlouvy o partnerovi Microsoftu pomocí ID tenanta CSP nepřímého prodejce (Microsoft ID).

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

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [Chyba REST partnerského centra](error-codes.md).

### <a name="response-example-success"></a>Příklad odpovědi (úspěch)

Následující příklad odpovědi úspěšně vrátí, jestli nepřímý prodejce podepsal smlouvu s partnerem Microsoftu.

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

### <a name="response-examples-failure"></a>Příklady odezvy (neúspěch)

Pokud stav podepisování smlouvy Microsoft Partner na nepřímý prodejce nemůžete vrátit, můžete dostávat odpovědi podobné následujícím příkladům.

#### <a name="non-guid-formatted-csp-tenant-id"></a>ID tenanta CSP naformátovaného jiným IDENTIFIKÁTORem

V případě, že ID tenanta CSP, které jste předali do rozhraní API, není identifikátor GUID, vrátí se následující příklad odpovědi.

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

#### <a name="non-numeric-mpn-id"></a>ID programu MPN, které není číselné

Následující příklad odpovědi se vrátí, když ID MPN (PGA/PLA), které jste předali do rozhraní API, není číselné.

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

Následující příklad odpovědi se vrátí, když jste neprošli předáním ID MPN (PGA/PLA) nebo ID tenanta CSP do rozhraní API. Do rozhraní API musíte předat jeden ze dvou typů ID.

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Bylo předáno ID MPN i ID tenanta CSP.

Následující příklad odpovědi je vrácen při předání ID MPN (PGA/PLA) a ID tenanta CSP do rozhraní API. Rozhraní API musíte předat *jenom jeden* ze dvou typů identifikátorů.

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>ID programu MPN pro nepřímý prodej CSP (PGA/PLA) není platné nebo se nemigruje z partnerského centra pro členství do partnerského centra.

Následující příklad odpovědi se vrátí, když předaný nepřímý prodejce MPN (PGA/PLA) buď není platný, nebo není migrován z partnerského centra členství v partnerském centru. [Další informace](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>Oblast nepřímých poskytovatelů CSP a oblast nepřímých prodejců CSP se neshoduje.

Následující příklad odpovědi se vrátí, pokud oblast nepřímých prodejců (PGA/PLA) neodpovídá oblasti nepřímého zprostředkovatele. [Přečtěte si další informace](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq) o oblastech CSP.

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

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>Účet nepřímého prodejce CSP existuje v partnerském centru, ale nepodepsal aktivaci.

Následující příklad odpovědi se vrátí, když účet nepřímý prodejce CSP v partnerském centru nepodepsal aktivaci. [Další informace](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

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

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>K danému ID MPN není přidružený žádný účet nepřímý prodejce CSP.

Následující příklad odpovědi se vrátí, když partnerské Centrum dokáže rozpoznat ID MPN (PGA/PLA) předané v žádosti, ale k danému ID MPN (PGA/PLA) se nepřidruží žádný zápis CSP. [Další informace](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

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

Následující příklad odpovědi se vrátí, když Partnerská centra nenajde žádný účet přidružený k ID tenanta předanému v žádosti.

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Nenašly se žádné technologie MPA s daným ID tenanta.

Následující příklad odpovědi se vrátí, když Partnerská centra nemůže najít žádný signaturu technologie MPA s daným ID tenanta. [Další informace](https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq)

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
