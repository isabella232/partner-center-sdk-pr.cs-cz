---
title: Odebrání uživatele zákazníka z role
description: Jak odebrat uživatele z role adresáře v rámci účtu zákazníka
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 36dc742c4f713131b4996d7dc945b6dd008a3ef5
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445642"
---
# <a name="remove-a-customer-user-from-a-role"></a><span data-ttu-id="e6edb-103">Odebrání uživatele zákazníka z role</span><span class="sxs-lookup"><span data-stu-id="e6edb-103">Remove a customer user from a role</span></span>

<span data-ttu-id="e6edb-104">Jak odebrat uživatele z role adresáře v rámci účtu zákazníka</span><span class="sxs-lookup"><span data-stu-id="e6edb-104">How to remove a user from a directory role within a customer account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6edb-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e6edb-105">Prerequisites</span></span>

- <span data-ttu-id="e6edb-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e6edb-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e6edb-107">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="e6edb-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e6edb-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6edb-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e6edb-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="e6edb-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e6edb-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="e6edb-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e6edb-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="e6edb-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e6edb-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="e6edb-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e6edb-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e6edb-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e6edb-114">C\#</span><span class="sxs-lookup"><span data-stu-id="e6edb-114">C\#</span></span>

<span data-ttu-id="e6edb-115">Chcete-li odebrat uživatele z role adresáře, vyberte zákazníka s uživatelem, který chcete upravit pomocí volání metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) , a od této role zadejte roli pomocí metody [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) s ID role adresáře.</span><span class="sxs-lookup"><span data-stu-id="e6edb-115">To remove a user from a directory role, select the customer with the user to modify with a call to the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, From there, specify the role using the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID.</span></span> <span data-ttu-id="e6edb-116">Pak přejděte k metodě [**UserMembers. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) a Identifikujte uživatele, který chcete odebrat, a metodu [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) pro odebrání uživatele z role.</span><span class="sxs-lookup"><span data-stu-id="e6edb-116">Then, access the [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) method to identify the user to remove, and the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) method to remove the user from the role.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

<span data-ttu-id="e6edb-117">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e6edb-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e6edb-118">**Project**: **třída** microsoft Partner SDK samples: RemoveCustomerUserMemberFromDirectoryRole. cs</span><span class="sxs-lookup"><span data-stu-id="e6edb-118">**Project**: Partner Center SDK Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e6edb-119">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="e6edb-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e6edb-120">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="e6edb-120">Request syntax</span></span>

| <span data-ttu-id="e6edb-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="e6edb-121">Method</span></span>     | <span data-ttu-id="e6edb-122">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="e6edb-122">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e6edb-123">**DSTRANIT**</span><span class="sxs-lookup"><span data-stu-id="e6edb-123">**DELETE**</span></span> | <span data-ttu-id="e6edb-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers/{User-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e6edb-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e6edb-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e6edb-125">URI parameter</span></span>

<span data-ttu-id="e6edb-126">K identifikaci správného zákazníka, role a uživatele použijte následující parametry identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="e6edb-126">Use the following URI parameters to identify the correct customer, role, and user.</span></span>

| <span data-ttu-id="e6edb-127">Název</span><span class="sxs-lookup"><span data-stu-id="e6edb-127">Name</span></span>                   | <span data-ttu-id="e6edb-128">Typ</span><span class="sxs-lookup"><span data-stu-id="e6edb-128">Type</span></span>     | <span data-ttu-id="e6edb-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e6edb-129">Required</span></span> | <span data-ttu-id="e6edb-130">Popis</span><span class="sxs-lookup"><span data-stu-id="e6edb-130">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="e6edb-131">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="e6edb-131">**customer-tenant-id**</span></span> | <span data-ttu-id="e6edb-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="e6edb-132">**guid**</span></span> | <span data-ttu-id="e6edb-133">Y</span><span class="sxs-lookup"><span data-stu-id="e6edb-133">Y</span></span>        | <span data-ttu-id="e6edb-134">Hodnota je identifikátor **zákazníka (zákazníka** ), který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="e6edb-134">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="e6edb-135">**ID role**</span><span class="sxs-lookup"><span data-stu-id="e6edb-135">**role-id**</span></span>            | <span data-ttu-id="e6edb-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="e6edb-136">**guid**</span></span> | <span data-ttu-id="e6edb-137">Y</span><span class="sxs-lookup"><span data-stu-id="e6edb-137">Y</span></span>        | <span data-ttu-id="e6edb-138">Hodnota je identifikátor GUID s formátovaným **ID** , který identifikuje roli.</span><span class="sxs-lookup"><span data-stu-id="e6edb-138">The value is a GUID formatted **role-id** that identifies the role.</span></span>                |
| <span data-ttu-id="e6edb-139">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="e6edb-139">**user-id**</span></span>            | <span data-ttu-id="e6edb-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="e6edb-140">**guid**</span></span> | <span data-ttu-id="e6edb-141">Y</span><span class="sxs-lookup"><span data-stu-id="e6edb-141">Y</span></span>        | <span data-ttu-id="e6edb-142">Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který identifikuje jeden uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="e6edb-142">The value is a GUID formatted **user-id** that identifies a single user account.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="e6edb-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="e6edb-143">Request headers</span></span>

<span data-ttu-id="e6edb-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e6edb-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e6edb-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="e6edb-145">Request body</span></span>

<span data-ttu-id="e6edb-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="e6edb-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e6edb-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="e6edb-147">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e6edb-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="e6edb-148">REST response</span></span>

<span data-ttu-id="e6edb-149">Pokud se uživatel z role úspěšně odebere, tělo odpovědi je prázdné.</span><span class="sxs-lookup"><span data-stu-id="e6edb-149">If the user is removed from the role successfully, the response body is empty.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e6edb-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e6edb-150">Response success and error codes</span></span>

<span data-ttu-id="e6edb-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="e6edb-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e6edb-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="e6edb-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e6edb-153">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e6edb-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e6edb-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e6edb-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
