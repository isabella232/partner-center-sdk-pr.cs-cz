---
title: Získání informací o využití licencí
description: Jak získat informace o využití licencí na úrovni úloh pro Office a Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea3658089ce7eb5c1ad7cc65c3db34f9b6353cdd
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445969"
---
# <a name="get-licenses-usage-information"></a>Získání informací o využití licencí

Jak získat informace o využití licencí na úrovni úloh pro Office a Dynamics.

## <a name="prerequisites"></a>Požadavky

Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Parametr         | Typ     | Popis | Povinné |
|-------------------|----------|-------------|----------|
| top               | řetězec   | Počet řádků dat, které se v požadavku vrátí. Maximální hodnota a výchozí hodnota, pokud není zadaná, je 10 000. Pokud dotaz obsahuje více řádků, obsahuje text odpovědi další odkaz, který můžete použít k vyžádání další stránky dat. | No |
| Přeskočit              | int      | Počet řádků, které se v dotazu přeskočí Tento parametr použijte k stránkování velkých datových sad. Například top=10000 a skip=0 načte prvních 10 000 řádků dat, top=10000 a skip=10000 načte dalších 1 0000 řádků dat atd. | No |
| filter            | řetězec   | Parametr *filter* požadavku obsahuje jeden nebo více příkazů, které filtruje řádky v odpovědi. Každý příkaz obsahuje pole a hodnotu, které jsou přidruženy k operátorům nebo , a příkazy **`eq`** **`ne`** lze kombinovat pomocí **`and`** nebo **`or`** . Tady je několik příkladů *parametrů* filtru:<br/><br/>*filter=workloadCode eq 'SFB'*<br/><br/>*filter=workloadCode eq 'SFB'* nebo (*channel eq 'Reseller'*)<br/><br/>Můžete zadat následující pole:<br/><br/>**workloadCode (kód úlohy)**<br/>**název úlohy**<br/>**serviceCode (kód služby)**<br/>**Název_služby**<br/>**Kanál**<br/>**customerTenantId**<br/>**customerName**<br/>**Productid**<br/>**Productname** | No |
| Groupby           | řetězec   | Příkaz, který použije agregaci dat pouze na zadaná pole. Můžete zadat následující pole:<br/><br/>**workloadCode (kód úlohy)**<br/>**název úlohy**<br/>**serviceCode (kód služby)**<br/>**Název_služby**<br/>**channelcustomerTenantId**<br/>**customerName**<br/>**Productid**<br/>**Productname**<br/><br/>Vrácené řádky dat budou obsahovat pole zadaná v *parametru groupby* a následující:<br/><br/>**licensesActive**<br/>**licensesQualified** | No |
| processedDateTime | DateTime | Můžete zadat datum, od kterého se data o využití zpracují. Výchozí hodnota je nejnovější datum zpracování dat. | No |

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu bude text odpovědi obsahovat následující pole obsahující data o využití licencí.

| Pole             | Typ     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode (kód úlohy)      | řetězec   | Kód úlohy                                 |
| název úlohy      | řetězec   | Název úlohy                                 |
| serviceCode (kód služby)       | řetězec   | Kód služby                                  |
| Název_služby       | řetězec   | Název služby                                  |
| Kanál           | řetězec   | Název kanálu, prodejce                        |
| customerTenantId  | řetězec   | Jedinečný identifikátor zákazníka            |
| customerName      | řetězec   | Jméno zákazníka                                 |
| productId         | řetězec   | Jedinečný identifikátor produktu             |
| Productname       | řetězec   | Název produktu                                  |
| licensesActive    | long     | Počet aktivních licencí na úlohu        |
| licensesQualified | long     | Počet kvalifikovaných licencí pro úlohu |
| processedDateTime | DateTime | Datum posledního zpracování dat         |

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
