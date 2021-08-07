---
title: Změna fakturačního cyklu
description: Zjistěte, jak aktualizovat předplatné zákazníka na měsíční nebo roční fakturaci pomocí Partnerské centrum API. Můžete to provést také z řídicího Partnerské centrum řídicího panelu.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: c45d599ace7895c03bc163cddde7cbb057ff60a06c58af39a2baacb3d557e72e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992156"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Změna fakturačního období zákaznického předplatného

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Aktualizuje objednávku [z](order-resources.md) měsíční na roční fakturaci nebo z roční na měsíční fakturaci.

Na Partnerské centrum můžete tuto operaci provést tak, že přejdete na stránku s podrobnostmi o předplatném zákazníka. Tam se zobrazí možnost, která definuje aktuální fakturační cyklus předplatného a umožňuje ho změnit a odeslat.

**Tento článek** je mimo rozsah:

- Změna fakturačního cyklu zkušebních období
- Změna fakturačních cyklů u všech neročního období nabídek (měsíčních, šestiletých) & předplatných Azure
- Změna fakturačních cyklů pro neaktivní předplatná
- Změna fakturačních cyklů pro předplatná Microsoft online služby založená na licencích

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID objednávky.

## <a name="c"></a>C\#

Pokud chcete změnit četnost fakturačního cyklu, aktualizujte [**vlastnost Order.BillingCycle.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)

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

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda    | Identifikátor URI žádosti                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **Oprava** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/orders/{ID_objednávky} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Tato tabulka uvádí požadovaný parametr dotazu pro změnu množství předplatného.

| Název                   | Typ | Vyžadováno | Popis                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **customer-tenant-id** | Identifikátor GUID |    Y     | Identifikátor GUID **naformátovaný jako customer-tenant-id,** který identifikuje zákazníka |
| **ID objednávky**           | Identifikátor GUID |    Y     | Identifikátor objednávky                                                 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Následující tabulky popisují vlastnosti v textu požadavku.

### <a name="order"></a>Objednávka

| Vlastnost           | Typ             | Vyžadováno | Popis                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | řetězec           |    N     | Identifikátor objednávky zadaný po úspěšném vytvoření objednávky |
|ReferenčníCustomerId | řetězec           |    Y     | Identifikátor zákazníka                                                    |
| BillingCycle       | řetězec           |    Y     | Určuje frekvenci, s jakou se partner účtuje za tuto objednávku. Podporované hodnoty jsou názvy členů, které najdete v [části BillingCycleType](product-resources.md#billingcycletype). |
| Položky řádku          | pole objektů |    Y     | Pole prostředků [OrderLineItem](#orderlineitem)                      |
| Datum vytvoření       | datetime         |    N     | Datum vytvoření objednávky ve formátu data a času                        |
| Atributy         | Objekt           |    N     | Obsahuje ObjectType: OrderLineItem.                                     |

### <a name="orderlineitem"></a>OrderLineItem (PoložkaŘádku Objednávky)

| Vlastnost             | Typ   | Vyžadováno | Popis                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | číslo |    Y     | Číslo položky řádku začínající 0                                              |
| ID nabídky              | řetězec |    Y     | ID nabídky                                                                |
| SubscriptionId       | řetězec |    Y     | ID předplatného                                                         |
| Friendlyname         | řetězec |    N     | Popisný název předplatného definovaného partnerem, který pomáhá jednoznačně definovat |
| Množství             | číslo |    Y     | Počet licencí nebo instancí                                                |
| Id partneraZáznam    | řetězec |    N     | ID MPN záznamu partnera                                                |
| Atributy           | Objekt |    N     | Obsahuje ObjectType: OrderLineItem.                                             |

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

V případě úspěchu vrátí tato metoda v textu odpovědi aktualizované pořadí odběru.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

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