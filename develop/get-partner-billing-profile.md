---
title: Získání fakturačního profilu partnera
description: Získá objekt reprezentující Fakturační profil partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5b3d2bb9d1d9f5c3003fdb8b031aaff17ecb80f03afc4c5aea87a838063c73d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995896"
---
# <a name="get-partner-billing-profile"></a>Získání fakturačního profilu partnera

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Získá objekt reprezentující Fakturační profil partnera.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="c"></a>C\#

Pokud chcete získat Fakturační profil partnera, použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **BillingProfile** . Nakonec zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) .

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: PartnerCenterSDK. FeaturesSamples **třída**: GetBillingProfile. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                              |
|---------|--------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí objekt **BillingProfile** v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
Date: Tue, 22 Mar 2016 17:10:02 GMT

{
    "companyName":"TEST_TEST_BugBash1",
    "address":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"1 Microsoft Way",
        "addressLine2":"","postalCode":"98052"
    },
    "primaryContact":{
        "firstName":"James",
        "lastName":"Burk",
        "phoneNumber":"2066017143"
    },
    "purchaseOrderNumber":"9888",
    "taxId":"12-345678",
    "billingCurrency":"USD",
    "profileType":"BillingProfile",
    "links":{
        "self":{
            "uri":"/profiles/billing",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"BillingProfile"
    }
}
```
