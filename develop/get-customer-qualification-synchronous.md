---
title: Získání kvalifikace zákazníka
description: Naučte se používat synchronní ověřování k získání kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra. Partneři to můžou použít k ověření zákazníků vzdělávání.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d215ddb105efe3acd1182c4ff4bb25b045b121f0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446339"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="28448-104">Získat kvalifikaci zákazníka prostřednictvím synchronního ověřování</span><span class="sxs-lookup"><span data-stu-id="28448-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="28448-105">Naučte se synchronně získat kvalifikaci zákazníka prostřednictvím rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="28448-105">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="28448-106">Informace o tom, jak to provést asynchronně, najdete v tématu [získání kvalifikace zákazníka prostřednictvím asynchronního ověřování](get-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="28448-106">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28448-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="28448-107">Prerequisites</span></span>

- <span data-ttu-id="28448-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="28448-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="28448-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="28448-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="28448-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="28448-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="28448-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="28448-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="28448-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="28448-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="28448-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="28448-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="28448-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="28448-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="28448-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="28448-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="28448-116">C\#</span><span class="sxs-lookup"><span data-stu-id="28448-116">C\#</span></span>

<span data-ttu-id="28448-117">Chcete-li získat kvalifikaci zákazníka, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="28448-117">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="28448-118">Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="28448-118">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="28448-119">Nakonec zavolejte [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) , aby se načetla kvalifikace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="28448-119">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="28448-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="28448-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="28448-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="28448-121">Request syntax</span></span>

| <span data-ttu-id="28448-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="28448-122">Method</span></span>  | <span data-ttu-id="28448-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="28448-123">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="28448-124">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="28448-124">**GET**</span></span> | <span data-ttu-id="28448-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Qualification HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="28448-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="28448-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="28448-126">URI parameter</span></span>

<span data-ttu-id="28448-127">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech kvalifikací.</span><span class="sxs-lookup"><span data-stu-id="28448-127">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="28448-128">Název</span><span class="sxs-lookup"><span data-stu-id="28448-128">Name</span></span>               | <span data-ttu-id="28448-129">Typ</span><span class="sxs-lookup"><span data-stu-id="28448-129">Type</span></span>   | <span data-ttu-id="28448-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="28448-130">Required</span></span> | <span data-ttu-id="28448-131">Popis</span><span class="sxs-lookup"><span data-stu-id="28448-131">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="28448-132">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="28448-132">**customer-tenant-id**</span></span> | <span data-ttu-id="28448-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="28448-133">string</span></span> | <span data-ttu-id="28448-134">Yes</span><span class="sxs-lookup"><span data-stu-id="28448-134">Yes</span></span>      | <span data-ttu-id="28448-135">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="28448-135">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="28448-136">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="28448-136">Request headers</span></span>

<span data-ttu-id="28448-137">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="28448-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="28448-138">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="28448-138">Request body</span></span>

<span data-ttu-id="28448-139">Žádné</span><span class="sxs-lookup"><span data-stu-id="28448-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="28448-140">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="28448-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="28448-141">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="28448-141">REST response</span></span>

<span data-ttu-id="28448-142">V případě úspěchu tato metoda vrátí hodnotu kvalifikace v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="28448-142">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="28448-143">Níže je uveden příklad volání **Get** na zákazníka s kvalifikací pro **vzdělávání** .</span><span class="sxs-lookup"><span data-stu-id="28448-143">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="28448-144">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="28448-144">Response success and error codes</span></span>

<span data-ttu-id="28448-145">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="28448-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="28448-146">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="28448-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="28448-147">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="28448-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="28448-148">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="28448-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="28448-149">Související články</span><span class="sxs-lookup"><span data-stu-id="28448-149">Related articles</span></span>

- [<span data-ttu-id="28448-150">Aktualizace kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="28448-150">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)