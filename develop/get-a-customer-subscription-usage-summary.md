---
title: Získat Souhrn využití pro předplatné zákazníka
description: Pomocí prostředku SubscriptionUsageSummary můžete v aktuálním fakturačním období získat Souhrn využití předplatných konkrétní služby nebo prostředku Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30334b6f08829eccf0693b566c11f94cb3ece976
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766797"
---
# <a name="get-usage-summary-for-customers-subscription"></a>Získat Souhrn využití pro předplatné zákazníka

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Pomocí prostředku **SubscriptionUsageSummary** můžete získat Souhrn využití předplatných pro zákazníka. Tento prostředek představuje souhrn využití předplatných konkrétní služby nebo prostředku Azure během aktuálního fakturačního období.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor předplatného

## <a name="c"></a>C\#

Získání souhrnu využití předplatného pro předplatné zákazníka:

1. Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .

2. Pak zavolejte vlastnost Subscriptions a také vlastnost **UsageSummary** . Dokončete voláním metod Get () nebo GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

Příklad naleznete v následujících tématech:

- Ukázka: [aplikace testů konzoly](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Třída: **GetSubscriptionUsageSummary.cs**

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/usagesummary HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o využití ohodnocených zákazníkem.

| Název                   | Typ     | Vyžadováno | Popis                               |
|------------------------|----------|----------|-------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Identifikátor GUID, který odpovídá zákazníkovi.     |
| **ID předplatného**    | **guid** | Y        | Identifikátor GUID odpovídající identifikátoru předplatného. Pro plán Azure se jedná o identifikátor odpovídajícího [prostředku pro předplatné](subscription-resources.md#subscription)partnerského centra, který představuje plán Azure. *V části plánování prostředků předplatného Azure zadejte **ID plánu** jako **ID předplatného** v této trase.* |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek **SubscriptionUsageSummary** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Příklad odpovědi pro předplatná Microsoft Azure (MS-AZR-0145P)

V tomto příkladu si zákazník koupil nabídku **145P Azure PayG** .

*Pro zákazníky s předplatnými Microsoft Azure (MS-AZR-0145P) nedojde k žádné změně v odpovědi rozhraní API.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Příklad odpovědi REST pro plán Azure

V tomto příkladu si zákazník koupil plán Azure.

*Pro zákazníky s plány Azure jsou k dispozici následující změny odezvy rozhraní API:*

- **currencyLocale** se nahrazuje **currencyCode**
- **usdTotalCost** je nové pole.

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
