---
title: Ověření dostupnosti domény
description: Jak zjistit, jestli je doména k dispozici pro použití.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e2b8f0438516cc0aff9c4d8159c22de43ec582e4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530272"
---
# <a name="verify-domain-availability"></a>Ověření dostupnosti domény

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

Jak zjistit, jestli je doména k dispozici pro použití.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- Doména (například `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Chcete-li ověřit, zda je doména k dispozici, nejprve zavolejte [**IAggregatePartner. domény**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) , abyste získali rozhraní pro operace domény. Pak zavolejte metodu [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) s doménou ke kontrole. Tato metoda načte rozhraní k operacím dostupným pro konkrétní doménu. Nakonec zavolejte metodu [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) , abyste viděli, zda doména již existuje.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Project**: **třída** microsoft Partner SDK samples: CheckDomainAvailability. cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                              |
|----------|--------------------------------------------------------------------------|
| **ZÁHLAVÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Domains/{Domain} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K ověření dostupnosti domény použijte následující parametr dotazu.

| Název       | Typ       | Vyžadováno | Popis                                   |
|------------|------------|----------|-----------------------------------------------|
| **Domain** | **řetězec** | Y        | Řetězec identifikující doménu, kterou chcete ověřit. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádná

### <a name="request-example"></a>Příklad požadavku

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpověď REST

Pokud doména existuje, není k dispozici pro použití a vrátí se kód stavu odpovědi 200 OK. Pokud se doména nenajde, je dostupná pro použití a vrátí se kód stavu odpovědi 404, který se nenalezne.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Příklad odpovědi, pokud se už doména používá

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Příklad odpovědi pro dobu, kdy je doména k dispozici

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
