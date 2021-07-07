---
title: Nastavení uživatelských rolí pro zákazníka
description: V rámci účtu zákazníka je k dispozici sada rolí adresáře. K těmto rolím můžete přiřadit uživatelské účty.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a035d711ffa91200fa7b479ed5ec53929aa4feaf
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446696"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="b22d7-104">Nastavení uživatelských rolí pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="b22d7-104">Set user roles for a customer</span></span>

<span data-ttu-id="b22d7-105">V rámci účtu zákazníka je k dispozici sada rolí adresáře.</span><span class="sxs-lookup"><span data-stu-id="b22d7-105">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="b22d7-106">K těmto rolím můžete přiřadit uživatelské účty.</span><span class="sxs-lookup"><span data-stu-id="b22d7-106">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b22d7-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b22d7-107">Prerequisites</span></span>

- <span data-ttu-id="b22d7-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b22d7-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b22d7-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b22d7-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b22d7-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b22d7-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b22d7-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b22d7-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b22d7-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b22d7-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b22d7-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b22d7-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b22d7-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b22d7-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b22d7-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b22d7-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b22d7-116">C\#</span><span class="sxs-lookup"><span data-stu-id="b22d7-116">C\#</span></span>

<span data-ttu-id="b22d7-117">K přiřazení role adresáře uživateli zákazníka vytvořte novou [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) s příslušnými podrobnostmi o uživateli.</span><span class="sxs-lookup"><span data-stu-id="b22d7-117">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="b22d7-118">Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) se zadaným ID zákazníka k identifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b22d7-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="b22d7-119">Odtud k určení role použijte metodu [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) s ID role adresáře.</span><span class="sxs-lookup"><span data-stu-id="b22d7-119">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="b22d7-120">Pak přejděte ke kolekci **UserMembers** a pomocí metody [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) přidejte nového uživatelského člena do kolekce uživatelských členů přiřazených k této roli.</span><span class="sxs-lookup"><span data-stu-id="b22d7-120">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

<span data-ttu-id="b22d7-121">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b22d7-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b22d7-122">**Project**: **třída** microsoft Partner SDK samples: AddUserMemberToDirectoryRole. cs</span><span class="sxs-lookup"><span data-stu-id="b22d7-122">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b22d7-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b22d7-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b22d7-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b22d7-124">Request syntax</span></span>

| <span data-ttu-id="b22d7-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="b22d7-125">Method</span></span>   | <span data-ttu-id="b22d7-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b22d7-126">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b22d7-127">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="b22d7-127">**POST**</span></span> | <span data-ttu-id="b22d7-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b22d7-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b22d7-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b22d7-129">URI parameter</span></span>

<span data-ttu-id="b22d7-130">K identifikaci správného zákazníka a role použijte následující parametry identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="b22d7-130">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="b22d7-131">Chcete-li identifikovat uživatele, kterému chcete přiřadit roli, zadejte identifikační informace v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="b22d7-131">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="b22d7-132">Název</span><span class="sxs-lookup"><span data-stu-id="b22d7-132">Name</span></span>                   | <span data-ttu-id="b22d7-133">Typ</span><span class="sxs-lookup"><span data-stu-id="b22d7-133">Type</span></span>     | <span data-ttu-id="b22d7-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b22d7-134">Required</span></span> | <span data-ttu-id="b22d7-135">Popis</span><span class="sxs-lookup"><span data-stu-id="b22d7-135">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b22d7-136">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="b22d7-136">**customer-tenant-id**</span></span> | <span data-ttu-id="b22d7-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="b22d7-137">**guid**</span></span> | <span data-ttu-id="b22d7-138">Y</span><span class="sxs-lookup"><span data-stu-id="b22d7-138">Y</span></span>        | <span data-ttu-id="b22d7-139">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="b22d7-139">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="b22d7-140">**ID role**</span><span class="sxs-lookup"><span data-stu-id="b22d7-140">**role-id**</span></span>            | <span data-ttu-id="b22d7-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="b22d7-141">**guid**</span></span> | <span data-ttu-id="b22d7-142">Y</span><span class="sxs-lookup"><span data-stu-id="b22d7-142">Y</span></span>        | <span data-ttu-id="b22d7-143">Hodnota je identifikátor GUID s formátovaným **ID** , který identifikuje roli, která se přiřadí uživateli.</span><span class="sxs-lookup"><span data-stu-id="b22d7-143">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="b22d7-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b22d7-144">Request headers</span></span>

