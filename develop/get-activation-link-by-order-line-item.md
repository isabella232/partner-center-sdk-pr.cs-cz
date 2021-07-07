---
title: Získání aktivačního odkazu podle položky řádku objednávky
description: Získá odkaz na aktivaci předplatného podle řádkové položky objednávky.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: aa02a5a5b4a281b96e32ee6d239cc440cf8af4ec
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760772"
---
# <a name="get-activation-link-by-order-line-item"></a>Získání aktivačního odkazu podle položky řádku objednávky

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Získá odkaz na aktivaci předplatného komerčního marketplace podle čísla položky řádku objednávky.

Na řídicím panelu Partnerské centrum můžete tuto operaci provést  výběrem  konkrétního předplatného v části Předplatné na hlavní stránce nebo výběrem odkazu Přejít na web **Publisher** vedle předplatného aktivovat na stránce Předplatná. 

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- Dokončená objednávka s produktem, který vyžaduje aktivaci.

## <a name="c"></a>C\#

Pokud chcete získat aktivační odkaz na řádkové položky, použijte kolekci [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s vybraným ID zákazníka. Potom zavolejte [**vlastnost Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a [**metodu ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) se zadaným  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id). Potom zavolejte [**metodu LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) s **byId()** s identifikátorem čísla položky řádku.  Nakonec zavolejte **metodu ActivationLinks().**

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato [](customer-resources.md#customer) metoda v textu odpovědi kolekci prostředků zákazníka.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
