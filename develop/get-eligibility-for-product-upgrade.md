---
title: Kontrola způsobilosti zákazníka k upgradu na plán Azure
description: Pomocí prostředku ProductUpgradeRequest můžete vrátit prostředek ProductUpgradesEligibility a zjistit, jestli má zákazník nárok na upgrade z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a72a9f2f3909ac4b3b74754b58a8d8d4745fbb2cadd101ad18cf487b1b02267a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996016"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Kontrola způsobilosti zákazníka k upgradu na plán Azure

Pomocí prostředku [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) můžete zkontrolovat, jestli má zákazník nárok na upgrade na plán Azure z předplatného Microsoft Azure (MS-AZR-0145P). Tato metoda vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) s nárokem zákazníka na upgrade produktu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele. Při použití [ověřování aplikací a uživatelů](enable-secure-app-model.md) s využitím rozhraní API pro Partnerské centrum aplikací postupujte podle modelu zabezpečené aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Produktová skupina.

## <a name="c"></a>C\#

Pokud chcete zkontrolovat, jestli má zákazník nárok na upgrade na plán Azure:

1. Vytvořte objekt **ProductUpgradesRequest** a jako produktové skupiny zadejte identifikátor zákazníka a "Azure".

2. Použijte **kolekci IAggregatePartner.ProductUpgrades.**
3. Zavolejte **metodu CheckEligibility** a předejte objekt **ProductUpgradesRequest,** který vrátí objekt **ProductUpgradesEligibility.**

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Text požadavku musí obsahovat prostředek [**ProductUpgradeRequest.**](product-upgrade-resources.md#productupgraderequest)

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
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
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
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
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
