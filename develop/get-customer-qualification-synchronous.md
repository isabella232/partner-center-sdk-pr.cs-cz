---
title: Získání kvalifikace zákazníka
description: Naučte se používat synchronní ověřování k získání kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra. Partneři to můžou použít k ověření zákazníků vzdělávání.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 82812091be9c13d64ac183c37461e3b63b2ec294
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2020
ms.locfileid: "97767142"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="fcda1-104">Získat kvalifikaci zákazníka prostřednictvím synchronního ověřování</span><span class="sxs-lookup"><span data-stu-id="fcda1-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="fcda1-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="fcda1-105">**Applies To**</span></span>

- <span data-ttu-id="fcda1-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="fcda1-106">Partner Center</span></span>

<span data-ttu-id="fcda1-107">Naučte se synchronně získat kvalifikaci zákazníka prostřednictvím rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fcda1-107">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="fcda1-108">Informace o tom, jak to provést asynchronně, najdete v tématu [získání kvalifikace zákazníka prostřednictvím asynchronního ověřování](get-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="fcda1-108">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcda1-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fcda1-109">Prerequisites</span></span>

- <span data-ttu-id="fcda1-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fcda1-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fcda1-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="fcda1-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fcda1-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fcda1-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fcda1-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="fcda1-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fcda1-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="fcda1-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fcda1-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="fcda1-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fcda1-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="fcda1-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fcda1-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fcda1-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="fcda1-118">C\#</span><span class="sxs-lookup"><span data-stu-id="fcda1-118">C\#</span></span>

<span data-ttu-id="fcda1-119">Chcete-li získat kvalifikaci zákazníka, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fcda1-119">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="fcda1-120">Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="fcda1-120">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="fcda1-121">Nakonec zavolejte [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby se načetla kvalifikace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fcda1-121">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="fcda1-122">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="fcda1-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fcda1-123">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="fcda1-123">Request syntax</span></span>

| <span data-ttu-id="fcda1-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="fcda1-124">Method</span></span>  | <span data-ttu-id="fcda1-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="fcda1-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fcda1-126">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="fcda1-126">**GET**</span></span> | <span data-ttu-id="fcda1-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Qualification HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fcda1-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fcda1-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fcda1-128">URI parameter</span></span>

<span data-ttu-id="fcda1-129">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech kvalifikací.</span><span class="sxs-lookup"><span data-stu-id="fcda1-129">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="fcda1-130">Název</span><span class="sxs-lookup"><span data-stu-id="fcda1-130">Name</span></span>               | <span data-ttu-id="fcda1-131">Typ</span><span class="sxs-lookup"><span data-stu-id="fcda1-131">Type</span></span>   | <span data-ttu-id="fcda1-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="fcda1-132">Required</span></span> | <span data-ttu-id="fcda1-133">Popis</span><span class="sxs-lookup"><span data-stu-id="fcda1-133">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="fcda1-134">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="fcda1-134">**customer-tenant-id**</span></span> | <span data-ttu-id="fcda1-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="fcda1-135">string</span></span> | <span data-ttu-id="fcda1-136">Yes</span><span class="sxs-lookup"><span data-stu-id="fcda1-136">Yes</span></span>      | <span data-ttu-id="fcda1-137">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="fcda1-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fcda1-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="fcda1-138">Request headers</span></span>

<span data-ttu-id="fcda1-139">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fcda1-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fcda1-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="fcda1-140">Request body</span></span>

<span data-ttu-id="fcda1-141">Žádné</span><span class="sxs-lookup"><span data-stu-id="fcda1-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fcda1-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="fcda1-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="fcda1-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="fcda1-143">REST response</span></span>

<span data-ttu-id="fcda1-144">V případě úspěchu tato metoda vrátí hodnotu kvalifikace v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="fcda1-144">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="fcda1-145">Níže je uveden příklad volání **Get** na zákazníka s kvalifikací pro **vzdělávání** .</span><span class="sxs-lookup"><span data-stu-id="fcda1-145">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fcda1-146">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="fcda1-146">Response success and error codes</span></span>

<span data-ttu-id="fcda1-147">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="fcda1-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fcda1-148">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="fcda1-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fcda1-149">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fcda1-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fcda1-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="fcda1-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="fcda1-151">Související články</span><span class="sxs-lookup"><span data-stu-id="fcda1-151">Related articles</span></span>

- [<span data-ttu-id="fcda1-152">Aktualizace kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="fcda1-152">Update a customer's qualification</span></span>](update-a-customer-s-qualification.md)
