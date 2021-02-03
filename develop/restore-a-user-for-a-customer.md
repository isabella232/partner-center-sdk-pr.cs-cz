---
title: Obnovení odstraněného uživatele pro zákazníka
description: Jak obnovit odstraněné uživatele podle ID zákazníka a ID uživatele.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767017"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="97ec1-103">Obnovení odstraněného uživatele pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="97ec1-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="97ec1-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="97ec1-104">**Applies To**</span></span>

- <span data-ttu-id="97ec1-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="97ec1-105">Partner Center</span></span>

<span data-ttu-id="97ec1-106">Jak obnovit odstraněné **uživatele** podle ID zákazníka a ID uživatele.</span><span class="sxs-lookup"><span data-stu-id="97ec1-106">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97ec1-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="97ec1-107">Prerequisites</span></span>

- <span data-ttu-id="97ec1-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="97ec1-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="97ec1-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="97ec1-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="97ec1-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="97ec1-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="97ec1-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="97ec1-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="97ec1-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="97ec1-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="97ec1-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="97ec1-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="97ec1-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="97ec1-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="97ec1-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="97ec1-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="97ec1-116">ID uživatele</span><span class="sxs-lookup"><span data-stu-id="97ec1-116">The user ID.</span></span> <span data-ttu-id="97ec1-117">Pokud nemáte ID uživatele, přečtěte si téma [zobrazení odstraněných uživatelů pro zákazníka](view-a-deleted-user.md).</span><span class="sxs-lookup"><span data-stu-id="97ec1-117">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="97ec1-118">Kdy je možné obnovit odstraněný uživatelský účet?</span><span class="sxs-lookup"><span data-stu-id="97ec1-118">When can you restore a deleted user account?</span></span>

<span data-ttu-id="97ec1-119">Stav uživatele je nastaven na "neaktivní" při odstranění uživatelského účtu.</span><span class="sxs-lookup"><span data-stu-id="97ec1-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="97ec1-120">Zůstane to po dobu třiceti dnů, po jejímž uplynutí se uživatelský účet a jeho přidružená data vyprázdní a provedou neobnovitelné.</span><span class="sxs-lookup"><span data-stu-id="97ec1-120">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="97ec1-121">Odstraněný uživatelský účet můžete obnovit jenom během tohoto 30denní okna.</span><span class="sxs-lookup"><span data-stu-id="97ec1-121">You can only restore a deleted user account during this thirty-day window.</span></span> <span data-ttu-id="97ec1-122">Po odstranění a označení jako neaktivní se uživatelský účet už nevrátí jako člen kolekce uživatelů (například pomocí příkazu [získat seznam všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="97ec1-122">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="97ec1-123">C\#</span><span class="sxs-lookup"><span data-stu-id="97ec1-123">C\#</span></span>

