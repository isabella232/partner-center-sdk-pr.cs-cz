---
title: Získání informací o nasazení licencí
description: Jak získat informace o nasazení pro Office a Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c47ab4f839c102c7a7bcab0169bf13955ab49beb97c48800e882598714347e67
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990711"
---
# <a name="get-licenses-deployment-information"></a>Získání informací o nasazení licencí

Jak získat informace o nasazení pro Office a Dynamics.

## <a name="prerequisites"></a>Požadavky

Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="uri-parameters"></a>Parametry identifikátoru URI

| Parametr         | Typ     | Popis | Povinné |
|-------------------|----------|-------------|----------|
| top               | řetězec   | Počet řádků dat, které se v požadavku vrátí. Maximální hodnota a výchozí hodnota, pokud není zadaná, je 10 000. Pokud dotaz obsahuje více řádků, obsahuje text odpovědi další odkaz, který můžete použít k vyžádání další stránky dat. | No |
| Přeskočit              | int      | Počet řádků, které se v dotazu přeskočí Tento parametr použijte k stránkování velkých datových sad. Například top=10000 a skip=0 načte prvních 10 000 řádků dat, top=10000 a skip=10000 načte dalších 1 0000 řádků dat atd. | No |
| filter            | řetězec   | Parametr *filter* požadavku obsahuje jeden nebo více příkazů, které filtruje řádky v odpovědi. Každý příkaz obsahuje pole a hodnotu, které jsou přidruženy k operátorům nebo , a příkazy `eq` `ne` lze kombinovat pomocí `and` nebo `or` . Tady je několik příkladů *parametrů* filtru:<br/><br/> *filter=serviceCode eq 'O365'*<br/> *filter=serviceCode eq 'O365'* nebo (*channel eq 'Reseller'*)<br/><br/> Můžete zadat následující pole:<br/><br/>**serviceCode (kód služby)**<br/>**Název_služby**<br/>**Kanál**<br/>**customerTenantId**<br/>**customerName**<br/>**Productid**<br/>**Productname**  | No |
| Groupby           | řetězec   | Příkaz, který použije agregaci dat pouze na zadaná pole. Můžete zadat následující pole:<br/><br/>**serviceCode (kód služby)**<br/>**Název_služby**<br/>**Kanál**<br/>**customerTenantId**<br/>**customerName**<br/>**Productid**<br/>**Productname**<br/><br/> Vrácené řádky dat budou obsahovat pole zadaná v *parametru groupby* a následující:<br/><br/>**licensesDeployed**<br/>**licensesSold**  | No |
| processedDateTime | DateTime | Můžete zadat datum, od kterého se data o využití zpracují. Výchozí hodnota je nejnovější datum zpracování dat. | No |

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje text odpovědi následující pole obsahující data o nasazených licencích.

| Pole             | Typ     | Description                           |
|-------------------|----------|---------------------------------------|
| serviceCode (kód služby)       | řetězec   | Kód služby                          |
| Název_služby       | řetězec   | Název služby                          |
| Kanál           | řetězec   | Název kanálu, prodejce                |
| customerTenantId  | řetězec   | Jedinečný identifikátor zákazníka    |
| customerName      | řetězec   | Jméno zákazníka                         |
| productId         | řetězec   | Jedinečný identifikátor produktu     |
| Productname       | řetězec   | Název produktu                          |
| licensesDeployed  | long     | Počet nasazených licencí           |
| licensesSold      | long     | Počet prodaných licencí               |
| processedDateTime | DateTime | Datum posledního zpracování dat |

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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
