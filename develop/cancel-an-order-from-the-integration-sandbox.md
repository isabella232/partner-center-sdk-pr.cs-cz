---
title: Zrušení objednávky z integračního sandboxu
description: Zjistěte, jak pomocí Partnerské centrum API zrušit různé typy objednávek předplatných z účtů sandboxu integrace.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c4843dc4626c2bb2cd1b2784f3df1c323e2eceea2edbb6330a9bd9dbcea4dc1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992207"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Zrušení objednávky z integračního sandboxu pomocí Partnerské centrum API

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak pomocí Partnerské centrum API zrušit různé typy objednávek předplatného z účtů sandboxu integrace. Tyto objednávky mohou zahrnovat rezervované instance, software a objednávky předplatného SaaS (Software jako služba) na komerčním marketplace.

> [!NOTE] 
> Upozorňujeme, že zrušení rezervovaných instancí nebo objednávek předplatného SaaS na komerčním marketplace je možné pouze z účtů sandboxu integrace. Všechny objednávky sandboxu, které jsou starší než 60 dnů, není možné zrušit z Partnerské centrum.

Pokud chcete zrušit produkční objednávky softwaru prostřednictvím rozhraní API, [použijte příkaz cancel-software-purchases](cancel-software-purchases.md).
Můžete také zrušit produkční objednávky softwaru prostřednictvím řídicího panelu pomocí [zrušení nákupu](/partner-center/csp-software-subscriptions).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- Partnerský účet sandboxu pro integraci se zákazníkem, který má aktivní rezervované instance, software nebo objednávky předplatného SaaS třetích stran.

## <a name="c"></a>C\#

Pokud chcete zrušit objednávku z sandboxu integrace, předejte přihlašovací údaje svého účtu metodě , abyste získali rozhraní pro [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) získání partnerských operací.

Pokud chcete vybrat konkrétní [objednávku,](order-resources.md#order)pomocí operací partnera a volání metody s identifikátorem zákazníka určete zákazníka a pak s identifikátorem objednávky určete objednávku a nakonec metodu nebo metodu pro [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) **`Orders.ById()`** **`Get`** **`GetAsync`** načtení.

Nastavte [**`Order.Status`**](order-resources.md#order) vlastnost na a pomocí metody `cancelled` **`Patch()`** aktualizujte pořadí.

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda     | Identifikátor URI žádosti                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Oprava** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/orders/{ID_objednávky} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K odstranění zákazníka použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci. |
| **ID objednávky** | **řetězec** | Y        | Hodnota je řetězec označující ID objednávek, které je potřeba zrušit. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a>Příklad požadavku

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí zrušenou objednávku.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
