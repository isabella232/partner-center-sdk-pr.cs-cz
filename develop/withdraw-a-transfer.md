---
title: Stažení přenosu
description: Jak stáhnout vytvořený přenos předplatných pro zákazníka.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a9e1e2a33d21fc1338a36b8ac96b528e70b61c86
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766652"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="e1224-103">Stažení přenosu</span><span class="sxs-lookup"><span data-stu-id="e1224-103">Withdraw a transfer</span></span>

<span data-ttu-id="e1224-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="e1224-104">**Applies to:**</span></span>

- <span data-ttu-id="e1224-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e1224-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1224-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e1224-106">Prerequisites</span></span>

- <span data-ttu-id="e1224-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e1224-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e1224-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1224-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e1224-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e1224-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e1224-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e1224-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e1224-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e1224-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e1224-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e1224-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e1224-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e1224-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e1224-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e1224-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e1224-115">Identifikátor přenosu pro existující přenos.</span><span class="sxs-lookup"><span data-stu-id="e1224-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e1224-116">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e1224-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e1224-117">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e1224-117">Request syntax</span></span>

| <span data-ttu-id="e1224-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="e1224-118">Method</span></span>    | <span data-ttu-id="e1224-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e1224-119">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e1224-120">**DSTRANIT**</span><span class="sxs-lookup"><span data-stu-id="e1224-120">**DELETE**</span></span>| <span data-ttu-id="e1224-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers/{Transfer-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e1224-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="e1224-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e1224-122">URI parameter</span></span>

<span data-ttu-id="e1224-123">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="e1224-123">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="e1224-124">Název</span><span class="sxs-lookup"><span data-stu-id="e1224-124">Name</span></span>            | <span data-ttu-id="e1224-125">Typ</span><span class="sxs-lookup"><span data-stu-id="e1224-125">Type</span></span>     | <span data-ttu-id="e1224-126">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e1224-126">Required</span></span> | <span data-ttu-id="e1224-127">Popis</span><span class="sxs-lookup"><span data-stu-id="e1224-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="e1224-128">**ID zákazníka**</span><span class="sxs-lookup"><span data-stu-id="e1224-128">**customer-id**</span></span> | <span data-ttu-id="e1224-129">řetězec</span><span class="sxs-lookup"><span data-stu-id="e1224-129">string</span></span>   | <span data-ttu-id="e1224-130">Yes</span><span class="sxs-lookup"><span data-stu-id="e1224-130">Yes</span></span>      | <span data-ttu-id="e1224-131">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e1224-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="e1224-132">**ID přenosu**</span><span class="sxs-lookup"><span data-stu-id="e1224-132">**transfer-id**</span></span> | <span data-ttu-id="e1224-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="e1224-133">string</span></span>   | <span data-ttu-id="e1224-134">Yes</span><span class="sxs-lookup"><span data-stu-id="e1224-134">Yes</span></span>      | <span data-ttu-id="e1224-135">Identifikátor ID přenosu, ve formátu GUID, který identifikuje přenos.</span><span class="sxs-lookup"><span data-stu-id="e1224-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="e1224-136">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e1224-136">Request headers</span></span>

<span data-ttu-id="e1224-137">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e1224-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="e1224-138">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e1224-138">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="e1224-139">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e1224-139">REST response</span></span>

<span data-ttu-id="e1224-140">V případě úspěchu tato metoda nevrátí žádný obsah (204).</span><span class="sxs-lookup"><span data-stu-id="e1224-140">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e1224-141">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e1224-141">Response success and error codes</span></span>

<span data-ttu-id="e1224-142">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e1224-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e1224-143">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e1224-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e1224-144">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e1224-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e1224-145">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e1224-145">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
