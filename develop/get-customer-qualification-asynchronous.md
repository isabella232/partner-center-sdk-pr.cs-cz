---
title: Získání kvalifikace zákazníka
description: Naučte se používat asynchronní ověřování k získání kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra. Partneři to můžou použít k ověření zákazníků vzdělávání.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 9f9b9aaddde0d66caf9c7ef32e8fba6d5e3aba36
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767143"
---
# <a name="get-a-customers-qualifications-via-asynchronous-validation"></a><span data-ttu-id="fd312-104">Získání kvalifikace zákazníka prostřednictvím asynchronního ověřování</span><span class="sxs-lookup"><span data-stu-id="fd312-104">Get a customer's qualifications via asynchronous validation</span></span>

<span data-ttu-id="fd312-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="fd312-105">**Applies To**</span></span>

- <span data-ttu-id="fd312-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="fd312-106">Partner Center</span></span>

<span data-ttu-id="fd312-107">Naučte se asynchronně získat kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fd312-107">Learn how to get a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="fd312-108">Informace o tom, jak to provést synchronně, najdete v tématu [získání kvalifikace zákazníka prostřednictvím synchronního ověřování](get-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="fd312-108">To learn how to do this synchronously, see [Get a customer's qualification via synchronous validation](get-customer-qualification-synchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd312-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fd312-109">Prerequisites</span></span>

- <span data-ttu-id="fd312-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fd312-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fd312-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="fd312-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fd312-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fd312-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fd312-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fd312-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fd312-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="fd312-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fd312-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="fd312-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fd312-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="fd312-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fd312-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fd312-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="fd312-118">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fd312-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fd312-119">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fd312-119">Request syntax</span></span>

| <span data-ttu-id="fd312-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="fd312-120">Method</span></span>  | <span data-ttu-id="fd312-121">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fd312-121">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fd312-122">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="fd312-122">**GET**</span></span> | <span data-ttu-id="fd312-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Qualifications HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fd312-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fd312-124">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fd312-124">URI parameter</span></span>

<span data-ttu-id="fd312-125">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech kvalifikací.</span><span class="sxs-lookup"><span data-stu-id="fd312-125">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="fd312-126">Název</span><span class="sxs-lookup"><span data-stu-id="fd312-126">Name</span></span>               | <span data-ttu-id="fd312-127">Typ</span><span class="sxs-lookup"><span data-stu-id="fd312-127">Type</span></span>   | <span data-ttu-id="fd312-128">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fd312-128">Required</span></span> | <span data-ttu-id="fd312-129">Popis</span><span class="sxs-lookup"><span data-stu-id="fd312-129">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="fd312-130">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="fd312-130">**customer-tenant-id**</span></span> | <span data-ttu-id="fd312-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="fd312-131">string</span></span> | <span data-ttu-id="fd312-132">Yes</span><span class="sxs-lookup"><span data-stu-id="fd312-132">Yes</span></span>      | <span data-ttu-id="fd312-133">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fd312-133">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fd312-134">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fd312-134">Request headers</span></span>

<span data-ttu-id="fd312-135">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fd312-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fd312-136">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fd312-136">Request body</span></span>

<span data-ttu-id="fd312-137">Žádné</span><span class="sxs-lookup"><span data-stu-id="fd312-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fd312-138">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fd312-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="fd312-139">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fd312-139">REST response</span></span>

<span data-ttu-id="fd312-140">V případě úspěchu tato metoda vrátí kolekci kvalifikací v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="fd312-140">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="fd312-141">Níže jsou uvedeny příklady volání **Get** na zákazníka s kvalifikací pro **vzdělávání** .</span><span class="sxs-lookup"><span data-stu-id="fd312-141">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fd312-142">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fd312-142">Response success and error codes</span></span>

<span data-ttu-id="fd312-143">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fd312-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fd312-144">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fd312-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fd312-145">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fd312-145">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="fd312-146">Příklady odpovědí</span><span class="sxs-lookup"><span data-stu-id="fd312-146">Response examples</span></span>

<span data-ttu-id="fd312-147">V této části najdete odpovědi, které se můžou zobrazit, když `vettingStatus` je zákazník:</span><span class="sxs-lookup"><span data-stu-id="fd312-147">This section shows responses you might receive when a customer's `vettingStatus` is:</span></span>

- <span data-ttu-id="fd312-148">Schválené</span><span class="sxs-lookup"><span data-stu-id="fd312-148">Approved</span></span>
- <span data-ttu-id="fd312-149">In Review (Probíhá kontrola)</span><span class="sxs-lookup"><span data-stu-id="fd312-149">In Review</span></span>
- <span data-ttu-id="fd312-150">Denied</span><span class="sxs-lookup"><span data-stu-id="fd312-150">Denied</span></span>

<span data-ttu-id="fd312-151">Příklad **schváleného** :</span><span class="sxs-lookup"><span data-stu-id="fd312-151">**Approved** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Approved",
    }
]

```

<span data-ttu-id="fd312-152">**V** příkladech Revize:</span><span class="sxs-lookup"><span data-stu-id="fd312-152">**In Review** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "InReview",
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

<span data-ttu-id="fd312-153">Příklad **odepření** :</span><span class="sxs-lookup"><span data-stu-id="fd312-153">**Denied** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Denied",
        "vettingReason": "Not an Education Customer", // example Vetting Reason
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="fd312-154">Související články</span><span class="sxs-lookup"><span data-stu-id="fd312-154">Related articles</span></span>

- [<span data-ttu-id="fd312-155">Aktualizace kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="fd312-155">Update a customer's qualifications</span></span>](update-a-customer-s-qualifications.md)