<span data-ttu-id="b22d7-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b22d7-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b22d7-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b22d7-146">Request body</span></span>

<span data-ttu-id="b22d7-147">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="b22d7-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="b22d7-148">Název</span><span class="sxs-lookup"><span data-stu-id="b22d7-148">Name</span></span>                  | <span data-ttu-id="b22d7-149">Typ</span><span class="sxs-lookup"><span data-stu-id="b22d7-149">Type</span></span>       | <span data-ttu-id="b22d7-150">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b22d7-150">Required</span></span> | <span data-ttu-id="b22d7-151">Popis</span><span class="sxs-lookup"><span data-stu-id="b22d7-151">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="b22d7-152">**Účet**</span><span class="sxs-lookup"><span data-stu-id="b22d7-152">**Id**</span></span>                | <span data-ttu-id="b22d7-153">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="b22d7-153">**string**</span></span> | <span data-ttu-id="b22d7-154">Y</span><span class="sxs-lookup"><span data-stu-id="b22d7-154">Y</span></span>        | <span data-ttu-id="b22d7-155">ID uživatele, kterého chcete přidat do role.</span><span class="sxs-lookup"><span data-stu-id="b22d7-155">The ID of the user to add to the role.</span></span> |
| <span data-ttu-id="b22d7-156">**DisplayName**</span><span class="sxs-lookup"><span data-stu-id="b22d7-156">**DisplayName**</span></span>       | <span data-ttu-id="b22d7-157">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="b22d7-157">**string**</span></span> | <span data-ttu-id="b22d7-158">Y</span><span class="sxs-lookup"><span data-stu-id="b22d7-158">Y</span></span>        | <span data-ttu-id="b22d7-159">Popisné zobrazované jméno uživatele</span><span class="sxs-lookup"><span data-stu-id="b22d7-159">The friendly display name of the user.</span></span> |
| <span data-ttu-id="b22d7-160">**Třídy**</span><span class="sxs-lookup"><span data-stu-id="b22d7-160">**UserPrincipalName**</span></span> | <span data-ttu-id="b22d7-161">**řetězec**</span><span class="sxs-lookup"><span data-stu-id="b22d7-161">**string**</span></span> | <span data-ttu-id="b22d7-162">Y</span><span class="sxs-lookup"><span data-stu-id="b22d7-162">Y</span></span>        | <span data-ttu-id="b22d7-163">Název objektu zabezpečení uživatele.</span><span class="sxs-lookup"><span data-stu-id="b22d7-163">The name of the user principal.</span></span>        |
| <span data-ttu-id="b22d7-164">**Atributy**</span><span class="sxs-lookup"><span data-stu-id="b22d7-164">**Attributes**</span></span>        | <span data-ttu-id="b22d7-165">**předmětů**</span><span class="sxs-lookup"><span data-stu-id="b22d7-165">**object**</span></span> | <span data-ttu-id="b22d7-166">Y</span><span class="sxs-lookup"><span data-stu-id="b22d7-166">Y</span></span>        | <span data-ttu-id="b22d7-167">Obsahuje ObjectType: "UserMember"</span><span class="sxs-lookup"><span data-stu-id="b22d7-167">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="b22d7-168">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b22d7-168">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="b22d7-169">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b22d7-169">REST response</span></span>

<span data-ttu-id="b22d7-170">Tato metoda vrátí uživatelský účet s ID role připojené, když se uživateli úspěšně přiřadí role.</span><span class="sxs-lookup"><span data-stu-id="b22d7-170">This method returns the user account with the role ID attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b22d7-171">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b22d7-171">Response success and error codes</span></span>

<span data-ttu-id="b22d7-172">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b22d7-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b22d7-173">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b22d7-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b22d7-174">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b22d7-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b22d7-175">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b22d7-175">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
