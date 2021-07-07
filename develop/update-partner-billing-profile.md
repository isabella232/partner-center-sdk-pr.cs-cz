---
title: Aktualizace fakturačního profilu partnera
description: Aktualizuje Fakturační profil partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 2b09a0045df15d774c892a59fba8502d4d4f7024
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529762"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="f1d8b-103">Aktualizace fakturačního profilu partnera</span><span class="sxs-lookup"><span data-stu-id="f1d8b-103">Update the partner billing profile</span></span>

<span data-ttu-id="f1d8b-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f1d8b-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f1d8b-105">Aktualizuje Fakturační profil partnera.</span><span class="sxs-lookup"><span data-stu-id="f1d8b-105">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1d8b-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f1d8b-106">Prerequisites</span></span>

- <span data-ttu-id="f1d8b-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f1d8b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f1d8b-108">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="f1d8b-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="f1d8b-109">C\#</span><span class="sxs-lookup"><span data-stu-id="f1d8b-109">C\#</span></span>

<span data-ttu-id="f1d8b-110">Pokud chcete aktualizovat fakturační profil partnera, načtěte si stávající profil.</span><span class="sxs-lookup"><span data-stu-id="f1d8b-110">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="f1d8b-111">Jakmile profil aktualizujete, použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **BillingProfile** .</span><span class="sxs-lookup"><span data-stu-id="f1d8b-111">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="f1d8b-112">Nakonec zavolejte metodu **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="f1d8b-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="f1d8b-113">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f1d8b-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f1d8b-114">**Project**: **třída** microsoft Partner SDK samples: UpdateBillingProfile. cs</span><span class="sxs-lookup"><span data-stu-id="f1d8b-114">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f1d8b-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f1d8b-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f1d8b-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f1d8b-116">Request syntax</span></span>

| <span data-ttu-id="f1d8b-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="f1d8b-117">Method</span></span>  | <span data-ttu-id="f1d8b-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f1d8b-118">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="f1d8b-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="f1d8b-119">**PUT**</span></span> | <span data-ttu-id="f1d8b-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f1d8b-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f1d8b-121">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f1d8b-121">Request headers</span></span>

<span data-ttu-id="f1d8b-122">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f1d8b-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f1d8b-123">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f1d8b-123">Request body</span></span>

<span data-ttu-id="f1d8b-124">Žádné</span><span class="sxs-lookup"><span data-stu-id="f1d8b-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f1d8b-125">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f1d8b-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f1d8b-126">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f1d8b-126">REST response</span></span>

<span data-ttu-id="f1d8b-127">V případě úspěchu tato metoda vrátí objekt **BillingProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="f1d8b-127">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f1d8b-128">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f1d8b-128">Response success and error codes</span></span>

<span data-ttu-id="f1d8b-129">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f1d8b-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f1d8b-130">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f1d8b-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f1d8b-131">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f1d8b-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f1d8b-132">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f1d8b-132">Response example</span></span>

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
