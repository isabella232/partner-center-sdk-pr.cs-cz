---
title: Nastavení uživatelských rolí pro zákazníka
description: V rámci účtu zákazníka je k dispozici sada rolí adresáře. K těmto rolím můžete přiřadit uživatelské účty.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f42120e40e54ff8bd6242634d97268091abf8e1c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766948"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="1bdc8-104">Nastavení uživatelských rolí pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="1bdc8-104">Set user roles for a customer</span></span>

<span data-ttu-id="1bdc8-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-105">**Applies To**</span></span>

- <span data-ttu-id="1bdc8-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="1bdc8-106">Partner Center</span></span>

<span data-ttu-id="1bdc8-107">V rámci účtu zákazníka je k dispozici sada rolí adresáře.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-107">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="1bdc8-108">K těmto rolím můžete přiřadit uživatelské účty.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-108">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bdc8-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1bdc8-109">Prerequisites</span></span>

- <span data-ttu-id="1bdc8-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1bdc8-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1bdc8-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1bdc8-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1bdc8-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1bdc8-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1bdc8-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1bdc8-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1bdc8-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="1bdc8-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1bdc8-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1bdc8-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1bdc8-118">C\#</span><span class="sxs-lookup"><span data-stu-id="1bdc8-118">C\#</span></span>

<span data-ttu-id="1bdc8-119">K přiřazení role adresáře uživateli zákazníka vytvořte novou [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) s příslušnými podrobnostmi o uživateli.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-119">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="1bdc8-120">Pak zavolejte metodu [**IAggregatePartner. Customer. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) se zadaným ID zákazníka k identifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-120">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="1bdc8-121">Odtud k určení role použijte metodu [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) s ID role adresáře.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-121">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="1bdc8-122">Pak přejděte ke kolekci **UserMembers** a pomocí metody [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) přidejte nového uživatelského člena do kolekce uživatelských členů přiřazených k této roli.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-122">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

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

<span data-ttu-id="1bdc8-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1bdc8-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1bdc8-124">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: AddUserMemberToDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="1bdc8-124">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1bdc8-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1bdc8-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1bdc8-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="1bdc8-126">Request syntax</span></span>

| <span data-ttu-id="1bdc8-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="1bdc8-127">Method</span></span>   | <span data-ttu-id="1bdc8-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1bdc8-128">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1bdc8-129">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-129">**POST**</span></span> | <span data-ttu-id="1bdc8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1bdc8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1bdc8-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1bdc8-131">URI parameter</span></span>

<span data-ttu-id="1bdc8-132">K identifikaci správného zákazníka a role použijte následující parametry identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-132">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="1bdc8-133">Chcete-li identifikovat uživatele, kterému chcete přiřadit roli, zadejte identifikační informace v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-133">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="1bdc8-134">Název</span><span class="sxs-lookup"><span data-stu-id="1bdc8-134">Name</span></span>                   | <span data-ttu-id="1bdc8-135">Typ</span><span class="sxs-lookup"><span data-stu-id="1bdc8-135">Type</span></span>     | <span data-ttu-id="1bdc8-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1bdc8-136">Required</span></span> | <span data-ttu-id="1bdc8-137">Popis</span><span class="sxs-lookup"><span data-stu-id="1bdc8-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1bdc8-138">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-138">**customer-tenant-id**</span></span> | <span data-ttu-id="1bdc8-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-139">**guid**</span></span> | <span data-ttu-id="1bdc8-140">Y</span><span class="sxs-lookup"><span data-stu-id="1bdc8-140">Y</span></span>        | <span data-ttu-id="1bdc8-141">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="1bdc8-142">**ID role**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-142">**role-id**</span></span>            | <span data-ttu-id="1bdc8-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-143">**guid**</span></span> | <span data-ttu-id="1bdc8-144">Y</span><span class="sxs-lookup"><span data-stu-id="1bdc8-144">Y</span></span>        | <span data-ttu-id="1bdc8-145">Hodnota je identifikátor GUID s formátovaným **ID** , který identifikuje roli, která se přiřadí uživateli.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-145">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="1bdc8-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1bdc8-146">Request headers</span></span>

<span data-ttu-id="1bdc8-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1bdc8-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1bdc8-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1bdc8-148">Request body</span></span>

<span data-ttu-id="1bdc8-149">Tato tabulka popisuje požadované vlastnosti v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-149">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="1bdc8-150">Název</span><span class="sxs-lookup"><span data-stu-id="1bdc8-150">Name</span></span>                  | <span data-ttu-id="1bdc8-151">Typ</span><span class="sxs-lookup"><span data-stu-id="1bdc8-151">Type</span></span>       | <span data-ttu-id="1bdc8-152">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1bdc8-152">Required</span></span> | <span data-ttu-id="1bdc8-153">Popis</span><span class="sxs-lookup"><span data-stu-id="1bdc8-153">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="1bdc8-154">**Účet**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-154">**Id**</span></span>                | <span data-ttu-id="1bdc8-155">**řetezce**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-155">**string**</span></span> | <span data-ttu-id="1bdc8-156">Y</span><span class="sxs-lookup"><span data-stu-id="1bdc8-156">Y</span></span>        | <span data-ttu-id="1bdc8-157">ID uživatele, kterého chcete přidat do role.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-157">The Id of the user to add to the role.</span></span> |
| <span data-ttu-id="1bdc8-158">**DisplayName**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-158">**DisplayName**</span></span>       | <span data-ttu-id="1bdc8-159">**řetezce**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-159">**string**</span></span> | <span data-ttu-id="1bdc8-160">Y</span><span class="sxs-lookup"><span data-stu-id="1bdc8-160">Y</span></span>        | <span data-ttu-id="1bdc8-161">Popisné zobrazované jméno uživatele</span><span class="sxs-lookup"><span data-stu-id="1bdc8-161">The friendly display name of the user.</span></span> |
| <span data-ttu-id="1bdc8-162">**Třídy**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-162">**UserPrincipalName**</span></span> | <span data-ttu-id="1bdc8-163">**řetezce**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-163">**string**</span></span> | <span data-ttu-id="1bdc8-164">Y</span><span class="sxs-lookup"><span data-stu-id="1bdc8-164">Y</span></span>        | <span data-ttu-id="1bdc8-165">Název objektu zabezpečení uživatele.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-165">The name of the user principal.</span></span>        |
| <span data-ttu-id="1bdc8-166">**Atributy**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-166">**Attributes**</span></span>        | <span data-ttu-id="1bdc8-167">**předmětů**</span><span class="sxs-lookup"><span data-stu-id="1bdc8-167">**object**</span></span> | <span data-ttu-id="1bdc8-168">Y</span><span class="sxs-lookup"><span data-stu-id="1bdc8-168">Y</span></span>        | <span data-ttu-id="1bdc8-169">Obsahuje ObjectType: "UserMember"</span><span class="sxs-lookup"><span data-stu-id="1bdc8-169">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="1bdc8-170">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1bdc8-170">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="1bdc8-171">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1bdc8-171">REST response</span></span>

<span data-ttu-id="1bdc8-172">Tato metoda vrátí uživatelský účet s ID role připojené, když se uživateli úspěšně přiřadí role.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-172">This method returns the user account with the role id attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1bdc8-173">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="1bdc8-173">Response success and error codes</span></span>

<span data-ttu-id="1bdc8-174">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1bdc8-175">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="1bdc8-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1bdc8-176">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1bdc8-176">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1bdc8-177">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1bdc8-177">Response example</span></span>

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
