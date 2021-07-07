---
title: Vytvoření samoobslužné zásady
description: Jak vytvořit nové samoobslužné zásady
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14f46e22fbd294c765b745204cf62474250cbfbd
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973684"
---
# <a name="create-a-selfservepolicy"></a>Vytvoření zásady SelfServePolicy

Tento článek vysvětluje, jak vytvořit nové samoobslužné zásady.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.

## <a name="c"></a>C\#

Vytvoření samoobslužné zásady:

1. Zavolejte [**metodu IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) nebo [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) s informacemi o samoobslužných zásadách.

``` csharp
// IAggregatePartner partnerOperations;
string customerIdAsEntity;

var selfServePolicy = new SelfServePolicy
{
    SelfServeEntity = new SelfServeEntity
    {
        SelfServeEntityType = "customer",
        TenantID = customerIdAsEntity,
    },
    Grantor = new Grantor
    {
        GrantorType = "billToPartner",
        TenantID = partnerIdAsGrantor,
    },
    Permissions = new Permission[]
    {
        new Permission
        {
        Action = "Purchase",
        Resource = "AzureReservedInstances",
        },
    },
};

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// creates the self-serve policy
SelfServePolicy createdSelfServePolicy = scopedPartnerOperations.selfServePolicies.Create(selfServePolicy);
```

Příklad najdete v následujícím příkladu:

- Ukázka: [Konzolová testovací aplikace](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Třída: **CreateSelfServePolicies.cs**


## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                       |
|----------|-------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1 |

### <a name="request-headers"></a>Hlavičky požadavku

- Vyžaduje se ID požadavku a ID korelace.
- Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje požadované vlastnosti v textu požadavku.

| Název                              | Typ   | Description                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [Samoobslužné zásady](self-serve-policy-resources.md#selfservepolicy)| object | Informace o samoobslužné zásadách. |

#### <a name="selfservepolicy"></a>Samoobslužné zásady

Tato tabulka popisuje minimální povinná pole z prostředku [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) potřebná k vytvoření nové samoobslužné zásady.

| Vlastnost              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| Samoobslužná rezervace       | Samoobslužná rezervace  | Samoobslužná entita, které je udělen přístup.                                                     |
| Grantor               | Grantor          | Grantor, který uděluje přístup.                                                                    |
| Oprávnění           | Pole oprávnění| Pole [prostředků](self-serve-policy-resources.md#permission) oprávnění.                                                                     |


### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu toto rozhraní API vrátí [prostředek SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) pro nové samoobslužné zásady.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

Tato metoda vrátí následující kódy chyb:

| Stavový kód HTTP     | Kód chyby   | Description                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 409                  | 600041       | Samoobslužné zásady už existují.                                                     |


### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```
