---
title: Načtení zásad konfigurace zákazníka
description: Jak načíst zadané zásady konfigurace pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 27e01b7c7ec0920d1e6123379fb318827f5389a9c6b297d630ac60dce6933faf
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996882"
---
# <a name="retrieve-a-customers-configuration-policy"></a>Načtení zásad konfigurace zákazníka

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo

Jak načíst zadané zásady konfigurace pro zadaného zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor zásady.

## <a name="c"></a>C\#

Pokud chcete načíst zásadu konfigurace pro zadaného zákazníka, nejdřív zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro konkrétního zákazníka. V dalším kroku zavolejte metodu [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady, aby se načetlo rozhraní pro operace zásad konfigurace pro zadané zásady. Nakonec voláním metody [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) načtěte zásady konfigurace.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: **třída** microsoft Partner SDK samples: GetConfigurationPolicy. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření žádosti použijte následující cestu a parametry dotazu.

| Název        | Typ   | Vyžadováno | Popis                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka. |
| ID zásady   | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zásadu.   |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádná

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu odpověď obsahuje požadovaný prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 443
MS-CorrelationId: abe150cf-c677-435c-b5d5-b34899a6d1ec
MS-RequestId: ab3abfe7-dce7-46c0-ab20-4fd49bc3e2f7
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:08:27 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API 1",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-07-25T11:03:03.8457116-07:00",
    "lastModifiedDate": "2017-07-25T11:04:00.8149974-07:00",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
