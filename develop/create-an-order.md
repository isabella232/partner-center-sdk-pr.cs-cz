---
title: Vytvoření objednávky zákazníka
description: Naučte se používat Partnerské centrum API k vytvoření objednávky pro zákazníka. Článek obsahuje požadavky, kroky a příklady.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3a86a99f43bdeec5e4c560ab59e1924b76c0636
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973536"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Vytvoření objednávky pro zákazníka pomocí Partnerské centrum API

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud for US Government

Vytvoření objednávky **produktů rezervovaných instancí virtuálních** počítače Azure se *vztahuje pouze* na:

- Partnerské centrum

Informace o tom, co je aktuálně k dispozici k prodeji, najdete v tématu Nabídky partnerů [v Cloud Solution Provider programu](/partner-center/csp-offers).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor nabídky.

## <a name="c"></a>C\#

Vytvoření objednávky pro zákazníka:

1. Vytvořte instanci objektu [**Order**](order-resources.md) a nastavte vlastnost **ReferenceCustomerID** na ID zákazníka pro zaznamenání zákazníka.

2. Vytvořte seznam objektů [**OrderLineItem**](order-resources.md#orderlineitem) a přiřaďte ho k vlastnosti **LineItems** objednávky. Každá položka řádku objednávky obsahuje informace o nákupu pro jednu nabídku. Musíte mít alespoň jednu řádkovou položku objednávky.

3. Získání rozhraní pro řazení operací. Nejprve zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a identifikujte zákazníka. Dále načtěte rozhraní z [**vlastnosti Orders.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)

4. Zavolejte [**metodu Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) a předejte [**objekt Order.**](order-resources.md)

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class:** CreateOrder.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka použijte následující parametr cesty.

| Název        | Typ   | Vyžadováno | Popis                                                |
|-------------|--------|----------|------------------------------------------------------------|
| id zákazníka | řetězec | Yes      | Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

#### <a name="order"></a>Objednávka

Tato tabulka popisuje [vlastnosti Order](order-resources.md) v textu požadavku.

| Vlastnost             | Typ                        | Vyžadováno                        | Popis                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | řetězec                      | No                              | Identifikátor objednávky zadaný po úspěšném vytvoření objednávky.   |
| referenčníCustomerId  | řetězec                      | No                              | Identifikátor zákazníka. |
| billingCycle         | řetězec                      | No                              | Určuje frekvenci, s jakou se partner účtuje za tuto objednávku. Podporované hodnoty jsou názvy členů, které najdete v [části BillingCycleType](product-resources.md#billingcycletype). Výchozí hodnota je "Měsíčně" nebo "OneTime" při vytváření objednávky. Toto pole se použije při úspěšném vytvoření objednávky. |
| položky řádku            | pole prostředků [OrderLineItem](order-resources.md#orderlineitem) | Yes      | Itemized list of the offers the customer is purchasing including the quantity.        |
| currencyCode         | řetězec                      | No                              | Jen pro čtení. Měna použitá při zadávání objednávky. Použije se při úspěšném vytvoření objednávky.           |
| datum vytvoření         | datetime                    | No                              | Jen pro čtení. Datum vytvoření objednávky ve formátu data a času. Použije se při úspěšném vytvoření objednávky.                                   |
| status               | řetězec                      | No                              | Jen pro čtení. Stav objednávky  Podporované hodnoty jsou názvy členů, které najdete v [OrderStatus](order-resources.md#orderstatus).        |
| Odkazy                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | Propojení prostředků odpovídající objednávce |
| atributy           | [Atributy prostředků](utility-resources.md#resourceattributes) | No                              | Atributy metadat odpovídající order. |

#### <a name="orderlineitem"></a>OrderLineItem (PoložkaŘádku Objednávky)

Tato tabulka popisuje vlastnosti [OrderLineItem](order-resources.md#orderlineitem) v textu požadavku.

>[!NOTE]
>Záznam partnerIdOnRecord by měl být poskytnut pouze v případě, že nepřímý poskytovatel zadá objednávku jménem nepřímého prodejce. Slouží k uložení ID Microsoft Partner Network nepřímého prodejce (nikdy ID nepřímého poskytovatele).

| Název                 | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Yes      | Každá položka řádku v kolekci získá jedinečné číslo řádku, počítá se od 0 do count-1.                                                                                                                                                 |
| ID nabídky              | řetězec | Yes      | Identifikátor nabídky.                                                                                                                                                                                                                      |
| subscriptionId       | řetězec | No       | Identifikátor předplatného.                                                                                                                                                                                                               |
| PARENTSubscriptionId | řetězec | No       | Nepovinný parametr. ID nadřazeného předplatného v nabídce doplňku. Platí jenom pro PATCH.                                                                                                                                                     |
| Friendlyname         | řetězec | No       | Nepovinný parametr. Popisný název předplatného definovaného partnerem, který pomáhá jednoznačně rozpoznat.                                                                                                                                              |
| quantity             | int    | Yes      | Počet licencí pro předplatné založené na licencích.                                                                                                                                                                                   |
| id partneraZáznam    | řetězec | No       | Když nepřímý poskytovatel zadá objednávku jménem nepřímého prodejce, zadejte do tohoto pole pouze ID MPN nepřímého prodejce **(nikdy** ID nepřímého poskytovatele). Tím se zajistí správné účtování pobídek. |
| provisioningContext  | Slovníkový<řetězec, řetězec>                | No       |  Informace vyžadované pro zřizování některých položek v katalogu. Vlastnost provisioningVariables ve SKU určuje, které vlastnosti jsou vyžadovány pro konkrétní položky v katalogu.                  |
| Odkazy                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | No       |  Jen pro čtení. Propojení prostředků odpovídající položce řádku Order (Objednávka).  |
| atributy           | [Atributy prostředků](utility-resources.md#resourceattributes) | No       | Atributy metadat odpovídající OrderLineItem. |
| renewsTo             | Pole objektů                          | No    |Pole prostředků [RenewsTo.](order-resources.md#renewsto)                                                                            |

##### <a name="renewsto"></a>RenewsTo

Tato tabulka popisuje vlastnosti [RenewsTo](order-resources.md#renewsto) v textu požadavku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | Reprezentace doby trvání období prodloužení podle ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc) a **P1Y** (1 rok). |

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí metoda [v textu](order-resources.md) odpovědi prostředek Order.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
