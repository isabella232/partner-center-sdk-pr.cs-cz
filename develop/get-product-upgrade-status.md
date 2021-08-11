---
title: Získání stavu upgradu produktu pro zákazníka
description: Pomocí prostředku ProductUpgradeRequest můžete určit stav upgradu produktu zákazníka na novou produktové skupiny, například z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e33ac61d77fc4e14ff6f7801e2c15a968cf9f1a667087df612c0f76b216f891a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995743"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>Získání stavu upgradu produktu pro zákazníka

Stav upgradu na novou produktové rodinu můžete získat pomocí prostředku [**ProductUpgradeRequest.**](product-upgrade-resources.md#productupgraderequest) Tento prostředek se použije při upgradu zákazníka z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure. Úspěšný požadavek vrátí [**prostředek ProductUpgradesEligibility.**](product-upgrade-resources.md#productupgradeseligibility)

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele. Při použití [ověřování aplikací a uživatelů](enable-secure-app-model.md) s využitím rozhraní API pro Partnerské centrum aplikací postupujte podle modelu zabezpečené aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Produktová skupina.

- ID upgradu žádosti o upgrade

## <a name="c"></a>C\#

Pokud chcete zkontrolovat, jestli má zákazník nárok na upgrade na plán Azure:

1. Vytvořte objekt **ProductUpgradesRequest** a jako produktové skupiny zadejte identifikátor zákazníka a "Azure".

2. Použijte **kolekci IAggregatePartner.ProductUpgrades.**

3. Zavolejte **metodu ById** a předejte **id upgradu.**

4. Zavolejte **metodu CheckStatus** a předejte objekt **ProductUpgradesRequest,** který vrátí objekt **ProductUpgradeStatus.**

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti |
|----------|-----------------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{id_upgradu}/stav HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Pomocí následujícího parametru dotazu zadejte zákazníka, pro kterého máte stav upgradu produktu.

| Název               | Typ | Vyžadováno | Popis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **id upgradu** | Identifikátor GUID | Yes | Hodnota je identifikátor upgradu ve formátu GUID. Tento identifikátor můžete použít k určení upgradu, který chcete sledovat. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Text požadavku musí obsahovat prostředek [**ProductUpgradeRequest.**](product-upgrade-resources.md#productupgraderequest)

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v těle prostředek [**ProductUpgradesEligibility.**](product-upgrade-resources.md#productupgradeseligibility)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
