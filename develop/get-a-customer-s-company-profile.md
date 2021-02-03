---
title: Získání firemního profilu zákazníka
description: Získá profil společnosti zákazníka.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c26a86ecb96e5e7942ba179f8a3cc704abab7df5
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766875"
---
# <a name="get-a-customers-company-profile"></a>Získání firemního profilu zákazníka

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Získá profil společnosti zákazníka.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra. V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**. Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**. Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** . ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Chcete-li získat profil společnosti pro zákazníka, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka pro identifikaci zákazníka. Pak Získejte rozhraní [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) zákazníka z vlastnosti [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) , aby bylo možné získat přístup k vlastnosti společnosti. Dále Získejte rozhraní [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) z vlastnosti [**ICustomerProfileCollection. Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) a zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) .

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

**Ukázka**: [Stáhněte si sadu SDK partnerského centra](https://go.microsoft.com/fwlink/p/?LinkId=746681). **Projekt**: PartnerSdk. FeatureSamples **Třída**: GetCustomerCompanyProfile.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Chcete-li získat profil společnosti pro zákazníka, zavolejte funkci **IAggregatePartner. GetCustomers (). byId** s identifikátorem zákazníka a Identifikujte zákazníka. Pak Získejte rozhraní **ICustomerProfileCollection** zákazníka ze funkce [**getprofiles**], aby bylo možné získat přístup k vlastnosti společnosti. Dále Získejte rozhraní **ICustomerReadonlyProfile** z funkce **ICustomerProfileCollection. getcompany** a zavolejte funkci **Get** .

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                             |
|---------|-------------------------------------------------------------------------|
| **Čtěte** | *{baseURL}*/v1/Customers/{Customer-tenant-ID}/Profiles/Company HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K získání profilu společnosti použijte následující parametr dotazu.

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y        | Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda informace v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```
