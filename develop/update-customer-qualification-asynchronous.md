---
title: Aktualizace kvalifikace zákazníka
description: Provede asynchronní aktualizace kvalifikací zákazníka, včetně adresy přidružené k profilu.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: d7dd3593894ce91ddc7b96d604b80153d41d3a67
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572093"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="5a649-103">Asynchronní aktualizace kvalifikací zákazníka</span><span class="sxs-lookup"><span data-stu-id="5a649-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="5a649-104">Asynchronně aktualizuje kvalifikace zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5a649-104">Updates a customer's qualifications asynchronously.</span></span>

<span data-ttu-id="5a649-105">Partner může provést asynchronní aktualizaci kvalifikací zákazníka, pokud jde o "vzdělávání" nebo "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="5a649-105">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="5a649-106">Další hodnoty, "none" a "neziskové" nelze nastavit.</span><span class="sxs-lookup"><span data-stu-id="5a649-106">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a649-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5a649-107">Prerequisites</span></span>

- <span data-ttu-id="5a649-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5a649-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5a649-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="5a649-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5a649-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5a649-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5a649-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="5a649-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5a649-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="5a649-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5a649-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="5a649-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5a649-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="5a649-114">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5a649-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5a649-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5a649-116">C\#</span><span class="sxs-lookup"><span data-stu-id="5a649-116">C\#</span></span>

<span data-ttu-id="5a649-117">Chcete-li vytvořit kvalifikaci zákazníka pro "vzdělávání", nejprve vytvořte objekt reprezentující typ kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="5a649-117">To create a customer's qualification for "Education", first create an object representing the qualification type.</span></span> <span data-ttu-id="5a649-118">Pak zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5a649-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="5a649-119">Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="5a649-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="5a649-120">Nakonec zavolejte `CreateQualifications()` nebo `CreateQualificationsAsync()` s typem kvalifikace Object jako vstupní parametr.</span><span class="sxs-lookup"><span data-stu-id="5a649-120">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object as an input parameter.</span></span>

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

