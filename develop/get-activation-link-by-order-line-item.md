---
title: Získání aktivačního odkazu podle položky řádku objednávky
description: Načte odkaz na aktivaci předplatného podle pořadí položek řádku.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c0e84888870571cf6bd21306f527863f2aa7ee85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766840"
---
# <a name="get-activation-link-by-order-line-item"></a>Získání aktivačního odkazu podle položky řádku objednávky

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Získá odkaz na aktivaci předplatného komerčního webu Marketplace číslem položky řádku objednávky.

Na řídicím panelu partnerského centra můžete tuto operaci provést výběrem **konkrétního předplatného** na **hlavní** stránce nebo výběrem odkazu **Přejít na web vydavatele** vedle předplatného, které chcete aktivovat na stránce **předplatná** .

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- Bylo dokončeno pořadí s produktem, který vyžaduje aktivaci.

## <a name="c"></a>C\#

Chcete-li získat aktivační odkaz na řádkovou položku, použijte svou kolekci [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s vybraným ID zákazníka. Pak zavolejte vlastnost [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) se zadaným pořadím  [**ČísloObjednávky**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id). Pak zavolejte [**položky řádku**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) s metodou **ById ()** s identifikátorem položky řádku.  Nakonec zavolejte metodu **ActivationLinks ()** .

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customerId}/Orders/{OrderID}/LineItems/{lineItemNumber}/activationlinks HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu tato metoda vrátí kolekci [zákaznických](customer-resources.md#customer) prostředků v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

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
