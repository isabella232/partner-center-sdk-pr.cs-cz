---
title: Získejte podrobnosti o žádosti o služby podle ID.
description: Jak načíst podrobnosti o existující žádosti o služby zákazníkům podle ID.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ad22e5940781d514b00a6a25ca772fab338dc5584df09ac5a29fb2559e9538a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995692"
---
# <a name="get-service-request-details-by-id"></a>Získání podrobností žádostí o službu podle ID

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Jak načíst podrobnosti o existující žádosti o služby zákazníkům pomocí identifikátoru žádosti o služby

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID žádosti o služby.

## <a name="c"></a>C\#

Pokud chcete načíst podrobnosti o existující žádosti o služby zákazníkům, zavolejte metodu [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) a předejte [**ServiceRequest.Id,**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) abyste identifikovali a vrátili rozhraní pro konkrétní objekt [**ServiceRequest.**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest as ServiceRequest;

ServiceRequest serviceRequestDetails = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Get();

Console.WriteLine(string.Format("The primary contact for the service request {0} is {1} {2}.",
    serviceRequestDetails.Title,
    serviceRequestDetails.PrimaryContact.FirstName,
    serviceRequestDetails.PrimaryContact.LastName,
));
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda    | Identifikátor URI žádosti                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{id_požadavku_služby} HTTP/1.1  |

### <a name="uri-parameter"></a>Parametr URI

Pomocí následujícího parametru URI získejte zadaný požadavek na službu.

| Název                  | Typ     | Vyžadováno | Popis                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **id_události_služby** | **guid** | Y        | Identifikátor GUID, který identifikuje požadavek na službu. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda **v** textu odpovědi prostředek žádosti o služby.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
