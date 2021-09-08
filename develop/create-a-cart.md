---
title: Vytvoření košíku
description: Naučte se používat rozhraní API partnerského centra k přidání objednávky pro zákazníka na vozík. Téma obsahuje informace o tom, jak vytvořit vozík a všechny požadované součásti.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 2827a2de7dc1c136fe4ea8735e12dc4b88e5e9bf
ms.sourcegitcommit: 5f27733d7c984c29f71c8b9c8ba5f89753eeabc4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2021
ms.locfileid: "123557265"
---
# <a name="create-a-cart-with-a-customer-order"></a>Vytvoření košíku s objednávkou zákazníka

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Můžete přidat objednávku pro zákazníka na vozík. další informace o tom, co je aktuálně k dispozici pro prodej, najdete [v tématu partnerské nabídky v programu Cloud Solution Provider](/partner-center/csp-offers).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Vytvoření objednávky pro zákazníka:

1. Vytvoří instanci objektu košíku.

2. Vytvořte seznam objektů **CartLineItem** a přiřaďte seznam k vlastnosti položky řádku košíku. Každá položka řádku vozíku obsahuje informace o nákupu pro jeden produkt. Musíte mít aspoň jednu položku řádku košíku.

3. Získejte rozhraní k zavozíkování operací voláním metody **IAggregatePartner. Customers. ById** s ID zákazníka, které zákazníka identifikuje, a následným načtením rozhraní z vlastnosti **košíku** .

4. Voláním metody **Create** nebo **CreateAsync** vytvořte košík.

5. K dokončení ověření identity a zahrnutí dalších prodejců se podívejte na následující ukázky ukázkových požadavků a odpovědí:

### <a name="request-sample"></a>Ukázka žádosti

```csharp

{
    "PartnerOnRecordAttestationAccepted":true,     "lineItems": [
        {
            "id": 0,
            "catalogItemId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "quantity": 1,
            "billingCycle": "monthly",
            "termDuration": "P1M",
            "renewsTo": null,
            "provisioningContext": {},
            "coterminousSubscriptionId": null
        },
        {
            "id": 1,
            "catalogItemId": "CFQ7TTC0LFLS:0002:CFQ7TTC0KDLJ",
            "quantity": 2,
            "billingCycle": "monthly",
            "termDuration": "P1Y",
            "participants": [
                {
                    "key": "transaction_reseller",
                    "value": "5357564"
                },
                 {
                    "key": "additional_transaction_reseller",                     
                    "value": "517285"
                },
                 {
                    "key": "additional_transaction_reseller", 
                    "value": "5357563"
                }
            ]
        }
    ]
}


```

### <a name="response-sample"></a>Ukázka odpovědi

```csharp

{
    "id": "3e22b548-647d-4223-9675-1fcb6cb57665",
    "creationTimestamp": "2021-08-18T17:29:52.3517492Z",
    "lastModifiedTimestamp": "2021-08-18T17:29:52.3517553Z",
    "expirationTimestamp": "2021-08-25T17:30:11.2406416Z",
    "lastModifiedUser": "da62a0dc-35e9-4601-b48e-a047bd3ec7c1",
    "status": "Active",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "quantity": 1,
            "currencyCode": "USD",
            "billingCycle": "monthly",
            "termDuration": "P1M",
            "provisioningContext": {},
            "orderGroup": "0"
        },
        {
            "id": 1,
            "catalogItemId": "CFQ7TTC0LFLS:0002:CFQ7TTC0KDLJ",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "monthly",
            "termDuration": "P1Y",
            "participants": [
                {
                    "key": "transaction_reseller",
                    "value": "5357564"
                },
                {
                    "key": "additional_transaction_reseller", 
                    "value": "517285"
                },
                {
                    "key": "additional_transaction_reseller", 
                    "value": "5357563"
                }
            ],
            "provisioningContext": {},
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/carts/3e22b548-647d-4223-9675-1fcb6cb57665",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}


```


### <a name="c-example"></a>\#Příklad C

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

1. Vytvoří instanci objektu košíku.

2. Vytvoří seznam objektů **CartLineItem** a přiřadí seznam k položkám na řádku košíku. Každá položka řádku vozíku obsahuje informace o nákupu pro jeden produkt. Musíte mít aspoň jednu položku řádku košíku.

3. Získejte rozhraní k zavozíkování operací voláním funkce **IAggregatePartner. GetCustomers (). byId** s ID zákazníka pro identifikaci zákazníka a následným načtením rozhraní z funkce **getkošík** .

4. Chcete-li vytvořit košík, zavolejte funkci **Create** .

## <a name="java-example"></a>Příklad Java

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

1. Vytvoří instanci objektu košíku.

2. Vytvoří seznam objektů **CartLineItem** a přiřadí seznam k položkám na řádku košíku. Každá položka řádku vozíku obsahuje informace o nákupu pro jeden produkt. Musíte mít aspoň jednu položku řádku košíku.

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

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts HTTP/1.1                        |

### <a name="uri-parameter"></a>Parametr URI

K identifikaci zákazníka použijte následující parametr cesty.

