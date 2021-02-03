---
title: Nákup doplňku k předplatnému
description: Jak zakoupit doplněk do stávajícího předplatného.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766970"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Nákup doplňku k předplatnému

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud for US Government

Jak zakoupit doplněk do stávajícího předplatného.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného. Toto je stávající předplatné, pro které se má koupit nabídka doplňku.

- ID nabídky, která identifikuje nabídku doplňku k nákupu.

## <a name="purchasing-an-add-on-through-code"></a>Nákup doplňku prostřednictvím kódu

Když si nakoupíte doplněk k předplatnému, které aktualizujete původní pořadí předplatného, s pořadím pro doplněk. V následujícím seznamu je KódZákazníka ID zákazníka, subscriptionId je ID předplatného a addOnOfferId je ID nabídky pro doplněk.

Tady je postup:

1.  Získejte rozhraní pro operace pro předplatné.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Pomocí tohoto rozhraní můžete vytvořit instanci objektu předplatného. Tím získáte podrobnosti o nadřazeném předplatném, včetně ID objednávky.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Vytvoří instanci objektu New [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) . Tato instance objednávky se používá k aktualizaci původního pořadí používaného k zakoupení předplatného. Přidejte jednu položku řádku do objednávky, která představuje doplněk.
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

Chcete-li zakoupit doplněk, Začněte získáním rozhraní pro operace předplatného voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, který identifikuje zákazníka, a pomocí metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pro identifikaci předplatného, které obsahuje nabídku doplňku. Použijte toto [**rozhraní**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) k načtení podrobností o předplatném voláním [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Proč potřebujete podrobnosti o předplatném? Protože potřebujete ID objednávky pořadí předplatného. To je pořadí, v jakém se má doplněk aktualizovat.

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

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: AddSubscriptionAddOn.cs

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
| ParentSubscriptionId | řetězec | Y        | ID nadřazeného předplatného, které má nabídku doplňku. |
| FriendlyName         | řetězec | N        | Popisný název této položky řádku                        |
| Množství             | číslo | Y        | Počet licencí.                                      |
| PartnerIdOnRecord    | řetězec | N        | ID MPN partnera záznamu                         |
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

V případě úspěchu tato metoda vrátí aktualizované pořadí předplatného v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

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
