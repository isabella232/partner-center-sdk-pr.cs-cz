---
title: Nákup doplňku k předplatnému
description: Jak zakoupit doplněk do stávajícího předplatného.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8b700a2ad41a37ca0ad745f3e7767449974b18a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547678"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Nákup doplňku k předplatnému

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government

Jak zakoupit doplněk do stávajícího předplatného.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného. Toto je stávající předplatné, pro které se má koupit nabídka doplňku.

- ID nabídky, která identifikuje nabídku doplňku k nákupu.

## <a name="purchasing-an-add-on-through-code"></a>Nákup doplňku prostřednictvím kódu

Při nákupu doplňku k předplatnému se aktualizuje původní pořadí předplatného s pořadím pro doplněk. V následujícím seznamu je KódZákazníka ID zákazníka, subscriptionId je ID předplatného a addOnOfferId je ID nabídky pro doplněk.

Tady je postup:

1.  Získejte rozhraní pro operace pro předplatné.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Pomocí tohoto rozhraní můžete vytvořit instanci objektu předplatného. Tím získáte podrobnosti o nadřazeném předplatném, včetně ID objednávky.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Vytvoří instanci objektu New [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) . Tato instance objednávky se používá k aktualizaci původního pořadí používaného k zakoupení předplatného. Přidejte do pořadí, který představuje doplněk, jednu položku s jedním řádkem.
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  Aktualizuje původní pořadí pro předplatné s novým pořadím pro doplněk.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Chcete-li zakoupit doplněk, Začněte získáním rozhraní pro operace předplatného voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, který identifikuje zákazníka, a pomocí metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pro identifikaci předplatného, které obsahuje nabídku doplňku. Použijte toto [**rozhraní**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) k načtení podrobností o předplatném voláním [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Podrobnosti o předplatném obsahují ID objednávky pořadí předplatného, což je pořadí, v jakém se má doplněk aktualizovat.

Dále vytvořte instanci objektu New [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) a naplňte ji jednou instancí [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) , která obsahuje informace pro identifikaci doplňku, jak je znázorněno v následujícím fragmentu kódu. Pomocí tohoto nového objektu aktualizujete pořadí předplatného pomocí doplňku. Nakonec zavolejte metodu [**patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) a aktualizujte pořadí předplatného, a to po prvním identifikaci zákazníka pomocí [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) a ORDER by Order [**. ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: **třída** microsoft Partner SDK samples: AddSubscriptionAddOn. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **POUŽITA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka a objednávky použijte následující parametry.

| Název                   | Typ     | Vyžadováno | Popis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka (zákazníka** ), který identifikuje zákazníka. |
| **ID objednávky**           | **guid** | Y        | Identifikátor objednávky.                                                              |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

V následujících tabulkách jsou popsány vlastnosti v textu požadavku.

## <a name="order"></a>Objednávka

| Název                | Typ             | Vyžadováno | Popis                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | řetězec           | N        | ID objednávky                                        |
| ReferenceCustomerId | řetězec           | Y        | ID zákazníka.                                     |
| Položky řádku           | pole objektů | Y        | Pole objektů [OrderLineItem](#orderlineitem) |
| CreationDate        | řetězec           | N        | Datum vytvoření objednávky ve formátu data a času. |
| Atributy          | object           | N        | Obsahuje "ObjectType": "Order".                      |

## <a name="orderlineitem"></a>OrderLineItem

| Název                 | Typ   | Vyžadováno | Popis                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | číslo | Y        | Číslo položky řádku začínající na 0.                       |
| Hodnotami OfferId              | řetězec | Y        | ID nabídky doplňku                                  |
| SubscriptionId       | řetězec | N        | ID zakoupeného předplatného doplňku.                 |
| ID nadřazeného odběru | řetězec | Y        | ID nadřazeného předplatného, které má nabídku doplňku. |
| Friendlyname         | řetězec | N        | Popisný název této řádkové položky.                        |
| Množství             | číslo | Y        | Počet licencí                                      |
| Id partneraZáznam    | řetězec | N        | ID MPN záznamu partnera.                         |
| Atributy           | object | N        | Obsahuje "ObjectType": "OrderLineItem".                      |

### <a name="request-example"></a>Příklad požadavku

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
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
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

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

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
    "billingCycle": "none",
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
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
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
