---
title: Získání fakturačního profilu partnera
description: Získá objekt reprezentující Fakturační profil partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 94c5ff8fc351282ca3b4721511f02ba6a0cc403c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767031"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="cc8c6-103">Získání fakturačního profilu partnera</span><span class="sxs-lookup"><span data-stu-id="cc8c6-103">Get partner billing profile</span></span>

<span data-ttu-id="cc8c6-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="cc8c6-104">**Applies To**</span></span>

- <span data-ttu-id="cc8c6-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="cc8c6-105">Partner Center</span></span>
- <span data-ttu-id="cc8c6-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="cc8c6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cc8c6-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="cc8c6-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cc8c6-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cc8c6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cc8c6-109">Získá objekt reprezentující Fakturační profil partnera.</span><span class="sxs-lookup"><span data-stu-id="cc8c6-109">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc8c6-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="cc8c6-110">Prerequisites</span></span>

- <span data-ttu-id="cc8c6-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cc8c6-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cc8c6-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="cc8c6-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="cc8c6-113">C\#</span><span class="sxs-lookup"><span data-stu-id="cc8c6-113">C\#</span></span>

<span data-ttu-id="cc8c6-114">Pokud chcete získat Fakturační profil partnera, použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **BillingProfile** .</span><span class="sxs-lookup"><span data-stu-id="cc8c6-114">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="cc8c6-115">Nakonec zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="cc8c6-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="cc8c6-116">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cc8c6-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cc8c6-117">**Projekt**: PartnerCenterSDK. FeaturesSamples **Třída**: GetBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="cc8c6-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cc8c6-118">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="cc8c6-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cc8c6-119">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="cc8c6-119">Request syntax</span></span>

| <span data-ttu-id="cc8c6-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="cc8c6-120">Method</span></span>  | <span data-ttu-id="cc8c6-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="cc8c6-121">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="cc8c6-122">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="cc8c6-122">**GET**</span></span> | <span data-ttu-id="cc8c6-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cc8c6-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cc8c6-124">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="cc8c6-124">Request headers</span></span>

<span data-ttu-id="cc8c6-125">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cc8c6-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cc8c6-126">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="cc8c6-126">Request body</span></span>

<span data-ttu-id="cc8c6-127">Žádné</span><span class="sxs-lookup"><span data-stu-id="cc8c6-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cc8c6-128">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="cc8c6-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="cc8c6-129">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="cc8c6-129">REST response</span></span>

<span data-ttu-id="cc8c6-130">V případě úspěchu tato metoda vrátí objekt **BillingProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="cc8c6-130">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cc8c6-131">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="cc8c6-131">Response success and error codes</span></span>

<span data-ttu-id="cc8c6-132">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="cc8c6-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cc8c6-133">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="cc8c6-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cc8c6-134">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cc8c6-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cc8c6-135">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="cc8c6-135">Response example</span></span>

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
