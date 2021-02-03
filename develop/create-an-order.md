---
title: Vytvoření objednávky zákazníka
description: Naučte se používat rozhraní API partnerského centra k vytvoření objednávky pro zákazníka. Článek obsahuje požadavky, kroky a příklady.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767126"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Vytvoření objednávky pro zákazníka pomocí rozhraní API partnerského centra

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud for US Government

Vytvoření **objednávky pro rezervované instance virtuálních počítačů Azure** se týká *jenom* těchto produktů:

- Partnerské centrum

Informace o tom, co je aktuálně k dispozici pro prodej, najdete v tématu [partnerské nabídky v programu Cloud Solution Provider](/partner-center/csp-offers).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor nabídky

## <a name="c"></a>C\#

Vytvoření objednávky pro zákazníka:

1. Vytvořte instanci objektu [**Order**](order-resources.md) a nastavte vlastnost **ReferenceCustomerID** na ID zákazníka pro záznam zákazníka.

2. Vytvořte seznam objektů [**OrderLineItem**](order-resources.md#orderlineitem) a přiřaďte seznam k vlastnosti **položky řádku** objednávky. Každá položka řádku objednávky obsahuje informace o nákupu pro jednu nabídku. Musíte mít aspoň jednu položku řádku objednávky.

3. Získejte rozhraní k seřazení operací. Nejdřív zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, abyste zákazníka identifikovali. Dále načtěte rozhraní z vlastnosti [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .

4. Zavolejte metodu [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) a předejte objekt [**Order**](order-resources.md) .

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

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: CreateOrder.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka použijte následující parametr cesty.

| Název        | Typ   | Vyžadováno | Popis                                                |
|-------------|--------|----------|------------------------------------------------------------|
| ID zákazníka | řetězec | Yes      | Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

#### <a name="order"></a>Objednávka

Tato tabulka popisuje vlastnosti [objednávky](order-resources.md) v textu žádosti.

| Vlastnost             | Typ                        | Vyžadováno                        | Popis                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | řetězec                      | No                              | Identifikátor objednávky, který je zadán po úspěšném vytvoření objednávky.   |
| referenceCustomerId  | řetězec                      | No                              | Identifikátor zákazníka. |
| billingCycle         | řetězec                      | No                              | Určuje četnost, s jakou se má partner fakturovat v této objednávce. Podporované hodnoty jsou názvy členů nalezené v [BillingCycleType](product-resources.md#billingcycletype). Výchozí hodnota je "Month" nebo "jednorázová" při vytváření objednávky. Toto pole se použije po úspěšném vytvoření objednávky. |
| Položky řádku            | pole prostředků [OrderLineItem](order-resources.md#orderlineitem) | Yes      | Seznam položek nabídek, které zákazník kupuje, včetně množství.        |
| currencyCode         | řetězec                      | No                              | Jen pro čtení. Měna použitá při umístění objednávky Použito po úspěšném vytvoření objednávky.           |
| creationDate         | datetime                    | No                              | Jen pro čtení. Datum vytvoření objednávky ve formátu data a času. Použito po úspěšném vytvoření objednávky.                                   |
| status               | řetězec                      | No                              | Jen pro čtení. Stav objednávky.  Podporované hodnoty jsou názvy členů nalezené v [OrderStatus](order-resources.md#orderstatus).        |
| odkazy                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | Odkazy na prostředky odpovídající objednávce. |
| atributy           | [ResourceAttributes](utility-resources.md#resourceattributes) | No                              | Atributy metadat odpovídající pořadí. |

#### <a name="orderlineitem"></a>OrderLineItem

Tato tabulka popisuje vlastnosti [OrderLineItem](order-resources.md#orderlineitem) v textu požadavku.

>[!NOTE]
>PartnerIdOnRecord by měla být poskytnuta pouze v případě, že nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce. Slouží k ukládání Microsoft Partner Network ID nepřímých prodejců (nikdy ID nepřímého poskytovatele).

| Název                 | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Yes      | Každá položka řádku v kolekci získá jedinečné číslo řádku, počítáno od 0 do Count-1.                                                                                                                                                 |
| Hodnotami OfferId              | řetězec | Yes      | Identifikátor nabídky                                                                                                                                                                                                                      |
| subscriptionId       | řetězec | No       | Identifikátor předplatného.                                                                                                                                                                                                               |
| parentSubscriptionId | řetězec | No       | Nepovinný parametr. ID nadřazeného odběru v nabídce doplňku Platí pouze pro opravu.                                                                                                                                                     |
| friendlyName         | řetězec | No       | Nepovinný parametr. Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost.                                                                                                                                              |
| quantity             | int    | Yes      | Počet licencí pro předplatné založené na licencích.                                                                                                                                                                                   |
| partnerIdOnRecord    | řetězec | No       | Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **nepřímého prodejce** (nikdy ID nepřímého poskytovatele). To zajišťuje správné účetnictví pro motivaci. |
| provisioningContext  | Řetězec<slovníku, řetězec>                | No       |  Informace požadované pro zřizování některých položek v katalogu. Vlastnost provisioningVariables v SKU indikuje, které vlastnosti jsou požadovány pro konkrétní položky v katalogu.                  |
| odkazy                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | No       |  Jen pro čtení. Odkazy na prostředky odpovídající položce řádku objednávky.  |
| atributy           | [ResourceAttributes](utility-resources.md#resourceattributes) | No       | Atributy metadat odpovídající OrderLineItem. |
| renewsTo             | Pole objektů                          | No    |Pole prostředků [RenewsTo](order-resources.md#renewsto)                                                                            |

##### <a name="renewsto"></a>RenewsTo

Tato tabulka popisuje vlastnosti [RenewsTo](order-resources.md#renewsto) v textu požadavku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | ISO 8601 představuje dobu trvání období obnovy. Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok). |

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

V případě úspěchu metoda vrátí zdroj [objednávky](order-resources.md) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

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
