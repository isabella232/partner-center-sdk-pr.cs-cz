---
title: Získání kvalifikace zákazníka
description: Naučte se používat asynchronní ověřování k získání kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra. Partneři to můžou použít k ověření zákazníků vzdělávání.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: df605e4d400d29e14fd0b44bef34f88bbc7ca8b2
ms.sourcegitcommit: 7d59c58ee36b217bd5cac089f918059e9dbb8a62
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2021
ms.locfileid: "110027924"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="1dd0d-104">Asynchronní získání kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="1dd0d-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="1dd0d-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="1dd0d-105">**Applies To**</span></span>

- <span data-ttu-id="1dd0d-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="1dd0d-106">Partner Center</span></span>

<span data-ttu-id="1dd0d-107">Jak získat asynchronně kvalifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dd0d-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1dd0d-108">Prerequisites</span></span>

- <span data-ttu-id="1dd0d-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1dd0d-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1dd0d-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1dd0d-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1dd0d-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1dd0d-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1dd0d-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1dd0d-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1dd0d-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="1dd0d-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1dd0d-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1dd0d-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1dd0d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="1dd0d-117">C\#</span></span>

<span data-ttu-id="1dd0d-118">Chcete-li získat kvalifikace zákazníka, zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-118">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="1dd0d-119">Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="1dd0d-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="1dd0d-120">Nakonec zavolejte `GetQualifications()` nebo `GetQualificationsAsync()` načtěte kvalifikace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-120">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="1dd0d-121">**Ukázka**: [ukázková aplikace konzoly](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="1dd0d-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="1dd0d-122">**Projekt**: **Třída** SdkSamples: GetCustomerQualifications. cs</span><span class="sxs-lookup"><span data-stu-id="1dd0d-122">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1dd0d-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1dd0d-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1dd0d-124">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="1dd0d-124">Request syntax</span></span>

| <span data-ttu-id="1dd0d-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="1dd0d-125">Method</span></span>  | <span data-ttu-id="1dd0d-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1dd0d-126">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1dd0d-127">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="1dd0d-127">**GET**</span></span> | <span data-ttu-id="1dd0d-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/kvalifikace HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1dd0d-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1dd0d-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1dd0d-129">URI parameter</span></span>

<span data-ttu-id="1dd0d-130">Tato tabulka uvádí požadovaný parametr dotazu pro získání veškeré kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-130">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="1dd0d-131">Název</span><span class="sxs-lookup"><span data-stu-id="1dd0d-131">Name</span></span>               | <span data-ttu-id="1dd0d-132">Typ</span><span class="sxs-lookup"><span data-stu-id="1dd0d-132">Type</span></span>   | <span data-ttu-id="1dd0d-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1dd0d-133">Required</span></span> | <span data-ttu-id="1dd0d-134">Popis</span><span class="sxs-lookup"><span data-stu-id="1dd0d-134">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="1dd0d-135">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="1dd0d-135">**customer-tenant-id**</span></span> | <span data-ttu-id="1dd0d-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="1dd0d-136">string</span></span> | <span data-ttu-id="1dd0d-137">Yes</span><span class="sxs-lookup"><span data-stu-id="1dd0d-137">Yes</span></span>      | <span data-ttu-id="1dd0d-138">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-138">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1dd0d-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1dd0d-139">Request headers</span></span>

<span data-ttu-id="1dd0d-140">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1dd0d-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1dd0d-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1dd0d-141">Request body</span></span>

<span data-ttu-id="1dd0d-142">Žádné</span><span class="sxs-lookup"><span data-stu-id="1dd0d-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1dd0d-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1dd0d-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="1dd0d-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1dd0d-144">REST response</span></span>

<span data-ttu-id="1dd0d-145">V případě úspěchu vrátí tato metoda v textu odpovědi kolekci kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-145">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="1dd0d-146">Níže jsou uvedené příklady volání **GET** u zákazníka s **kvalifikaceí na vzdělávání.**</span><span class="sxs-lookup"><span data-stu-id="1dd0d-146">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1dd0d-147">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="1dd0d-147">Response success and error codes</span></span>

<span data-ttu-id="1dd0d-148">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1dd0d-149">Ke čtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="1dd0d-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1dd0d-150">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1dd0d-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="1dd0d-151">Příklady odpovědí</span><span class="sxs-lookup"><span data-stu-id="1dd0d-151">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="1dd0d-152">Schválené</span><span class="sxs-lookup"><span data-stu-id="1dd0d-152">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="1dd0d-153">In Review (Probíhá kontrola)</span><span class="sxs-lookup"><span data-stu-id="1dd0d-153">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="1dd0d-154">Denied</span><span class="sxs-lookup"><span data-stu-id="1dd0d-154">Denied</span></span>

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

#### <a name="state-owned-entity-samples"></a><span data-ttu-id="1dd0d-155">Ukázky entit vlastněných státem</span><span class="sxs-lookup"><span data-stu-id="1dd0d-155">State Owned Entity Samples</span></span>

<span data-ttu-id="1dd0d-156">**Entita vlastněná státem prostřednictvím ukázky POST**</span><span class="sxs-lookup"><span data-stu-id="1dd0d-156">**State Owned Entity via POST sample**</span></span>

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

<span data-ttu-id="1dd0d-157">**Ukázka státem vlastněné entity prostřednictvím získání kvalifikace**</span><span class="sxs-lookup"><span data-stu-id="1dd0d-157">**State Owned Entity via Get Qualifications sample**</span></span>

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="1dd0d-158">**Entita vlastněná státem prostřednictvím získání kvalifikace se vzděláváním**</span><span class="sxs-lookup"><span data-stu-id="1dd0d-158">**State Owned Entity via Get Qualifications with Education**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “Education”,
        “vettingStatus”: “Approved”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="1dd0d-159">**Vlastní entita s příslušným stavem prostřednictvím získání kvalifikací v RSZ**</span><span class="sxs-lookup"><span data-stu-id="1dd0d-159">**State Owned Entity via Get Qualifications with GCC**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “GovernmentCommunityCloud”,
        “vettingStatus”: “Approved”,
        “vettingCreateDate”: “2021-05-06T19:59:56.6832021+00:00”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="1dd0d-160">Související články</span><span class="sxs-lookup"><span data-stu-id="1dd0d-160">Related articles</span></span>

- [<span data-ttu-id="1dd0d-161">Aktualizace kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="1dd0d-161">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
