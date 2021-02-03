---
title: Opětovná aktivace pozastaveného předplatného
description: Znovu aktivuje předplatné, které bylo dříve pozastaveno kvůli neplatbě. Na řídicím panelu partnerského centra se tato operace dá provést při prvním výběru zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17c63e9c6d4c9e111bfea28e97319696534fa122
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766956"
---
# <a name="reactivate-a-suspended-subscription"></a>Opětovná aktivace pozastaveného předplatného

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Znovu aktivuje [předplatné](subscription-resources.md) , které bylo dříve pozastaveno kvůli neplatbě.

Na řídicím panelu partnerského centra se tato operace dá provést při prvním [výběru zákazníka](get-a-customer-by-name.md). Pak vyberte příslušné předplatné, které chcete přejmenovat. Chcete-li dokončit, klikněte na tlačítko **aktivní** a pak vyberte **Odeslat.**

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného.

## <a name="c"></a>C\#

Pokud chcete znovu aktivovat předplatné zákazníka, nejdřív [získejte předplatné](get-a-subscription-by-id.md)a pak změňte vlastnost [**status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) odběru. Informace o **stavových** kódech naleznete v [SubscriptionStatus Enumeration/dotnet/API/Microsoft. Store. partnercenter. Models. Subscriptions. SubscriptionStatus). Po provedení změny použijte svou kolekci [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) . Poté zavolejte vlastnost [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a potom metodu [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) . Potom dokončete voláním metody [**patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) .

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: FeatureSamplesApplication. **Třída**: UpdateSubscription

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **POUŽITA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{ID-for-Subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro opětovnou aktivaci předplatného.

| Název                    | Typ     | Vyžadováno | Popis                               |
|-------------------------|----------|----------|-------------------------------------------|
| **Customer-tenant-ID**  | **guid** | Y        | Identifikátor GUID, který odpovídá zákazníkovi.     |
| **ID pro předplatné** | **guid** | Y        | Identifikátor GUID, který odpovídá předplatnému. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

V těle žádosti se vyžaduje prostředek s úplným **předplatným** . Ujistěte se, že se vlastnost **status** aktualizovala.

### <a name="request-example"></a>Příklad požadavku

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí aktualizované vlastnosti prostředku [předplatného](subscription-resources.md) v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
