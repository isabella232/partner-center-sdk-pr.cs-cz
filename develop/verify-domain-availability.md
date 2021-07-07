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
# <a name="verify-domain-availability"></a><span data-ttu-id="4a67a-103">Ověření dostupnosti domény</span><span class="sxs-lookup"><span data-stu-id="4a67a-103">Verify domain availability</span></span>

<span data-ttu-id="4a67a-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4a67a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4a67a-105">Jak zjistit, jestli je doména k dispozici pro použití.</span><span class="sxs-lookup"><span data-stu-id="4a67a-105">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a67a-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4a67a-106">Prerequisites</span></span>

- <span data-ttu-id="4a67a-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4a67a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4a67a-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="4a67a-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4a67a-109">Doména (například `contoso.onmicrosoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="4a67a-109">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="4a67a-110">C\#</span><span class="sxs-lookup"><span data-stu-id="4a67a-110">C\#</span></span>

<span data-ttu-id="4a67a-111">Chcete-li ověřit, zda je doména k dispozici, nejprve zavolejte [**IAggregatePartner. domény**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) , abyste získali rozhraní pro operace domény.</span><span class="sxs-lookup"><span data-stu-id="4a67a-111">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="4a67a-112">Pak zavolejte metodu [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) s doménou ke kontrole.</span><span class="sxs-lookup"><span data-stu-id="4a67a-112">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="4a67a-113">Tato metoda načte rozhraní k operacím dostupným pro konkrétní doménu.</span><span class="sxs-lookup"><span data-stu-id="4a67a-113">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="4a67a-114">Nakonec zavolejte metodu [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) , abyste viděli, zda doména již existuje.</span><span class="sxs-lookup"><span data-stu-id="4a67a-114">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="4a67a-115">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4a67a-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4a67a-116">**Project**: **třída** microsoft Partner SDK samples: CheckDomainAvailability. cs</span><span class="sxs-lookup"><span data-stu-id="4a67a-116">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4a67a-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="4a67a-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4a67a-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="4a67a-118">Request syntax</span></span>

| <span data-ttu-id="4a67a-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="4a67a-119">Method</span></span>   | <span data-ttu-id="4a67a-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="4a67a-120">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="4a67a-121">**ZÁHLAVÍ**</span><span class="sxs-lookup"><span data-stu-id="4a67a-121">**HEAD**</span></span> | <span data-ttu-id="4a67a-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Domains/{Domain} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4a67a-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4a67a-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="4a67a-123">URI parameter</span></span>

<span data-ttu-id="4a67a-124">K ověření dostupnosti domény použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="4a67a-124">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="4a67a-125">Název</span><span class="sxs-lookup"><span data-stu-id="4a67a-125">Name</span></span>       | <span data-ttu-id="4a67a-126">Typ</span><span class="sxs-lookup"><span data-stu-id="4a67a-126">Type</span></span>       | <span data-ttu-id="4a67a-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="4a67a-127">Required</span></span> | <span data-ttu-id="4a67a-128">Popis</span><span class="sxs-lookup"><span data-stu-id="4a67a-128">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="4a67a-129">**Domain**</span><span class="sxs-lookup"><span data-stu-id="4a67a-129">**domain**</span></span> | <span data-ttu-id="4a67a-130">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="4a67a-130">**string**</span></span> | <span data-ttu-id="4a67a-131">Y</span><span class="sxs-lookup"><span data-stu-id="4a67a-131">Y</span></span>        | <span data-ttu-id="4a67a-132">Řetězec identifikující doménu, kterou chcete ověřit.</span><span class="sxs-lookup"><span data-stu-id="4a67a-132">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4a67a-133">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="4a67a-133">Request headers</span></span>

<span data-ttu-id="4a67a-134">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4a67a-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4a67a-135">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="4a67a-135">Request body</span></span>

<span data-ttu-id="4a67a-136">Žádná</span><span class="sxs-lookup"><span data-stu-id="4a67a-136">None</span></span>

### <a name="request-example"></a><span data-ttu-id="4a67a-137">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="4a67a-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4a67a-138">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="4a67a-138">REST response</span></span>

<span data-ttu-id="4a67a-139">Pokud doména existuje, není k dispozici pro použití a vrátí se kód stavu odpovědi 200 OK.</span><span class="sxs-lookup"><span data-stu-id="4a67a-139">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="4a67a-140">Pokud se doména nenajde, je dostupná pro použití a vrátí se kód stavu odpovědi 404, který se nenalezne.</span><span class="sxs-lookup"><span data-stu-id="4a67a-140">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4a67a-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="4a67a-141">Response success and error codes</span></span>

<span data-ttu-id="4a67a-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="4a67a-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4a67a-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="4a67a-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4a67a-144">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4a67a-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="4a67a-145">Příklad odpovědi, pokud se už doména používá</span><span class="sxs-lookup"><span data-stu-id="4a67a-145">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="4a67a-146">Příklad odpovědi pro dobu, kdy je doména k dispozici</span><span class="sxs-lookup"><span data-stu-id="4a67a-146">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