<span data-ttu-id="5a649-121">**Ukázka**: [ukázková aplikace konzoly](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="5a649-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="5a649-122">**Project**: **třída** SdkSamples: CreateCustomerQualification. cs</span><span class="sxs-lookup"><span data-stu-id="5a649-122">**Project**: SdkSamples **Class**: CreateCustomerQualification.cs</span></span>

<span data-ttu-id="5a649-123">Pokud chcete aktualizovat kvalifikaci zákazníka tak, aby se **GovernmentCommunityCloud** na stávajícího zákazníkovi bez kvalifikace, partner taky musí zahrnovat [**ValidationCode**](utility-resources.md#validationcode)zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5a649-123">To update a customer's qualification to **GovernmentCommunityCloud** on an existing customer without a qualification, the partner is also required to include the customer's [**ValidationCode**](utility-resources.md#validationcode).</span></span> <span data-ttu-id="5a649-124">Nejprve vytvořte objekt reprezentující typ kvalifikace.</span><span class="sxs-lookup"><span data-stu-id="5a649-124">First, create an object representing the qualification type.</span></span> <span data-ttu-id="5a649-125">Pak zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5a649-125">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="5a649-126">Pak pomocí vlastnosti [**kvalifikace**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) načtěte rozhraní [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) .</span><span class="sxs-lookup"><span data-stu-id="5a649-126">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="5a649-127">Nakonec volejte `CreateQualifications()` nebo `CreateQualificationsAsync()` s objektem typu kvalifikace a ověřovacím kódem jako vstupní parametry.</span><span class="sxs-lookup"><span data-stu-id="5a649-127">Finally, call `CreateQualifications()` or `CreateQualificationsAsync()` with the qualification type object and the validation code as input parameters.</span></span>

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

<span data-ttu-id="5a649-128">**Ukázka**: [ukázková aplikace konzoly](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="5a649-128">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="5a649-129">**Project**: **třída** SdkSamples: CreateCustomerQualificationWithGCC. cs</span><span class="sxs-lookup"><span data-stu-id="5a649-129">**Project**: SdkSamples **Class**: CreateCustomerQualificationWithGCC.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5a649-130">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="5a649-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5a649-131">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="5a649-131">Request syntax</span></span>

| <span data-ttu-id="5a649-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="5a649-132">Method</span></span>  | <span data-ttu-id="5a649-133">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5a649-133">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5a649-134">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="5a649-134">**POST**</span></span> | <span data-ttu-id="5a649-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer_ID}/Qualifications? kód = {VALIDATIONCODE} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5a649-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5a649-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5a649-136">URI parameter</span></span>

<span data-ttu-id="5a649-137">K aktualizaci kvalifikace použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="5a649-137">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="5a649-138">Název</span><span class="sxs-lookup"><span data-stu-id="5a649-138">Name</span></span>                   | <span data-ttu-id="5a649-139">Typ</span><span class="sxs-lookup"><span data-stu-id="5a649-139">Type</span></span> | <span data-ttu-id="5a649-140">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="5a649-140">Required</span></span> | <span data-ttu-id="5a649-141">Popis</span><span class="sxs-lookup"><span data-stu-id="5a649-141">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5a649-142">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="5a649-142">**customer-tenant-id**</span></span> | <span data-ttu-id="5a649-143">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="5a649-143">GUID</span></span> | <span data-ttu-id="5a649-144">Yes</span><span class="sxs-lookup"><span data-stu-id="5a649-144">Yes</span></span>      | <span data-ttu-id="5a649-145">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="5a649-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="5a649-146">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="5a649-146">**validationCode**</span></span>     | <span data-ttu-id="5a649-147">int</span><span class="sxs-lookup"><span data-stu-id="5a649-147">int</span></span>  | <span data-ttu-id="5a649-148">No</span><span class="sxs-lookup"><span data-stu-id="5a649-148">No</span></span>       | <span data-ttu-id="5a649-149">Je potřeba jenom pro Government Community Cloud.</span><span class="sxs-lookup"><span data-stu-id="5a649-149">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="5a649-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5a649-150">Request headers</span></span>

<span data-ttu-id="5a649-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5a649-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5a649-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="5a649-152">Request body</span></span>

<span data-ttu-id="5a649-153">Tato tabulka popisuje objekt kvalifikace v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="5a649-153">This table describes the qualification object in the request body.</span></span>

<span data-ttu-id="5a649-154">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="5a649-154">Property</span></span> | <span data-ttu-id="5a649-155">Typ</span><span class="sxs-lookup"><span data-stu-id="5a649-155">Type</span></span> | <span data-ttu-id="5a649-156">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="5a649-156">Required</span></span> | <span data-ttu-id="5a649-157">Popis</span><span class="sxs-lookup"><span data-stu-id="5a649-157">Description</span></span>
-------- | ---- | -------- | -----------
<span data-ttu-id="5a649-158">Qualification</span><span class="sxs-lookup"><span data-stu-id="5a649-158">Qualification</span></span> | <span data-ttu-id="5a649-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="5a649-159">string</span></span> | <span data-ttu-id="5a649-160">Yes</span><span class="sxs-lookup"><span data-stu-id="5a649-160">Yes</span></span> | <span data-ttu-id="5a649-161">Hodnota řetězce z výčtu [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .</span><span class="sxs-lookup"><span data-stu-id="5a649-161">The string value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="5a649-162">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="5a649-162">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a><span data-ttu-id="5a649-163">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5a649-163">REST response</span></span>

<span data-ttu-id="5a649-164">V případě úspěchu tato metoda vrátí objekt kvalifikace v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="5a649-164">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="5a649-165">Níže je uveden příklad volání **post** na zákazníka (s předchozí kvalifikací **none**) s kvalifikací **vzdělávání** .</span><span class="sxs-lookup"><span data-stu-id="5a649-165">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5a649-166">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="5a649-166">Response success and error codes</span></span>

<span data-ttu-id="5a649-167">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5a649-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5a649-168">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="5a649-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5a649-169">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5a649-169">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5a649-170">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="5a649-170">Response example</span></span>

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a><span data-ttu-id="5a649-171">Související články</span><span class="sxs-lookup"><span data-stu-id="5a649-171">Related articles</span></span>

- [<span data-ttu-id="5a649-172">Získání kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="5a649-172">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="5a649-173">Získání ověřovacích kódů partnera</span><span class="sxs-lookup"><span data-stu-id="5a649-173">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)
