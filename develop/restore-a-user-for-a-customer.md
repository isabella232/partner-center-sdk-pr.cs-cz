---
title: Obnovení odstraněného uživatele pro zákazníka
description: Jak obnovit odstraněného uživatele podle ID zákazníka a ID uživatele
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23caf91c6b29b292c2638b4a1ad208c606c47492
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445710"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="a33f5-103">Obnovení odstraněného uživatele pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="a33f5-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="a33f5-104">Jak obnovit odstraněného **uživatele podle** ID zákazníka a ID uživatele</span><span class="sxs-lookup"><span data-stu-id="a33f5-104">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a33f5-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a33f5-105">Prerequisites</span></span>

- <span data-ttu-id="a33f5-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a33f5-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a33f5-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="a33f5-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="a33f5-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a33f5-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a33f5-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a33f5-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a33f5-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="a33f5-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a33f5-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="a33f5-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a33f5-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a33f5-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a33f5-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a33f5-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a33f5-114">ID uživatele.</span><span class="sxs-lookup"><span data-stu-id="a33f5-114">The user ID.</span></span> <span data-ttu-id="a33f5-115">Pokud id uživatele nemáte, podívejte se na stránku [Zobrazení odstraněných uživatelů pro zákazníka.](view-a-deleted-user.md)</span><span class="sxs-lookup"><span data-stu-id="a33f5-115">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="a33f5-116">Kdy můžete obnovit odstraněný uživatelský účet?</span><span class="sxs-lookup"><span data-stu-id="a33f5-116">When can you restore a deleted user account?</span></span>

