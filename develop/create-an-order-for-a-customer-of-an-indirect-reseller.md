---
title: Vytvořit objednávku zákazníka pro nepřímý prodejce
description: Naučte se používat rozhraní API partnerského centra k vytvoření objednávky pro zákazníka nepřímého prodejce. Článek obsahuje požadavky, kroky a příklady.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253ba2289ea1f58e7d8eaa960d7d0daaa887f0d
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973535"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Vytvoření objednávky pro zákazníka nepřímého prodejce

Jak vytvořit objednávku pro zákazníka nepřímého prodejce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor nabídky položky, která se má koupit

- Identifikátor tenanta nepřímého prodejce.

## <a name="c"></a>C\#

Chcete-li vytvořit objednávku pro zákazníka nepřímého prodejce:

1. Získejte kolekci nepřímých prodejců, kteří mají relaci s přihlášeným partnerem.

2. Získat místní proměnnou na položku v kolekci, která odpovídá ID nepřímého prodejce. Tento krok vám pomůže při vytváření objednávky získat přístup k vlastnosti [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) prodejce.

3. Vytvořte instanci objektu [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) a nastavte vlastnost [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) na identifikátor zákazníka, aby bylo možné záznam zákazníka zaznamenat.

4. Vytvořte seznam objektů [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) a přiřaďte seznam k vlastnosti [**položky řádku**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) objednávky. Každá položka řádku objednávky obsahuje informace o nákupu pro jednu nabídku. Nezapomeňte v každé položce řádku naplnit vlastnost [**PARTNERIDONRECORD**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) číslem MPN nepřímého prodejce. Musíte mít aspoň jednu položku řádku objednávky.

5. Získejte rozhraní k seřazení operací voláním metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, které zákazníka identifikují, a potom načtěte rozhraní z vlastnosti [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .

6. Voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) vytvořte objednávku.

### <a name="c-example"></a>\#Příklad C

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**ukázka**: [konzola test app](console-test-app.md)**Project**: **třída** pro ukázkové sady SDK partnerského centra: PlaceOrderForCustomer. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka použijte následující parametr cesty.

| Název        | Typ   | Vyžadováno | Popis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

#### <a name="order"></a>Objednávka

Tato tabulka popisuje vlastnosti **objednávky** v textu žádosti.

| Název | Typ | Vyžadováno | Popis |
| ---- | ---- | -------- | ----------- |
| id | řetězec | No | Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky. |
| referenceCustomerId | řetězec | Yes | Identifikátor zákazníka. |
| billingCycle | řetězec | No | Frekvence, s jakou se má partner fakturovat v této objednávce Výchozí hodnota je &quot; měsíčně &quot; a po úspěšném vytvoření objednávky se použije. Podporované hodnoty jsou názvy členů nalezené v [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype). Poznámka: funkce každoroční fakturace zatím není obecně dostupná. Brzy se přiblíží podpora pro roční fakturaci. |
| Položky řádku | pole objektů | Yes | Pole prostředků [**OrderLineItem**](#orderlineitem) |
| creationDate | řetězec | No | Datum vytvoření objednávky ve formátu data a času. Použito po úspěšném vytvoření objednávky. |
| atributy | object | No | Obsahuje "ObjectType": "Order". |

#### <a name="orderlineitem"></a>OrderLineItem

Tato tabulka popisuje vlastnosti **OrderLineItem** v textu požadavku.

| Název | Typ | Vyžadováno | Popis |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Yes | Každá položka řádku v kolekci získá jedinečné číslo řádku, počítáno od 0 do Count-1. |
| Hodnotami OfferId | řetězec | Yes | Identifikátor nabídky |
| subscriptionId | řetězec | No | Identifikátor předplatného. |
| parentSubscriptionId | řetězec | No | Nepovinný parametr. ID nadřazeného odběru v nabídce doplňku Platí pouze pro opravu. |
| friendlyName | řetězec | No | Nepovinný parametr. Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost. |
| quantity | int | Yes | Počet licencí pro předplatné založené na licencích. |
| partnerIdOnRecord | řetězec | No | Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **nepřímého prodejce** (nikdy ID nepřímého poskytovatele). To zajišťuje správné účetnictví pro motivaci. **Nepodaří-li se poskytnout ID programu MPN pro prodejce nezpůsobí selhání objednávky. Prodejce však není zaznamenán a v důsledku toho nemůžou výpočty s nesekvencí zahrnovat prodej.** |
| atributy | object | No | Obsahuje "ObjectType": "OrderLineItem". |

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
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

V případě úspěchu obsahuje tělo odpovědi vyplněný prostředek [objednávky](order-resources.md) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
