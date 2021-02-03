---
title: Registrace předplatného
description: Zaregistrujte stávající předplatné, aby bylo povolené řazení rezervací Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766968"
---
# <a name="register-a-subscription"></a>Registrace předplatného

**Platí pro**

- Partnerské centrum

Zaregistrujte stávající [předplatné](subscription-resources.md) , aby bylo povolené řazení rezervací Azure.

Pokud si chcete koupit rezervaci Azure, musíte mít aspoň jedno stávající předplatné Azure CSP. Tato metoda umožňuje zaregistrovat stávající předplatné Azure CSP a povolit ho k nákupu rezervací Azure.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- ID předplatného.

## <a name="c"></a>C\#

Pokud chcete zaregistrovat předplatné zákazníka, načtěte rozhraní k operacím předplatného tak, že zavoláte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka. Pak zavolejte metodu [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) s ID předplatného k identifikaci předplatného, které zaregistrujete.

Nakonec zavolejte metodu Register **. Register ()** pro registraci předplatného a NAČTĚTE identifikátor URI, který se dá použít k získání stavu registrace předplatného. Další informace najdete v tématu [získání stavu registrace předplatného](get-subscription-registration-status.md).

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda    | Identifikátor URI žádosti                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrations HTTP/1.1 |

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

V případě úspěchu odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který lze použít k načtení stavu registrace předplatného. Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API. Příklad toho, jak načíst stav, najdete v tématu [získání stavu registrace předplatného](get-subscription-registration-status.md).

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

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
