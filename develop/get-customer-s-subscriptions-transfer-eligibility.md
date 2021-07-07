---
title: Získání způsobilosti pro převod předplatných zákazníka
description: Jak získat kolekci předplatných zákazníka, která jsou oprávněná/ineligibile pro přenos.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: fe8af76d1e1456754dec79291ec0853fb253d108
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446288"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a><span data-ttu-id="0ebad-103">Získání způsobilosti pro převod předplatných zákazníka</span><span class="sxs-lookup"><span data-stu-id="0ebad-103">Get a customer's subscriptions transfer eligibility</span></span>

<span data-ttu-id="0ebad-104">Jak získat kolekci předplatných zákazníka, která jsou oprávněná nebo neoprávněná pro přenos.</span><span class="sxs-lookup"><span data-stu-id="0ebad-104">How to get a collection of a customer's subscriptions that are eligible/ineligible for transfer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ebad-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0ebad-105">Prerequisites</span></span>

- <span data-ttu-id="0ebad-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0ebad-107">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="0ebad-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0ebad-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0ebad-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0ebad-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0ebad-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0ebad-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="0ebad-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0ebad-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="0ebad-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0ebad-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="0ebad-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0ebad-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0ebad-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="0ebad-114">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0ebad-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0ebad-115">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0ebad-115">Request syntax</span></span>

| <span data-ttu-id="0ebad-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="0ebad-116">Method</span></span>  | <span data-ttu-id="0ebad-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0ebad-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0ebad-118">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="0ebad-118">**GET**</span></span> | <span data-ttu-id="0ebad-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/transferseligibility? transferType = {Transfer-Type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0ebad-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0ebad-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0ebad-120">URI parameter</span></span>

<span data-ttu-id="0ebad-121">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech předplatných.</span><span class="sxs-lookup"><span data-stu-id="0ebad-121">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="0ebad-122">Název</span><span class="sxs-lookup"><span data-stu-id="0ebad-122">Name</span></span>               | <span data-ttu-id="0ebad-123">Typ</span><span class="sxs-lookup"><span data-stu-id="0ebad-123">Type</span></span>   | <span data-ttu-id="0ebad-124">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0ebad-124">Required</span></span> | <span data-ttu-id="0ebad-125">Popis</span><span class="sxs-lookup"><span data-stu-id="0ebad-125">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="0ebad-126">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="0ebad-126">customer-tenant-id</span></span> | <span data-ttu-id="0ebad-127">řetězec</span><span class="sxs-lookup"><span data-stu-id="0ebad-127">string</span></span> | <span data-ttu-id="0ebad-128">Yes</span><span class="sxs-lookup"><span data-stu-id="0ebad-128">Yes</span></span>      | <span data-ttu-id="0ebad-129">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0ebad-129">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="0ebad-130">typ přenosu</span><span class="sxs-lookup"><span data-stu-id="0ebad-130">transfer-type</span></span>      | <span data-ttu-id="0ebad-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="0ebad-131">string</span></span> | <span data-ttu-id="0ebad-132">Yes</span><span class="sxs-lookup"><span data-stu-id="0ebad-132">Yes</span></span>      | <span data-ttu-id="0ebad-133">Typ zamýšleného přenosu.</span><span class="sxs-lookup"><span data-stu-id="0ebad-133">The type of transfer that is intended.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="0ebad-134">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0ebad-134">Request headers</span></span>

<span data-ttu-id="0ebad-135">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0ebad-136">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0ebad-136">Request body</span></span>

<span data-ttu-id="0ebad-137">Žádné</span><span class="sxs-lookup"><span data-stu-id="0ebad-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0ebad-138">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0ebad-138">Request example</span></span>

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="0ebad-139">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0ebad-139">REST response</span></span>

<span data-ttu-id="0ebad-140">V případě úspěchu tato metoda vrátí kolekci prostředků [TransferEligibility](transfer-eligibility-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="0ebad-140">If successful, this method returns a collection of [TransferEligibility](transfer-eligibility-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0ebad-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0ebad-141">Response success and error codes</span></span>

<span data-ttu-id="0ebad-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0ebad-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0ebad-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0ebad-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0ebad-144">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0ebad-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0ebad-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0ebad-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
Date: Tue, 24 Mar 2020 23:43:25 GMT

[
  {
    "id": "548FA265-5F40-4765-9A6B-47826F72A4BF",
    "isEligible": false,
    "reason": "Subscription: 548FA265-5F40-4765-9A6B-47826F72A4BF is in state: Deleted"
  },
  {
    "id": "E2A3AEB3-70A7-42E3-930C-7519EEDDC45A",
    "isEligible": false,
    "reason": "Subscription: E2A3AEB3-70A7-42E3-930C-7519EEDDC45A is in state: Suspended"
  },
  {
    "id": "4B600A9A-DF56-4564-A75A-6CC6D2D0C9F9",
    "isEligible": false,
    "reason": "subscription is already part of another transfer request id : 31a06eac-c527-458a-a6b4-0de197a45996"
  },
  {
    "id": "D3350F46-AA29-4F6F-95A0-E3011988915C",
    "isEligible": true
  }
  {
    "id": "E82B2F4A-736A-4E2B-955C-C1A4C56C0171",
    "isEligible": true
  }
]
```
