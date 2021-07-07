---
title: Získání uživatelských rolí pro zákazníka
description: Získá seznam všech rolí/oprávnění připojených k uživatelskému účtu. Mezi varianty patří získání seznamu všech oprávnění pro zákazníka a získání seznamu uživatelů, kteří mají danou roli.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f58e8b7eae5bb47265bb1ac83fcdcd160f735d2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445914"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="b7647-104">Získání uživatelských rolí pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="b7647-104">Get user roles for a customer</span></span>

<span data-ttu-id="b7647-105">Získá seznam všech rolí/oprávnění připojených k uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="b7647-105">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="b7647-106">Mezi varianty patří získání seznamu všech oprávnění pro zákazníka a získání seznamu uživatelů, kteří mají danou roli.</span><span class="sxs-lookup"><span data-stu-id="b7647-106">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7647-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b7647-107">Prerequisites</span></span>

- <span data-ttu-id="b7647-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b7647-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b7647-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="b7647-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b7647-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b7647-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b7647-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b7647-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b7647-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b7647-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b7647-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b7647-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b7647-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b7647-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b7647-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b7647-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b7647-116">C\#</span><span class="sxs-lookup"><span data-stu-id="b7647-116">C\#</span></span>

<span data-ttu-id="b7647-117">Pokud chcete načíst všechny role adresáře pro určitého zákazníka, napřed si načtěte zadané ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b7647-117">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="b7647-118">Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="b7647-118">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="b7647-119">Poté zavolejte vlastnost **DirectoryRoles** , za kterou následuje metoda **Get ()** nebo **GetAsync ()**.</span><span class="sxs-lookup"><span data-stu-id="b7647-119">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="b7647-120">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b7647-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b7647-121">**Project**: **třída** microsoft Partner SDK samples: GetCustomerDirectoryRoles. cs</span><span class="sxs-lookup"><span data-stu-id="b7647-121">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="b7647-122">Pokud chcete načíst seznam zákaznických uživatelů, kteří mají danou roli, nejdřív načtěte zadané ID zákazníka a ID role adresáře.</span><span class="sxs-lookup"><span data-stu-id="b7647-122">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="b7647-123">Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="b7647-123">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="b7647-124">Pak zavolejte vlastnost **DirectoryRoles** , potom metodu **ById ()** , pak vlastnost **UserMembers** , za kterou následuje metoda **Get ()** nebo **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="b7647-124">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="b7647-125">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b7647-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b7647-126">**Project**: PartnerSDK. FeatureSamples **třída**: GetCustomerDirectoryRoleUserMembers. cs</span><span class="sxs-lookup"><span data-stu-id="b7647-126">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b7647-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b7647-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b7647-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b7647-128">Request syntax</span></span>

| <span data-ttu-id="b7647-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="b7647-129">Method</span></span>  | <span data-ttu-id="b7647-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b7647-130">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b7647-131">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b7647-131">**GET**</span></span> | <span data-ttu-id="b7647-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b7647-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="b7647-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b7647-133">**GET**</span></span> | <span data-ttu-id="b7647-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b7647-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="b7647-135">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="b7647-135">**GET**</span></span> | <span data-ttu-id="b7647-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers</span><span class="sxs-lookup"><span data-stu-id="b7647-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="b7647-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="b7647-137">URI parameter</span></span>

<span data-ttu-id="b7647-138">K identifikaci správného zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="b7647-138">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="b7647-139">Název</span><span class="sxs-lookup"><span data-stu-id="b7647-139">Name</span></span>                   | <span data-ttu-id="b7647-140">Typ</span><span class="sxs-lookup"><span data-stu-id="b7647-140">Type</span></span>     | <span data-ttu-id="b7647-141">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b7647-141">Required</span></span> | <span data-ttu-id="b7647-142">Popis</span><span class="sxs-lookup"><span data-stu-id="b7647-142">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b7647-143">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="b7647-143">**customer-tenant-id**</span></span> | <span data-ttu-id="b7647-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="b7647-144">**guid**</span></span> | <span data-ttu-id="b7647-145">Y</span><span class="sxs-lookup"><span data-stu-id="b7647-145">Y</span></span>        | <span data-ttu-id="b7647-146">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="b7647-146">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="b7647-147">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="b7647-147">**user-id**</span></span>            | <span data-ttu-id="b7647-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="b7647-148">**guid**</span></span> | <span data-ttu-id="b7647-149">N</span><span class="sxs-lookup"><span data-stu-id="b7647-149">N</span></span>        | <span data-ttu-id="b7647-150">Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="b7647-150">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="b7647-151">**ID role**</span><span class="sxs-lookup"><span data-stu-id="b7647-151">**role-id**</span></span>            | <span data-ttu-id="b7647-152">**guid**</span><span class="sxs-lookup"><span data-stu-id="b7647-152">**guid**</span></span> | <span data-ttu-id="b7647-153">N</span><span class="sxs-lookup"><span data-stu-id="b7647-153">N</span></span>        | <span data-ttu-id="b7647-154">Hodnota je **ID formátované role** identifikátoru GUID, která patří do typu role.</span><span class="sxs-lookup"><span data-stu-id="b7647-154">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="b7647-155">Tato ID můžete získat dotazem na všechny role adresáře pro zákazníka v rámci všech uživatelských účtů.</span><span class="sxs-lookup"><span data-stu-id="b7647-155">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="b7647-156">(Druhý scénář výše).</span><span class="sxs-lookup"><span data-stu-id="b7647-156">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b7647-157">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b7647-157">Request headers</span></span>

<span data-ttu-id="b7647-158">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b7647-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b7647-159">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b7647-159">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="b7647-160">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b7647-160">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="b7647-161">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b7647-161">REST response</span></span>

<span data-ttu-id="b7647-162">V případě úspěchu tato metoda vrátí seznam rolí přidružených k danému uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="b7647-162">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b7647-163">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b7647-163">Response success and error codes</span></span>

<span data-ttu-id="b7647-164">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b7647-164">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b7647-165">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b7647-165">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b7647-166">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b7647-166">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b7647-167">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b7647-167">Response example</span></span>

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
