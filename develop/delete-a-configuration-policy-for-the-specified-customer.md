---
title: Odstranění zásad konfigurace pro konkrétního zákazníka
description: Jak odstranit zásadu konfigurace pro zadaný identifikátor zákazníka a zásady.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 586878367fc0873ef0fb1415799b2b7022954053
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766881"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="7201f-103">Odstranění zásad konfigurace pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="7201f-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="7201f-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="7201f-104">**Applies to:**</span></span>

- <span data-ttu-id="7201f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="7201f-105">Partner Center</span></span>
- <span data-ttu-id="7201f-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="7201f-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="7201f-107">Jak odstranit zásadu konfigurace pro zadaný identifikátor zákazníka a zásady.</span><span class="sxs-lookup"><span data-stu-id="7201f-107">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7201f-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7201f-108">Prerequisites</span></span>

- <span data-ttu-id="7201f-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7201f-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7201f-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="7201f-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7201f-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7201f-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7201f-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="7201f-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7201f-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="7201f-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7201f-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="7201f-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7201f-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="7201f-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7201f-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7201f-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7201f-117">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="7201f-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="7201f-118">C\#</span><span class="sxs-lookup"><span data-stu-id="7201f-118">C\#</span></span>

<span data-ttu-id="7201f-119">Postup odstranění zásad konfigurace pro určitého zákazníka:</span><span class="sxs-lookup"><span data-stu-id="7201f-119">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="7201f-120">Zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka, aby se načetlo rozhraní pro operace zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7201f-120">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="7201f-121">Voláním metody [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásad načtěte rozhraní pro operace zásad konfigurace pro zadané zásady.</span><span class="sxs-lookup"><span data-stu-id="7201f-121">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="7201f-122">Chcete-li odstranit zásadu konfigurace, zavolejte metodu [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) nebo [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) .</span><span class="sxs-lookup"><span data-stu-id="7201f-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="7201f-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7201f-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7201f-124">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: DeleteConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="7201f-124">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7201f-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="7201f-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7201f-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="7201f-126">Request syntax</span></span>

| <span data-ttu-id="7201f-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="7201f-127">Method</span></span>     | <span data-ttu-id="7201f-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="7201f-128">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7201f-129">**DSTRANIT**</span><span class="sxs-lookup"><span data-stu-id="7201f-129">**DELETE**</span></span> | <span data-ttu-id="7201f-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7201f-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="7201f-131">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="7201f-131">URI parameters</span></span>

<span data-ttu-id="7201f-132">Při vytváření žádosti použít následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="7201f-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="7201f-133">Název</span><span class="sxs-lookup"><span data-stu-id="7201f-133">Name</span></span>        | <span data-ttu-id="7201f-134">Typ</span><span class="sxs-lookup"><span data-stu-id="7201f-134">Type</span></span>   | <span data-ttu-id="7201f-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="7201f-135">Required</span></span> | <span data-ttu-id="7201f-136">Popis</span><span class="sxs-lookup"><span data-stu-id="7201f-136">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="7201f-137">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="7201f-137">customer-id</span></span> | <span data-ttu-id="7201f-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="7201f-138">string</span></span> | <span data-ttu-id="7201f-139">Yes</span><span class="sxs-lookup"><span data-stu-id="7201f-139">Yes</span></span>      | <span data-ttu-id="7201f-140">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7201f-140">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="7201f-141">ID zásady</span><span class="sxs-lookup"><span data-stu-id="7201f-141">policy-id</span></span>   | <span data-ttu-id="7201f-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="7201f-142">string</span></span> | <span data-ttu-id="7201f-143">Yes</span><span class="sxs-lookup"><span data-stu-id="7201f-143">Yes</span></span>      | <span data-ttu-id="7201f-144">Řetězec ve formátu GUID, který identifikuje zásadu, která se má odstranit.</span><span class="sxs-lookup"><span data-stu-id="7201f-144">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7201f-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="7201f-145">Request headers</span></span>

<span data-ttu-id="7201f-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7201f-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7201f-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="7201f-147">Request body</span></span>

<span data-ttu-id="7201f-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="7201f-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="7201f-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="7201f-149">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7201f-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="7201f-150">REST response</span></span>

<span data-ttu-id="7201f-151">V případě úspěchu vrátí odpověď 204 bez stavového kódu obsahu.</span><span class="sxs-lookup"><span data-stu-id="7201f-151">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7201f-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="7201f-152">Response success and error codes</span></span>

<span data-ttu-id="7201f-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="7201f-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7201f-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="7201f-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7201f-155">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7201f-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7201f-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="7201f-156">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
