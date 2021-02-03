---
title: Získání seznamu nároků Azure pro předplatné
description: Pomocí prostředku AzureEntitlement můžete získat kolekci prostředků nároků Azure, které patří do předplatného.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: d7d0a10c571dc073bd49e82084f3b7ece7234daf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766790"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="75b1d-103">Získání seznamu nároků Azure pro předplatné</span><span class="sxs-lookup"><span data-stu-id="75b1d-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="75b1d-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="75b1d-104">**Applies to:**</span></span>

- <span data-ttu-id="75b1d-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="75b1d-105">Partner Center</span></span>

<span data-ttu-id="75b1d-106">Pomocí [prostředku nároku na Azure](subscription-resources.md#azureentitlement) (**AzureEntitlement**) můžete získat kolekci prostředků, které patří do předplatného.</span><span class="sxs-lookup"><span data-stu-id="75b1d-106">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75b1d-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="75b1d-107">Prerequisites</span></span>

- <span data-ttu-id="75b1d-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="75b1d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="75b1d-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="75b1d-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="75b1d-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="75b1d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="75b1d-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="75b1d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="75b1d-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="75b1d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="75b1d-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="75b1d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="75b1d-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="75b1d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="75b1d-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="75b1d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="75b1d-116">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="75b1d-116">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="75b1d-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="75b1d-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="75b1d-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="75b1d-118">Request syntax</span></span>

| <span data-ttu-id="75b1d-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="75b1d-119">Method</span></span>  | <span data-ttu-id="75b1d-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="75b1d-120">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="75b1d-121">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="75b1d-121">**GET**</span></span> | <span data-ttu-id="75b1d-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/azureentitlements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="75b1d-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="75b1d-123">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="75b1d-123">URI parameters</span></span>

<span data-ttu-id="75b1d-124">V následující tabulce jsou uvedeny požadované parametry dotazu pro získání všech nároků Azure pro předplatné.</span><span class="sxs-lookup"><span data-stu-id="75b1d-124">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="75b1d-125">Název</span><span class="sxs-lookup"><span data-stu-id="75b1d-125">Name</span></span>                   | <span data-ttu-id="75b1d-126">Typ</span><span class="sxs-lookup"><span data-stu-id="75b1d-126">Type</span></span>     | <span data-ttu-id="75b1d-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="75b1d-127">Required</span></span> | <span data-ttu-id="75b1d-128">Popis</span><span class="sxs-lookup"><span data-stu-id="75b1d-128">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="75b1d-129">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="75b1d-129">**customer-tenant-id**</span></span> | <span data-ttu-id="75b1d-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="75b1d-130">**guid**</span></span> | <span data-ttu-id="75b1d-131">Y</span><span class="sxs-lookup"><span data-stu-id="75b1d-131">Y</span></span>        | <span data-ttu-id="75b1d-132">Identifikátor GUID, který odpovídá zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="75b1d-132">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="75b1d-133">**ID předplatného**</span><span class="sxs-lookup"><span data-stu-id="75b1d-133">**subscription-id**</span></span>       | <span data-ttu-id="75b1d-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="75b1d-134">**guid**</span></span> | <span data-ttu-id="75b1d-135">Y</span><span class="sxs-lookup"><span data-stu-id="75b1d-135">Y</span></span>        | <span data-ttu-id="75b1d-136">Identifikátor GUID, který odpovídá předplatnému.</span><span class="sxs-lookup"><span data-stu-id="75b1d-136">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="75b1d-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="75b1d-137">Request headers</span></span>

<span data-ttu-id="75b1d-138">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="75b1d-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="75b1d-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="75b1d-139">Request body</span></span>

<span data-ttu-id="75b1d-140">Žádné</span><span class="sxs-lookup"><span data-stu-id="75b1d-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="75b1d-141">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="75b1d-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="75b1d-142">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="75b1d-142">REST response</span></span>

<span data-ttu-id="75b1d-143">V případě úspěchu tato metoda vrátí kolekci prostředků [**AzureEntitlement**](subscription-resources.md#azureentitlement) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="75b1d-143">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="75b1d-144">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="75b1d-144">Response success and error codes</span></span>

<span data-ttu-id="75b1d-145">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="75b1d-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="75b1d-146">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="75b1d-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="75b1d-147">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="75b1d-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="75b1d-148">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="75b1d-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }
```
