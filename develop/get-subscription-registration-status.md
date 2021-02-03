---
title: Získání stavu registrace předplatných
description: Získejte stav předplatného, které je zaregistrované pro použití s Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767034"
---
# <a name="get-subscription-registration-status"></a>Získání stavu registrace předplatných

**Platí pro**

- Partnerské centrum

Jak získat stav registrace předplatného u zákaznického předplatného, u kterého je povolené nakupování Azure Reserved VM Instances.

K zakoupení rezervované instance virtuálního počítače Azure pomocí rozhraní API partnerského centra musíte mít aspoň jedno stávající předplatné Azure CSP. Metoda [Register a Subscription](register-a-subscription.md) umožňuje zaregistrovat stávající předplatné Azure CSP a povolit ho pro nákup Azure Reserved VM Instances. Tato metoda umožňuje načíst stav této registrace.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného.

## <a name="c"></a>C\#

Pokud chcete získat stav registrace předplatného, začněte tím, že k identifikaci zákazníka použijete metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka. Potom Získejte rozhraní k operacím předplatného voláním metody [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) s ID předplatného k identifikaci předplatného. Dále pomocí vlastnosti RegistrationStatus Získejte rozhraní pro operace stavu registrace aktuálního předplatného a zavolejte metodu **Get** nebo **GetAsync** pro načtení objektu **SubscriptionRegistrationStatus** .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Čtěte**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrationstatus HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

K identifikaci zákazníka a předplatného použijte následující parametry cesty.

| Název                    | Typ       | Vyžadováno | Popis                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| ID zákazníka             | řetězec     | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.         |
| ID předplatného         | řetězec     | Yes      | Řetězec ve formátu GUID, který identifikuje odběr.     |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu obsahuje tělo odpovědi prostředek [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

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
