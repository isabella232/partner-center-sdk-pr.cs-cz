---
title: Získání seznamu objednávek podle typu fakturačního cyklu a zákazníka
description: Získá kolekci prostředků objednávek pro zadaný typ zákazníka a fakturačního cyklu.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 1c11779ee2ac80539a36db92f1ec811b054c858bf72d5ffbcce4d0bd86eed93e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994604"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a>Získání seznamu objednávek podle typu fakturačního cyklu a zákazníka

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Získá kolekci prostředků objednávky, které odpovídají danému typu zákazníka a fakturačního cyklu. Mezi časem, kdy je objednávka odeslána a kdy se objeví v kolekci objednávek zákazníka, je zpoždění až 15 minut.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Získání kolekce objednávek zákazníka:

1. Použijte kolekci [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s vybraným ID zákazníka.

2. Zavolejte [**vlastnost Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) a **metodu ByBillingCycleType()** se zadaným [**typem BillingCycleType.**](product-resources.md#billingcycletype)
3. Volejte [**metodu Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync)

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/orders?billingType={typ_fakturačního_cyklu} HTTP/1.1  |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání kolekce objednávek podle ID zákazníka a typu fakturačního cyklu.

| Název                   | Typ     | Vyžadováno | Popis                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| customer-tenant-id     | řetězec   | Yes      | Řetězec ve formátu GUID odpovídající zákazníkovi.    |
| typ fakturačního cyklu     | řetězec   | No       | Řetězec odpovídající typu fakturačního cyklu.         |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí kolekci [prostředků Order](order-resources.md) v textu odpovědi.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 97fa8b4f-6576-4cd9-dd19-ac7c97a023a7
MS-RequestId: 3c6a034c-82ee-4095-d50f-9b530a415f1f
MS-CV: nb4/b3Yl2keY0eYR.0
MS-ServerId: 202010607
Date: Thu, 15 Mar 2018 20:44:40 GMT

{
    "totalCount": 2,
    "items": [
        {
            "id": "9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4B:000Z:DZH318Z0DSPL",
                    "friendlyName": "Reserved_VM_Instance_Standard_D1_AP_East_1_Year",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4B/skus/000Z?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T02:17:15.6455674Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Order"
            }
        },
        {
            "id": "s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4Z:002P:DZH318Z0CL2D",
                    "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_3_Years",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4Z/skus/002P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T01:42:36.8440279Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": { "objectType": "Order" }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType":
        "Collection"
    }
}
```
