---
title: Odvolání převodu
description: Jak zrušit vytvořený převod předplatných pro zákazníka.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3c15cf09b4e466e178c7afb5f9d324fe1199418e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445200"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="77519-103">Odvolání převodu</span><span class="sxs-lookup"><span data-stu-id="77519-103">Withdraw a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77519-104">Požadavky</span><span class="sxs-lookup"><span data-stu-id="77519-104">Prerequisites</span></span>

- <span data-ttu-id="77519-105">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="77519-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="77519-106">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="77519-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="77519-107">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="77519-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="77519-108">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="77519-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="77519-109">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="77519-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="77519-110">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="77519-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="77519-111">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="77519-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="77519-112">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="77519-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="77519-113">Identifikátor přenosu pro existující přenos.</span><span class="sxs-lookup"><span data-stu-id="77519-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="77519-114">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="77519-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="77519-115">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="77519-115">Request syntax</span></span>

| <span data-ttu-id="77519-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="77519-116">Method</span></span>    | <span data-ttu-id="77519-117">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="77519-117">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="77519-118">**Odstranit**</span><span class="sxs-lookup"><span data-stu-id="77519-118">**DELETE**</span></span>| <span data-ttu-id="77519-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/transfers/{ID_přenosu} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="77519-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="77519-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="77519-120">URI parameter</span></span>

<span data-ttu-id="77519-121">K identifikaci zákazníka použijte následující parametr cesty.</span><span class="sxs-lookup"><span data-stu-id="77519-121">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="77519-122">Název</span><span class="sxs-lookup"><span data-stu-id="77519-122">Name</span></span>            | <span data-ttu-id="77519-123">Typ</span><span class="sxs-lookup"><span data-stu-id="77519-123">Type</span></span>     | <span data-ttu-id="77519-124">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="77519-124">Required</span></span> | <span data-ttu-id="77519-125">Popis</span><span class="sxs-lookup"><span data-stu-id="77519-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="77519-126">**id zákazníka**</span><span class="sxs-lookup"><span data-stu-id="77519-126">**customer-id**</span></span> | <span data-ttu-id="77519-127">řetězec</span><span class="sxs-lookup"><span data-stu-id="77519-127">string</span></span>   | <span data-ttu-id="77519-128">Yes</span><span class="sxs-lookup"><span data-stu-id="77519-128">Yes</span></span>      | <span data-ttu-id="77519-129">Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="77519-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="77519-130">**id přenosu**</span><span class="sxs-lookup"><span data-stu-id="77519-130">**transfer-id**</span></span> | <span data-ttu-id="77519-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="77519-131">string</span></span>   | <span data-ttu-id="77519-132">Yes</span><span class="sxs-lookup"><span data-stu-id="77519-132">Yes</span></span>      | <span data-ttu-id="77519-133">Identifikátor GUID formátovaný jako transfer-id, který identifikuje přenos.</span><span class="sxs-lookup"><span data-stu-id="77519-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="77519-134">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="77519-134">Request headers</span></span>

<span data-ttu-id="77519-135">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="77519-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="77519-136">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="77519-136">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="77519-137">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="77519-137">REST response</span></span>

<span data-ttu-id="77519-138">V případě úspěchu vrátí tato metoda hodnotu Žádný obsah (204).</span><span class="sxs-lookup"><span data-stu-id="77519-138">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="77519-139">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="77519-139">Response success and error codes</span></span>

<span data-ttu-id="77519-140">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="77519-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="77519-141">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="77519-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="77519-142">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="77519-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="77519-143">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="77519-143">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
