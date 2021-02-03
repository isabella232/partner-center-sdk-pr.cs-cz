---
title: Zobrazení odstraněných uživatelů pro zákazníka
description: Načte seznam odstraněných prostředků CustomerUser pro zákazníka podle ID zákazníka. Volitelně můžete nastavit velikost stránky. Je nutné, abyste zadali filtr.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766929"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="b4411-105">Zobrazení odstraněných uživatelů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="b4411-105">View deleted users for a customer</span></span>

<span data-ttu-id="b4411-106">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="b4411-106">**Applies To**</span></span>

- <span data-ttu-id="b4411-107">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b4411-107">Partner Center</span></span>

<span data-ttu-id="b4411-108">Načte seznam odstraněných prostředků CustomerUser pro zákazníka podle ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b4411-108">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="b4411-109">Volitelně můžete nastavit velikost stránky.</span><span class="sxs-lookup"><span data-stu-id="b4411-109">You can optionally set a page size.</span></span> <span data-ttu-id="b4411-110">Je nutné, abyste zadali filtr.</span><span class="sxs-lookup"><span data-stu-id="b4411-110">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4411-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b4411-111">Prerequisites</span></span>

- <span data-ttu-id="b4411-112">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b4411-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b4411-113">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b4411-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b4411-114">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b4411-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b4411-115">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b4411-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b4411-116">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b4411-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b4411-117">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b4411-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b4411-118">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b4411-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b4411-119">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b4411-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="b4411-120">Co se stane, když odstraníte uživatelský účet?</span><span class="sxs-lookup"><span data-stu-id="b4411-120">What happens when you delete a user account?</span></span>

