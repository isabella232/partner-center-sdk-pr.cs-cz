---
title: Aktualizace kvalifikace zákazníka
description: Naučte se aktualizovat kvalifikace zákazníka prostřednictvím asynchronního screeningu nebo dozvíte ČSFD, včetně adresy přidružené k profilu.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 703585eeaba93b6d7a510a3174a78a28f22e1510
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711929"
---
# <a name="update-a-customers-qualifications-asynchronously"></a><span data-ttu-id="bda72-103">Asynchronní aktualizace kvalifikací zákazníka</span><span class="sxs-lookup"><span data-stu-id="bda72-103">Update a customer's qualifications asynchronously</span></span>

<span data-ttu-id="bda72-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="bda72-104">**Applies To**</span></span>

- <span data-ttu-id="bda72-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="bda72-105">Partner Center</span></span>

<span data-ttu-id="bda72-106">Naučte se asynchronně aktualizovat kvalifikace zákazníka prostřednictvím rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="bda72-106">Learn how to update a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="bda72-107">Pokud se chcete dozvědět, jak to provést synchronně, přečtěte si téma [aktualizace kvalifikace zákazníka prostřednictvím synchronního ověřování](update-customer-qualification-synchronous.md).</span><span class="sxs-lookup"><span data-stu-id="bda72-107">To learn how to do this synchronously, see [Update a customer's qualification via synchronous validation](update-customer-qualification-synchronous.md).</span></span>

<span data-ttu-id="bda72-108">Partner může provést asynchronní aktualizaci kvalifikací zákazníka, pokud jde o "vzdělávání" nebo "GovernmentCommunityCloud".</span><span class="sxs-lookup"><span data-stu-id="bda72-108">A partner can update a customer's qualifications asynchronously to be "Education" or "GovernmentCommunityCloud".</span></span> <span data-ttu-id="bda72-109">Další hodnoty, "none" a "neziskové" nelze nastavit.</span><span class="sxs-lookup"><span data-stu-id="bda72-109">Other values, "None" and "Nonprofit", cannot be set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bda72-110">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="bda72-110">Prerequisites</span></span>

- <span data-ttu-id="bda72-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bda72-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bda72-112">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="bda72-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="bda72-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bda72-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="bda72-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="bda72-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="bda72-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="bda72-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="bda72-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="bda72-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="bda72-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="bda72-117">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="bda72-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bda72-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="bda72-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="bda72-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bda72-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="bda72-120">Request syntax</span></span>

| <span data-ttu-id="bda72-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="bda72-121">Method</span></span>  | <span data-ttu-id="bda72-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="bda72-122">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bda72-123">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="bda72-123">**POST**</span></span> | <span data-ttu-id="bda72-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer_ID}/Qualifications? kód = {VALIDATIONCODE} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bda72-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="bda72-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="bda72-125">URI parameter</span></span>

<span data-ttu-id="bda72-126">K aktualizaci kvalifikace použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="bda72-126">Use the following query parameter to update the qualification.</span></span>

| <span data-ttu-id="bda72-127">Název</span><span class="sxs-lookup"><span data-stu-id="bda72-127">Name</span></span>                   | <span data-ttu-id="bda72-128">Typ</span><span class="sxs-lookup"><span data-stu-id="bda72-128">Type</span></span> | <span data-ttu-id="bda72-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="bda72-129">Required</span></span> | <span data-ttu-id="bda72-130">Popis</span><span class="sxs-lookup"><span data-stu-id="bda72-130">Description</span></span>                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bda72-131">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="bda72-131">**customer-tenant-id**</span></span> | <span data-ttu-id="bda72-132">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="bda72-132">GUID</span></span> | <span data-ttu-id="bda72-133">Yes</span><span class="sxs-lookup"><span data-stu-id="bda72-133">Yes</span></span>      | <span data-ttu-id="bda72-134">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="bda72-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="bda72-135">**validationCode**</span><span class="sxs-lookup"><span data-stu-id="bda72-135">**validationCode**</span></span>     | <span data-ttu-id="bda72-136">int</span><span class="sxs-lookup"><span data-stu-id="bda72-136">int</span></span>  | <span data-ttu-id="bda72-137">No</span><span class="sxs-lookup"><span data-stu-id="bda72-137">No</span></span>       | <span data-ttu-id="bda72-138">Je potřeba jenom pro cloudovou komunitu státní správy.</span><span class="sxs-lookup"><span data-stu-id="bda72-138">Only needed for Government Community Cloud.</span></span>                                                                                                            |

### <a name="request-headers"></a><span data-ttu-id="bda72-139">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="bda72-139">Request headers</span></span>

<span data-ttu-id="bda72-140">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bda72-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bda72-141">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="bda72-141">Request body</span></span>

<span data-ttu-id="bda72-142">Celočíselná hodnota z výčtu [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .</span><span class="sxs-lookup"><span data-stu-id="bda72-142">The integer value from the [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enum.</span></span>

### <a name="request-example"></a><span data-ttu-id="bda72-143">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="bda72-143">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a><span data-ttu-id="bda72-144">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="bda72-144">REST response</span></span>

<span data-ttu-id="bda72-145">V případě úspěchu tato metoda vrátí objekt kvalifikace v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="bda72-145">If successful, this method returns a qualifications object in the response body.</span></span> <span data-ttu-id="bda72-146">Níže je uveden příklad volání **post** na zákazníka (s předchozí kvalifikací **none**) s kvalifikací **vzdělávání** .</span><span class="sxs-lookup"><span data-stu-id="bda72-146">Below is an example of the **POST** call on a customer (with a previous qualification of **None**) with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bda72-147">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="bda72-147">Response success and error codes</span></span>

<span data-ttu-id="bda72-148">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="bda72-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bda72-149">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="bda72-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bda72-150">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bda72-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bda72-151">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="bda72-151">Response example</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="bda72-152">Související články</span><span class="sxs-lookup"><span data-stu-id="bda72-152">Related articles</span></span>

- [<span data-ttu-id="bda72-153">Získání kvalifikace zákazníka</span><span class="sxs-lookup"><span data-stu-id="bda72-153">Get a customer's qualifications</span></span>](./get-customer-qualification-asynchronous.md)
- [<span data-ttu-id="bda72-154">Získání ověřovacích kódů partnera</span><span class="sxs-lookup"><span data-stu-id="bda72-154">Get a partner's validation codes</span></span>](get-a-partner-s-validation-codes.md)