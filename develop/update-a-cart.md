---
title: Aktualizace košíku
description: Jak aktualizovat objednávku pro zákazníka na vozíku
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766731"
---
# <a name="update-a-cart"></a>Aktualizace košíku

**Platí pro**

- Partnerské centrum

Jak aktualizovat objednávku pro zákazníka na vozíku

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID košíku pro existující košík.

## <a name="c"></a>C\#

Chcete-li aktualizovat objednávku pro zákazníka, Získejte pomocí metody **Get ()** vozík pomocí funkce **ById ()** . Proveďte potřebné změny košíku. Nyní zavolejte metodu **Put** pomocí ID zákazníka a košíku pomocí metody **ById ()** .

Nakonec zavolejte metodu **Put ()** nebo **PutAsync ()** pro vytvoření objednávky.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{Cart-ID} HTTP/1.1              |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka použijte následující parametry cesty a určete, který vozík se má aktualizovat.

| Název            | Typ     | Vyžadováno | Popis                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID zákazníka** | řetězec   | Yes      | Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.             |
| **košík – ID**     | řetězec   | Yes      | Identifikátor košíku formátovaného identifikátorem GUID, který identifikuje vozík.                     |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje vlastnosti [košíku](cart-resources.md) v textu žádosti.

| Vlastnost              | Typ             | Vyžadováno        | Popis                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | řetězec           | No              | Identifikátor košíku, který se zadal po úspěšném vytvoření košíku.                                  |
| creationTimeStamp     | DateTime         | No              | Datum, kdy byl košík vytvořen, ve formátu data a času. Použito po úspěšném vytvoření košíku.        |
| lastModifiedTimeStamp | DateTime         | No              | Datum poslední aktualizace košíku ve formátu data a času. Použito po úspěšném vytvoření košíku.    |
| expirationTimeStamp   | DateTime         | No              | Datum, kdy vyprší platnost košíku, ve formátu data a času.  Použito po úspěšném vytvoření košíku.            |
| lastModifiedUser      | řetězec           | No              | Uživatel, který kartu naposledy aktualizoval. Použito po úspěšném vytvoření košíku.                             |
| Položky řádku             | Pole objektů | Yes             | Pole prostředků [CartLineItem](cart-resources.md#cartlineitem)                                               |

Tato tabulka popisuje vlastnosti [CartLineItem](cart-resources.md#cartlineitem) v textu požadavku.

| Vlastnost             | Typ                        | Vyžadováno     | Popis                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | řetězec                      | No           | Jedinečný identifikátor položky řádku košíku Použito po úspěšném vytvoření košíku.                |
| catalogId            | řetězec                      | Yes          | Identifikátor položky katalogu                                                                       |
| friendlyName         | řetězec                      | No           | Nepovinný parametr. Popisný název položky definované partnerem, který vám umožní určit nejednoznačnost.              |
| quantity             | int                         | Yes          | Počet licencí nebo instancí.     |
| currencyCode         | řetězec                      | No           | Kód měny.                                                                                 |
| billingCycle         | Objekt                      | Yes          | Typ fakturačního cyklu nastaveného pro aktuální období.                                              |
| členům         | Seznam párů řetězců objektů | No           | Kolekce účastníků na nákupu                                                      |
| provisioningContext  | Řetězec<slovníku, řetězec>  | No           | Kontext použitý ke zřízení nabídky.                                                          |
| pořadí           | řetězec                      | No           | Skupina, která označuje, které položky lze umístit dohromady.                                            |
| error                | Objekt                      | No           | Používá se po vytvoření košíku v případě chyby.                                                 |

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
