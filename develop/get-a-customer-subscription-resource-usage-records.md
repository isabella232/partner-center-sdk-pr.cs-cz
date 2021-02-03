---
title: Získat data o využití pro předplatné podle prostředku
description: Pomocí prostředku ResourceUsageRecord můžete získat záznamy o využití prostředků zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e815430730dd7182380e9efd1fea80f9e84d2ce7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766798"
---
# <a name="get-usage-data-for-subscription-by-resource"></a>Získat data o využití pro předplatné podle prostředku

**Platí pro:**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak získat prostředek **ResourceUsageRecord** . Tento prostředek představuje agregovaný součet za měsíc pro jednotlivé prostředky zřízené v plánu Azure. Tento prostředek můžete použít k získání záznamů o využití prostředků zákazníka pro konkrétní služby nebo prostředky Azure během aktuálního fakturačního období. Toto rozhraní API vrací data, která nebyla dříve k dispozici prostřednictvím rozhraní API útraty Azure.

*Tato trasa nepodporuje odběry Microsoft Azure (MS-AZR-0145P).*

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor předplatného

## <a name="c"></a>C\#

Postup získání záznamů o využití prostředků zákazníka pro konkrétní službu nebo prostředek Azure během aktuálního fakturačního období:

1. Použijte svou kolekci **IAggregatePartner. Customers** pro volání metody **ById ()** .

2. Zavolejte vlastnost Subscriptions a také **UsageRecords** a pak vlastnost **Resources (prostředky** ). Dokončete voláním metod Get () nebo GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

Příklad naleznete v následujících tématech:

- Ukázka: [aplikace testů konzoly](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Třída: **GetSubscriptionUsageRecordsByResource.cs**

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/resourceusagerecords HTTP/1.1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek **PagedResourceCollection \<ResourceUsageRecord>** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
