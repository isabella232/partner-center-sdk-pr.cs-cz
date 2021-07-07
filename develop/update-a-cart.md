---
title: Aktualizace košíku
description: Jak aktualizovat objednávku zákazníka v košíku
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8954d4dad39f9b1a1b9a2f213e0231f01856fcd2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446679"
---
# <a name="update-a-cart"></a>Aktualizace košíku

Jak aktualizovat objednávku zákazníka v košíku

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID košíku pro existující košík

## <a name="c"></a>C\#

Pokud chcete aktualizovat objednávku zákazníka, získejte košík pomocí metody **Get()** předáním ID zákazníků a košíků pomocí funkce **ById().** Proveďte potřebné změny v košíku. Teď zavolejte **metodu Put** pomocí ID zákazníků a košíků pomocí metody **ById().**

Nakonec zavolejte **metodu Put()** nebo **PutAsync()** a vytvořte pořadí.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/carts/{ID_košíku} HTTP/1.1              |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

Pomocí následujících parametrů cesty identifikujte zákazníka a zadejte košík, který se má aktualizovat.

| Název            | Typ     | Vyžadováno | Popis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **id zákazníka** | řetězec   | Yes      | Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.             |
| **cart-id**     | řetězec   | Yes      | Identifikátor CART-ID formátovaný identifikátorem GUID, který identifikuje košík.                     |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje vlastnosti [Cart](cart-resources.md) (Košík) v textu požadavku.

| Vlastnost              | Typ             | Vyžadováno        | Popis                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | No              | Identifikátor košíku, který se dodá po úspěšném vytvoření košíku.                                  |
| creationTimeStamp     | DateTime         | No              | Datum vytvoření košíku ve formátu data a času. Použije se při úspěšném vytvoření košíku.        |
| lastModifiedTimeStamp | DateTime         | No              | Datum poslední aktualizace košíku ve formátu data a času Použije se při úspěšném vytvoření košíku.    |
| expirationTimeStamp   | DateTime         | No              | Datum, kdy vyprší platnost košíku ve formátu data a času.  Použije se při úspěšném vytvoření košíku.            |
| lastModifiedUser      | řetězec           | No              | Uživatel, který naposledy aktualizoval košík Použije se při úspěšném vytvoření košíku.                             |
| položky řádku             | Pole objektů | Yes             | Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)                                               |

Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.

| Vlastnost             | Typ                        | Vyžadováno     | Popis                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | řetězec                      | No           | Jedinečný identifikátor řádkové položky košíku. Použije se při úspěšném vytvoření košíku.                |
| id katalogu            | řetězec                      | Yes          | Identifikátor položky katalogu.                                                                       |
| Friendlyname         | řetězec                      | No           | Nepovinný parametr. Popisný název položky definované partnerem, který pomáhá jednoznačně rozpoznat.              |
| quantity             | int                         | Yes          | Počet licencí nebo instancí     |
| currencyCode         | řetězec                      | No           | Kód měny                                                                                 |
| billingCycle         | Objekt                      | Yes          | Typ fakturačního cyklu nastavený pro aktuální období                                              |
| Účastníci         | Seznam párů řetězců objektů | No           | Kolekce účastníků nákupu.                                                      |
| provisioningContext  | Slovníkový<řetězec, řetězec>  | No           | Kontext používaný ke zřízení nabídky.                                                          |
| orderGroup           | řetězec                      | No           | Skupina, která označuje, které položky lze umístit dohromady.                                            |
| error                | Objekt                      | No           | Použije se po vytvoření košíku v případě chyby.                                                 |

### <a name="request-example"></a>Příklad požadavku

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
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
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
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
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
