---
title: Získání kvalifikace zákazníka
description: Naučte se používat asynchronní ověřování k získání kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra. Partneři to můžou použít k ověření zákazníků vzdělávání.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 2c860d4a35104131197e06d4712f4ef41ba0008e
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711904"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="e5f40-104">Asynchronní získání kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="e5f40-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="e5f40-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="e5f40-105">**Applies To**</span></span>

- <span data-ttu-id="e5f40-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e5f40-106">Partner Center</span></span>

<span data-ttu-id="e5f40-107">Jak získat asynchronně kvalifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e5f40-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5f40-108">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="e5f40-108">Prerequisites</span></span>

- <span data-ttu-id="e5f40-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e5f40-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e5f40-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e5f40-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e5f40-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e5f40-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e5f40-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e5f40-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e5f40-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e5f40-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e5f40-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e5f40-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e5f40-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e5f40-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e5f40-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e5f40-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="e5f40-117">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e5f40-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e5f40-118">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e5f40-118">Request syntax</span></span>

| <span data-ttu-id="e5f40-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="e5f40-119">Method</span></span>  | <span data-ttu-id="e5f40-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e5f40-120">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e5f40-121">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="e5f40-121">**GET**</span></span> | <span data-ttu-id="e5f40-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Qualifications HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e5f40-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e5f40-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e5f40-123">URI parameter</span></span>

<span data-ttu-id="e5f40-124">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech kvalifikací.</span><span class="sxs-lookup"><span data-stu-id="e5f40-124">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="e5f40-125">Název</span><span class="sxs-lookup"><span data-stu-id="e5f40-125">Name</span></span>               | <span data-ttu-id="e5f40-126">Typ</span><span class="sxs-lookup"><span data-stu-id="e5f40-126">Type</span></span>   | <span data-ttu-id="e5f40-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e5f40-127">Required</span></span> | <span data-ttu-id="e5f40-128">Popis</span><span class="sxs-lookup"><span data-stu-id="e5f40-128">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e5f40-129">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="e5f40-129">**customer-tenant-id**</span></span> | <span data-ttu-id="e5f40-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="e5f40-130">string</span></span> | <span data-ttu-id="e5f40-131">Yes</span><span class="sxs-lookup"><span data-stu-id="e5f40-131">Yes</span></span>      | <span data-ttu-id="e5f40-132">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e5f40-132">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e5f40-133">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e5f40-133">Request headers</span></span>

<span data-ttu-id="e5f40-134">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e5f40-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e5f40-135">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e5f40-135">Request body</span></span>

<span data-ttu-id="e5f40-136">Žádné</span><span class="sxs-lookup"><span data-stu-id="e5f40-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e5f40-137">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e5f40-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="e5f40-138">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e5f40-138">REST response</span></span>

<span data-ttu-id="e5f40-139">V případě úspěchu tato metoda vrátí kolekci kvalifikací v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e5f40-139">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="e5f40-140">Níže jsou uvedeny příklady volání **Get** na zákazníka s kvalifikací pro **vzdělávání** .</span><span class="sxs-lookup"><span data-stu-id="e5f40-140">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e5f40-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e5f40-141">Response success and error codes</span></span>

<span data-ttu-id="e5f40-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e5f40-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e5f40-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e5f40-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e5f40-144">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e5f40-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="e5f40-145">Příklady odpovědí</span><span class="sxs-lookup"><span data-stu-id="e5f40-145">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="e5f40-146">Schválené</span><span class="sxs-lookup"><span data-stu-id="e5f40-146">Approved</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Approved",
        }
    ]
}

```

#### <a name="in-review"></a><span data-ttu-id="e5f40-147">In Review (Probíhá kontrola)</span><span class="sxs-lookup"><span data-stu-id="e5f40-147">In Review</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "InReview",
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

#### <a name="denied"></a><span data-ttu-id="e5f40-148">Denied</span><span class="sxs-lookup"><span data-stu-id="e5f40-148">Denied</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Denied",
            "vettingReason": "Not an Education Customer", // example Vetting Reason
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

## <a name="related-articles"></a><span data-ttu-id="e5f40-149">Související články</span><span class="sxs-lookup"><span data-stu-id="e5f40-149">Related articles</span></span>

- [<span data-ttu-id="e5f40-150">Aktualizace kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="e5f40-150">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)