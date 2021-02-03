---
title: Projděte si nárok zákazníka na upgrade na plán Azure
description: Prostředek ProductUpgradeRequest můžete použít k vrácení prostředku ProductUpgradesEligibility, abyste zjistili, jestli má zákazník nárok na upgrade z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766659"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Projděte si nárok zákazníka na upgrade na plán Azure

**Platí pro:**

- Partnerské centrum

Pomocí prostředku [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) můžete ověřit, jestli má zákazník nárok na upgrade na plán Azure z předplatného služby Microsoft Azure (MS-AZR-0145P). Tato metoda vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) s nárokem na upgrade produktu zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele. Použijte [zabezpečený model aplikace](enable-secure-app-model.md) při použití ověřování aplikací a uživatelů s rozhraními API partnerského centra.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Produktová řada.

## <a name="c"></a>C\#

Pokud chcete zjistit, jestli má zákazník nárok na upgrade na plán Azure, postupujte takto:

1. Vytvořte objekt **ProductUpgradesRequest** a zadejte identifikátor zákazníka a "Azure" jako produktovou řadu.

2. Použijte kolekci **IAggregatePartner. ProductUpgrades** .
3. Zavolejte metodu **CheckEligibility** a předejte ji do objektu **ProductUpgradesRequest** , který vrátí objekt **ProductUpgradesEligibility** .

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

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tělo žádosti musí obsahovat prostředek [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .

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

V případě úspěchu tato metoda vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) v těle.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
