---
title: Akceptovat přenos předplatných
description: Naučte se používat REST API partnerského centra k přijetí přenosu předplatných pro zákazníka. Zahrnuje syntaxi žádostí REST, hlavičky a odpovědi REST.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd9a6788b3dd022470e516ba928a6cd873970e53
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/11/2020
ms.locfileid: "97767072"
---
# <a name="accept-a-transfer-of-subscriptions-for-a-customer-using-partner-center-rest-apis"></a>Přijetí přenosu předplatných pro zákazníka pomocí rozhraní REST API partnerského centra

**Platí pro:**

- Partnerské centrum

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor přenosu pro existující přenos.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers/{Transfer-ID}/Accept HTTP/1.1                    |

### <a name="uri-parameter"></a>Parametr URI

Použijte následující parametr cesty k identifikaci zákazníka a určení přenosu, který chcete přijmout.

| Název            | Typ     | Vyžadováno | Popis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID zákazníka** | řetězec   | Yes      | Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.             |
| **ID přenosu** | řetězec   | Yes      | Identifikátor ID přenosu, ve formátu GUID, který identifikuje přenos.             |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-example"></a>Příklad požadavku

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/aa2bddb6-9cc8-4949-80fe-a37d5e0a13ba/accept HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí naplněný prostředek [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 3389
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Date: Wed, 25 Mar 2020 19:13:06 GMT

{
  "orders": [
    {
      "id": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "alternateId": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "5344C201-3099-44E5-B333-C3EB0401EDE0",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Customer Engagement Plan (36 mo)",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:23.183+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6IjIxYjkyMzkzLWZmY2UtNGJjNy04N2M1LTYyY2ZhODk3ZDhmOSIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    },
    {
      "id": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "alternateId": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "1A90EE13-2CB4-4785-BB0F-542813F00A37",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Business Central Essential",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:34.59+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6Ijc0MTRiOGVhLWMxNjctNGNjNC1iYzhlLWI0M2VmYzE3N2E0NiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    }
  ],
  "transferErrors": [
    {
      "transferGroupId": "1",
      "lineItems": [
        {
          "id": 1,
          "subscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "entitlementId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "offerId": "A4179D30-CC09-49F0-977E-DC2CB70B874F",
          "friendlyName": "Project Online Essentials",
          "quantity": 1,
          "transferGroupId": "1",
          "addonItems": [ ],
          "partnerIdOnRecord": "5139005",
          "billingCycle": "annual",
          "sourceSubscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A"
        }
      ],
      "code": 900103,
      "description": "Subscription SyncState must be SyncComplete for the Subscription to be a source in a Subscription Ownership Transfer. Subscription: 637ff8f6-d842-4573-8da8-89765356cd1a, current state: None",
      "attributes": {
        "objectType": "TransferError"
      }
    }
  ],
  "attributes": {
    "objectType": "TransferSubmitResult"
  }
}
```
