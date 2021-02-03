---
title: Aktualizace fakturačního profilu partnera
description: Aktualizuje Fakturační profil partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 34e7d2396d6dbdd45a6cf87a3bda481f51326f1e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766815"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="d0897-103">Aktualizace fakturačního profilu partnera</span><span class="sxs-lookup"><span data-stu-id="d0897-103">Update the partner billing profile</span></span>

<span data-ttu-id="d0897-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="d0897-104">**Applies To**</span></span>

- <span data-ttu-id="d0897-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="d0897-105">Partner Center</span></span>
- <span data-ttu-id="d0897-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d0897-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d0897-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="d0897-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d0897-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d0897-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d0897-109">Aktualizuje Fakturační profil partnera.</span><span class="sxs-lookup"><span data-stu-id="d0897-109">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0897-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d0897-110">Prerequisites</span></span>

- <span data-ttu-id="d0897-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d0897-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d0897-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d0897-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="d0897-113">C\#</span><span class="sxs-lookup"><span data-stu-id="d0897-113">C\#</span></span>

<span data-ttu-id="d0897-114">Pokud chcete aktualizovat fakturační profil partnera, načtěte si stávající profil.</span><span class="sxs-lookup"><span data-stu-id="d0897-114">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="d0897-115">Jakmile profil aktualizujete, použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **BillingProfile** .</span><span class="sxs-lookup"><span data-stu-id="d0897-115">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="d0897-116">Nakonec zavolejte metodu **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="d0897-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="d0897-117">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d0897-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d0897-118">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdateBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="d0897-118">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d0897-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d0897-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d0897-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d0897-120">Request syntax</span></span>

| <span data-ttu-id="d0897-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="d0897-121">Method</span></span>  | <span data-ttu-id="d0897-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d0897-122">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="d0897-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="d0897-123">**PUT**</span></span> | <span data-ttu-id="d0897-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d0897-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d0897-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d0897-125">Request headers</span></span>

<span data-ttu-id="d0897-126">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d0897-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d0897-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d0897-127">Request body</span></span>

<span data-ttu-id="d0897-128">Žádné</span><span class="sxs-lookup"><span data-stu-id="d0897-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d0897-129">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d0897-129">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 613
Expect: 100-continue

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="d0897-130">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d0897-130">REST response</span></span>

<span data-ttu-id="d0897-131">V případě úspěchu tato metoda vrátí objekt **BillingProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="d0897-131">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d0897-132">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d0897-132">Response success and error codes</span></span>

<span data-ttu-id="d0897-133">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d0897-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d0897-134">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d0897-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d0897-135">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d0897-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d0897-136">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d0897-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
Date: Mon, 21 Mar 2016 05:47:16 GMT

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```
