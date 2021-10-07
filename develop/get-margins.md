---
title: Načte seznam okrajů pro daného partnera.
description: Načte seznam okrajů pro daného partnera.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 3b36d2d560f3afe43af45e6001f6d407acf3f537
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646382"
---
# <a name="get-margins"></a>Získat okraje

**Platí pro**: partnerské Centrum 

**Příslušné role**: globální správce | Agent správce

Partneři můžou získat seznam aktivních marží pro daného partnera. Tato metoda vrací okraje na základě partnera a dostupných počátečních a koncových dat. 

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.


## <a name="rest-request"></a>Žádost REST
[GET]/v1/Margins

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Margins HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/margins HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda seznam okrajů.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo neúspěch a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
  "pageSize": 1,
  "totalSize": 2,
  "results": [
    {
      "id": "97620c21cc32_97cdce68-cce4-42aa-9410-233fd0269502",
      "productId": "DZH318Z08L40",
      "publisherName": "Market Place Test",
      "productTitle": "Software As A Service Support Preview App",
      "productType": "SaaS",
      "marginPercentage": 10.0,
      "startDate": "2021-08-04T23:16:22.4736653Z",
      "endDate": "2022-03-31T23:59:59Z",
      "status": "live",
      "statusDate": "2021-08-04T23:16:22.4736653Z"
    },
    {
      "id": "9f342f8c8f59_3be201f5-256d-4488-bd5c-6ffdeb9877ea",
      "productId": "DZH318Z08L40",
      "publisherName": "Market Place Test",
      "productTitle": "Software As A Service Support Preview App",
      "productType": "SaaS",
      "marginPercentage": 1.0,
      "startDate": "2021-08-05T21:44:35.8870924Z",
      "endDate": "2022-03-31T23:59:59Z",
      "status": "live",
      "statusDate": "2021-08-05T21:44:35.8870924Z"
    }
  ]
}
```
