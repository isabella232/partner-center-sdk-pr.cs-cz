---
title: Získání uživatelských rolí pro zákazníka
description: Získá seznam všech rolí/oprávnění připojených k uživatelskému účtu. Mezi varianty patří získání seznamu všech oprávnění pro zákazníka a získání seznamu uživatelů, kteří mají danou roli.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766720"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="8174a-104">Získání uživatelských rolí pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="8174a-104">Get user roles for a customer</span></span>

<span data-ttu-id="8174a-105">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="8174a-105">**Applies To**</span></span>

- <span data-ttu-id="8174a-106">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="8174a-106">Partner Center</span></span>

<span data-ttu-id="8174a-107">Získá seznam všech rolí/oprávnění připojených k uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="8174a-107">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="8174a-108">Mezi varianty patří získání seznamu všech oprávnění pro zákazníka a získání seznamu uživatelů, kteří mají danou roli.</span><span class="sxs-lookup"><span data-stu-id="8174a-108">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8174a-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8174a-109">Prerequisites</span></span>

- <span data-ttu-id="8174a-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8174a-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8174a-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="8174a-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="8174a-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8174a-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8174a-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="8174a-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8174a-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="8174a-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8174a-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="8174a-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8174a-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="8174a-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8174a-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8174a-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="8174a-118">C\#</span><span class="sxs-lookup"><span data-stu-id="8174a-118">C\#</span></span>

<span data-ttu-id="8174a-119">Pokud chcete načíst všechny role adresáře pro určitého zákazníka, napřed si načtěte zadané ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="8174a-119">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="8174a-120">Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="8174a-120">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="8174a-121">Poté zavolejte vlastnost **DirectoryRoles** , za kterou následuje metoda **Get ()** nebo **GetAsync ()**.</span><span class="sxs-lookup"><span data-stu-id="8174a-121">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="8174a-122">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8174a-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8174a-123">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetCustomerDirectoryRoles.cs</span><span class="sxs-lookup"><span data-stu-id="8174a-123">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="8174a-124">Pokud chcete načíst seznam zákaznických uživatelů, kteří mají danou roli, nejdřív načtěte zadané ID zákazníka a ID role adresáře.</span><span class="sxs-lookup"><span data-stu-id="8174a-124">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="8174a-125">Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="8174a-125">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="8174a-126">Pak zavolejte vlastnost **DirectoryRoles** , potom metodu **ById ()** , pak vlastnost **UserMembers** , za kterou následuje metoda **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="8174a-126">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="8174a-127">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8174a-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8174a-128">**Projekt**: PartnerSDK. FeatureSamples **Třída**: GetCustomerDirectoryRoleUserMembers.cs</span><span class="sxs-lookup"><span data-stu-id="8174a-128">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8174a-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="8174a-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8174a-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="8174a-130">Request syntax</span></span>

| <span data-ttu-id="8174a-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="8174a-131">Method</span></span>  | <span data-ttu-id="8174a-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="8174a-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8174a-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="8174a-133">**GET**</span></span> | <span data-ttu-id="8174a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8174a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="8174a-135">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="8174a-135">**GET**</span></span> | <span data-ttu-id="8174a-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8174a-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="8174a-137">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="8174a-137">**GET**</span></span> | <span data-ttu-id="8174a-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers</span><span class="sxs-lookup"><span data-stu-id="8174a-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="8174a-139">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8174a-139">URI parameter</span></span>

<span data-ttu-id="8174a-140">K identifikaci správného zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="8174a-140">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="8174a-141">Název</span><span class="sxs-lookup"><span data-stu-id="8174a-141">Name</span></span>                   | <span data-ttu-id="8174a-142">Typ</span><span class="sxs-lookup"><span data-stu-id="8174a-142">Type</span></span>     | <span data-ttu-id="8174a-143">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="8174a-143">Required</span></span> | <span data-ttu-id="8174a-144">Popis</span><span class="sxs-lookup"><span data-stu-id="8174a-144">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8174a-145">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="8174a-145">**customer-tenant-id**</span></span> | <span data-ttu-id="8174a-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="8174a-146">**guid**</span></span> | <span data-ttu-id="8174a-147">Y</span><span class="sxs-lookup"><span data-stu-id="8174a-147">Y</span></span>        | <span data-ttu-id="8174a-148">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="8174a-148">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="8174a-149">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="8174a-149">**user-id**</span></span>            | <span data-ttu-id="8174a-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="8174a-150">**guid**</span></span> | <span data-ttu-id="8174a-151">N</span><span class="sxs-lookup"><span data-stu-id="8174a-151">N</span></span>        | <span data-ttu-id="8174a-152">Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="8174a-152">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="8174a-153">**ID role**</span><span class="sxs-lookup"><span data-stu-id="8174a-153">**role-id**</span></span>            | <span data-ttu-id="8174a-154">**guid**</span><span class="sxs-lookup"><span data-stu-id="8174a-154">**guid**</span></span> | <span data-ttu-id="8174a-155">N</span><span class="sxs-lookup"><span data-stu-id="8174a-155">N</span></span>        | <span data-ttu-id="8174a-156">Hodnota je **ID formátované role** identifikátoru GUID, která patří do typu role.</span><span class="sxs-lookup"><span data-stu-id="8174a-156">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="8174a-157">Tato ID můžete získat dotazem na všechny role adresáře pro zákazníka v rámci všech uživatelských účtů.</span><span class="sxs-lookup"><span data-stu-id="8174a-157">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="8174a-158">(Druhý scénář výše).</span><span class="sxs-lookup"><span data-stu-id="8174a-158">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8174a-159">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="8174a-159">Request headers</span></span>

<span data-ttu-id="8174a-160">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8174a-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8174a-161">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="8174a-161">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="8174a-162">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="8174a-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="8174a-163">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="8174a-163">REST response</span></span>

<span data-ttu-id="8174a-164">V případě úspěchu tato metoda vrátí seznam rolí přidružených k danému uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="8174a-164">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8174a-165">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="8174a-165">Response success and error codes</span></span>

<span data-ttu-id="8174a-166">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="8174a-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8174a-167">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="8174a-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8174a-168">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8174a-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8174a-169">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="8174a-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
