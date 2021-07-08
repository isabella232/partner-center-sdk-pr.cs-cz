---
title: Získání seznamu nároků Azure pro předplatné
description: K získání kolekce prostředků nároků Azure, které patří do předplatného, můžete použít prostředek AzureEnti zaměnění.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 280da155122ed9efd99838d7819fb34f8f7ec52c
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874359"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="8a1f3-103">Získání seznamu nároků Azure pro předplatné</span><span class="sxs-lookup"><span data-stu-id="8a1f3-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="8a1f3-104">K získání kolekce [prostředků,](subscription-resources.md#azureentitlement) které patří do předplatného, můžete použít prostředek nároku Azure (**AzureEnti sku).**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-104">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a1f3-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8a1f3-105">Prerequisites</span></span>

- <span data-ttu-id="8a1f3-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8a1f3-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8a1f3-107">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8a1f3-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8a1f3-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8a1f3-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8a1f3-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8a1f3-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8a1f3-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8a1f3-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8a1f3-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8a1f3-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8a1f3-114">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-114">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="8a1f3-115">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="8a1f3-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8a1f3-116">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="8a1f3-116">Request syntax</span></span>

| <span data-ttu-id="8a1f3-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="8a1f3-117">Method</span></span>  | <span data-ttu-id="8a1f3-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8a1f3-118">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="8a1f3-119">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-119">**GET**</span></span> | <span data-ttu-id="8a1f3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{ID_předplatného}/azureentiments HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8a1f3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8a1f3-121">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="8a1f3-121">URI parameters</span></span>

<span data-ttu-id="8a1f3-122">Následující tabulka uvádí požadované parametry dotazu k získání všech oprávnění Azure pro předplatné.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-122">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="8a1f3-123">Název</span><span class="sxs-lookup"><span data-stu-id="8a1f3-123">Name</span></span>                   | <span data-ttu-id="8a1f3-124">Typ</span><span class="sxs-lookup"><span data-stu-id="8a1f3-124">Type</span></span>     | <span data-ttu-id="8a1f3-125">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8a1f3-125">Required</span></span> | <span data-ttu-id="8a1f3-126">Popis</span><span class="sxs-lookup"><span data-stu-id="8a1f3-126">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="8a1f3-127">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-127">**customer-tenant-id**</span></span> | <span data-ttu-id="8a1f3-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-128">**guid**</span></span> | <span data-ttu-id="8a1f3-129">Y</span><span class="sxs-lookup"><span data-stu-id="8a1f3-129">Y</span></span>        | <span data-ttu-id="8a1f3-130">Identifikátor GUID odpovídající zákazníkovi.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-130">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="8a1f3-131">**id předplatného**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-131">**subscription-id**</span></span>       | <span data-ttu-id="8a1f3-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="8a1f3-132">**guid**</span></span> | <span data-ttu-id="8a1f3-133">Y</span><span class="sxs-lookup"><span data-stu-id="8a1f3-133">Y</span></span>        | <span data-ttu-id="8a1f3-134">Identifikátor GUID odpovídající předplatnému.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-134">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="8a1f3-135">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8a1f3-135">Request headers</span></span>

<span data-ttu-id="8a1f3-136">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8a1f3-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8a1f3-137">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8a1f3-137">Request body</span></span>

<span data-ttu-id="8a1f3-138">Žádné</span><span class="sxs-lookup"><span data-stu-id="8a1f3-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8a1f3-139">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8a1f3-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="8a1f3-140">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8a1f3-140">REST response</span></span>

<span data-ttu-id="8a1f3-141">V případě úspěchu vrátí tato metoda v textu odpovědi kolekci prostředků [**AzureEnti pro**](subscription-resources.md#azureentitlement) správu.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-141">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8a1f3-142">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="8a1f3-142">Response success and error codes</span></span>

<span data-ttu-id="8a1f3-143">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8a1f3-144">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="8a1f3-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8a1f3-145">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8a1f3-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8a1f3-146">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8a1f3-146">Response example</span></span>

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
