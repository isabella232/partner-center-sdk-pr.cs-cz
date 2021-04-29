---
title: Zrušení objednávky z integrace izolovaného prostoru
description: Naučte se používat rozhraní API partnerského centra ke zrušení různých typů objednávek předplatného z účtů izolovaného prostoru integrace.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3bf862c62804a56e6f73dd3ec36d2e9eb65f997
ms.sourcegitcommit: f59a9311c8a37d45695caf74794ec1697426acc9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2021
ms.locfileid: "108210015"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Zrušení objednávky z izolovaného prostoru integrace pomocí rozhraní API partnerského centra

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozované společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak pomocí rozhraní API partnerského centra zrušit různé typy objednávek předplatného z účtů karantény integrace. Takové objednávky můžou zahrnovat rezervované instance, software a komerční objednávky předplatného SaaS (software jako služba) na webu Marketplace.

>[!NOTE] 
>Pamatujte na to, že zrušení rezervovaných instancí nebo komerčních předplatných SaaS na webu Marketplace je možné pouze z účtů karantény integrace. Jakékoli objednávky izolovaného prostoru (sandbox), které jsou starší než 60 dní, nelze zrušit z partnerského centra. Pokud potřebujete pomoc, můžete se obrátit na podporu partnerského centra. 

Pokud chcete zrušit výrobní zakázky softwaru prostřednictvím rozhraní API, použijte [Zrušit – software – nákupy](cancel-software-purchases.md).
Pomocí [zrušit nákup](/partner-center/csp-software-subscriptions)můžete také zrušit výrobní zakázky softwaru prostřednictvím řídicího panelu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- Partnerský účet integrace izolovaného prostoru (sandbox) se zákazníkem s aktivní rezervovanou instancí/softwarem nebo SaaS předplatnými třetích stran.

## <a name="c"></a>C\#

Pokud chcete objednávku zrušit z karantény integrace Integration, předejte přihlašovací údaje účtu do [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metody, abyste získali [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) rozhraní pro získání partnerských operací.

Chcete-li vybrat konkrétní [objednávku](order-resources.md#order), použijte operace partnera a [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metodu volání s identifikátorem zákazníka a určete tak zákazníka, následovaný **`Orders.ById()`** identifikátorem objednávky a určete tak objednávku a nakonec **`Get`** nebo **`GetAsync`** metodu, kterou chcete načíst.

Nastavte [**`Order.Status`**](order-resources.md#order) vlastnost na `cancelled` a použijte **`Patch()`** metodu pro aktualizaci pořadí.

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

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda     | Identifikátor URI žádosti                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **POUŽITA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K odstranění zákazníka použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci. |
| **ID objednávky** | **řetězec** | Y        | Hodnota je řetězec, který označuje ID objednávek, které je třeba zrušit. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu vrátí tato metoda objednávku Canceled.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