<span data-ttu-id="97ec1-124">Chcete-li obnovit uživatele, vytvořte novou instanci třídy [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) a nastavte hodnotu vlastnosti [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) na [**userState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span><span class="sxs-lookup"><span data-stu-id="97ec1-124">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="97ec1-125">Odstraněné uživatele obnovíte tak, že nastavíte stav uživatele na aktivní.</span><span class="sxs-lookup"><span data-stu-id="97ec1-125">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="97ec1-126">Zbývající pole v prostředku uživatele není nutné znovu naplňovat.</span><span class="sxs-lookup"><span data-stu-id="97ec1-126">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="97ec1-127">Tyto hodnoty se automaticky obnoví z odstraněného neaktivního prostředku uživatele.</span><span class="sxs-lookup"><span data-stu-id="97ec1-127">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="97ec1-128">Dále použijte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka a metodu [**Users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pro identifikaci uživatele.</span><span class="sxs-lookup"><span data-stu-id="97ec1-128">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="97ec1-129">Nakonec zavolejte metodu [**patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) a předejte instanci **CustomerUser** , aby odeslala požadavek na obnovení uživatele.</span><span class="sxs-lookup"><span data-stu-id="97ec1-129">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

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

<span data-ttu-id="97ec1-130">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="97ec1-130">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="97ec1-131">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: CustomerUserRestore.cs</span><span class="sxs-lookup"><span data-stu-id="97ec1-131">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="97ec1-132">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="97ec1-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="97ec1-133">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="97ec1-133">Request syntax</span></span>

| <span data-ttu-id="97ec1-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="97ec1-134">Method</span></span>    | <span data-ttu-id="97ec1-135">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="97ec1-135">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="97ec1-136">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="97ec1-136">**PATCH**</span></span> | <span data-ttu-id="97ec1-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="97ec1-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="97ec1-138">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="97ec1-138">URI parameter</span></span>

<span data-ttu-id="97ec1-139">Pomocí následujících parametrů dotazu zadejte ID zákazníka a ID uživatele.</span><span class="sxs-lookup"><span data-stu-id="97ec1-139">Use the following query parameters to specify the customer id and user id.</span></span>

| <span data-ttu-id="97ec1-140">Název</span><span class="sxs-lookup"><span data-stu-id="97ec1-140">Name</span></span>                   | <span data-ttu-id="97ec1-141">Typ</span><span class="sxs-lookup"><span data-stu-id="97ec1-141">Type</span></span>     | <span data-ttu-id="97ec1-142">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="97ec1-142">Required</span></span> | <span data-ttu-id="97ec1-143">Popis</span><span class="sxs-lookup"><span data-stu-id="97ec1-143">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="97ec1-144">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="97ec1-144">**customer-tenant-id**</span></span> | <span data-ttu-id="97ec1-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="97ec1-145">**guid**</span></span> | <span data-ttu-id="97ec1-146">Y</span><span class="sxs-lookup"><span data-stu-id="97ec1-146">Y</span></span>        | <span data-ttu-id="97ec1-147">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky na daného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="97ec1-147">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="97ec1-148">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="97ec1-148">**user-id**</span></span>            | <span data-ttu-id="97ec1-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="97ec1-149">**guid**</span></span> | <span data-ttu-id="97ec1-150">Y</span><span class="sxs-lookup"><span data-stu-id="97ec1-150">Y</span></span>        | <span data-ttu-id="97ec1-151">Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="97ec1-151">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="97ec1-152">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="97ec1-152">Request headers</span></span>

<span data-ttu-id="97ec1-153">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="97ec1-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="97ec1-154">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="97ec1-154">Request body</span></span>

<span data-ttu-id="97ec1-155">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="97ec1-155">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="97ec1-156">Název</span><span class="sxs-lookup"><span data-stu-id="97ec1-156">Name</span></span>       | <span data-ttu-id="97ec1-157">Typ</span><span class="sxs-lookup"><span data-stu-id="97ec1-157">Type</span></span>   | <span data-ttu-id="97ec1-158">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="97ec1-158">Required</span></span> | <span data-ttu-id="97ec1-159">Popis</span><span class="sxs-lookup"><span data-stu-id="97ec1-159">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="97ec1-160">State</span><span class="sxs-lookup"><span data-stu-id="97ec1-160">State</span></span>      | <span data-ttu-id="97ec1-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="97ec1-161">string</span></span> | <span data-ttu-id="97ec1-162">Y</span><span class="sxs-lookup"><span data-stu-id="97ec1-162">Y</span></span>        | <span data-ttu-id="97ec1-163">Stav uživatele</span><span class="sxs-lookup"><span data-stu-id="97ec1-163">The user state.</span></span> <span data-ttu-id="97ec1-164">Chcete-li obnovit odstraněného uživatele, musí tento řetězec obsahovat "aktivní".</span><span class="sxs-lookup"><span data-stu-id="97ec1-164">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="97ec1-165">Atributy</span><span class="sxs-lookup"><span data-stu-id="97ec1-165">Attributes</span></span> | <span data-ttu-id="97ec1-166">object</span><span class="sxs-lookup"><span data-stu-id="97ec1-166">object</span></span> | <span data-ttu-id="97ec1-167">N</span><span class="sxs-lookup"><span data-stu-id="97ec1-167">N</span></span>        | <span data-ttu-id="97ec1-168">Obsahuje "ObjectType": "CustomerUser".</span><span class="sxs-lookup"><span data-stu-id="97ec1-168">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="97ec1-169">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="97ec1-169">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="97ec1-170">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="97ec1-170">REST response</span></span>

<span data-ttu-id="97ec1-171">V případě úspěchu vrátí odpověď obnovené informace o uživateli v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="97ec1-171">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="97ec1-172">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="97ec1-172">Response success and error codes</span></span>

<span data-ttu-id="97ec1-173">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="97ec1-173">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="97ec1-174">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="97ec1-174">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="97ec1-175">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="97ec1-175">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="97ec1-176">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="97ec1-176">Response example</span></span>

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
