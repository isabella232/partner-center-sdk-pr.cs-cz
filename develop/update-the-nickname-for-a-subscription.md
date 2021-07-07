---
title: Aktualizace přezdívky pro předplatné
description: Aktualizuje popisný název nebo přezdívku pro předplatné zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 195a85fcf29b3e4c9fe0e578d4d8cb80ca068c40
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530000"
---
# <a name="update-the-nickname-for-a-subscription"></a>Aktualizace přezdívky pro předplatné

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Aktualizuje popisný název nebo přezdívku pro předplatné [zákazníka.](subscription-resources.md) Tento název se Partnerské centrum, který vám pomůže rozlišit předplatná v účtu zákazníka.

Na řídicím Partnerské centrum můžete tuto operaci provést tak, že nejprve [vyberete zákazníka](get-a-customer-by-name.md). Pak vyberte předplatné, které chcete přejmenovat. Dokončete to tak, že v poli Název předplatného **změníte** název a pak vyberete **Odeslat.**

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného.

## <a name="c"></a>C\#

Pokud chcete aktualizovat přezdívku předplatného zákazníka, nejprve [získejte](get-a-subscription-by-id.md)předplatné a pak změňte vlastnost [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) předplatného. Po změně použijte kolekci [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a zavolejte [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) Potom zavolejte [**vlastnost Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) a pak [**metodu ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) Potom dokončete voláním [**metody Patch().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** PartnerSDK.FeatureSamples – **třída:** UpdateSubscription.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda    | Identifikátor URI žádosti                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **Oprava** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{id-pro-předplatné} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Tato tabulka uvádí požadovaný parametr dotazu pro aktualizaci přezdívky předplatného.

| Název                    | Typ     | Vyžadováno | Popis                          |
|-------------------------|----------|----------|--------------------------------------|
| **customer-tenant-id**  | **guid** | Y        | ID **tenanta zákazníka** (GUID). |
| **id-for-subscription** | **guid** | Y        | ID předplatného (GUID).        |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

V textu **požadavku** se vyžaduje úplný prostředek předplatného. Ujistěte se, že byla aktualizována vlastnost **FriendlyName.**

### <a name="request-example"></a>Příklad požadavku

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "<subscriptionID>",
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
    OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda [v](subscription-resources.md) textu odpovědi aktualizované vlastnosti prostředku předplatného.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

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
    "Id": "<subscriptionID>",
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
