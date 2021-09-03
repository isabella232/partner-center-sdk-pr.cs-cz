---
title: Získání seznamu produktů (podle země)
description: Pomocí prostředku produktu můžete získat kolekci produktů podle země zákazníka.
ms.date: 02/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 601fc2c8012d92d6964f0aaa29a3a46d732df300
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456048"
---
# <a name="get-a-list-of-products-by-country"></a>Získání seznamu produktů (podle země)

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Pomocí následujících metod můžete získat kolekci produktů dostupných v určité zemi.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- Země.

## <a name="c"></a>C\#

Získání seznamu produktů:

1. Pomocí kolekce **IAggregatePartner. Products** vyberte zemi pomocí metody **ByCountry ()** .

2. Vyberte zobrazení katalogu pomocí metody **ByTargetView ()** .

3. Volitelné Vyberte rozsah rezervace pomocí metody **ByReservationScope ()** .

4. Volitelné Vyberte cílový segment pomocí metody **ByTargetSegment ()** .

5. Volání metody **Get ()** nebo **GetAsync ()** pro vrácení kolekce.

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

1. Použijte funkci **IAggregatePartner. GetProducts** k výběru země pomocí funkce **byCountry ()** .

2. Vyberte zobrazení katalogu pomocí funkce **byTargetView ()** .
3. Volitelné Vyberte cílový segment pomocí funkce **byTargetSegment ()** .

4. Zavolejte funkci **Get ()** , která vrátí kolekci.

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

1. Spusťte příkaz [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) .

2. Vyberte katalog zadáním parametru **Catalog** .
3. Volitelné Vyberte cílový segment zadáním parametru **segmentu** .

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products? Country = {country} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

K získání seznamu produktů použijte následující cestu a parametry dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | řetězec   | Yes      | ID země nebo oblasti                                                  |
| targetView             | řetězec   | Yes      | Určuje cílové zobrazení katalogu. Podporované hodnoty jsou: <br/><br/>**Azure**, který zahrnuje všechny položky Azure<br/><br/>**AzureReservations**, která zahrnuje všechny položky rezervace Azure<br/><br/>**AzureReservationsVM**, která zahrnuje všechny položky rezervace virtuálních počítačů (VM)<br/><br/>**AzureReservationsSQL**, která zahrnuje všechny položky rezervace SQL<br/><br/>**AzureReservationsCosmosDb**, která zahrnuje všechny položky rezervace Cosmos databáze<br/><br/>**MicrosoftAzure**, která zahrnuje položky pro předplatná Microsoft Azure (**MS-AZR-0145P**) a plány Azure<br/><br/>**OnlineServices**, která zahrnuje všechny online položky služeb. Tato targetView zahrnuje komerční tržiště, tradiční služby založené na licencích a nové služby založené na licencích pro Commerce.<br/><br/>**Software**, který zahrnuje všechny softwarové položky<br/><br/>**SoftwareSUSELinux**, která zahrnuje všechny položky softwaru SUSE Linux<br/><br/>**SoftwarePerpetual**, která zahrnuje všechny trvalé softwarové položky<br/><br/>**SoftwareSubscriptions**, která zahrnuje všechny položky předplatného softwaru    |
| targetSegment          | řetězec   | No       | Identifikuje cílový segment. Zobrazení pro různé cílové skupiny. Podporované hodnoty jsou: <br/><br/>**prodejn**<br/>**školení**<br/>**schod**<br/>**neziskové**  |
| reservationScope | řetězec   | No | Při dotazování na seznam produktů pro Azure Reservations určete, že se `reservationScope=AzurePlan` má získat seznam produktů, které se vztahují k plánům Azure. vyloučením tohoto parametru získáte seznam produktů pro rezervace Azure, které se vztahují na předplatná Microsoft Azure (**MS-AZR-0145P**).  |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-examples"></a>Příklady požadavků

#### <a name="products-by-country"></a>Produkty podle země

podle tohoto příkladu získejte seznam produktů podle země pro předplatná Microsoft Azure (MS-AZR-0145P) a plány Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Rezervace virtuálních počítačů Azure (plán Azure)

Podle tohoto příkladu Získejte seznam produktů podle zemí pro rezervace virtuálních počítačů Azure, které platí pro plány Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>rezervace virtuálních počítačů Azure pro předplatná Microsoft Azure (MS-AZR-0145P)

podle tohoto příkladu získejte seznam produktů podle zemí pro rezervace virtuálních počítačů Azure, které platí pro odběry služby Microsoft Azure AZR (MS--0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="new-commerce-license-based-services"></a>Nové obchodní služby založené na licencích

> [!Note] 
> Nové obchodní změny jsou momentálně dostupné jenom pro partnery, kteří jsou součástí M365/D365 New Commerce Experience Technical Preview.

Podle tohoto příkladu Získejte seznam produktů podle země pro nové služby založené na licencích na licencování jako součást nového prostředí pro obchod s Technical Preview. Nové služby založené na licencích pro Commerce Services se identifikují podle ID a displayNames hodnot **OnlineServicesNCE**. Viz příklad odpovědi níže.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=OnlineServices HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci prostředků [**produktu**](product-resources.md#product) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).

Tato metoda vrací následující kódy chyb:

| Stavový kód HTTP     | Kód chyby   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Přístup k požadovanému targetSegment není povolený.                                                     |
| 403                  | 400036       | Přístup k požadovanému objektu targetView není povolený.                                                        |

### <a name="response-example-for-azure-vm-reservations-azure-plan"></a>Příklad odpovědi na rezervace virtuálních počítače Azure (plán Azure)

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

### <a name="response-example-for-new-commerce-license-based-services"></a>Příklad odpovědi pro nové komerční služby založené na licencích

> [!Note] 
> Nové obchodní změny jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview

```http
{
  "totalCount": 19,
  "items": [{
      "id": "CFQ7TTC0LH18",
      "title": "Microsoft 365 Business Basic",
      "description": "Best for businesses that need professional email, cloud file storage, and online meetings & chat. Desktop versions of Office apps like Excel, Word, and PowerPoint not included. For businesses with up to 300 employees.",
      "productType": {
        "id": "OnlineServicesNCE",
        "displayName": "OnlineServicesNCE"
      },
      "isMicrosoftProduct": true,
      "publisherName": "Microsoft Corporation",
      "links": {
        "skus": {
          "uri": "/products/CFQ7TTC0LH18/skus?country=US",
          "method": "GET",
          "headers": []
        },
        "self": {
          "uri": "/products/CFQ7TTC0LH18?country=US",
          "method": "GET",
          "headers": []
        }
      }
    },
    ...
  ],
  "links": {
    "self": {
      "uri": "/products?country=US&targetView=OnlineServices",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```

