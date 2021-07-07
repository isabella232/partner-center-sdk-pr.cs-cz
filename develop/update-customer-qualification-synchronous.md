---
title: Aktualizace kvalifikace zákazníka
description: Zjistěte, jak aktualizovat kvalifikace zákazníka prostřednictvím synchronního prověřování nebo prověřování, včetně adresy přidružené k profilu.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446645"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="2d29d-103">Aktualizace kvalifikace zákazníka prostřednictvím synchronního ověření</span><span class="sxs-lookup"><span data-stu-id="2d29d-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="2d29d-104">Zjistěte, jak synchronně aktualizovat kvalifikace zákazníka prostřednictvím Partnerské centrum API.</span><span class="sxs-lookup"><span data-stu-id="2d29d-104">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="2d29d-105">Informace o tom, jak to provést asynchronně, najdete v tématu Aktualizace kvalifikace zákazníka [prostřednictvím asynchronního ověřování](update-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="2d29d-105">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="2d29d-106">Partner může aktualizovat kvalifikace zákazníka na "Vzdělávání" nebo "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="2d29d-106">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="2d29d-107">Ostatní hodnoty None (Žádný) a Nonprofit (Neziskové organizace) nelze nastavit.</span><span class="sxs-lookup"><span data-stu-id="2d29d-107">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d29d-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2d29d-108">Prerequisites</span></span>

- <span data-ttu-id="2d29d-109">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2d29d-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2d29d-110">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="2d29d-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2d29d-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2d29d-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2d29d-112">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2d29d-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2d29d-113">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="2d29d-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2d29d-114">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="2d29d-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2d29d-115">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="2d29d-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2d29d-116">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2d29d-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2d29d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="2d29d-117">C\#</span></span>

<span data-ttu-id="2d29d-118">Pokud chcete aktualizovat kvalifikace zákazníka na "Vzdělávání", zavolejte **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** u stávajícího  [**zákazníka**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span><span class="sxs-lookup"><span data-stu-id="2d29d-118">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="2d29d-119">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2d29d-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2d29d-120">**Project:** PartnerSDK.FeatureSamples **– třída:** CustomerQualificationOperations.cs</span><span class="sxs-lookup"><span data-stu-id="2d29d-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="2d29d-121">Pokud chcete aktualizovat kvalifikace zákazníka na **GovernmentCommunityCloud** u stávajícího zákazníka bez kvalifikace, musí partner zahrnout ověřovací kód [**zákazníka.**](utility-resources.md#validationcode)</span><span class="sxs-lookup"><span data-stu-id="2d29d-121">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="2d29d-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="2d29d-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2d29d-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="2d29d-123">Request syntax</span></span>

| <span data-ttu-id="2d29d-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="2d29d-124">Method</span></span>  | <span data-ttu-id="2d29d-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2d29d-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2d29d-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="2d29d-126">**PUT**</span></span> | <span data-ttu-id="2d29d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2d29d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2d29d-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2d29d-128">URI parameter</span></span>

<span data-ttu-id="2d29d-129">K aktualizaci kvalifikace použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="2d29d-129">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="2d29d-130">Název</span><span class="sxs-lookup"><span data-stu-id="2d29d-130">Name</span></span>                   | <span data-ttu-id="2d29d-131">Typ</span><span class="sxs-lookup"><span data-stu-id="2d29d-131">Type</span></span> | <span data-ttu-id="2d29d-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="2d29d-132">Required</span></span> | <span data-ttu-id="2d29d-133">Popis</span><span class="sxs-lookup"><span data-stu-id="2d29d-133">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2d29d-134">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="2d29d-134">**customer-tenant-id**</span></span> | <span data-ttu-id="2d29d-135">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="2d29d-135">GUID</span></span> | <span data-ttu-id="2d29d-136">Yes</span><span class="sxs-lookup"><span data-stu-id="2d29d-136">Yes</span></span>      | <span data-ttu-id="2d29d-137">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="2d29d-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="2d29d-138">**validationCode (kód ověření)**</span><span class="sxs-lookup"><span data-stu-id="2d29d-138">**validationCode**</span></span>     | <span data-ttu-id="2d29d-139">int</span><span class="sxs-lookup"><span data-stu-id="2d29d-139">int</span></span>  | <span data-ttu-id="2d29d-140">No</span><span class="sxs-lookup"><span data-stu-id="2d29d-140">No</span></span>       | <span data-ttu-id="2d29d-141">Je potřeba jenom pro Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="2d29d-141">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="2d29d-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2d29d-142">Request headers</span></span>

<span data-ttu-id="2d29d-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2d29d-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2d29d-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2d29d-144">Request body</span></span>

<span data-ttu-id="2d29d-145">Celočíselná hodnota z [**výčtu CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)</span><span class="sxs-lookup"><span data-stu-id="2d29d-145">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="2d29d-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="2d29d-146">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="2d29d-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2d29d-147">REST response</span></span>

<span data-ttu-id="2d29d-148">V případě úspěchu vrátí tato metoda v textu odpovědi [**aktualizovanou**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) vlastnost Kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="2d29d-148">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2d29d-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="2d29d-149">Response success and error codes</span></span>

<span data-ttu-id="2d29d-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2d29d-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2d29d-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="2d29d-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2d29d-152">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2d29d-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2d29d-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="2d29d-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="2d29d-154">Související články</span><span class="sxs-lookup"><span data-stu-id="2d29d-154">Related articles</span></span>

- [<span data-ttu-id="2d29d-155">Získání kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="2d29d-155">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="2d29d-156">Získání ověřovacích kódů partnera</span><span class="sxs-lookup"><span data-stu-id="2d29d-156">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
