---
title: Získání všech žádostí o službu pro zákazníka
description: Získá všechny žádosti o služby zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ffcbbb9cf14b1b2a5b3becab541d3042c3cad508
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760670"
---
# <a name="get-all-service-requests-for-a-customer"></a>Získání všech žádostí o službu pro zákazníka

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Získá všechny žádosti o služby zákazníka.

Na řídicím Partnerské centrum můžete tuto operaci provést tak, že nejprve [vyberete zákazníka](get-a-customer-by-name.md). Pak na levém **bočním** panelu vyberte Správa služeb. Žádosti o služby zákazníka se zobrazují v části **Lístky podpory**.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Pokud chcete zobrazit seznam všech žádostí o služby zákazníka, použijte kolekci **IAggregatePartner.Customers** a zavolejte [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) Potom zavolejte [**vlastnost ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) a pak metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) nebo [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync)

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** PartnerCenterSDK.FeaturesSamples **– třída:** CustomerManagedServices.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/servicerequests HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Pomocí následujícího parametru dotazu získejte všechny žádosti o služby pro zákazníka.

| Název                   | Typ     | Vyžadováno | Popis                            |
|------------------------|----------|----------|----------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Identifikátor GUID odpovídající zákazníkovi. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

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

V případě úspěchu vrátí tato  metoda v textu odpovědi kolekci prostředků žádosti o služby.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

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
