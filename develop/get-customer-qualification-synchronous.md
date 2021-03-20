---
title: Získání kvalifikace zákazníka
description: Naučte se používat synchronní ověřování k získání kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra. Partneři to můžou použít k ověření zákazníků vzdělávání.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e39ace3b598736abed6ab22021a8b93d473486a3
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711879"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="b5c3d-104">Získat kvalifikaci zákazníka prostřednictvím synchronního ověřování</span><span class="sxs-lookup"><span data-stu-id="b5c3d-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="b5c3d-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="b5c3d-105">**Applies To**</span></span>

- <span data-ttu-id="b5c3d-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b5c3d-106">Partner Center</span></span>

<span data-ttu-id="b5c3d-107">Naučte se synchronně získat kvalifikaci zákazníka prostřednictvím rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-107">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="b5c3d-108">Informace o tom, jak to provést asynchronně, najdete v tématu [získání kvalifikace zákazníka prostřednictvím asynchronního ověřování](get-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="b5c3d-108">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5c3d-109">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="b5c3d-109">Prerequisites</span></span>

- <span data-ttu-id="b5c3d-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b5c3d-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b5c3d-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b5c3d-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b5c3d-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b5c3d-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b5c3d-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b5c3d-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b5c3d-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b5c3d-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b5c3d-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b5c3d-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b5c3d-118">C\#</span><span class="sxs-lookup"><span data-stu-id="b5c3d-118">C\#</span></span>

<span data-ttu-id="b5c3d-119">Chcete-li získat kvalifikaci zákazníka, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-119">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="b5c3d-120">Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="b5c3d-120">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="b5c3d-121">Nakonec zavolejte [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby se načetla kvalifikace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-121">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="b5c3d-122">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b5c3d-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b5c3d-123">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b5c3d-123">Request syntax</span></span>

| <span data-ttu-id="b5c3d-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="b5c3d-124">Method</span></span>  | <span data-ttu-id="b5c3d-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b5c3d-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b5c3d-126">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b5c3d-126">**GET**</span></span> | <span data-ttu-id="b5c3d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Qualification HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b5c3d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b5c3d-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b5c3d-128">URI parameter</span></span>

<span data-ttu-id="b5c3d-129">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech kvalifikací.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-129">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="b5c3d-130">Název</span><span class="sxs-lookup"><span data-stu-id="b5c3d-130">Name</span></span>               | <span data-ttu-id="b5c3d-131">Typ</span><span class="sxs-lookup"><span data-stu-id="b5c3d-131">Type</span></span>   | <span data-ttu-id="b5c3d-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b5c3d-132">Required</span></span> | <span data-ttu-id="b5c3d-133">Popis</span><span class="sxs-lookup"><span data-stu-id="b5c3d-133">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="b5c3d-134">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="b5c3d-134">**customer-tenant-id**</span></span> | <span data-ttu-id="b5c3d-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="b5c3d-135">string</span></span> | <span data-ttu-id="b5c3d-136">Yes</span><span class="sxs-lookup"><span data-stu-id="b5c3d-136">Yes</span></span>      | <span data-ttu-id="b5c3d-137">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b5c3d-138">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b5c3d-138">Request headers</span></span>

<span data-ttu-id="b5c3d-139">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b5c3d-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b5c3d-140">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b5c3d-140">Request body</span></span>

<span data-ttu-id="b5c3d-141">Žádné</span><span class="sxs-lookup"><span data-stu-id="b5c3d-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b5c3d-142">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b5c3d-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="b5c3d-143">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b5c3d-143">REST response</span></span>

<span data-ttu-id="b5c3d-144">V případě úspěchu tato metoda vrátí hodnotu kvalifikace v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-144">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="b5c3d-145">Níže je uveden příklad volání **Get** na zákazníka s kvalifikací pro **vzdělávání** .</span><span class="sxs-lookup"><span data-stu-id="b5c3d-145">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b5c3d-146">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b5c3d-146">Response success and error codes</span></span>

<span data-ttu-id="b5c3d-147">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b5c3d-148">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b5c3d-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b5c3d-149">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b5c3d-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b5c3d-150">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b5c3d-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="b5c3d-151">Související články</span><span class="sxs-lookup"><span data-stu-id="b5c3d-151">Related articles</span></span>

- [<span data-ttu-id="b5c3d-152">Aktualizace kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="b5c3d-152">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)