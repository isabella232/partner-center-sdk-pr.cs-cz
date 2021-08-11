---
title: Odstranění samoobslužných zásad
description: Postup odstranění samoobslužných zásad
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c638054e7d2b2eb6083c771bc6bdbee56af206907213c9b389176144d5230199
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994995"
---
# <a name="delete-a-selfservepolicy"></a>Odstranění zásady SelfServePolicy

Tento článek vysvětluje, jak aktualizovat samoobslužné zásady.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.

## <a name="c"></a>C\#

Odstranění samoobslužných zásad:

1. Voláním [**metody IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) s identifikátorem entity načtěte rozhraní operací se zásadami.

2. Pokud chcete [**odstranit samoobslužné**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) zásady, zavolejte metodu Delete nebo [**DeleteAsync.**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync)

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

Příklad najdete v následujícím příkladu:

- Ukázka: [Konzolová testovací aplikace](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Třída: **DeleteSelfServePolicies.cs**

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Odstranit** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1 |

**Parametr URI**

K získání zadaného produktu použijte následující parametry cesty.

| Název                       | Typ         | Vyžadováno | Popis                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-id**     | **řetězec**   | Yes      | Řetězec, který identifikuje samoobslužné zásady.                 |

### <a name="request-headers"></a>Hlavičky požadavku

- Vyžaduje se ID požadavku a ID korelace.
- Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a>Odpověď REST

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
