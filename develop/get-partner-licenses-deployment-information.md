---
title: Získání informací o nasazení licencí pro partnery
description: Jak získat informace o nasazení licencí partnerů agregované tak, aby zahrnovaly všechny zákazníky.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2464242fc6dc4e7464511eac5d4197630e22fac0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445968"
---
# <a name="get-partner-licenses-deployment-information"></a>Získání informací o nasazení licencí pro partnery

Jak získat informace o nasazení licencí partnerů agregované tak, aby zahrnovaly všechny zákazníky.

> [!NOTE]
> Tento scénář je nástavěn pomocí [možnosti Získat informace o nasazení licencí.](get-licenses-deployment-information.md)

## <a name="prerequisites"></a>Požadavky

Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.

## <a name="c"></a>C\#

Pokud chcete načíst agregovaná data při nasazení licencí, nejprve z vlastnosti [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) získejte rozhraní pro operace shromažďování analýz na úrovni partnera. Pak z vlastnosti Licence načtěte rozhraní do analytické kolekce licencí na [**úrovni**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) partnera. Nakonec zavolejte [**metodu Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) a získejte agregovaná data o nasazení licencí. Pokud je metoda úspěšná, získáte kolekci objektů [**PartnerLicensesDeploymentInsights.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights)

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                           |
|---------|---------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu text odpovědi obsahuje kolekci [prostředků PartnerLicensesDeploymentInsights,](analytics-resources.md#partnerlicensesdeploymentinsights) které poskytují informace o nasazených licencích.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
    "totalCount": 2,
    "items": [{
            "proratedDeploymentPercent": 0.0,
            "licensesSold": 343,
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }, {
            "proratedDeploymentPercent": 1.0,
            "licensesSold": 4464,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
