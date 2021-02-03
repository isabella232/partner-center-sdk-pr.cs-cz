---
title: Změna fakturačního cyklu
description: Naučte se aktualizovat předplatné zákazníka na měsíční nebo roční fakturaci pomocí rozhraní API partnerského centra. Můžete to provést taky z řídicího panelu partnerského centra.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2020
ms.locfileid: "97767114"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Změna fakturačního cyklu zákaznického předplatného

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Aktualizuje [objednávku](order-resources.md) z měsíčního na roční fakturace nebo z roční na měsíční fakturaci.

Na řídicím panelu partnerského centra můžete tuto operaci provést přechodem na stránku s podrobnostmi o předplatném zákazníka. Po tomto případě se zobrazí možnost definující aktuální fakturační cyklus pro předplatné s možností změny a odeslání.

**Mimo rozsah** tohoto článku:

- Změna fakturačního cyklu pro zkušební verze
- Změna fakturačních cyklů pro jakékoli neroční nabídky za období (měsíčně, 6 let) & předplatných Azure
- Změna fakturačních cyklů pro neaktivní předplatná
- Změna fakturačních cyklů pro odběry založené na licencích Microsoft online služby

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID objednávky.

## <a name="c"></a>C\#

Chcete-li změnit četnost fakturačního cyklu, aktualizujte vlastnost [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) .

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **POUŽITA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Tato tabulka uvádí požadovaný parametr dotazu pro změnu množství předplatného.

| Název                   | Typ | Vyžadováno | Popis                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **Customer-tenant-ID** | Identifikátor GUID |    Y     | IDENTIFIKÁTOR zákazníka s formátováním **ID tenanta** , který identifikuje zákazníka |
| **ID objednávky**           | Identifikátor GUID |    Y     | Identifikátor objednávky                                                 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

V následujících tabulkách jsou popsány vlastnosti v textu požadavku.

### <a name="order"></a>Objednávka

| Vlastnost           | Typ             | Vyžadováno | Popis                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | řetězec           |    N     | Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky |
|ReferenceCustomerId | řetězec           |    Y     | Identifikátor zákazníka                                                    |
| BillingCycle       | řetězec           |    Y     | Určuje četnost, s jakou se má partner fakturovat v této objednávce. Podporované hodnoty jsou názvy členů nalezené v [BillingCycleType](product-resources.md#billingcycletype). |
| Položky řádku          | pole objektů |    Y     | Pole prostředků [OrderLineItem](#orderlineitem)                      |
| CreationDate       | datetime         |    N     | Datum vytvoření objednávky ve formátu data a času                        |
| Atributy         | Objekt           |    N     | Obsahuje ObjectType: "OrderLineItem"                                     |

### <a name="orderlineitem"></a>OrderLineItem

| Vlastnost             | Typ   | Vyžadováno | Popis                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | číslo |    Y     | Číslo položky řádku začínající na 0                                              |
| Hodnotami OfferId              | řetězec |    Y     | ID nabídky                                                                |
| SubscriptionId       | řetězec |    Y     | ID předplatného                                                         |
| FriendlyName         | řetězec |    N     | Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost |
| Množství             | číslo |    Y     | Počet licencí nebo instancí                                                |
| PartnerIdOnRecord    | řetězec |    N     | ID MPN partnera záznamu                                                |
| Atributy           | Objekt |    N     | Obsahuje ObjectType: "OrderLineItem"                                             |

### <a name="request-example"></a>Příklad požadavku

Aktualizace na roční fakturaci

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí aktualizované pořadí předplatného v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "Annual",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```