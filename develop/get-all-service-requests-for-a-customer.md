---
title: Získání všech žádostí o službu pro zákazníka
description: Získá všechny žádosti o služby zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f473c7a7d43b1a3929d983fb23dae92fdafbc0f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767050"
---
# <a name="get-all-service-requests-for-a-customer"></a>Získání všech žádostí o službu pro zákazníka

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Získá všechny žádosti o služby zákazníka.

Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md). Pak na levém bočním panelu vyberte **Správa služeb** . Žádosti o služby zákazníka se zobrazí v části **lístky podpory**.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Pokud chcete zobrazit seznam všech žádostí o služby zákazníka, použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) . Potom zavolejte vlastnost [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) a za ní volejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) .

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: CustomerManagedServices.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/servicerequests HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K získání všech žádostí o služby pro zákazníka použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                            |
|------------------------|----------|----------|----------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Identifikátor GUID odpovídající zákazníkovi... |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí kolekci prostředků **žádosti o službu** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 742
Content-Type: application/json
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
Date: Tue, 24 Nov 2015 07:19:21 GMT

{
    "totalCount": 1,
    "items": [{
        "title": "Test",
        "severity": 0,
        "id": "615112491169010",
        "status": 1,
        "primaryContact": {
            "lastName": "LastName",
            "firstName": "FirstName"
        },
        "createdDate": "2015-11-24T01:07:00.863",
        "lastModifiedDate": "2015-11-24T01:17:10.61",
        "lastClosedDate": "0001-01-01T00:00:00",
        "attributes": {
            "objectType": "ServiceRequest"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
