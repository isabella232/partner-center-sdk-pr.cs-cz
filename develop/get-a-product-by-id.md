---
title: Získání produktu podle ID
description: Získá zadaný produkt prostředku s použitím ID produktu.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 8aca626597e9ec903ebecca7d55577ba636c518e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766762"
---
# <a name="get-a-product-by-id"></a>Získání produktu podle ID

**Platí pro**

- Partnerské centrum

Získá zadaný produkt prostředku s použitím ID produktu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID produktu.

## <a name="c"></a>C\#

Chcete-li najít konkrétní produkt podle ID, použijte kolekci **IAggregatePartner. Products** , vyberte zemi pomocí metody **ByCountry ()** a potom zavolejte metodu **ById ()** . Nakonec voláním metody **Get ()** nebo **GetAsync ()** vraťte produkt.

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

Chcete-li najít konkrétní produkt podle ID, použijte funkci **IAggregatePartner. GetProducts** , vyberte zemi pomocí funkce **byCountry ()** a potom zavolejte funkci **byId ()** . Nakonec zavolejte funkci **Get ()** , která vrátí produkt.

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

Chcete-li najít konkrétní produkt podle ID, spusťte příkaz [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) a zadejte parametr **ProductID** . Parametr **CountryCode** je možností, pokud není zadaný, použije se země přidružená k prodejci.

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}? Country = {Country} HTTP/1.1  |

### <a name="uri-parameter"></a>Parametr URI

K získání zadaného produktu použijte následující parametry cesty.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ID produktu             | řetězec   | Yes      | Řetězec, který identifikuje produkt.                           |
| country                | řetězec   | Yes      | ID země nebo oblasti.                                            |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi [produktový](product-resources.md#product) prostředek.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

Tato metoda vrací následující kódy chyb:

| Stavový kód HTTP     | Kód chyby   | Description                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 400013       | Produkt nebyl nalezen.                                                     |

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
