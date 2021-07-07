---
title: Odstranění zásad konfigurace pro konkrétního zákazníka
description: Jak odstranit zásady konfigurace pro zadaného zákazníka a identifikátor zásady.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d6a7d392bd6af6850eb7716528e6745943bb7bb
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973022"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a>Odstranění zásad konfigurace pro konkrétního zákazníka

**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)

Jak odstranit zásady konfigurace pro zadaného zákazníka a identifikátor zásady.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor zásady.

## <a name="c"></a>C\#

Odstranění zásad konfigurace pro konkrétního zákazníka:

1. Voláním [**metody IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka načtěte rozhraní pro operace u zadaného zákazníka.

2. Voláním [**metody ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady načtěte rozhraní pro operace zásad konfigurace pro zadané zásady.

3. Pokud chcete [**odstranit zásady**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) konfigurace, zavolejte metodu Delete nebo [**DeleteAsync.**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync)

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** SDK pro Partnerské centrum Samples **Class**: DeleteConfigurationPolicy.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda     | Identifikátor URI žádosti                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| **Odstranit** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/policies/{ID_zásad} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Při vytváření požadavku použijte následující parametry cesty.

| Název        | Typ   | Vyžadováno | Popis                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| id zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.         |
| ID zásady   | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zásadu, kterou chcete odstranit. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádná

### <a name="request-example"></a>Příklad požadavku

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí odpověď stavový kód 204 Žádný obsah.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
