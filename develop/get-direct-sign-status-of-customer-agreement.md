---
title: Získejte stav přímého podepisování zákazníka pro zákaznickou smlouvu Microsoftu.
description: Pomocí prostředku DirectSignedCustomerAgreementStatus můžete získat stav přímého podepisování zákazníka (přímé přijetí) smlouvy o zákaznících Microsoftu.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766664"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Získání stavu přímého podepisování zákazníka (přímé přijetí) smlouvy o zákaznících Microsoftu

**Platí pro:**

- Partnerské centrum

Partner Center v současné době podporuje prostředek **DirectSignedCustomerAgreementStatus** jenom ve veřejném cloudu Microsoftu.

Tento prostředek *nelze použít* pro:

- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek vysvětluje, jak můžete načíst stav přímého přijetí smlouvy o zákaznících Microsoftu v rámci zákazníka.

## <a name="rest-request"></a>Žádost REST

Pokud chcete načíst stav přímého souhlasu zákazníka s zákaznickou smlouvou Microsoftu, vytvořte žádost REST, která načte [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) pro zákazníka.

### <a name="request-syntax"></a>Syntaxe žádosti

Použijte následující syntaxi žádosti:

| Metoda | Identifikátor URI žádosti                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

S vaším požadavkem můžete použít následující parametry identifikátoru URI:

| Název             | Typ | Vyžadováno | Popis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| Customer-tenant-ID | Identifikátor GUID | Yes | Hodnota je **CustomerTenantId** ve formátu GUID, který umožňuje určit ID tenanta zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek [ **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) v těle odpovědi.

Prostředek má vlastnost **podepsatelných** , která označuje stav přímého podepisování (přímého přijetí) zákazníka.

- Hodnota **true** označuje, že smlouva byla podepsána (přijata) přímo zákazníkem.

- Hodnota **false** znamená, že *smlouva nebyla* podepsána (přijata) přímo zákazníkem.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.

Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
