---
title: Aktualizace žádosti o službu
description: Jak aktualizovat existující žádost o služby zákazníkům, kterou poskytovatel cloudového řešení uzavřel s Microsoftem jménem zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1df0d1f5fa4630b346d1c8b9cffabb86ce34cfb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766998"
---
# <a name="update-a-service-request"></a>Aktualizace žádosti o službu

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Jak aktualizovat existující žádost o služby zákazníkům, kterou poskytovatel cloudového řešení uzavřel s Microsoftem jménem zákazníka.

Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md). Pak na levém bočním panelu vyberte **Správa služeb** . V části **žádosti o podporu** vyberte příslušný požadavek služby. Chcete-li dokončit, proveďte požadované změny žádosti o služby a pak vyberte **Odeslat.**

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID žádosti o službu.

## <a name="c"></a>C\#

Chcete-li aktualizovat žádost o služby zákazníka, zavolejte metodu [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) s ID žádosti služby a identifikujte a vraťte rozhraní žádosti o služby. Pak zavolejte metodu [**IServiceRequest. patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) nebo [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) a aktualizujte žádost o službu. Chcete-li zadat aktualizované hodnoty, vytvořte nový prázdný objekt [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) a nastavte pouze hodnoty vlastností, které chcete změnit. Pak předejte tento objekt ve volání metody patch nebo PatchAsync.

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdatePartnerServiceRequest.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **POUŽITA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{ServiceRequest-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K aktualizaci žádosti o službu použijte následující parametr identifikátoru URI.

| Název                  | Typ     | Vyžadováno | Popis                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **ServiceRequest-ID** | **guid** | Y        | Identifikátor GUID, který identifikuje požadavek služby. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Text žádosti by měl obsahovat prostředek [ServiceRequest](service-request-resources.md) . Jediné požadované hodnoty jsou ty, které se mají aktualizovat.

### <a name="request-example"></a>Příklad požadavku

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí prostředek **žádosti o službu** s aktualizovanými vlastnostmi v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
