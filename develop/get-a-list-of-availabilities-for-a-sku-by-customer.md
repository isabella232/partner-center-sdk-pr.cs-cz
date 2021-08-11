---
title: Získání seznamu dostupností pro skladovou položku (podle zákazníka)
description: Můžete získat kolekci dostupnosti pro určitý produkt a SKU podle zákazníka pomocí identifikátorů zákazníka, produktu a SKU.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 682f4ece9098817f25e7709f3a8b9010d661fd1042589785778f5c434c37ed8e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995454"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a>Získání seznamu dostupností pro skladovou položku (podle zákazníka)

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Následující metody můžete použít k získání kolekce dostupnosti pro určitý produkt a SKU k dispozici konkrétnímu zákazníkovi.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor produktu (**ID produktu**).

- Identifikátor SKU (**SKU-ID**).

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda | Identifikátor URI žádosti                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/skus/{SKU-ID} HTTP/1.1 |

### <a name="request-uri-parameters"></a>Parametry identifikátoru URI žádosti

| Název               | Typ | Vyžadováno | Popis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| Customer-tenant-ID | Identifikátor GUID | Yes | Hodnota je **číslo zákazníka**, který je ve formátu GUID, což je identifikátor, který umožňuje zadat zákazníka. |
| ID produktu | řetězec | Yes | Řetězec, který identifikuje produkt. |
| SKU – ID | řetězec | Yes | Řetězec, který identifikuje SKU. |

### <a name="request-header"></a>Hlavička požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a>Odpověď REST

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

Tato metoda vrací následující kódy chyb:

| Stavový kód HTTP | Kód chyby | Description |
|------------------|------------|-------------|
| 404 | 400013 | Nadřazený produkt nebyl nalezen. |

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Microsoft Azure plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
