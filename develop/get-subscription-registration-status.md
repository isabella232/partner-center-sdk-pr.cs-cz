---
title: Získání stavu registrace předplatných
description: Získejte stav předplatného, které je zaregistrované pro použití s Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e39f94c0eac402a0be3afde84279aa637868f96
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445948"
---
# <a name="get-subscription-registration-status"></a>Získání stavu registrace předplatných

Jak získat stav registrace předplatného pro zákaznické předplatné, které bylo povoleno pro nákup Azure Reserved VM Instances.

Pokud si chcete koupit rezervovanou instanci virtuálního počítače Azure pomocí rozhraní PARTNERSKÉ CENTRUM API, musíte mít alespoň jedno stávající předplatné Azure CSP. Metoda [Registrace předplatného](register-a-subscription.md) vám umožní zaregistrovat stávající předplatné Azure CSP a povolit ho pro nákup Azure Reserved VM Instances. Tato metoda umožňuje načíst stav této registrace.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného.

## <a name="c"></a>C\#

Pokud chcete získat stav registrace předplatného, začněte tím, že k identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka. Pak získejte rozhraní pro operace předplatného voláním metody [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) s ID předplatného pro identifikaci předplatného. Dále pomocí vlastnosti RegistrationStatus získejte rozhraní pro operace stavu registrace aktuálního předplatného a zavolejte metodu **Get** nebo **GetAsync** pro načtení **objektu SubscriptionRegistrationStatus.**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda    | Identifikátor URI žádosti                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Dostat**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/stav registrace HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka a předplatného použijte následující parametry cesty.

| Název                    | Typ       | Vyžadováno | Popis                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| id zákazníka             | řetězec     | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.         |
| id předplatného         | řetězec     | Yes      | Řetězec ve formátu GUID, který identifikuje odběr.     |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu bude tělo odpovědi obsahovat [prostředek SubscriptionRegistrationStatus.](subscription-resources.md#subscriptionregistrationstatus)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
