---
title: Odstranění zásad konfigurace pro konkrétního zákazníka
description: Jak odstranit zásadu konfigurace pro zadaný identifikátor zákazníka a zásady.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ac9f369ee7b2ba6c6b643bf6ec8d49e99755935181c7db58b616bef427a5a314
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995114"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a>Odstranění zásad konfigurace pro konkrétního zákazníka

**Platí pro**: partnerské Centrum | Partnerské centrum pro Microsoft Cloud Německo

Jak odstranit zásadu konfigurace pro zadaný identifikátor zákazníka a zásady.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

- Identifikátor zásady.

## <a name="c"></a>C\#

Postup odstranění zásad konfigurace pro určitého zákazníka:

1. Zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro operace zadaného zákazníka.

2. Voláním metody [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásad načtěte rozhraní pro operace zásad konfigurace pro zadané zásady.

3. Chcete-li odstranit zásadu konfigurace, zavolejte metodu [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) nebo [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) .

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: **třída** microsoft Partner SDK samples: DeleteConfigurationPolicy. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda     | Identifikátor URI žádosti                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| **DSTRANIT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} HTTP/1.1 |

#### <a name="uri-parameters"></a>Parametry identifikátoru URI

Při vytváření žádosti použít následující parametry cesty.

| Název        | Typ   | Vyžadováno | Popis                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| ID zákazníka | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zákazníka.         |
| ID zásady   | řetězec | Yes      | Řetězec ve formátu GUID, který identifikuje zásadu, která se má odstranit. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

V případě úspěchu vrátí odpověď 204 bez stavového kódu obsahu.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