<span data-ttu-id="b4411-121">Stav uživatele je nastaven na "neaktivní" při odstranění uživatelského účtu.</span><span class="sxs-lookup"><span data-stu-id="b4411-121">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="b4411-122">Zůstane to po dobu třiceti dnů, po jejímž uplynutí se uživatelský účet a jeho přidružená data vyprázdní a provedou neobnovitelné.</span><span class="sxs-lookup"><span data-stu-id="b4411-122">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="b4411-123">Pokud chcete obnovit odstraněný uživatelský účet v rámci třiceti dnů, přečtěte si téma [Obnovení odstraněného uživatele pro zákazníka](restore-a-user-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="b4411-123">If you want to restore a deleted user account within the thirty day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="b4411-124">Po odstranění a označení "neaktivní" již uživatelský účet nebude vrácen jako člen kolekce uživatelů (například pomocí příkazu [získat seznam všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="b4411-124">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="b4411-125">Chcete-li získat seznam odstraněných uživatelů, které ještě nebyly smazány, je nutné zadat dotaz na uživatelské účty, které byly nastaveny na neaktivní.</span><span class="sxs-lookup"><span data-stu-id="b4411-125">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="b4411-126">C\#</span><span class="sxs-lookup"><span data-stu-id="b4411-126">C\#</span></span>

<span data-ttu-id="b4411-127">Chcete-li načíst seznam odstraněných uživatelů, vytvořte dotaz, který filtruje uživatele zákazníka, jejichž stav je nastaven na neaktivní.</span><span class="sxs-lookup"><span data-stu-id="b4411-127">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="b4411-128">Nejprve vytvořte filtr vytvořením instance objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) s parametry, jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="b4411-128">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="b4411-129">Pak vytvořte dotaz pomocí metody [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) .</span><span class="sxs-lookup"><span data-stu-id="b4411-129">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="b4411-130">Pokud nechcete stránkované výsledky, můžete místo toho použít metodu [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) .</span><span class="sxs-lookup"><span data-stu-id="b4411-130">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="b4411-131">V dalším kroku použijte k identifikaci zákazníka metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b4411-131">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="b4411-132">Nakonec zavolejte metodu [**dotazu**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) pro odeslání žádosti.</span><span class="sxs-lookup"><span data-stu-id="b4411-132">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

<span data-ttu-id="b4411-133">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4411-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b4411-134">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetCustomerInactiveUsers.cs</span><span class="sxs-lookup"><span data-stu-id="b4411-134">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b4411-135">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b4411-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b4411-136">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b4411-136">Request syntax</span></span>

| <span data-ttu-id="b4411-137">Metoda</span><span class="sxs-lookup"><span data-stu-id="b4411-137">Method</span></span>  | <span data-ttu-id="b4411-138">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b4411-138">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b4411-139">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b4411-139">**GET**</span></span> | <span data-ttu-id="b4411-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? size = {size} &Filter = {Filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b4411-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b4411-141">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b4411-141">URI parameter</span></span>

<span data-ttu-id="b4411-142">Při vytváření žádosti použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="b4411-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="b4411-143">Název</span><span class="sxs-lookup"><span data-stu-id="b4411-143">Name</span></span>        | <span data-ttu-id="b4411-144">Typ</span><span class="sxs-lookup"><span data-stu-id="b4411-144">Type</span></span>   | <span data-ttu-id="b4411-145">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b4411-145">Required</span></span> | <span data-ttu-id="b4411-146">Popis</span><span class="sxs-lookup"><span data-stu-id="b4411-146">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b4411-147">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="b4411-147">customer-id</span></span> | <span data-ttu-id="b4411-148">guid</span><span class="sxs-lookup"><span data-stu-id="b4411-148">guid</span></span>   | <span data-ttu-id="b4411-149">Yes</span><span class="sxs-lookup"><span data-stu-id="b4411-149">Yes</span></span>      | <span data-ttu-id="b4411-150">Hodnota je identifikátor zákazníka, který je ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b4411-150">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="b4411-151">size</span><span class="sxs-lookup"><span data-stu-id="b4411-151">size</span></span>        | <span data-ttu-id="b4411-152">int</span><span class="sxs-lookup"><span data-stu-id="b4411-152">int</span></span>    | <span data-ttu-id="b4411-153">No</span><span class="sxs-lookup"><span data-stu-id="b4411-153">No</span></span>       | <span data-ttu-id="b4411-154">Počet výsledků, které se mají zobrazit v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="b4411-154">The number of results to be displayed at one time.</span></span> <span data-ttu-id="b4411-155">Tento parametr je volitelný.</span><span class="sxs-lookup"><span data-stu-id="b4411-155">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="b4411-156">filter</span><span class="sxs-lookup"><span data-stu-id="b4411-156">filter</span></span>      | <span data-ttu-id="b4411-157">filter</span><span class="sxs-lookup"><span data-stu-id="b4411-157">filter</span></span> | <span data-ttu-id="b4411-158">Yes</span><span class="sxs-lookup"><span data-stu-id="b4411-158">Yes</span></span>      | <span data-ttu-id="b4411-159">Dotaz, který filtruje hledání uživatelů</span><span class="sxs-lookup"><span data-stu-id="b4411-159">The query that filters the user search.</span></span> <span data-ttu-id="b4411-160">Chcete-li načíst odstraněné uživatele, je nutné zahrnout a zakódovat následující řetězec: {"Field": "UserState", "value": "neaktivní", "operator": "Equals"}.</span><span class="sxs-lookup"><span data-stu-id="b4411-160">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b4411-161">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b4411-161">Request headers</span></span>

<span data-ttu-id="b4411-162">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b4411-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b4411-163">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b4411-163">Request body</span></span>

<span data-ttu-id="b4411-164">Žádné</span><span class="sxs-lookup"><span data-stu-id="b4411-164">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b4411-165">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b4411-165">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="b4411-166">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b4411-166">REST response</span></span>

<span data-ttu-id="b4411-167">V případě úspěchu tato metoda vrátí kolekci prostředků [CustomerUser](user-resources.md#customeruser) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b4411-167">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b4411-168">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b4411-168">Response success and error codes</span></span>

<span data-ttu-id="b4411-169">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b4411-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b4411-170">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b4411-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b4411-171">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b4411-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b4411-172">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b4411-172">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
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
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
