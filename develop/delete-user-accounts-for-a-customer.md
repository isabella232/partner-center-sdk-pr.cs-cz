---
title: Odstranění uživatelských účtů pro zákazníka
description: Jak odstranit existující uživatelský účet pro zákazníka.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766878"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="46d8c-103">Odstranění uživatelských účtů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="46d8c-103">Delete a user account for a customer</span></span>

<span data-ttu-id="46d8c-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="46d8c-104">**Applies to:**</span></span>

- <span data-ttu-id="46d8c-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="46d8c-105">Partner Center</span></span>

<span data-ttu-id="46d8c-106">Tento článek vysvětluje, jak odstranit existující uživatelský účet pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="46d8c-106">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46d8c-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="46d8c-107">Prerequisites</span></span>

- <span data-ttu-id="46d8c-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="46d8c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="46d8c-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="46d8c-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="46d8c-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="46d8c-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="46d8c-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="46d8c-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="46d8c-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="46d8c-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="46d8c-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="46d8c-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="46d8c-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="46d8c-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="46d8c-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="46d8c-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="46d8c-116">ID uživatele</span><span class="sxs-lookup"><span data-stu-id="46d8c-116">A user ID.</span></span> <span data-ttu-id="46d8c-117">Pokud nemáte ID uživatele, přečtěte si téma [získání seznamu všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="46d8c-117">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="46d8c-118">Odstranění uživatelského účtu</span><span class="sxs-lookup"><span data-stu-id="46d8c-118">Deleting a user account</span></span>

<span data-ttu-id="46d8c-119">Po odstranění uživatelského účtu se stav uživatele nastaví na **neaktivní** po dobu třiceti dnů.</span><span class="sxs-lookup"><span data-stu-id="46d8c-119">When you delete a user account, the user state is set to **inactive** for thirty days.</span></span> <span data-ttu-id="46d8c-120">Po 30 dnech se uživatelský účet a jeho přidružená data vyprázdní a provedou neobnovitelné.</span><span class="sxs-lookup"><span data-stu-id="46d8c-120">After thirty days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="46d8c-121">[Odstraněný uživatelský účet můžete obnovit pro zákazníka](restore-a-user-for-a-customer.md) , pokud je neaktivní účet v rámci třiceti dnů.</span><span class="sxs-lookup"><span data-stu-id="46d8c-121">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the thirty day window.</span></span> <span data-ttu-id="46d8c-122">Když ale obnovíte účet, který se odstranil a je označený jako neaktivní, účet se už nevrátí jako člen kolekce uživatelů (například když [získáte seznam všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="46d8c-122">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="46d8c-123">C\#</span><span class="sxs-lookup"><span data-stu-id="46d8c-123">C\#</span></span>

<span data-ttu-id="46d8c-124">Odstranění existujícího uživatelského účtu zákazníka:</span><span class="sxs-lookup"><span data-stu-id="46d8c-124">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="46d8c-125">K identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="46d8c-125">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="46d8c-126">Voláním metody User [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) Identifikujte uživatele.</span><span class="sxs-lookup"><span data-stu-id="46d8c-126">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="46d8c-127">Voláním metody [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) odstraňte uživatele a nastavte stav uživatele na neaktivní.</span><span class="sxs-lookup"><span data-stu-id="46d8c-127">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="46d8c-128">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="46d8c-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="46d8c-129">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: DeleteCustomerUser.cs</span><span class="sxs-lookup"><span data-stu-id="46d8c-129">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="46d8c-130">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="46d8c-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="46d8c-131">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="46d8c-131">Request syntax</span></span>

| <span data-ttu-id="46d8c-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="46d8c-132">Method</span></span>     | <span data-ttu-id="46d8c-133">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="46d8c-133">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="46d8c-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="46d8c-134">DELETE</span></span>     | <span data-ttu-id="46d8c-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="46d8c-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="46d8c-136">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="46d8c-136">URI parameters</span></span>

<span data-ttu-id="46d8c-137">K identifikaci zákazníka a uživatele použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="46d8c-137">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="46d8c-138">Název</span><span class="sxs-lookup"><span data-stu-id="46d8c-138">Name</span></span>                   | <span data-ttu-id="46d8c-139">Typ</span><span class="sxs-lookup"><span data-stu-id="46d8c-139">Type</span></span>     | <span data-ttu-id="46d8c-140">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="46d8c-140">Required</span></span> | <span data-ttu-id="46d8c-141">Popis</span><span class="sxs-lookup"><span data-stu-id="46d8c-141">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="46d8c-142">Customer-tenant-ID</span><span class="sxs-lookup"><span data-stu-id="46d8c-142">customer-tenant-id</span></span>     | <span data-ttu-id="46d8c-143">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="46d8c-143">GUID</span></span>     | <span data-ttu-id="46d8c-144">Y</span><span class="sxs-lookup"><span data-stu-id="46d8c-144">Y</span></span>        | <span data-ttu-id="46d8c-145">Hodnota je **zákazníkem** formátovaného identifikátoru GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="46d8c-145">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="46d8c-146">user-id</span><span class="sxs-lookup"><span data-stu-id="46d8c-146">user-id</span></span>                | <span data-ttu-id="46d8c-147">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="46d8c-147">GUID</span></span>     | <span data-ttu-id="46d8c-148">Y</span><span class="sxs-lookup"><span data-stu-id="46d8c-148">Y</span></span>        | <span data-ttu-id="46d8c-149">Hodnota je **uživatelské ID** formátované identifikátorem GUID, které patří jedinému uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="46d8c-149">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="46d8c-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="46d8c-150">Request headers</span></span>

<span data-ttu-id="46d8c-151">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="46d8c-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="46d8c-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="46d8c-152">Request body</span></span>

<span data-ttu-id="46d8c-153">Žádné</span><span class="sxs-lookup"><span data-stu-id="46d8c-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="46d8c-154">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="46d8c-154">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="46d8c-155">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="46d8c-155">REST response</span></span>

<span data-ttu-id="46d8c-156">V případě úspěchu tato metoda vrátí kód stavu **204 bez obsahu** .</span><span class="sxs-lookup"><span data-stu-id="46d8c-156">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="46d8c-157">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="46d8c-157">Response success and error codes</span></span>

<span data-ttu-id="46d8c-158">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="46d8c-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="46d8c-159">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="46d8c-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="46d8c-160">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="46d8c-160">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="46d8c-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="46d8c-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
