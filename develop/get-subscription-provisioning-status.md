---
title: Získání stavu zřizování předplatných
description: Jak získat stav zřizování předplatného pro předplatné zákazníka
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b36776279171186da7d81f9c1ff3d0828206fc2749ab8108f882ad7460575d60
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995556"
---
# <a name="get-subscription-provisioning-status"></a>Získání stavu zřizování předplatných

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Jak získat stav zřizování předplatného pro předplatné zákazníka

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor předplatného.

- K provedení této operace se u předplatného vyžaduje delegovaná oprávnění správce.

## <a name="c"></a>C\#

Pokud chcete získat stav zřizování předplatného, začněte k identifikaci zákazníka pomocí metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka. Pak získejte rozhraní pro operace předplatného voláním metody [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID předplatného. Dále pomocí vlastnosti [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) získejte rozhraní pro operace stavu zřizování aktuálního předplatného a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) nebo [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) která načte [**objekt SubscriptionProvisioningStatus.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus)

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/provisioningstatus HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka a předplatného použijte následující parametry cesty.

| Název            | Typ   | Vyžadováno | Popis                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| id zákazníka     | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.     |
| id předplatného | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje odběr. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu bude text odpovědi obsahovat [prostředek SubscriptionProvisioningStatus.](subscription-resources.md#subscriptionprovisioningstatus)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a>Poznámky

- Během přiřazení změny licence se pole stavu ve [stavu SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) nastaví na Pending (Čeká na vyřízení).

- Pole stavu se aktualizuje každých 15 minut.
