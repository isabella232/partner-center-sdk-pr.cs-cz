---
title: Odstranění zásad konfigurace pro konkrétního zákazníka
description: Jak odstranit zásady konfigurace pro zadaného zákazníka a identifikátor zásady.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d6a7d392bd6af6850eb7716528e6745943bb7bb
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973022"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="e6ad2-103">Odstranění zásad konfigurace pro konkrétního zákazníka</span><span class="sxs-lookup"><span data-stu-id="e6ad2-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="e6ad2-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud (Německo)</span><span class="sxs-lookup"><span data-stu-id="e6ad2-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e6ad2-105">Jak odstranit zásady konfigurace pro zadaného zákazníka a identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-105">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6ad2-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e6ad2-106">Prerequisites</span></span>

- <span data-ttu-id="e6ad2-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e6ad2-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e6ad2-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e6ad2-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6ad2-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e6ad2-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e6ad2-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e6ad2-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="e6ad2-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e6ad2-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="e6ad2-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e6ad2-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e6ad2-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6ad2-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e6ad2-115">Identifikátor zásady.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="e6ad2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e6ad2-116">C\#</span></span>

<span data-ttu-id="e6ad2-117">Odstranění zásad konfigurace pro konkrétního zákazníka:</span><span class="sxs-lookup"><span data-stu-id="e6ad2-117">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="e6ad2-118">Voláním [**metody IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka načtěte rozhraní pro operace u zadaného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-118">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="e6ad2-119">Voláním [**metody ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) s ID zásady načtěte rozhraní pro operace zásad konfigurace pro zadané zásady.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-119">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="e6ad2-120">Pokud chcete [**odstranit zásady**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) konfigurace, zavolejte metodu Delete nebo [**DeleteAsync.**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync)</span><span class="sxs-lookup"><span data-stu-id="e6ad2-120">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="e6ad2-121">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e6ad2-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e6ad2-122">**Project:** SDK pro Partnerské centrum Samples **Class**: DeleteConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="e6ad2-122">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e6ad2-123">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="e6ad2-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e6ad2-124">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="e6ad2-124">Request syntax</span></span>

| <span data-ttu-id="e6ad2-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="e6ad2-125">Method</span></span>     | <span data-ttu-id="e6ad2-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e6ad2-126">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e6ad2-127">**Odstranit**</span><span class="sxs-lookup"><span data-stu-id="e6ad2-127">**DELETE**</span></span> | <span data-ttu-id="e6ad2-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/policies/{ID_zásad} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e6ad2-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="e6ad2-129">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="e6ad2-129">URI parameters</span></span>

<span data-ttu-id="e6ad2-130">Při vytváření požadavku použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="e6ad2-131">Název</span><span class="sxs-lookup"><span data-stu-id="e6ad2-131">Name</span></span>        | <span data-ttu-id="e6ad2-132">Typ</span><span class="sxs-lookup"><span data-stu-id="e6ad2-132">Type</span></span>   | <span data-ttu-id="e6ad2-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e6ad2-133">Required</span></span> | <span data-ttu-id="e6ad2-134">Popis</span><span class="sxs-lookup"><span data-stu-id="e6ad2-134">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="e6ad2-135">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="e6ad2-135">customer-id</span></span> | <span data-ttu-id="e6ad2-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="e6ad2-136">string</span></span> | <span data-ttu-id="e6ad2-137">Yes</span><span class="sxs-lookup"><span data-stu-id="e6ad2-137">Yes</span></span>      | <span data-ttu-id="e6ad2-138">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-138">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="e6ad2-139">ID zásady</span><span class="sxs-lookup"><span data-stu-id="e6ad2-139">policy-id</span></span>   | <span data-ttu-id="e6ad2-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="e6ad2-140">string</span></span> | <span data-ttu-id="e6ad2-141">Yes</span><span class="sxs-lookup"><span data-stu-id="e6ad2-141">Yes</span></span>      | <span data-ttu-id="e6ad2-142">Řetězec ve formátu GUID, který identifikuje zásadu, kterou chcete odstranit.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-142">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e6ad2-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e6ad2-143">Request headers</span></span>

<span data-ttu-id="e6ad2-144">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e6ad2-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e6ad2-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e6ad2-145">Request body</span></span>

<span data-ttu-id="e6ad2-146">Žádná</span><span class="sxs-lookup"><span data-stu-id="e6ad2-146">None</span></span>

### <a name="request-example"></a><span data-ttu-id="e6ad2-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e6ad2-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e6ad2-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e6ad2-148">REST response</span></span>

<span data-ttu-id="e6ad2-149">V případě úspěchu vrátí odpověď stavový kód 204 Žádný obsah.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-149">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e6ad2-150">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="e6ad2-150">Response success and error codes</span></span>

<span data-ttu-id="e6ad2-151">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e6ad2-152">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="e6ad2-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e6ad2-153">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e6ad2-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e6ad2-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e6ad2-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
