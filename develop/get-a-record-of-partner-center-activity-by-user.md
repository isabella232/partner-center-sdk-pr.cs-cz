---
title: Získání záznamu o aktivitě Partnerského centra
description: Jak načíst záznam o operacích provedených uživatelem partnera nebo aplikací v časovém období
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aec933d4b681d99080619505792bde56bdd25580
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873967"
---
# <a name="get-a-record-of-partner-center-activity"></a>Získání záznamu o aktivitě Partnerského centra

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Tento článek popisuje, jak načíst záznam operací provedených partnerským uživatelem nebo aplikací v průběhu časového období.

Pomocí tohoto rozhraní API můžete načíst záznamy auditu za posledních 30 dnů od aktuálního data nebo pro rozsah dat určený zahrnutím počátečního a/nebo koncového data. Upozorňujeme ale, že z důvodů výkonu je dostupnost dat protokolu aktivit omezená na předchozích 90 dnů. Požadavky s počátečním datem delším než 90 dní před aktuálním datem obdrží výjimku chybný požadavek (kód chyby: 400) a příslušnou zprávu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

## <a name="c"></a>C\#

Pokud chcete načíst záznam Partnerské centrum operací, nejprve vytvořte rozsah dat pro záznamy, které chcete načíst. Následující příklad kódu používá pouze počáteční datum, ale můžete také zahrnout koncové datum. Další informace najdete v tématu [**Metoda**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) dotazu. Dále vytvořte proměnné, které potřebujete pro typ filtru, který chcete použít, a přiřaďte příslušné hodnoty. Pokud chcete například filtrovat podle podřetězce názvu společnosti, vytvořte proměnnou pro podřetězec. Pokud chcete filtrovat podle ID zákazníka, vytvořte proměnnou pro jeho id.

V následujícím příkladu je k dispozici vzorový kód pro filtrování podle podřetězce názvu společnosti, ID zákazníka nebo typu prostředku. Vyberte jednu a okomentování ostatních. V každém případě nejprve vytvoříte instanci objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) pomocí [**výchozího**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) konstruktoru pro vytvoření filtru. Budete muset předat řetězec, který obsahuje pole k hledání, a odpovídající operátor, který se má použít, jak je znázorněno níže. Musíte také zadat řetězec, podle který chcete filtrovat.

Dále pomocí vlastnosti [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) získejte rozhraní pro operace se záznamy auditu a voláním metody [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) nebo [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) spusťte filtr a získejte kolekci [**záznamů AuditRecord,**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) které představují první stránku výsledku. Metodě předejte počáteční datum, volitelné koncové datum, které zde není použité, a objekt [**IQuery,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) který představuje dotaz na entitu. Objekt IQuery se vytvoří předáním výše vytvořeného filtru do metody [**BuildSimpleQuery objektu**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) [**QueryFactory.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)

Jakmile máte počáteční stránku položek, pomocí metody [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) vytvořte enumerátor, který můžete použít k iteraci zbývajícími stránkami.

```csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (for example "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource.
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }

    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum **ukázky:** Auditování

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1                                                                                                     |
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1                                                                                   |
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1 |
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1          |
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1      |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření požadavku použijte následující parametry dotazu.

| Název      | Typ   | Vyžadováno | Popis                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Datum_spuštění | date   | No       | Počáteční datum ve formátu rrrr-mm-dd. Pokud se žádná možnost zadá, sada výsledků dotazu se nastaví na 30 dní před datem žádosti. Tento parametr je volitelný, pokud je zadán filtr.                                          |
| Enddate   | date   | No       | Koncové datum ve formátu rrrr-mm-dd. Tento parametr je volitelný, pokud je zadán filtr. Pokud je koncové datum vynecháno nebo nastaveno na hodnotu null, požadavek vrátí maximální okno nebo jako koncové datum použije ještě dnes , podle toho, která hodnota je menší. |
| filter    | řetězec | No       | Filtr, který se má použít. Tento parametr musí být zakódovaný řetězec. Tento parametr je volitelný, pokud je zadáno počáteční nebo koncové datum.                                                                                              |

### <a name="filter-syntax"></a>Syntaxe filtru
Parametr filtru musíte vytvořit jako řadu párů klíč-hodnota oddělených čárkami. Každý klíč a hodnota musí být jednotlivě uvozené a oddělené dvojtečkou. Celý filtr musí být kódovaný.

Nekódovaný příklad vypadá jako tento:

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

Následující tabulka popisuje požadované páry klíč-hodnota:

| Klíč                 | Hodnota                             |
|:--------------------|:----------------------------------|
| Pole               | Pole, které chcete filtrovat. Podporované hodnoty najdete v [syntaxi požadavku](get-a-record-of-partner-center-activity-by-user.md#rest-request).                                         |
| Hodnota               | Hodnota, podle které se má filtrovat. Případ hodnoty se ignoruje. Podporují se následující parametry hodnot, jak je znázorněno v [syntaxi požadavku](get-a-record-of-partner-center-activity-by-user.md#rest-request):<br/><br/>                                                                *searchSubstring* – nahraďte názvem společnosti. Můžete zadat podřetězec, který odpovídá části názvu společnosti (například bude `bri` odpovídat `Fabrikam, Inc` ).<br/>**Příklad:**`"Value":"bri"`<br/><br/>                                                                *customerId* – nahraďte řetězcem ve formátu GUID, který představuje identifikátor zákazníka.<br/>**Příklad:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`<br/><br/>                                                                                        *resourceType* – nahraďte typem prostředku, pro který se mají načíst záznamy auditu (například Předplatné). Dostupné typy prostředků jsou definované v [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).<br/>**Příklad:**`"Value":"Subscription"`                                 |
| Operátor          | Operátor, který se má použít. Podporované operátory najdete v [syntaxi požadavku](get-a-record-of-partner-center-activity-by-user.md#rest-request).   |

### <a name="request-headers"></a>Hlavičky požadavku

- Další informace najdete v tématu [Hlavičky REST](headers.md)centra součástí.

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí sadu aktivit, které splňují filtry.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```