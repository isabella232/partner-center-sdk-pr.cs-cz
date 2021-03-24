---
title: Získání kvalifikace zákazníka
description: Naučte se používat asynchronní ověřování k získání kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra. Partneři to můžou použít k ověření zákazníků vzdělávání.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 09801792c059873b9f6b842e99286eda09d38b1a
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030561"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="e6f87-104">Asynchronní získání kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="e6f87-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="e6f87-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="e6f87-105">**Applies To**</span></span>

- <span data-ttu-id="e6f87-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="e6f87-106">Partner Center</span></span>

<span data-ttu-id="e6f87-107">Jak získat asynchronně kvalifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6f87-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6f87-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e6f87-108">Prerequisites</span></span>

- <span data-ttu-id="e6f87-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e6f87-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="e6f87-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e6f87-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6f87-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e6f87-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e6f87-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e6f87-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e6f87-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e6f87-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e6f87-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e6f87-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e6f87-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e6f87-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6f87-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e6f87-117">C\#</span><span class="sxs-lookup"><span data-stu-id="e6f87-117">C\#</span></span>

<span data-ttu-id="e6f87-118">Chcete-li získat kvalifikace zákazníka, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6f87-118">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="e6f87-119">Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="e6f87-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="e6f87-120">Nakonec zavolejte `GetQualifications()` nebo `GetQualificationsAsync()` načtěte kvalifikace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6f87-120">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="e6f87-121">**Ukázka**: [ukázková aplikace konzoly](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="e6f87-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="e6f87-122">**Projekt**: **Třída** SdkSamples: GetCustomerQualifications. cs</span><span class="sxs-lookup"><span data-stu-id="e6f87-122">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e6f87-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e6f87-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e6f87-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e6f87-124">Request syntax</span></span>

| <span data-ttu-id="e6f87-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="e6f87-125">Method</span></span>  | <span data-ttu-id="e6f87-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e6f87-126">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e6f87-127">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="e6f87-127">**GET**</span></span> | <span data-ttu-id="e6f87-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Qualifications HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e6f87-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e6f87-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e6f87-129">URI parameter</span></span>

<span data-ttu-id="e6f87-130">Tato tabulka obsahuje seznam požadovaných parametrů dotazu pro získání všech kvalifikací.</span><span class="sxs-lookup"><span data-stu-id="e6f87-130">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="e6f87-131">Název</span><span class="sxs-lookup"><span data-stu-id="e6f87-131">Name</span></span>               | <span data-ttu-id="e6f87-132">Typ</span><span class="sxs-lookup"><span data-stu-id="e6f87-132">Type</span></span>   | <span data-ttu-id="e6f87-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e6f87-133">Required</span></span> | <span data-ttu-id="e6f87-134">Popis</span><span class="sxs-lookup"><span data-stu-id="e6f87-134">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e6f87-135">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="e6f87-135">**customer-tenant-id**</span></span> | <span data-ttu-id="e6f87-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="e6f87-136">string</span></span> | <span data-ttu-id="e6f87-137">Yes</span><span class="sxs-lookup"><span data-stu-id="e6f87-137">Yes</span></span>      | <span data-ttu-id="e6f87-138">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6f87-138">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e6f87-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e6f87-139">Request headers</span></span>

<span data-ttu-id="e6f87-140">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e6f87-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e6f87-141">Request body</span></span>

<span data-ttu-id="e6f87-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="e6f87-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e6f87-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e6f87-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="e6f87-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e6f87-144">REST response</span></span>

<span data-ttu-id="e6f87-145">V případě úspěchu tato metoda vrátí kolekci kvalifikací v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e6f87-145">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="e6f87-146">Níže jsou uvedeny příklady volání **Get** na zákazníka s kvalifikací pro **vzdělávání** .</span><span class="sxs-lookup"><span data-stu-id="e6f87-146">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e6f87-147">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e6f87-147">Response success and error codes</span></span>

<span data-ttu-id="e6f87-148">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e6f87-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e6f87-149">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e6f87-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e6f87-150">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e6f87-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="e6f87-151">Příklady odpovědí</span><span class="sxs-lookup"><span data-stu-id="e6f87-151">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="e6f87-152">Schválené</span><span class="sxs-lookup"><span data-stu-id="e6f87-152">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="e6f87-153">In Review (Probíhá kontrola)</span><span class="sxs-lookup"><span data-stu-id="e6f87-153">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="e6f87-154">Denied</span><span class="sxs-lookup"><span data-stu-id="e6f87-154">Denied</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="e6f87-155">Související články</span><span class="sxs-lookup"><span data-stu-id="e6f87-155">Related articles</span></span>

- [<span data-ttu-id="e6f87-156">Aktualizace kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="e6f87-156">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
