---
title: Získání dat o využití pro předplatné podle měřiče
description: Pomocí kolekce prostředků MeterUsageRecord můžete získat záznamy o využití měřičů zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766800"
---
# <a name="get-usage-data-for-subscription-by-meter"></a>Získání dat o využití pro předplatné podle měřiče

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Pomocí kolekce prostředků **MeterUsageRecord** můžete získat záznamy o využití měřičů zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období. Tato kolekce prostředků představuje agregovaný součet pro každý měřič pro aktuální fakturační cyklus v rámci celého plánu Azure.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného

*Tato nová trasa je ekvivalentní k `subscriptions/{subscription-id}/usagerecords/resources` , což bude i nadále fungovat jenom pro předplatná Microsoft Azure (MS-AZR-0145P).* Tato nová trasa bude podporovat předplatná Microsoft Azure (MS-AZR-0145P) i plány Azure. Chcete-li získat tyto informace pro plán Azure, musíte přepnout do této nové trasy. Kromě vlastností uvedených v následujících částech je odpověď stejná jako u staré trasy.

## <a name="c"></a>C\#

Postup získání záznamů využití měřiče zákazníka pro konkrétní službu nebo prostředek Azure během aktuálního fakturačního období:

1. Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .

2. Zavolejte vlastnost Subscriptions a pak vlastnost **měřiče** ( **UsageRecords**). Dokončete voláním metod Get () nebo GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

Příklad naleznete v následující ukázce:

- Ukázka: [aplikace testů konzoly](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Třída: **GetSubscriptionUsageRecordsByMeter.cs**

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/meterusagerecords HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání informací o využití ohodnocených zákazníkem.

| Název                   | Typ     | Vyžadováno | Popis                               |
|------------------------|----------|----------|-------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Identifikátor GUID, který odpovídá zákazníkovi.     |
| **ID předplatného**    | **guid** | Y        | Identifikátor GUID odpovídající identifikátoru [prostředku předplatného](subscription-resources.md#subscription)partnerského centra, který představuje předplatné Microsoft Azure (MS-AZR-0145P) nebo plán Azure. *V části plánování prostředků předplatného Azure zadejte **ID plánu** jako **ID předplatného** v této trase.* |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek **PagedResourceCollection \<MeterUsageRecord>** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Příklad odpovědi pro předplatná Microsoft Azure (MS-AZR-0145P)

V tomto příkladu si zákazník koupil **145P Azure PayG**.

*Pro zákazníky s předplatným Microsoft Azure (MS-AZR-0145P) nedojde k žádné změně v odpovědi rozhraní API.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Příklad odpovědi REST pro plán Azure

V tomto příkladu si zákazník koupil plán Azure.

*Pro zákazníky s plány Azure jsou v odpovědi rozhraní API tyto změny:*

- **currencyLocale** se nahrazuje **currencyCode**
- **usdTotalCost** je nové pole.

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
