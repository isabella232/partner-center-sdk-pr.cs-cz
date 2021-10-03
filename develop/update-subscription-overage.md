---
title: Aktualizuje nadlimitní využití pro daného zákazníka.
description: Aktualizuje nadlimitní využití pro daného zákazníka.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 58590a1882cfe94ddd9779f9e9f766f3e62cffd6
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/02/2021
ms.locfileid: "129383438"
---
# <a name="update-overage"></a>Aktualizovat nadlimitní využití

**Platí pro**

- Partnerské centrum

**Příslušné role**

- Globální správce
- Agent správce

> [!Note] 
> nové obchodní změny jsou aktuálně k dispozici pouze partnerům, kteří jsou součástí Microsoft 365/Dynamics 365 new Commerce experience technical preview.

Slouží k nastavení překročení pro daného zákazníka na předplatné spotřeby. Lze ji také použít k odebrání nadlimitního využití nastavením na hodnotu false (NEPRAVDA). Nadlimitní služba umožňuje zákazníkům i nadále používat služby, pokud používají službu nad rámec stanovených limitů. Nadlimitní využití vymezuje průběžné platby za využívání předplatného, které se budou nacházet.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Jedno ID předplatného pro přechodné předplatné.

## <a name="rest-request"></a>Žádost REST
[PUT]/Customers/{Customer-tenant-ID}/Subscriptions/overage
### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/overage HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Pokud chcete vrátit nadlimitní využití zákazníka, použijte následující parametry dotazu.

| Název                    | Typ     | Vyžadováno | Popis                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Customer-tenant-ID**  | **guid** | Y        | Identifikátor GUID odpovídající tenantovi zákazníka.             |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku


| Název                    | Typ     | Description                                       |
|-------------------------|----------|---------------------------------------------------|
| **azureEntitlementId**  | **guid** | Identifikátor GUID definující předplatné spotřeby pro nadlimitní využití             |
| **partnerId**  | **guid** | ID MPN nepřímého prodejce Dá se použít jenom pro model dvou vrstev (nepřímý zprostředkovatel).            |

| **overageEnabled**   |  **bool** | Definuje, jestli je pro dané předplatné spotřeby povolené nadlimitní využití.             |


### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "overageEnabled": true
}

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda nadlimitní využití pro zákazníka.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "type": "PhoneServices",
    "overageEnabled": true,
    "links": {
        "overage": {
            "uri": "/customers/f62cf10b-8f76-4fc4-9774-c5291f8faf86/subscriptions/overage",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Overage"
    }
}
```
