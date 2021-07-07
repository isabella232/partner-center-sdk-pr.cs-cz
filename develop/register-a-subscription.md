---
title: Registrace předplatného
description: Zaregistrujte stávající předplatné, aby bylo povolené pro objednávání rezervací Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d26a7c77f60e6ef817cde80b9e97c88bd8bdc786
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446611"
---
# <a name="register-a-subscription"></a>Registrace předplatného

Zaregistrujte stávající [předplatné,](subscription-resources.md) aby bylo povolené pro objednávání rezervací Azure.

Pokud si chcete koupit rezervaci Azure, musíte mít alespoň jedno stávající předplatné Azure CSP. Tato metoda vám umožní zaregistrovat stávající předplatné Azure CSP a umožnit mu nákup rezervací Azure.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného.

## <a name="c"></a>C\#

Pokud chcete zaregistrovat předplatné zákazníka, načtěte rozhraní pro operace předplatného voláním metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a identifikujte zákazníka. Potom zavolejte [**metodu Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) s ID předplatného a identifikujte předplatné, které registrujete.

Nakonec zavolejte **metodu Registration.Register()** pro registraci předplatného a načtěte identifikátor URI, který lze použít k získání stavu registrace předplatného. Další informace najdete v tématu [Získání stavu registrace předplatného.](get-subscription-registration-status.md)

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda    | Identifikátor URI žádosti                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Příspěvek**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/registrace HTTP/1.1 |

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
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
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

V případě úspěchu odpověď obsahuje **hlavičku Location** s identifikátorem URI, který lze použít k načtení stavu registrace předplatného. Uložte si tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API. Příklad načtení stavu najdete v tématu Získání [stavu registrace předplatného.](get-subscription-registration-status.md)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
