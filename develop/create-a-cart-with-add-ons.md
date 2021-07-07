---
title: Vytvoření košíku s doplňky
description: Naučte se používat Partnerské centrum API k přidání objednávky zákazníka s doplňky prostřednictvím košíku. Článek obsahuje požadavky a kroky pro vytvoření košíku s doplňky.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 513a9607b9194c36253630c91de9622325317c3a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973753"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Vytvoření košíku s doplňky k objednávce zákazníka

Doplňky si můžete koupit prostřednictvím košíku. Další informace o tom, co je aktuálně k dispozici k prodeji, najdete v tématu Nabídky partnerů [v Cloud Solution Provider programu](/partner-center/csp-offers).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Košík umožňuje nákup základní nabídky a odpovídajících doplňků. Při vytváření košíku postupujte takto:

1. Vytvoření instance objektu [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart)

2. Vytvořte seznam objektů [**CartLineItem,**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) které představují základní nabídky, a přiřaďte tento seznam k vlastnosti [**LineItems košíku.**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)

3. Pod řádkovou položkou košíku každé základní nabídky naplňte seznam **AddOnItems** jinými objekty **CartLineItem,** které představují doplněk, který bude zakoupen na základě této základní nabídky.

4. Získejte rozhraní pro operace košíku pomocí [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) k volání metody [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka a načtením rozhraní z vlastnosti **Cart.**

5. Nakonec zavolejte [**metodu Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) nebo [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) a vytvořte košík.

### <a name="c-example"></a>Příklad \# jazyka C

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

Postupujte podle těchto kroků a vytvořte košík, který umožní nákup doplňků pro stávající základní předplatná:

1. Vytvořte košík **s** novým **CartLineItem** obsahujícím ID předplatného ve vlastnosti **ProvisioningContext** s klíčem ParentSubscriptionId.

2. Zavolejte **metodu Create** nebo **CreateAsync.**

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

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/carts HTTP/1.1                        |

#### <a name="uri-parameter"></a>Parametr URI

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
| položky řádku             | Pole objektů | Yes             | Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)                                             |

Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.

| Vlastnost             | Typ                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | řetězec                           | Jedinečný identifikátor řádkové položky košíku. Použije se při úspěšném vytvoření košíku.                                                                   |
| id katalogu            | řetězec                           | Identifikátor položky katalogu.                                                                                                                          |
| Friendlyname         | řetězec                           | Nepovinný parametr. Popisný název položky definované partnerem, který pomáhá jednoznačně rozpoznat.                                                                 |
| quantity             | int                              | Počet licencí nebo instancí                                                                                                                  |
| currencyCode         | řetězec                           | Kód měny                                                                                                                                    |
| billingCycle         | Objekt                           | Typ fakturačního cyklu nastaveného pro aktuální období.                                                                                                 |
| členům         | Seznam párů řetězců objektů      | Kolekce PartnerId na záznamu (MPN ID) na nákupu.                                                                                          |
| provisioningContext  | Řetězec<slovníku, řetězec>       | Kontext použitý ke zřízení nabídky.                                                                                                             |
| pořadí           | řetězec                           | Skupina, která označuje, které položky lze umístit dohromady.                                                                                               |
| addonItems           | Seznam objektů **CartLineItem** | Kolekce položek řádků košíku pro doplňky, které budou koupeny k základnímu předplatnému, které je výsledkem nákupu položky řádku nadřazeného košíku. |
| error                | Objekt                           | Používá se po vytvoření košíku, pokud dojde k chybě.                                                                                                    |

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
