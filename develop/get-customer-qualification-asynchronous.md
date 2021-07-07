---
title: Získání kvalifikace zákazníka
description: Zjistěte, jak pomocí asynchronního ověřování získat kvalifikaci zákazníka prostřednictvím Partnerské centrum API. Partneři můžou tuto metodu použít k ověření zákazníků v oblasti vzdělávání.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 4795b6e1ad008f9d854dc7efbee0c2099aefa609
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446305"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="05979-104">Asynchronní získání kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="05979-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="05979-105">Jak asynchronně získat kvalifikaci zákazníka</span><span class="sxs-lookup"><span data-stu-id="05979-105">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05979-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="05979-106">Prerequisites</span></span>

- <span data-ttu-id="05979-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="05979-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="05979-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="05979-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="05979-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="05979-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="05979-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="05979-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="05979-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="05979-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="05979-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="05979-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="05979-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05979-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="05979-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="05979-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="05979-115">C\#</span><span class="sxs-lookup"><span data-stu-id="05979-115">C\#</span></span>

<span data-ttu-id="05979-116">Pokud chcete získat kvalifikaci zákazníka, zavolejte [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05979-116">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="05979-117">Potom pomocí [**vlastnosti Kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="05979-117">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="05979-118">Nakonec zavolejte `GetQualifications()` nebo `GetQualificationsAsync()` , abyste získali kvalifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05979-118">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="05979-119">**Ukázka:** [Konzolová ukázková aplikace](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="05979-119">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="05979-120">**Project:** SdkSamples **– třída:** GetCustomerQualifications.cs</span><span class="sxs-lookup"><span data-stu-id="05979-120">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="05979-121">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="05979-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="05979-122">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="05979-122">Request syntax</span></span>

| <span data-ttu-id="05979-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="05979-123">Method</span></span>  | <span data-ttu-id="05979-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="05979-124">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="05979-125">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="05979-125">**GET**</span></span> | <span data-ttu-id="05979-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/kvalifikace HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="05979-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="05979-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="05979-127">URI parameter</span></span>

<span data-ttu-id="05979-128">Tato tabulka uvádí požadovaný parametr dotazu pro získání veškeré kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="05979-128">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="05979-129">Název</span><span class="sxs-lookup"><span data-stu-id="05979-129">Name</span></span>               | <span data-ttu-id="05979-130">Typ</span><span class="sxs-lookup"><span data-stu-id="05979-130">Type</span></span>   | <span data-ttu-id="05979-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="05979-131">Required</span></span> | <span data-ttu-id="05979-132">Popis</span><span class="sxs-lookup"><span data-stu-id="05979-132">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="05979-133">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="05979-133">**customer-tenant-id**</span></span> | <span data-ttu-id="05979-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="05979-134">string</span></span> | <span data-ttu-id="05979-135">Yes</span><span class="sxs-lookup"><span data-stu-id="05979-135">Yes</span></span>      | <span data-ttu-id="05979-136">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="05979-136">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="05979-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="05979-137">Request headers</span></span>

<span data-ttu-id="05979-138">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="05979-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="05979-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="05979-139">Request body</span></span>

<span data-ttu-id="05979-140">Žádné</span><span class="sxs-lookup"><span data-stu-id="05979-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="05979-141">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="05979-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="05979-142">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="05979-142">REST response</span></span>

<span data-ttu-id="05979-143">V případě úspěchu vrátí tato metoda v textu odpovědi kolekci kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="05979-143">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="05979-144">Níže jsou uvedené příklady volání **GET** u zákazníka s **kvalifikaceí pro vzdělávání.**</span><span class="sxs-lookup"><span data-stu-id="05979-144">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="05979-145">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="05979-145">Response success and error codes</span></span>

<span data-ttu-id="05979-146">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="05979-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="05979-147">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="05979-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="05979-148">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="05979-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="05979-149">Příklady odpovědí</span><span class="sxs-lookup"><span data-stu-id="05979-149">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="05979-150">Schválené</span><span class="sxs-lookup"><span data-stu-id="05979-150">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="05979-151">In Review (Probíhá kontrola)</span><span class="sxs-lookup"><span data-stu-id="05979-151">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="05979-152">Denied</span><span class="sxs-lookup"><span data-stu-id="05979-152">Denied</span></span>

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

#### <a name="state-owned-entity-samples"></a><span data-ttu-id="05979-153">Ukázky entit vlastněných státem</span><span class="sxs-lookup"><span data-stu-id="05979-153">State Owned Entity Samples</span></span>

<span data-ttu-id="05979-154">**Entita vlastněná státem prostřednictvím ukázky POST**</span><span class="sxs-lookup"><span data-stu-id="05979-154">**State Owned Entity via POST sample**</span></span>

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

<span data-ttu-id="05979-155">**Ukázka státem vlastněné entity prostřednictvím získání kvalifikace**</span><span class="sxs-lookup"><span data-stu-id="05979-155">**State Owned Entity via Get Qualifications sample**</span></span>

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="05979-156">**Entita vlastněná státem prostřednictvím získání kvalifikace se vzděláváním**</span><span class="sxs-lookup"><span data-stu-id="05979-156">**State Owned Entity via Get Qualifications with Education**</span></span>

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

<span data-ttu-id="05979-157">**Entita vlastněná státem prostřednictvím získání kvalifikace s GCC**</span><span class="sxs-lookup"><span data-stu-id="05979-157">**State Owned Entity via Get Qualifications with GCC**</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="05979-158">Související články</span><span class="sxs-lookup"><span data-stu-id="05979-158">Related articles</span></span>

- [<span data-ttu-id="05979-159">Aktualizace kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="05979-159">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
