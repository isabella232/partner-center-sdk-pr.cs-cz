---
title: Zobrazení odstraněných uživatelů pro zákazníka
description: Načte seznam odstraněných prostředků CustomerUser pro zákazníka podle ID zákazníka. Volitelně můžete nastavit velikost stránky. Je nutné, abyste zadali filtr.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f4fec958a9a6bb580d35de1cf3007e1db3b2b650
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445302"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="7cf52-105">Zobrazení odstraněných uživatelů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="7cf52-105">View deleted users for a customer</span></span>

<span data-ttu-id="7cf52-106">Načte seznam odstraněných prostředků CustomerUser pro zákazníka podle ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7cf52-106">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="7cf52-107">Volitelně můžete nastavit velikost stránky.</span><span class="sxs-lookup"><span data-stu-id="7cf52-107">You can optionally set a page size.</span></span> <span data-ttu-id="7cf52-108">Je nutné, abyste zadali filtr.</span><span class="sxs-lookup"><span data-stu-id="7cf52-108">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cf52-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7cf52-109">Prerequisites</span></span>

- <span data-ttu-id="7cf52-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7cf52-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7cf52-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="7cf52-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7cf52-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7cf52-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7cf52-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="7cf52-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7cf52-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="7cf52-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7cf52-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="7cf52-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7cf52-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="7cf52-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7cf52-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7cf52-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="7cf52-118">Co se stane, když odstraníte uživatelský účet?</span><span class="sxs-lookup"><span data-stu-id="7cf52-118">What happens when you delete a user account?</span></span>

<span data-ttu-id="7cf52-119">Stav uživatele je nastaven na "neaktivní" při odstranění uživatelského účtu.</span><span class="sxs-lookup"><span data-stu-id="7cf52-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="7cf52-120">Trvá to po dobu 30 dnů, po jejímž uplynutí se uživatelský účet a jeho přidružená data vyprázdní a provedou jako neobnovitelné.</span><span class="sxs-lookup"><span data-stu-id="7cf52-120">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="7cf52-121">Pokud chcete obnovit odstraněný uživatelský účet v rámci 30denního okna, přečtěte si téma [Obnovení odstraněného uživatele pro zákazníka](restore-a-user-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="7cf52-121">If you want to restore a deleted user account within the 30-day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="7cf52-122">Po odstranění a označení "neaktivní" již uživatelský účet nebude vrácen jako člen kolekce uživatelů (například pomocí příkazu [získat seznam všech uživatelských účtů pro zákazníka](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="7cf52-122">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="7cf52-123">Chcete-li získat seznam odstraněných uživatelů, které ještě nebyly smazány, je nutné zadat dotaz na uživatelské účty, které byly nastaveny na neaktivní.</span><span class="sxs-lookup"><span data-stu-id="7cf52-123">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="7cf52-124">C\#</span><span class="sxs-lookup"><span data-stu-id="7cf52-124">C\#</span></span>

<span data-ttu-id="7cf52-125">Chcete-li načíst seznam odstraněných uživatelů, vytvořte dotaz, který filtruje uživatele zákazníka, jejichž stav je nastaven na neaktivní.</span><span class="sxs-lookup"><span data-stu-id="7cf52-125">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="7cf52-126">Nejprve vytvořte filtr vytvořením instance objektu [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) s parametry, jak je znázorněno v následujícím fragmentu kódu.</span><span class="sxs-lookup"><span data-stu-id="7cf52-126">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="7cf52-127">Pak vytvořte dotaz pomocí metody [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) .</span><span class="sxs-lookup"><span data-stu-id="7cf52-127">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="7cf52-128">Pokud nechcete stránkované výsledky, můžete místo toho použít metodu [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) .</span><span class="sxs-lookup"><span data-stu-id="7cf52-128">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="7cf52-129">V dalším kroku použijte k identifikaci zákazníka metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7cf52-129">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="7cf52-130">Nakonec zavolejte metodu [**dotazu**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) pro odeslání žádosti.</span><span class="sxs-lookup"><span data-stu-id="7cf52-130">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

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

