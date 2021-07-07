---
title: Odstranění zákaznického účet ze sandboxu pro integraci
description: Jak odstranit účet zákazníka z karantény integrace v produkčním prostředí (Tip)
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9d9e44ac9c40bd4e3c7e1a9e04253f853dfd96c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973124"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Odstranění zákaznického účet ze sandboxu pro integraci

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Tento článek vysvětluje, jak přerušit vztah mezi partnerem a účtem zákazníka a znovu získáte kvótu pro testování v izolovaném prostoru integrace (Tip) Integration.

> [!IMPORTANT]
> Když odstraníte účet zákazníka, vyprázdní se všechny prostředky přidružené k tomuto tenantovi zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Před odstraněním zákazníka z karantény integrace s tipem se musí zrušit všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru.

## <a name="c"></a>C\#

Odstranění zákazníka z izolovaného prostoru integrace s tipem:

1. Předání přihlašovacích údajů k účtu Tip metodě [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) k získání rozhraní [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) pro partnerské operace.

2. Pro načtení kolekce oprávnění použijte rozhraní partnerských operací:

    1. Pro určení zákazníka zavolejte metodu [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.

    2. Zavolejte vlastnost **oprávnění** .

    3. Pro načtení kolekce [**nároků**](entitlement-resources.md) zavolejte metodu **Get** nebo **GetAsync** .

3. Ujistěte se, že všechny nákupní objednávky Azure Reserved Virtual Machine Instances a softwaru pro tohoto zákazníka se zrušily. Pro každé [**oprávnění**](entitlement-resources.md) v kolekci:

    1. Použijte [**oprávnění. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) získat místní kopii odpovídajícího [pořadí](order-resources.md#order) z kolekce objednávek zákazníka.

    2. Nastavte vlastnost [**Order. status**](order-resources.md#order) na "zrušeno".

    3. K aktualizaci objednávky použijte metodu **patch ()** .

4. Zruší všechny objednávky. Například následující příklad kódu používá smyčku k cyklickému dotazování každého pořadí, dokud jeho stav není "zrušeno".

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be canceled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were canceled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. Zajistěte, aby byly všechny objednávky zrušené voláním metody **Delete** pro zákazníka.

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: partnerská **třída** PartnerCenterSDK. FeaturesSamples: DeleteCustomerFromTipAccount. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda     | Identifikátor URI žádosti                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID} HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

K odstranění zákazníka použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| Customer-tenant-ID     | Identifikátor GUID     | Y        | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda prázdnou odpověď.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
