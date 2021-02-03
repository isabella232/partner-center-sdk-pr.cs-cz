---
title: Vytvoření košíku s doplňky
description: Naučte se používat rozhraní API partnerského centra k přidání objednávky zákazníka s doplňky prostřednictvím košíku. Článek sdílí požadavky a kroky k vytvoření košíku s doplňky.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767128"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Vytvoření košíku s doplňky pro objednávku zákazníka

**Platí pro:**

- Partnerské centrum

Přidané doplňky můžete koupit prostřednictvím košíku. Další informace o tom, co je aktuálně k dispozici pro prodej, najdete [v tématu partnerské nabídky v programu Cloud Solution Provider](/partner-center/csp-offers).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Vozík umožňuje zakoupit základní nabídku a její odpovídající doplňky. Pomocí těchto kroků vytvořte košík:

1. Vytvoří instanci objektu [**košíku**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) .

2. Vytvořte seznam objektů [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) , které představují základní nabídky, a přiřaďte seznam k vlastnosti [**položky řádku**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) košíku.

3. V rámci položky řádku košíku základní nabídky vyplňte seznam **AddOnItems** dalšími objekty **CartLineItem** , které každý z nich představují doplněk, který bude koupen na základě této základní nabídky.

4. Získejte rozhraní pro operace na vozíku pomocí [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) k volání metody [**ICustomerCollection. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka a následnému načtení rozhraní z vlastnosti **košíku** .

5. Nakonec voláním metody [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) vytvořte košík.

### <a name="c-example"></a>\#Příklad C

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

Pomocí těchto kroků můžete vytvořit košík, který umožní nákup doplňků u stávajících základních předplatných:

1. Vytvořte **košík** s novým **CartLineItem** , který obsahuje ID předplatného ve vlastnosti **ProvisioningContext** s klíčem "ParentSubscriptionId".

2. Zavolejte metodu **Create** nebo **CreateAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts HTTP/1.1                        |

#### <a name="uri-parameter"></a>Parametr URI

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
| Položky řádku             | Pole objektů | Yes             | Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)                                             |

Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.

| Vlastnost             | Typ                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | řetězec                           | Jedinečný identifikátor položky řádku košíku Použito po úspěšném vytvoření košíku.                                                                   |
| catalogId            | řetězec                           | Identifikátor položky katalogu                                                                                                                          |
| friendlyName         | řetězec                           | Nepovinný parametr. Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.                                                                 |
| quantity             | int                              | Počet licencí nebo instancí.                                                                                                                  |
| currencyCode         | řetězec                           | Kód měny.                                                                                                                                    |
| billingCycle         | Objekt                           | Typ fakturačního cyklu nastaveného pro aktuální období.                                                                                                 |
| členům         | Seznam párů řetězců objektů      | Kolekce PartnerId na záznamu (MPNID) na nákupu.                                                                                          |
| provisioningContext  | Řetězec<slovníku, řetězec>       | Kontext použitý ke zřízení nabídky.                                                                                                             |
| pořadí           | řetězec                           | Skupina, která označuje, které položky lze umístit dohromady.                                                                                               |
| addonItems           | Seznam objektů **CartLineItem** | Kolekce položek řádků košíku pro doplňky, které budou koupeny k základnímu předplatnému, které je výsledkem nákupu položky řádku nadřazeného košíku. |
| error                | Objekt                           | Používá se po vytvoření košíku v případě chyby.                                                                                                    |

### <a name="request-example-new-base-subscription"></a>Příklad požadavku (nové základní předplatné)

Následující příklad REST ukazuje, jak vytvořit košík s položkami doplňku pro nové základní předplatné.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a>Příklad požadavku (stávající základní předplatné)

Následující příklad REST ukazuje, jak připojit doplňky ke stávajícímu základnímu předplatnému.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek vyplněné [vozíku](cart-resources.md) v těle odpovědi.

#### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

#### <a name="response-example-new-base-subscription"></a>Příklad odpovědi (nové základní předplatné)

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a>Příklad odpovědi (stávající základní předplatné)

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