<span data-ttu-id="7cf52-131">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7cf52-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7cf52-132">**Project**: **třída** microsoft Partner SDK samples: GetCustomerInactiveUsers. cs</span><span class="sxs-lookup"><span data-stu-id="7cf52-132">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7cf52-133">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="7cf52-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7cf52-134">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="7cf52-134">Request syntax</span></span>

| <span data-ttu-id="7cf52-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="7cf52-135">Method</span></span>  | <span data-ttu-id="7cf52-136">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="7cf52-136">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7cf52-137">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="7cf52-137">**GET**</span></span> | <span data-ttu-id="7cf52-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? size = {size} &Filter = {Filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7cf52-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7cf52-139">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="7cf52-139">URI parameter</span></span>

<span data-ttu-id="7cf52-140">Při vytváření žádosti použijte následující cestu a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="7cf52-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="7cf52-141">Název</span><span class="sxs-lookup"><span data-stu-id="7cf52-141">Name</span></span>        | <span data-ttu-id="7cf52-142">Typ</span><span class="sxs-lookup"><span data-stu-id="7cf52-142">Type</span></span>   | <span data-ttu-id="7cf52-143">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="7cf52-143">Required</span></span> | <span data-ttu-id="7cf52-144">Popis</span><span class="sxs-lookup"><span data-stu-id="7cf52-144">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7cf52-145">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="7cf52-145">customer-id</span></span> | <span data-ttu-id="7cf52-146">guid</span><span class="sxs-lookup"><span data-stu-id="7cf52-146">guid</span></span>   | <span data-ttu-id="7cf52-147">Yes</span><span class="sxs-lookup"><span data-stu-id="7cf52-147">Yes</span></span>      | <span data-ttu-id="7cf52-148">Hodnota je identifikátor zákazníka, který je ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="7cf52-148">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="7cf52-149">size</span><span class="sxs-lookup"><span data-stu-id="7cf52-149">size</span></span>        | <span data-ttu-id="7cf52-150">int</span><span class="sxs-lookup"><span data-stu-id="7cf52-150">int</span></span>    | <span data-ttu-id="7cf52-151">No</span><span class="sxs-lookup"><span data-stu-id="7cf52-151">No</span></span>       | <span data-ttu-id="7cf52-152">Počet výsledků, které se mají zobrazit v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="7cf52-152">The number of results to be displayed at one time.</span></span> <span data-ttu-id="7cf52-153">Tento parametr je volitelný.</span><span class="sxs-lookup"><span data-stu-id="7cf52-153">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="7cf52-154">filter</span><span class="sxs-lookup"><span data-stu-id="7cf52-154">filter</span></span>      | <span data-ttu-id="7cf52-155">filter</span><span class="sxs-lookup"><span data-stu-id="7cf52-155">filter</span></span> | <span data-ttu-id="7cf52-156">Yes</span><span class="sxs-lookup"><span data-stu-id="7cf52-156">Yes</span></span>      | <span data-ttu-id="7cf52-157">Dotaz, který filtruje hledání uživatelů</span><span class="sxs-lookup"><span data-stu-id="7cf52-157">The query that filters the user search.</span></span> <span data-ttu-id="7cf52-158">Chcete-li načíst odstraněné uživatele, je nutné zahrnout a zakódovat následující řetězec: {"Field": "UserState", "value": "neaktivní", "operator": "Equals"}.</span><span class="sxs-lookup"><span data-stu-id="7cf52-158">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7cf52-159">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="7cf52-159">Request headers</span></span>

<span data-ttu-id="7cf52-160">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7cf52-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7cf52-161">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="7cf52-161">Request body</span></span>

<span data-ttu-id="7cf52-162">Žádné</span><span class="sxs-lookup"><span data-stu-id="7cf52-162">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7cf52-163">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="7cf52-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7cf52-164">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="7cf52-164">REST response</span></span>

<span data-ttu-id="7cf52-165">V případě úspěchu tato metoda vrátí kolekci prostředků [CustomerUser](user-resources.md#customeruser) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="7cf52-165">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7cf52-166">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="7cf52-166">Response success and error codes</span></span>

<span data-ttu-id="7cf52-167">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="7cf52-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7cf52-168">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="7cf52-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7cf52-169">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7cf52-169">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7cf52-170">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="7cf52-170">Response example</span></span>

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