| Název            | Typ     | Vyžadováno | Popis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID zákazníka** | řetězec   | Yes      | Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.             |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje vlastnosti [košíku](cart-resources.md) v textu žádosti.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | No              | Identifikátor košíku, který se zadal po úspěšném vytvoření košíku.                                  |
| creationTimeStamp     | DateTime         | No              | Datum, kdy byl košík vytvořen, ve formátu data a času. Použito po úspěšném vytvoření košíku.         |
| lastModifiedTimeStamp | DateTime         | No              | Datum poslední aktualizace košíku ve formátu data a času. Použito po úspěšném vytvoření košíku.    |
| expirationTimeStamp   | DateTime         | No              | Datum, kdy vyprší platnost košíku, ve formátu data a času.  Použito po úspěšném vytvoření košíku.            |
| lastModifiedUser      | řetězec           | No              | Uživatel, který kartu naposledy aktualizoval. Použito po úspěšném vytvoření košíku.                             |
| Položky řádku             | Pole objektů | Yes             | Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)                                     |
| PartnerOnRecordAttestationAccepted | Logická hodnota | Yes | Potvrdí dokončení ověření identity. |

Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.

|      Vlastnost       |            Typ             | Vyžadováno |                                                                                         Popis                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         id          |           řetězec            |    No    |                                                     Jedinečný identifikátor položky řádku košíku Použito po úspěšném vytvoření košíku.                                                     |
|      catalogId      |           řetězec            |   Yes    |                                                                                Identifikátor položky katalogu                                                                                 |
|    friendlyName     |           řetězec            |    No    |                                                    Nepovinný parametr. Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.                                                    |
|      quantity       |             int             |   Yes    |                                                                            Počet licencí nebo instancí.                                                                             |
|    currencyCode     |           řetězec            |    No    |                                                                                     Kód měny.                                                                                      |
|    billingCycle     |           Objekt            |   Yes    |                                                                    Typ fakturačního cyklu nastaveného pro aktuální období.                                                                    |
|    členům     | Seznam párů řetězců objektů |    No    |                                                                Kolekce PartnerId na záznamu (MPNID) na nákupu.                                                                 |
| provisioningContext | Řetězec<slovníku, řetězec>  |    No    | Informace požadované pro zřizování některých položek v katalogu. Vlastnost provisioningVariables v SKU indikuje, které vlastnosti jsou požadovány pro konkrétní položky v katalogu. |
|     pořadí      |           řetězec            |    No    |                                                                   Skupina, která označuje, které položky lze umístit dohromady.                                                                   |
|        error        |           Objekt            |    No    |                                                                     Používá se po vytvoření košíku, pokud dojde k chybě.                                                                      |
|     renewsTo        | Pole objektů            |    No    |                                                    Pole prostředků [RenewsTo](cart-resources.md#renewsto)                                                                            |
|     AttestationAccepted        | Logická hodnota            |    No    |                                                   Označuje smlouvu o nabídkách nebo podmínkách SKU. Vyžaduje se jenom pro nabídky nebo skladové položky, kde SkuAttestationProperties nebo OfferAttestationProperties enforceAttestation má hodnotu true.                                                                             |
|  transaction_reseller | Řetězec | No | Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **nepřímého prodejce** (nikdy ID nepřímého poskytovatele). To zajišťuje správné účetnictví pro motivaci. |
| additional_transaction_reseller | Řetězec | No | Když nepřímý poskytovatel umístí objednávku jménem nepřímého prodejce, naplňte toto pole do ID MPN **dalšího nepřímého prodejce** (nikdy ID nepřímého poskytovatele). Pro tyto další prodejce nelze použít pobídky. Je možné zadat maximálně 5 nepřímých prodejců. Toto jsou pouze partneři, kteří se týkají v zemích EU/ESVO. |

Tato tabulka popisuje vlastnosti [RenewsTo](cart-resources.md#renewsto) v textu požadavku.

| Vlastnost              | Typ             | Vyžadováno        | Popis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | řetězec           | No              | ISO 8601 představuje dobu trvání období obnovy. Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok). |

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

V případě úspěchu tato metoda vrátí prostředek vyplněné [vozíku](cart-resources.md) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

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


## <a name="example-for-new-commerce-license-based-services"></a>Příklad pro nové obchodní služby založené na licencích

> [!Note] 
> Nové obchodní změny jsou momentálně dostupné jenom pro partnery, kteří jsou součástí M365/D365 New Commerce Experience Technical Preview.

### <a name="request-example"></a>Příklad požadavku

```http
POST /v1/customers/932c4101-dc08-461b-b4c1-75d80e905775/carts HTTP/1.1
Host: api.partnercenter.microsoft.com
Content-Type: application/json
Content-Length: 165

{
    "LineItems": [
        {
            "CatalogItemId":"CFQ7TTC0LFLZ:0002:CFQ7TTC0K4TS",
            "Quantity": 1,
            "TermDuration": "P1M",
                    "BillingCycle": "Monthly"
        }
    ]
}

```

### <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek vyplněné [vozíku](cart-resources.md) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http

{
    "id": "6b6ba6ea-d1ea-4c2c-9e1c-bec4f61e2049",
    "creationTimestamp": "2021-02-24T19:26:06.947164Z",
    "lastModifiedTimestamp": "2021-02-24T19:26:06.9471649Z",
    "expirationTimestamp": "2021-03-03T19:26:09.0035129Z",
    "lastModifiedUser": "004ec05e-8999-4d02-9315-2b1b667c0deb",
    "status": "Active",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "CFQ7TTC0LFLZ:0002:CFQ7TTC0K4TS",
            "quantity": 1,
            "currencyCode": "USD",
            "billingCycle": "monthly",
            "termDuration": "P1M",
            "provisioningContext": {},
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/932c4101-dc08-461b-b4c1-75d80e905775/carts/6b6ba6ea-d1ea-4c2c-9e1c-bec4f61e2049",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}



```
