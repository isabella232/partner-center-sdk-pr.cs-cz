---
title: Aktivace předplatného izolovaného prostoru pro produkty z komerčního tržiště
description: Naučte se používat rozhraní REST API pro C/# a partnerská centra k aktivaci předplatného pro komerční produkty z webu Marketplace.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/11/2020
ms.locfileid: "97767068"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a><span data-ttu-id="79eae-103">Aktivace předplatného izolovaného prostoru (sandbox) pro SaaS produkty z webu Marketplace pro povolení fakturace</span><span class="sxs-lookup"><span data-stu-id="79eae-103">Activate a sandbox subscription for commercial marketplace SaaS products to enable billing</span></span>

<span data-ttu-id="79eae-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="79eae-104">**Applies to:**</span></span>

- <span data-ttu-id="79eae-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="79eae-105">Partner Center</span></span>

<span data-ttu-id="79eae-106">Jak aktivovat předplatné pro produkty komerčního SaaS (software jako služba) z účtů izolovaného prostoru (sandbox) integrací pro povolení fakturace</span><span class="sxs-lookup"><span data-stu-id="79eae-106">How to activate a subscription for commercial marketplace Software as a Service (SaaS) products from integration sandbox accounts to enable billing.</span></span>

> [!NOTE]
> <span data-ttu-id="79eae-107">Předplatné pro produkty SaaS na komerčním webu Marketplace je možné aktivovat z účtů karantény integrace.</span><span class="sxs-lookup"><span data-stu-id="79eae-107">It's only possible to activate a subscription for commercial marketplace SaaS products from integration sandbox accounts.</span></span> <span data-ttu-id="79eae-108">Pokud máte produkční předplatné, musíte navštívit web vydavatele, aby se dokončil proces instalace.</span><span class="sxs-lookup"><span data-stu-id="79eae-108">If you have a production subscription, you must visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="79eae-109">Fakturace předplatného se zahájí až po dokončení instalace.</span><span class="sxs-lookup"><span data-stu-id="79eae-109">Subscription billing will begin only after setup is complete.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79eae-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="79eae-110">Prerequisites</span></span>

- <span data-ttu-id="79eae-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="79eae-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="79eae-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="79eae-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="79eae-113">Partnerský účet integrace izolovaného prostoru (sandbox) se zákazníkem s aktivním předplatným pro komerční SaaS produkty z webu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="79eae-113">An integration sandbox partner account with a customer having an active subscription for commercial marketplace SaaS products.</span></span>

- <span data-ttu-id="79eae-114">Pro partnery, kteří používají Partnerská rozhraní .NET SDK, musíte pro přístup k této funkci použít sadu SDK verze 1.14.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="79eae-114">For partners using Partner Center .NET SDK, you must use SDK version 1.14.0 or higher to access this capability.</span></span>

## <a name="c"></a><span data-ttu-id="79eae-115">C\#</span><span class="sxs-lookup"><span data-stu-id="79eae-115">C\#</span></span>

<span data-ttu-id="79eae-116">K aktivaci předplatného pro komerční produkty SaaS na webu Marketplace použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="79eae-116">Use the following steps to activate a subscription for commercial marketplace SaaS products:</span></span>

1. <span data-ttu-id="79eae-117">Zpřístupněte rozhraní k dostupným operacím předplatného.</span><span class="sxs-lookup"><span data-stu-id="79eae-117">Make an interface to the subscription operations available.</span></span> <span data-ttu-id="79eae-118">Musíte identifikovat zákazníka a zadat identifikátor předplatného zkušebního předplatného.</span><span class="sxs-lookup"><span data-stu-id="79eae-118">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. <span data-ttu-id="79eae-119">Aktivujte předplatné pomocí operace **aktivovat** .</span><span class="sxs-lookup"><span data-stu-id="79eae-119">Activate the subscription using the **Activate** operation.</span></span>

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a><span data-ttu-id="79eae-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="79eae-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="79eae-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="79eae-121">Request syntax</span></span>

| <span data-ttu-id="79eae-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="79eae-122">Method</span></span>     | <span data-ttu-id="79eae-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="79eae-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="79eae-124">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="79eae-124">**POST**</span></span> | <span data-ttu-id="79eae-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/Activate HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="79eae-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="79eae-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="79eae-126">URI parameter</span></span>

| <span data-ttu-id="79eae-127">Název</span><span class="sxs-lookup"><span data-stu-id="79eae-127">Name</span></span>                   | <span data-ttu-id="79eae-128">Typ</span><span class="sxs-lookup"><span data-stu-id="79eae-128">Type</span></span>     | <span data-ttu-id="79eae-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="79eae-129">Required</span></span> | <span data-ttu-id="79eae-130">Popis</span><span class="sxs-lookup"><span data-stu-id="79eae-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="79eae-131">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="79eae-131">**customer-tenant-id**</span></span> | <span data-ttu-id="79eae-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="79eae-132">**guid**</span></span> | <span data-ttu-id="79eae-133">Y</span><span class="sxs-lookup"><span data-stu-id="79eae-133">Y</span></span> | <span data-ttu-id="79eae-134">Hodnota je identifikátor zákazníka ve formátu GUID (**Customer-tenant-ID**), který umožňuje zadat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="79eae-134">The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer.</span></span> |
| <span data-ttu-id="79eae-135">**ID předplatného**</span><span class="sxs-lookup"><span data-stu-id="79eae-135">**subscription-id**</span></span> | <span data-ttu-id="79eae-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="79eae-136">**guid**</span></span> | <span data-ttu-id="79eae-137">Y</span><span class="sxs-lookup"><span data-stu-id="79eae-137">Y</span></span> | <span data-ttu-id="79eae-138">Hodnota je identifikátor předplatného ve formátu GUID (**ID předplatného**), který umožňuje zadat předplatné.</span><span class="sxs-lookup"><span data-stu-id="79eae-138">The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="79eae-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="79eae-139">Request headers</span></span>

<span data-ttu-id="79eae-140">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="79eae-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="79eae-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="79eae-141">Request body</span></span>

<span data-ttu-id="79eae-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="79eae-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="79eae-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="79eae-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a><span data-ttu-id="79eae-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="79eae-144">REST response</span></span>

<span data-ttu-id="79eae-145">Tato metoda vrátí vlastnost **ID předplatného** a **stavu** .</span><span class="sxs-lookup"><span data-stu-id="79eae-145">This method returns the **subscription-id** and **status** properties.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="79eae-146">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="79eae-146">Response success and error codes</span></span>

<span data-ttu-id="79eae-147">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="79eae-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="79eae-148">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="79eae-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="79eae-149">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="79eae-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="79eae-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="79eae-150">Response example</span></span>

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
