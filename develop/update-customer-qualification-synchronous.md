---
title: Aktualizace kvalifikace zákazníka
description: Naučte se aktualizovat kvalifikace zákazníka prostřednictvím synchronního screeningu nebo dozvíte ČSFD, včetně adresy přidružené k profilu.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c202d95beab771241a9665243be5f08ab6f82fd5
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711963"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="0dfaf-103">Aktualizace kvalifikace zákazníka prostřednictvím synchronního ověřování</span><span class="sxs-lookup"><span data-stu-id="0dfaf-103">Update a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="0dfaf-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="0dfaf-104">**Applies To**</span></span>

- <span data-ttu-id="0dfaf-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0dfaf-105">Partner Center</span></span>

<span data-ttu-id="0dfaf-106">Naučte se synchronně aktualizovat kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-106">Learn how to update a customer's qualifications synchronously via Partner Center APIs.</span></span> <span data-ttu-id="0dfaf-107">Informace o tom, jak to provést asynchronně, najdete v tématu [aktualizace kvalifikace zákazníka prostřednictvím asynchronního ověřování](update-customer-qualification-asynchronous.md).</span><span class="sxs-lookup"><span data-stu-id="0dfaf-107">To learn how to do this asynchronously, see [Update a customer's qualification via asynchronous validation](update-customer-qualification-asynchronous.md).</span></span>

<span data-ttu-id="0dfaf-108">Partner může aktualizovat kvalifikaci zákazníka na "vzdělávání" nebo "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="0dfaf-108">A partner can update a customer's qualification to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="0dfaf-109">Další hodnoty, "none" a "neziskové" nelze nastavit.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dfaf-110">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="0dfaf-110">Prerequisites</span></span>

- <span data-ttu-id="0dfaf-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0dfaf-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0dfaf-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0dfaf-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0dfaf-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0dfaf-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0dfaf-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0dfaf-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0dfaf-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="0dfaf-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0dfaf-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0dfaf-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0dfaf-119">C\#</span><span class="sxs-lookup"><span data-stu-id="0dfaf-119">C\#</span></span>

<span data-ttu-id="0dfaf-120">Pokud chcete aktualizovat kvalifikaci zákazníka na "vzdělávání", zavolejte **[Update/dotnet/API/Microsoft. Store. partnercenter. kvalifikaci. icustomerqualification. Update)** na stávajícím  [**zákazníkovi**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span><span class="sxs-lookup"><span data-stu-id="0dfaf-120">To update a customer's qualification to "Education", call **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** on an existing  [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).</span></span>

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

<span data-ttu-id="0dfaf-121">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0dfaf-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0dfaf-122">**Projekt**: PartnerSDK. FeatureSamples **Třída**: CustomerQualificationOperations. cs</span><span class="sxs-lookup"><span data-stu-id="0dfaf-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerQualificationOperations.cs</span></span>

<span data-ttu-id="0dfaf-123">Aktualizace kvalifikace zákazníka tak, aby se **GovernmentCommunityCloud** na stávajícího zákazníkovi bez kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification.</span></span>  <span data-ttu-id="0dfaf-124">Partner je taky nutný k zahrnutí [**ValidationCode**](utility-resources.md#validationcode)zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-124">The partner is also are required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span>

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a><span data-ttu-id="0dfaf-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0dfaf-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0dfaf-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0dfaf-126">Request syntax</span></span>

| <span data-ttu-id="0dfaf-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="0dfaf-127">Method</span></span>  | <span data-ttu-id="0dfaf-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0dfaf-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0dfaf-129">**PUT**</span><span class="sxs-lookup"><span data-stu-id="0dfaf-129">**PUT**</span></span> | <span data-ttu-id="0dfaf-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer_ID}/Qualification? kód = {VALIDATIONCODE} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0dfaf-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0dfaf-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0dfaf-131">URI parameter</span></span>

<span data-ttu-id="0dfaf-132">K aktualizaci kvalifikace použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-132">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="0dfaf-133">Název</span><span class="sxs-lookup"><span data-stu-id="0dfaf-133">Name</span></span>                   | <span data-ttu-id="0dfaf-134">Typ</span><span class="sxs-lookup"><span data-stu-id="0dfaf-134">Type</span></span> | <span data-ttu-id="0dfaf-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0dfaf-135">Required</span></span> | <span data-ttu-id="0dfaf-136">Popis</span><span class="sxs-lookup"><span data-stu-id="0dfaf-136">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0dfaf-137">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="0dfaf-137">**customer-tenant-id**</span></span> | <span data-ttu-id="0dfaf-138">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="0dfaf-138">GUID</span></span> | <span data-ttu-id="0dfaf-139">Yes</span><span class="sxs-lookup"><span data-stu-id="0dfaf-139">Yes</span></span>      | <span data-ttu-id="0dfaf-140">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="0dfaf-141">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="0dfaf-141">**validationCode**</span></span>     | <span data-ttu-id="0dfaf-142">int</span><span class="sxs-lookup"><span data-stu-id="0dfaf-142">int</span></span>  | <span data-ttu-id="0dfaf-143">No</span><span class="sxs-lookup"><span data-stu-id="0dfaf-143">No</span></span>       | <span data-ttu-id="0dfaf-144">Je potřeba jenom pro cloudovou komunitu státní správy.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-144">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="0dfaf-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0dfaf-145">Request headers</span></span>

<span data-ttu-id="0dfaf-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0dfaf-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0dfaf-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0dfaf-147">Request body</span></span>

<span data-ttu-id="0dfaf-148">Celočíselná hodnota z výčtu [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .</span><span class="sxs-lookup"><span data-stu-id="0dfaf-148">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="0dfaf-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0dfaf-149">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="0dfaf-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0dfaf-150">REST response</span></span>

<span data-ttu-id="0dfaf-151">V případě úspěchu tato metoda vrátí aktualizovanou vlastnost [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-151">If successful, this method returns updated [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0dfaf-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0dfaf-152">Response success and error codes</span></span>

<span data-ttu-id="0dfaf-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0dfaf-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0dfaf-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0dfaf-155">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0dfaf-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0dfaf-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0dfaf-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a><span data-ttu-id="0dfaf-157">Související články</span><span class="sxs-lookup"><span data-stu-id="0dfaf-157">Related articles</span></span>

- [<span data-ttu-id="0dfaf-158">Získání kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="0dfaf-158">Get a customer's qualification</span></span>](./get-customer-qualification-synchronous.md)
- [<span data-ttu-id="0dfaf-159">Získání ověřovacích kódů partnera</span><span class="sxs-lookup"><span data-stu-id="0dfaf-159">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)