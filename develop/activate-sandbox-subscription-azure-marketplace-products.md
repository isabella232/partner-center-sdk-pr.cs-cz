---
title: Aktivace předplatného sandboxu pro produkty komerčního marketplace
description: Naučte se používat C/# a Partnerské centrum ROZHRANÍ REST API k aktivaci předplatného sandboxu pro produkty komerčního marketplace.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b32c3e87462f58218771fc5da7da56ed177489cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025696"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="2150a-103">Aktivace předplatného sandboxu pro produkty SaaS komerčního marketplace a povolení fakturace</span><span class="sxs-lookup"><span data-stu-id="2150a-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="2150a-104">Postup aktivace předplatného pro produkty SaaS (Software jako služba) na komerčním marketplace z účtů sandboxu integrace a povolení fakturace</span><span class="sxs-lookup"><span data-stu-id="2150a-104">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="2150a-105">Předplatné pro produkty SaaS komerčního marketplace je možné aktivovat jenom z účtů sandboxu pro integraci.</span><span class="sxs-lookup"><span data-stu-id="2150a-105">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="2150a-106">Pokud máte produkční předplatné, musíte navštívit web vydavatele a dokončit proces nastavení.</span><span class="sxs-lookup"><span data-stu-id="2150a-106">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="2150a-107">Fakturace předplatného začne až po dokončení nastavení.</span><span class="sxs-lookup"><span data-stu-id="2150a-107">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2150a-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2150a-108">Prerequisites</span></span>

- <span data-ttu-id="2150a-109">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2150a-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2150a-110">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="2150a-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2150a-111">Partnerský účet sandboxu pro integraci se zákazníkem, který má aktivní předplatné pro komerční marketplace produktů SaaS.</span><span class="sxs-lookup"><span data-stu-id="2150a-111">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="2150a-112">Pro partnery, kteří Partnerské centrum .NET SDK, musíte pro přístup k této funkci použít sadu SDK verze 1.14.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="2150a-112">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="2150a-113">C\#</span><span class="sxs-lookup"><span data-stu-id="2150a-113">C\#</span></span>

<span data-ttu-id="2150a-114">K aktivaci předplatného pro produkty SaaS na komerčním marketplace použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="2150a-114">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="2150a-115">Zdělte rozhraní operací předplatného.</span><span class="sxs-lookup"><span data-stu-id="2150a-115">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="2150a-116">Musíte identifikovat zákazníka a zadat identifikátor předplatného zkušebního předplatného.</span><span class="sxs-lookup"><span data-stu-id="2150a-116">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="2150a-117">Aktivujte předplatné pomocí **operace Aktivovat.**</span><span class="sxs-lookup"><span data-stu-id="2150a-117">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="2150a-118">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="2150a-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2150a-119">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="2150a-119">Request syntax</span></span>

| <span data-ttu-id="2150a-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="2150a-120">Method</span></span>     | <span data-ttu-id="2150a-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2150a-121">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="2150a-122">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="2150a-122">**POST**</span></span> | <span data-ttu-id="2150a-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{ID_předplatného}/aktivace HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2150a-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2150a-124">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2150a-124">URI parameter</span></span>

| <span data-ttu-id="2150a-125">Název</span><span class="sxs-lookup"><span data-stu-id="2150a-125">Name</span></span>                   | <span data-ttu-id="2150a-126">Typ</span><span class="sxs-lookup"><span data-stu-id="2150a-126">Type</span></span>     | <span data-ttu-id="2150a-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="2150a-127">Required</span></span> | <span data-ttu-id="2150a-128">Popis</span><span class="sxs-lookup"><span data-stu-id="2150a-128">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2150a-129">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="2150a-129">**customer-tenant-id**</span></span> | <span data-ttu-id="2150a-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="2150a-130">**guid**</span></span> | <span data-ttu-id="2150a-131">Y</span><span class="sxs-lookup"><span data-stu-id="2150a-131">Y</span></span> | <span data-ttu-id="2150a-132">Hodnota je identifikátor tenanta zákazníka ve formátu GUID **(customer-tenant-id),** který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2150a-132">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="2150a-133">**id předplatného**</span><span class="sxs-lookup"><span data-stu-id="2150a-133">**subscription-id**</span></span> | <span data-ttu-id="2150a-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="2150a-134">**guid**</span></span> | <span data-ttu-id="2150a-135">Y</span><span class="sxs-lookup"><span data-stu-id="2150a-135">Y</span></span> | <span data-ttu-id="2150a-136">Hodnota je identifikátor předplatného ve formátu GUID **(id_předplatného),** který umožňuje zadat předplatné.</span><span class="sxs-lookup"><span data-stu-id="2150a-136">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2150a-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2150a-137">Request headers</span></span>

<span data-ttu-id="2150a-138">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2150a-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2150a-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2150a-139">Request body</span></span>

<span data-ttu-id="2150a-140">Žádné</span><span class="sxs-lookup"><span data-stu-id="2150a-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2150a-141">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="2150a-141">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="2150a-142">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2150a-142">REST response</span></span>

<span data-ttu-id="2150a-143">Tato metoda vrátí **vlastnosti subscription-id** **a status.**</span><span class="sxs-lookup"><span data-stu-id="2150a-143">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2150a-144">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="2150a-144">Response success and error codes</span></span>

<span data-ttu-id="2150a-145">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2150a-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2150a-146">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="2150a-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2150a-147">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2150a-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2150a-148">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="2150a-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
