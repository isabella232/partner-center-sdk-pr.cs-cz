---
title: Odstranění uživatelských účtů pro zákazníka
description: Postup odstranění existujícího uživatelského účtu pro zákazníka
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c45646da43b8926f911942374de5da07f318c526
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973056"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="f433a-103">Odstranění uživatelských účtů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="f433a-103">Delete a user account for a customer</span></span>

<span data-ttu-id="f433a-104">Tento článek vysvětluje, jak odstranit existující uživatelský účet zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f433a-104">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f433a-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f433a-105">Prerequisites</span></span>

- <span data-ttu-id="f433a-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f433a-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f433a-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="f433a-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f433a-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f433a-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f433a-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="f433a-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f433a-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="f433a-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f433a-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="f433a-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f433a-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f433a-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f433a-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f433a-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f433a-114">ID uživatele.</span><span class="sxs-lookup"><span data-stu-id="f433a-114">A user ID.</span></span> <span data-ttu-id="f433a-115">Pokud id uživatele nemáte, podívejte se na část Získání seznamu [všech uživatelských účtů pro zákazníka.](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="f433a-115">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="f433a-116">Odstranění uživatelského účtu</span><span class="sxs-lookup"><span data-stu-id="f433a-116">Deleting a user account</span></span>

<span data-ttu-id="f433a-117">Když odstraníte uživatelský účet, stav uživatele bude po dobu 30 dnů **neaktivní.**</span><span class="sxs-lookup"><span data-stu-id="f433a-117">When you delete a user account, the user state is set to **inactive** for 30 days.</span></span> <span data-ttu-id="f433a-118">Po 30 dnech se uživatelský účet a jeho přidružená data vyprázdní a nenapraví.</span><span class="sxs-lookup"><span data-stu-id="f433a-118">After thirty 30 days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="f433a-119">Odstraněný [uživatelský účet zákazníka můžete obnovit, pokud](restore-a-user-for-a-customer.md) se neaktivní účet nachází v 30denním okně.</span><span class="sxs-lookup"><span data-stu-id="f433a-119">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the 30-day window.</span></span> <span data-ttu-id="f433a-120">Když ale obnovíte odstraněný účet, který je označený jako neaktivní, nebude už tento účet vrácen jako člen kolekce uživatelů (například když získáte seznam všech uživatelských účtů pro [zákazníka).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="f433a-120">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="f433a-121">C\#</span><span class="sxs-lookup"><span data-stu-id="f433a-121">C\#</span></span>

<span data-ttu-id="f433a-122">Odstranění existujícího uživatelského účtu zákazníka:</span><span class="sxs-lookup"><span data-stu-id="f433a-122">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="f433a-123">K identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f433a-123">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="f433a-124">Voláním [**metody Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) identifikujte uživatele.</span><span class="sxs-lookup"><span data-stu-id="f433a-124">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="f433a-125">Voláním [**metody Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) odstraňte uživatele a nastavte stav uživatele na neaktivní.</span><span class="sxs-lookup"><span data-stu-id="f433a-125">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="f433a-126">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f433a-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f433a-127">**Project:** SDK pro Partnerské centrum Samples **Class:** DeleteCustomerUser.cs</span><span class="sxs-lookup"><span data-stu-id="f433a-127">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f433a-128">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="f433a-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f433a-129">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="f433a-129">Request syntax</span></span>

| <span data-ttu-id="f433a-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="f433a-130">Method</span></span>     | <span data-ttu-id="f433a-131">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f433a-131">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f433a-132">DELETE</span><span class="sxs-lookup"><span data-stu-id="f433a-132">DELETE</span></span>     | <span data-ttu-id="f433a-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/users/{ID_uživatele} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f433a-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f433a-134">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="f433a-134">URI parameters</span></span>

<span data-ttu-id="f433a-135">K identifikaci zákazníka a uživatele použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="f433a-135">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="f433a-136">Název</span><span class="sxs-lookup"><span data-stu-id="f433a-136">Name</span></span>                   | <span data-ttu-id="f433a-137">Typ</span><span class="sxs-lookup"><span data-stu-id="f433a-137">Type</span></span>     | <span data-ttu-id="f433a-138">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f433a-138">Required</span></span> | <span data-ttu-id="f433a-139">Popis</span><span class="sxs-lookup"><span data-stu-id="f433a-139">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f433a-140">customer-tenant-id</span><span class="sxs-lookup"><span data-stu-id="f433a-140">customer-tenant-id</span></span>     | <span data-ttu-id="f433a-141">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="f433a-141">GUID</span></span>     | <span data-ttu-id="f433a-142">Y</span><span class="sxs-lookup"><span data-stu-id="f433a-142">Y</span></span>        | <span data-ttu-id="f433a-143">Hodnota je ID tenanta zákazníka ve formátu GUID, které prodejci umožňuje filtrovat výsledky pro daného zákazníka. </span><span class="sxs-lookup"><span data-stu-id="f433a-143">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="f433a-144">user-id</span><span class="sxs-lookup"><span data-stu-id="f433a-144">user-id</span></span>                | <span data-ttu-id="f433a-145">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="f433a-145">GUID</span></span>     | <span data-ttu-id="f433a-146">Y</span><span class="sxs-lookup"><span data-stu-id="f433a-146">Y</span></span>        | <span data-ttu-id="f433a-147">Hodnota je ID uživatele ve **formátu** GUID, které patří k jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="f433a-147">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="f433a-148">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f433a-148">Request headers</span></span>

<span data-ttu-id="f433a-149">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f433a-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f433a-150">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f433a-150">Request body</span></span>

<span data-ttu-id="f433a-151">Žádné</span><span class="sxs-lookup"><span data-stu-id="f433a-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f433a-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f433a-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f433a-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f433a-153">REST response</span></span>

<span data-ttu-id="f433a-154">V případě úspěchu tato metoda vrátí stavový kód **204 Žádný** obsah.</span><span class="sxs-lookup"><span data-stu-id="f433a-154">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f433a-155">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="f433a-155">Response success and error codes</span></span>

<span data-ttu-id="f433a-156">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f433a-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f433a-157">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="f433a-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f433a-158">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f433a-158">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f433a-159">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f433a-159">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
