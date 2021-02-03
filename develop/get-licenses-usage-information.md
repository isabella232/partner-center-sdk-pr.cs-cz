---
title: Získání informací o využití licencí
description: Jak získat informace o využití licencí na úrovni úloh pro Office a Dynamics
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2020
ms.locfileid: "97766894"
---
# <a name="get-licenses-usage-information"></a>Získání informací o využití licencí

**Platí pro**

- Partnerské centrum

Jak získat informace o využití licencí na úrovni úloh pro Office a Dynamics

## <a name="prerequisites"></a>Požadavky

Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Usage/License/HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Parametr         | Typ     | Popis | Povinné |
|-------------------|----------|-------------|----------|
| top               | řetězec   | Počet řádků dat, který má být vrácen v požadavku. Maximální hodnota a výchozí hodnota, pokud není zadána, je 10000. Pokud je v dotazu více řádků, tělo odpovědi obsahuje další odkaz, který můžete použít k vyžádání další stránky dat. | No |
| Přeskočit              | int      | Počet řádků, které mají být v dotazu přeskočeny. Tento parametr použijte pro stránku s velkými datovými sadami. Například Top = 10000 a Skip = 0 načte prvních 10000 řádků dat, Top = 10000 a Skip = 10000 načte další 10000 řádků dat a tak dále. | No |
| filter            | řetězec   | Parametr *filtru* požadavku obsahuje jeden nebo více příkazů, které filtrují řádky v odpovědi. Každý příkaz obsahuje pole a hodnotu, které jsou spojeny s **`eq`** **`ne`** operátory nebo, a příkazy lze kombinovat pomocí operátoru OR **`and`** **`or`** . Tady je několik příkladů parametrů *filtru* :<br/><br/>*Filter = workloadCode EQ ' SFB '*<br/><br/>*Filter = workloadCode EQ ' SFB '* or (*Channel EQ ' prodejce '*)<br/><br/>Můžete zadat následující pole:<br/><br/>**workloadCode**<br/>**úloha úlohy**<br/>**serviceCode**<br/>**serviceName**<br/>**kanál**<br/>**customerTenantId**<br/>**customerName**<br/>**productId**<br/>**NázevVýrobku** | No |
| GroupBy           | řetězec   | Příkaz, který aplikuje agregaci dat pouze na zadaná pole. Můžete zadat následující pole:<br/><br/>**workloadCode**<br/>**úloha úlohy**<br/>**serviceCode**<br/>**serviceName**<br/>**channelcustomerTenantId**<br/>**customerName**<br/>**productId**<br/>**NázevVýrobku**<br/><br/>Vrácené řádky dat budou obsahovat pole zadaná v parametru *GroupBy* a také následující:<br/><br/>**licensesActive**<br/>**licensesQualified** | No |
| processedDateTime | DateTime | Jedna z nich může určovat datum, ze kterého byla zpracována data o využití. Výchozí hodnota je poslední datum, kdy byla data zpracována. | No |

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

V případě úspěchu obsahuje tělo odpovědi následující pole obsahující data o využití licencí.

| Pole             | Typ     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | řetězec   | Kód úlohy                                 |
| úloha úlohy      | řetězec   | Název úlohy                                 |
| serviceCode       | řetězec   | Kód služby                                  |
| serviceName       | řetězec   | Název služby                                  |
| kanál           | řetězec   | Název kanálu, prodejce                        |
| customerTenantId  | řetězec   | Jedinečný identifikátor pro zákazníka            |
| customerName      | řetězec   | Jméno zákazníka                                 |
| productId         | řetězec   | Jedinečný identifikátor produktu             |
| NázevVýrobku       | řetězec   | Název produktu                                  |
| licensesActive    | long     | Počet aktivních licencí na úlohu        |
| licensesQualified | long     | Počet kvalifikovaných licencí pro zatížení |
| processedDateTime | DateTime | Datum posledního zpracování dat         |

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
