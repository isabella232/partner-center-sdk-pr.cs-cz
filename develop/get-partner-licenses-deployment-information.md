---
title: Získání informací o nasazení licencí pro partnery
description: Jak získat agregované informace o nasazení partnerských licencí, aby zahrnovaly všechny zákazníky.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 229f63d4df4f59cd0fde2bd0fc5e3f10cf6b25c0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767030"
---
# <a name="get-partner-licenses-deployment-information"></a>Získání informací o nasazení licencí pro partnery

**Platí pro**

- Partnerské centrum

Jak získat agregované informace o nasazení partnerských licencí, aby zahrnovaly všechny zákazníky.

> [!NOTE]
> Tento scénář se nahrazuje [informacemi o nasazení získat licence](get-licenses-deployment-information.md).

## <a name="prerequisites"></a>Požadavky

Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="c"></a>C\#

Chcete-li načíst agregovaná data při nasazení licencí, nejprve z vlastnosti [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) Získejte rozhraní k operacím shromažďování na úrovni partnera úrovně Analytics. Pak z vlastnosti [**licence**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) načtěte rozhraní pro kolekci Analytics License licenses Analytics. Nakonec zavolejte metodu [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) , která načte agregovaná data při nasazení licencí. Pokud je metoda úspěšná, získáte kolekci objektů [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) .

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                           |
|---------|---------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/licenses/Deployment HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) , které poskytují informace o nasazených licencích.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
