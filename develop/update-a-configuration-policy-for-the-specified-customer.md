---
title: Aktualizace zásad konfigurace pro konkrétního zákazníka
description: Jak aktualizovat zadané zásady konfigurace pro zadaného zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bf3b6f4db7516779c157b647725368ff0e4a570
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767015"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>Aktualizace zásad konfigurace pro konkrétního zákazníka

**Platí pro**

- Partnerské centrum
- Partnerské centrum pro Microsoft Cloud pro Německo

Jak aktualizovat zadané zásady konfigurace pro zadaného zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor zásady.

## <a name="c"></a>C\#

Chcete-li aktualizovat existující zásady konfigurace pro zadaného zákazníka, vytvořte instanci nového objektu [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) , jak je znázorněno v následujícím fragmentu kódu. Hodnoty v tomto novém objektu nahradí odpovídající hodnoty v existujícím objektu. Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro operace zadaného zákazníka. V dalším kroku zavolejte metodu [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady, aby se načetlo rozhraní pro operace zásad konfigurace pro zadané zásady. Nakonec zavolejte metodu [**patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) nebo [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) a aktualizujte zásady konfigurace.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdateConfigurationPolicy.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Při vytváření žádosti použít následující parametry cesty.

| Název        | Typ   | Vyžadováno | Popis                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| ID zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.         |
| ID zásady   | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zásadu, která se má aktualizovat. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Tělo žádosti musí obsahovat objekt, který poskytuje informace o zásadách.

| Název            | Typ             | Vyžadováno | Aktualizovat | Description                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| id              | řetězec           | Yes      | No        | Řetězec ve formátu GUID, který identifikuje zásadu.                                                                                                    |
| name            | řetězec           | Yes      | Yes       | Popisný název zásady.                                                                                                                         |
| category        | řetězec           | Yes      | No        | Kategorie zásad                                                                                                                                     |
| description     | řetězec           | No       | Yes       | Popis zásady.                                                                                                                                  |
| devicesAssigned | číslo           | No       | No        | Počet zařízení.                                                                                                                                   |
| policySettings  | pole řetězců | Yes      | Yes       | Nastavení zásad: "žádné", "odebrat \_ \_ předinstalované výrobci OEM", "OOBE \_ User \_ Not \_ Local \_ admin", "Přeskočit \_ expresní \_ nastavení", "Přeskočit \_ registraci OEM" \_ Přeskočit \_ smlouvu EULA ". |

### <a name="request-example"></a>Příklad požadavku

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi prostředek [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pro novou zásadu.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
