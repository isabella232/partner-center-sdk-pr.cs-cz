---
title: Nákup doplňku k předplatnému
description: Jak zakoupit doplněk k existujícímu předplatnému
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5227b917faf663c129b1abed1d10318620667e9b47524eb8c91867fb6b453ee8
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997358"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Nákup doplňku k předplatnému

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government

Jak zakoupit doplněk k existujícímu předplatnému

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného. Jedná se o stávající předplatné, pro které si můžete koupit nabídku doplňku.

- ID nabídky, které identifikuje nabídku doplňku k nákupu.

## <a name="purchasing-an-add-on-through-code"></a>Zakoupení doplňku prostřednictvím kódu

Když zakoupíte doplněk k předplatnému, aktualizujete původní objednávku předplatného pomocí objednávky doplňku. V následujícím příkladu je customerId ID zákazníka, subscriptionId je ID předplatného a addOnOfferId je ID nabídky pro doplněk.

Tady je postup:

1.  Získejte rozhraní pro operace předplatného.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Pomocí tohoto rozhraní můžete vytvořit instanci objektu předplatného. Tím se zobrazí podrobnosti nadřazeného předplatného, včetně ID objednávky.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Vytvořte instanci nového [**objektu Order.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) Tato instance objednávky slouží k aktualizaci původní objednávky použité k nákupu předplatného. Přidejte jedno řádkové položky do pořadí, které představuje doplněk.
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

4.  Aktualizujte původní objednávku předplatného o novou objednávku doplňku.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Pokud si chcete koupit doplněk, začněte tím, že získáte rozhraní pro operace s předplatným voláním metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, abyste zákazníka identifikovali, a metodu [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) k identifikaci předplatného, které má nabídku doplňku. Pomocí tohoto [**rozhraní**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) můžete načíst podrobnosti o předplatném voláním [**get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Podrobnosti o předplatném obsahují ID objednávky předplatného, což je objednávka, která se má aktualizovat pomocí doplňku.

Dále vytvořte instanci nového objektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) a naplňte ho jedinou instancí [**LineItem,**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) která obsahuje informace pro identifikaci doplňku, jak je znázorněno v následujícím fragmentu kódu. Tento nový objekt použijete k aktualizaci objednávky předplatného pomocí doplňku. Nakonec zavolejte metodu [**Patch,**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) která aktualizuje objednávku předplatného, a to po první identifikaci zákazníka pomocí [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) a objednávky [**s Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

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

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** AddSubscriptionAddOn.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda    | Identifikátor URI žádosti                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **Oprava** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/orders/{ID_objednávky} HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka a objednávky použijte následující parametry.

| Název                   | Typ     | Vyžadováno | Popis                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Hodnota je IDENTIFIKÁTOR GUID **naformátovaný jako customer-tenant-id,** který identifikuje zákazníka. |
| **ID objednávky**           | **guid** | Y        | Identifikátor objednávky.                                                              |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Následující tabulky popisují vlastnosti v textu požadavku.

## <a name="order"></a>Objednávka

| Název                | Typ             | Vyžadováno | Popis                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | řetězec           | N        | ID objednávky                                        |
| ReferenčníCustomerId | řetězec           | Y        | ID zákazníka.                                     |
| Položky řádku           | pole objektů | Y        | Pole objektů [OrderLineItem.](#orderlineitem) |
| Datum vytvoření        | řetězec           | N        | Datum vytvoření objednávky ve formátu data a času. |
| Atributy          | object           | N        | Obsahuje "ObjectType": "Order".                      |

## <a name="orderlineitem"></a>OrderLineItem (PoložkaŘádku Objednávky)

| Název                 | Typ   | Vyžadováno | Popis                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | číslo | Y        | Číslo položky řádku začínající na 0.                       |
| ID nabídky              | řetězec | Y        | ID nabídky doplňku.                                  |
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
