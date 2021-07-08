---
title: Získání fakturačního profilu partnera
description: Získá objekt reprezentující Fakturační profil partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 225d8ea2d92933838ae47eaf3308276aa1f1684c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548970"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="fb2cc-103">Získání fakturačního profilu partnera</span><span class="sxs-lookup"><span data-stu-id="fb2cc-103">Get partner billing profile</span></span>

<span data-ttu-id="fb2cc-104">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fb2cc-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fb2cc-105">Získá objekt reprezentující Fakturační profil partnera.</span><span class="sxs-lookup"><span data-stu-id="fb2cc-105">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb2cc-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fb2cc-106">Prerequisites</span></span>

- <span data-ttu-id="fb2cc-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fb2cc-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fb2cc-108">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="fb2cc-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="fb2cc-109">C\#</span><span class="sxs-lookup"><span data-stu-id="fb2cc-109">C\#</span></span>

<span data-ttu-id="fb2cc-110">Pokud chcete získat Fakturační profil partnera, použijte svou kolekci **IAggregatePartner. Profiles** a zavolejte vlastnost **BillingProfile** .</span><span class="sxs-lookup"><span data-stu-id="fb2cc-110">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="fb2cc-111">Nakonec zavolejte metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) nebo [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="fb2cc-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="fb2cc-112">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fb2cc-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fb2cc-113">**Project**: PartnerCenterSDK. FeaturesSamples **třída**: GetBillingProfile. cs</span><span class="sxs-lookup"><span data-stu-id="fb2cc-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fb2cc-114">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fb2cc-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fb2cc-115">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fb2cc-115">Request syntax</span></span>

| <span data-ttu-id="fb2cc-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="fb2cc-116">Method</span></span>  | <span data-ttu-id="fb2cc-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fb2cc-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="fb2cc-118">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="fb2cc-118">**GET**</span></span> | <span data-ttu-id="fb2cc-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fb2cc-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fb2cc-120">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fb2cc-120">Request headers</span></span>

<span data-ttu-id="fb2cc-121">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fb2cc-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fb2cc-122">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fb2cc-122">Request body</span></span>

<span data-ttu-id="fb2cc-123">Žádné</span><span class="sxs-lookup"><span data-stu-id="fb2cc-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fb2cc-124">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fb2cc-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="fb2cc-125">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fb2cc-125">REST response</span></span>

<span data-ttu-id="fb2cc-126">V případě úspěchu tato metoda vrátí objekt **BillingProfile** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="fb2cc-126">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fb2cc-127">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fb2cc-127">Response success and error codes</span></span>

<span data-ttu-id="fb2cc-128">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fb2cc-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fb2cc-129">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fb2cc-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fb2cc-130">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fb2cc-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fb2cc-131">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fb2cc-131">Response example</span></span>

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
