---
title: Získání seznamu produktů (podle země)
description: Pomocí prostředku Product můžete získat kolekci produktů podle země zákazníka.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1258727ecbe7c5cc332624577fa8a355e28e3717
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874206"
---
# <a name="get-a-list-of-products-by-country"></a>Získání seznamu produktů (podle země)

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Následující metody můžete použít k získání kolekce produktů dostupných v konkrétní zemi.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- Země.

## <a name="c"></a>C\#

Získání seznamu produktů:

1. Pomocí kolekce **IAggregatePartner.Products** vyberte zemi pomocí metody **ByCountry().**

2. Vyberte zobrazení katalogu pomocí **metody ByTargetView().**

3. (Volitelné) Vyberte rozsah rezervace pomocí metody **ByReservationScope().**

4. (Volitelné) Vyberte cílový segment pomocí metody **ByTargetSegment().**

5. Voláním **metody Get()** nebo **GetAsync()** vrátíte kolekci.

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Získání seznamu produktů:

1. Pomocí funkce **IAggregatePartner.getProducts** vyberte zemi pomocí funkce **byCountry().**

2. Vyberte zobrazení katalogu pomocí **funkce byTargetView().**
3. (Volitelné) Vyberte cílový segment pomocí funkce **byTargetSegment().**

4. Voláním **funkce get()** vrátíte kolekci.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Získání seznamu produktů:

1. Spusťte příkaz [**Get-PartnerProduct.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)

2. Katalog vyberte zadáním **parametru Catalog.**
3. (Volitelné) Vyberte cílový segment zadáním **parametru Segment.**

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K získání seznamu produktů použijte následující cestu a parametry dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | řetězec   | Yes      | ID země nebo oblasti.                                                  |
| targetView             | řetězec   | Yes      | Identifikuje cílové zobrazení katalogu. Podporované hodnoty jsou: <br/><br/>**Azure**, který zahrnuje všechny položky Azure<br/><br/>**AzureReservations**, která zahrnuje všechny položky rezervací Azure<br/><br/>**AzureReservationsVM**, který zahrnuje všechny položky rezervace virtuálních počítačů<br/><br/>**AzureReservationsSQL**, který zahrnuje všechny SQL položek rezervace<br/><br/>**AzureReservationsCosmosDb**, který zahrnuje všechny Cosmos položek rezervace databáze<br/><br/>**MicrosoftAzure**, který obsahuje položky pro Microsoft Azure předplatná (**MS-AZR-0145P)** a plány Azure<br/><br/>**Onlineslužby**, které zahrnují všechny položky online služeb (včetně produktů komerčního marketplace)<br/><br/>**Software**, který zahrnuje všechny softwarové položky<br/><br/>**SoftwareSUSELinux**, který zahrnuje všechny položky softwaru SUSE Linux<br/><br/>**SoftwarePerpetual**, který zahrnuje všechny časově neomezené softwarové položky<br/><br/>**Předplatná softwaru**, která zahrnují všechny položky předplatného softwaru    |
| TargetSegment          | řetězec   | No       | Identifikuje cílový segment. Zobrazení pro různé cílové skupiny Podporované hodnoty jsou: <br/><br/>**Obchodní**<br/>**Vzdělávání**<br/>**Vláda**<br/>**Neziskové**  |
| reservationScope | řetězec   | No | Při dotazování na seznam produktů pro rezervace Azure zadejte a získejte seznam produktů, které se `reservationScope=AzurePlan` vztahují k plánům Azure. Tento parametr vyloučíte, pokud chcete získat seznam produktů pro rezervace Azure, které se vztahují na předplatná Microsoft Azure (**MS-AZR-0145P).**  |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-examples"></a>Příklady požadavků

#### <a name="products-by-country"></a>Products by country

V tomto příkladu získáte seznam produktů podle země pro předplatná Microsoft Azure (MS-AZR-0145P) a plány Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Rezervace virtuálních počítače Azure (plán Azure)

V tomto příkladu získáte seznam produktů podle země pro rezervace virtuálních počítače Azure, které se vztahují na plány Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Rezervace virtuálních Microsoft Azure Azure (MS-AZR-0145P) předplatná

Postupujte podle tohoto příkladu a získejte seznam produktů pro rezervace virtuálních počítače Azure podle země, které se vztahují k předplatným Microsoft Azure (MS-AZR-0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu bude tělo odpovědi obsahovat kolekci prostředků [**Product.**](product-resources.md#product)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)

Tato metoda vrátí následující kódy chyb:

| Stavový kód HTTP     | Kód chyby   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Přístup k požadovanému targetSegment není povolený.                                                     |
| 403                  | 400036       | Přístup k požadovanému objektu targetView není povolený.                                                        |

### <a name="response-example"></a>Příklad odpovědi

```http
{
    "totalCount": 19,
    "items": [
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
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