<span data-ttu-id="a33f5-117">Stav uživatele je při odstranění uživatelského účtu nastavený na "neaktivní".</span><span class="sxs-lookup"><span data-stu-id="a33f5-117">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="a33f5-118">Zůstane tak po dobu 30 dnů, po jejímž uplynutí se uživatelský účet a jeho přidružená data vyprázdní a nenapraví.</span><span class="sxs-lookup"><span data-stu-id="a33f5-118">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="a33f5-119">Odstraněný uživatelský účet můžete obnovit pouze během tohoto 30denního období.</span><span class="sxs-lookup"><span data-stu-id="a33f5-119">You can only restore a deleted user account during this 30-day window.</span></span> <span data-ttu-id="a33f5-120">Po odstranění a označení jako neaktivní už se uživatelský účet nebude vrátil jako člen kolekce uživatelů (například pomocí příkazu Získat seznam všech uživatelských účtů pro [zákazníka).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="a33f5-120">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="a33f5-121">C\#</span><span class="sxs-lookup"><span data-stu-id="a33f5-121">C\#</span></span>

<span data-ttu-id="a33f5-122">Pokud chcete obnovit uživatele, vytvořte novou instanci třídy [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) a nastavte hodnotu vlastnosti [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) na [**UserState.Active.**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)</span><span class="sxs-lookup"><span data-stu-id="a33f5-122">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="a33f5-123">Odstraněný uživatel obnovíte nastavením stavu uživatele na aktivní.</span><span class="sxs-lookup"><span data-stu-id="a33f5-123">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="a33f5-124">Zbývající pole v uživatelském prostředku není možné znovu zapopilovat.</span><span class="sxs-lookup"><span data-stu-id="a33f5-124">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="a33f5-125">Tyto hodnoty se automaticky obnoví z odstraněného neaktivního uživatelského prostředku.</span><span class="sxs-lookup"><span data-stu-id="a33f5-125">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="a33f5-126">Dále pomocí metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka identifikujte zákazníka a metodu [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) k identifikaci uživatele.</span><span class="sxs-lookup"><span data-stu-id="a33f5-126">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="a33f5-127">Nakonec zavolejte [**metodu Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) a předejte instanci **CustomerUser,** která odešle požadavek na obnovení uživatele.</span><span class="sxs-lookup"><span data-stu-id="a33f5-127">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

<span data-ttu-id="a33f5-128">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a33f5-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a33f5-129">**Project:** SDK pro Partnerské centrum Samples **Class:** CustomerUserRestore.cs</span><span class="sxs-lookup"><span data-stu-id="a33f5-129">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a33f5-130">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="a33f5-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a33f5-131">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="a33f5-131">Request syntax</span></span>

| <span data-ttu-id="a33f5-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="a33f5-132">Method</span></span>    | <span data-ttu-id="a33f5-133">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="a33f5-133">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a33f5-134">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="a33f5-134">**PATCH**</span></span> | <span data-ttu-id="a33f5-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/users/{ID_uživatele} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a33f5-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a33f5-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a33f5-136">URI parameter</span></span>

<span data-ttu-id="a33f5-137">Pomocí následujících parametrů dotazu zadejte ID zákazníka a ID uživatele.</span><span class="sxs-lookup"><span data-stu-id="a33f5-137">Use the following query parameters to specify the customer ID and user ID.</span></span>

| <span data-ttu-id="a33f5-138">Název</span><span class="sxs-lookup"><span data-stu-id="a33f5-138">Name</span></span>                   | <span data-ttu-id="a33f5-139">Typ</span><span class="sxs-lookup"><span data-stu-id="a33f5-139">Type</span></span>     | <span data-ttu-id="a33f5-140">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a33f5-140">Required</span></span> | <span data-ttu-id="a33f5-141">Popis</span><span class="sxs-lookup"><span data-stu-id="a33f5-141">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a33f5-142">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="a33f5-142">**customer-tenant-id**</span></span> | <span data-ttu-id="a33f5-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="a33f5-143">**guid**</span></span> | <span data-ttu-id="a33f5-144">Y</span><span class="sxs-lookup"><span data-stu-id="a33f5-144">Y</span></span>        | <span data-ttu-id="a33f5-145">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který prodejci umožňuje filtrovat výsledky na daného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="a33f5-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="a33f5-146">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="a33f5-146">**user-id**</span></span>            | <span data-ttu-id="a33f5-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="a33f5-147">**guid**</span></span> | <span data-ttu-id="a33f5-148">Y</span><span class="sxs-lookup"><span data-stu-id="a33f5-148">Y</span></span>        | <span data-ttu-id="a33f5-149">Hodnota je ID uživatele ve **formátu** GUID, které patří jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="a33f5-149">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="a33f5-150">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="a33f5-150">Request headers</span></span>

<span data-ttu-id="a33f5-151">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a33f5-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a33f5-152">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="a33f5-152">Request body</span></span>

<span data-ttu-id="a33f5-153">Tato tabulka popisuje požadované vlastnosti v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="a33f5-153">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="a33f5-154">Název</span><span class="sxs-lookup"><span data-stu-id="a33f5-154">Name</span></span>       | <span data-ttu-id="a33f5-155">Typ</span><span class="sxs-lookup"><span data-stu-id="a33f5-155">Type</span></span>   | <span data-ttu-id="a33f5-156">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="a33f5-156">Required</span></span> | <span data-ttu-id="a33f5-157">Popis</span><span class="sxs-lookup"><span data-stu-id="a33f5-157">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="a33f5-158">Stav</span><span class="sxs-lookup"><span data-stu-id="a33f5-158">State</span></span>      | <span data-ttu-id="a33f5-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="a33f5-159">string</span></span> | <span data-ttu-id="a33f5-160">Y</span><span class="sxs-lookup"><span data-stu-id="a33f5-160">Y</span></span>        | <span data-ttu-id="a33f5-161">Stav uživatele</span><span class="sxs-lookup"><span data-stu-id="a33f5-161">The user state.</span></span> <span data-ttu-id="a33f5-162">Pokud chcete odstraněného uživatele obnovit, musí tento řetězec obsahovat hodnotu "active".</span><span class="sxs-lookup"><span data-stu-id="a33f5-162">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="a33f5-163">Atributy</span><span class="sxs-lookup"><span data-stu-id="a33f5-163">Attributes</span></span> | <span data-ttu-id="a33f5-164">object</span><span class="sxs-lookup"><span data-stu-id="a33f5-164">object</span></span> | <span data-ttu-id="a33f5-165">N</span><span class="sxs-lookup"><span data-stu-id="a33f5-165">N</span></span>        | <span data-ttu-id="a33f5-166">Obsahuje "ObjectType": "CustomerUser".</span><span class="sxs-lookup"><span data-stu-id="a33f5-166">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="a33f5-167">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="a33f5-167">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="a33f5-168">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="a33f5-168">REST response</span></span>

<span data-ttu-id="a33f5-169">V případě úspěchu vrátí odpověď obnovené informace o uživateli v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="a33f5-169">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a33f5-170">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="a33f5-170">Response success and error codes</span></span>

<span data-ttu-id="a33f5-171">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="a33f5-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a33f5-172">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="a33f5-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a33f5-173">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a33f5-173">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a33f5-174">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="a33f5-174">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
