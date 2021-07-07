---
title: Vytvoření košíku
description: Zjistěte, jak pomocí Partnerské centrum API přidat objednávku zákazníka do košíku. Téma obsahuje informace o vytvoření košíku a všech předpokladech.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: dba54d4f6b97f3d0a51e2f87b32edca686466b89
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973770"
---
# <a name="create-a-cart-with-a-customer-order"></a>Vytvoření košíku s objednávkou zákazníka

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Objednávku zákazníka můžete přidat do košíku. Další informace o tom, co je aktuálně k dispozici k prodeji, najdete v tématu Nabídky partnerů [v Cloud Solution Provider programu](/partner-center/csp-offers).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Vytvoření objednávky pro zákazníka:

1. Vytvoření instance objektu Cart

2. Vytvořte seznam objektů **CartLineItem** a přiřaďte ho k vlastnosti LineItems košíku. Každá řádová položka košíku obsahuje informace o nákupu jednoho produktu. Musíte mít alespoň jednu řádkovou položku košíku.

3. Získejte rozhraní pro operace košíku voláním **metody IAggregatePartner.Customers.ById** s ID zákazníka k identifikaci zákazníka a načtením rozhraní z **vlastnosti Cart.**

4. Voláním **metody Create** nebo **CreateAsync** vytvořte košík.

### <a name="c-example"></a>Příklad \# jazyka C

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Vytvoření objednávky pro zákazníka:

1. Vytvoření instance objektu Cart

2. Vytvořte seznam objektů **CartLineItem** a přiřaďte ho řádkové položkám košíku. Každá řádová položka košíku obsahuje informace o nákupu jednoho produktu. Musíte mít alespoň jednu řádkovou položku košíku.

3. Získejte rozhraní pro operace košíku voláním funkce **IAggregatePartner.getCustomers().byId** s ID zákazníka k identifikaci zákazníka a načtením rozhraní z **funkce getCart.**

4. Voláním **funkce create** vytvořte košík.

## <a name="java-example"></a>Příklad v Javě

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Vytvoření objednávky pro zákazníka:

1. Vytvoření instance objektu Cart

2. Vytvořte seznam objektů **CartLineItem** a přiřaďte ho řádkové položkám košíku. Každá řádová položka košíku obsahuje informace o nákupu jednoho produktu. Musíte mít alespoň jednu řádkovou položku košíku.

3. Spuštěním příkazu [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) vytvořte košík.

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/carts HTTP/1.1                        |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci zákazníka použijte následující parametr cesty.

| Název            | Typ     | Vyžadováno | Popis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **id zákazníka** | řetězec   | Yes      | Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.             |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje vlastnosti [Cart](cart-resources.md) (Košík) v textu požadavku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | No              | Identifikátor košíku, který se dodá po úspěšném vytvoření košíku.                                  |
| creationTimeStamp     | DateTime         | No              | Datum vytvoření košíku ve formátu data a času. Použije se při úspěšném vytvoření košíku.         |
| lastModifiedTimeStamp | DateTime         | No              | Datum poslední aktualizace košíku ve formátu data a času Použije se při úspěšném vytvoření košíku.    |
| expirationTimeStamp   | DateTime         | No              | Datum, kdy vyprší platnost košíku ve formátu data a času.  Použije se při úspěšném vytvoření košíku.            |
| lastModifiedUser      | řetězec           | No              | Uživatel, který naposledy aktualizoval košík Použije se při úspěšném vytvoření košíku.                             |
| položky řádku             | Pole objektů | Yes             | Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)                                     |

Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.

|      Vlastnost       |            Typ             | Vyžadováno |                                                                                         Popis                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         id          |           řetězec            |    No    |                                                     Jedinečný identifikátor řádkové položky košíku. Použije se při úspěšném vytvoření košíku.                                                     |
|      id katalogu      |           řetězec            |   Yes    |                                                                                Identifikátor položky katalogu.                                                                                 |
|    Friendlyname     |           řetězec            |    No    |                                                    Nepovinný parametr. Popisný název položky definované partnerem, který pomáhá jednoznačně rozpoznat.                                                    |
|      quantity       |             int             |   Yes    |                                                                            Počet licencí nebo instancí                                                                             |
|    currencyCode     |           řetězec            |    No    |                                                                                     Kód měny                                                                                      |
|    billingCycle     |           Objekt            |   Yes    |                                                                    Typ fakturačního cyklu nastavený pro aktuální období                                                                    |
|    Účastníci     | Seznam párů řetězců objektů |    No    |                                                                Kolekce PartnerId on Record (MPNID) při nákupu.                                                                 |
| provisioningContext | Slovníkový<řetězec, řetězec>  |    No    | Informace vyžadované pro zřizování některých položek v katalogu. Vlastnost provisioningVariables ve SKU určuje, které vlastnosti jsou vyžadovány pro konkrétní položky v katalogu. |
|     orderGroup      |           řetězec            |    No    |                                                                   Skupina, která označuje, které položky lze umístit dohromady.                                                                   |
|        error        |           Objekt            |    No    |                                                                     Použije se po vytvoření košíku, pokud dojde k chybě.                                                                      |
|     renewsTo        | Pole objektů            |    No    |                                                    Pole prostředků [RenewsTo.](cart-resources.md#renewsto)                                                                            |

Tato tabulka popisuje vlastnosti [RenewsTo](cart-resources.md#renewsto) v textu požadavku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | Reprezentace doby trvání období prodloužení podle ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc) a **P1Y** (1 rok). |

### <a name="request-example"></a>Příklad požadavku

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v textu odpovědi naplněný prostředek [Cart.](cart-resources.md)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
