---
title: Získání rozpočtu útraty využití zákazníka
description: Rozpočet útraty (objekt SpendingBudget) můžete použít k aktualizaci souhrnu využití zákazníků (prostředek CustomerUsageSummary).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8be9ceaab6b7546de8eacba1e52e8766719e5125
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766866"
---
# <a name="get-a-customers-usage-spending-budget"></a>Získání rozpočtu útraty využití zákazníka

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Rozpočet útraty (objekt **SpendingBudget** ) můžete aktualizovat v [souhrnu využití zákazníků (prostředek **CustomerUsageSummary** )](customer-usage-resources.md#customerusagesummary).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aktualizace rozpočtu útraty využívání zákazníka:

1. Vytvoří nový objekt [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) s aktualizovanou velikostí.

2. Pomocí kolekce [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) volejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) se zadaným identifikátorem zákazníka.

3. Zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) , abyste získali rozpočet využití zákazníka.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/usagebudget HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Pro aktualizaci fakturačního profilu použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Úplný prostředek.

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí rozpočet útraty uživatele s aktualizovanou velikostí.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"GET",
            "headers":[]
        }
    }
}
```
