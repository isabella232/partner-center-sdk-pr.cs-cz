---
title: Resetování uživatelského hesla pro zákazníka
description: Resetování hesla je velmi podobné jako aktualizace dalších podrobností v existujícím uživatelském účtu pro zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e0df93c2db55ec0fe49fc0e3089b7e11928f32bb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766709"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="827bf-103">Resetování uživatelského hesla pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="827bf-103">Reset user password for a customer</span></span>

<span data-ttu-id="827bf-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="827bf-104">**Applies To**</span></span>

- <span data-ttu-id="827bf-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="827bf-105">Partner Center</span></span>

<span data-ttu-id="827bf-106">Resetování hesla je velmi podobné jako aktualizace dalších podrobností v existujícím uživatelském účtu pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="827bf-106">Resetting a password is very similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="827bf-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="827bf-107">Prerequisites</span></span>

- <span data-ttu-id="827bf-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="827bf-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="827bf-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="827bf-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="827bf-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="827bf-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="827bf-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="827bf-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="827bf-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="827bf-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="827bf-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="827bf-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="827bf-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="827bf-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="827bf-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="827bf-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="827bf-116">C\#</span><span class="sxs-lookup"><span data-stu-id="827bf-116">C\#</span></span>

<span data-ttu-id="827bf-117">Pokud chcete resetovat heslo pro zadaného uživatele zákazníka, napřed si načtěte zadané ID zákazníka a cílového uživatele.</span><span class="sxs-lookup"><span data-stu-id="827bf-117">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="827bf-118">Pak vytvořte nový objekt **CustomerUser** , který obsahuje informace pro existujícího zákazníka, ale s novým objektem **PasswordProfile** .</span><span class="sxs-lookup"><span data-stu-id="827bf-118">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="827bf-119">Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="827bf-119">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="827bf-120">Pak zavolejte vlastnost **Users** , metodu **ById ()** a poté metodu **patch** .</span><span class="sxs-lookup"><span data-stu-id="827bf-120">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// CustomerUser specifiedUser;

var selectedCustomer = partnerOperations.Customers.ById(selectedCustomerId).Get();
var userToUpdate = new CustomerUser()
   {
      PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "newPassword" },
      DisplayName = "Roger Federer",
      FirstName = "Roger",
      LastName = "Federer",
      UsageLocation = "US",
      UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
   };

// update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="827bf-121">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="827bf-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="827bf-122">**Projekt**: PartnerSDK. FeatureSamples **Třída**: CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="827bf-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="827bf-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="827bf-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="827bf-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="827bf-124">Request syntax</span></span>

| <span data-ttu-id="827bf-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="827bf-125">Method</span></span>    | <span data-ttu-id="827bf-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="827bf-126">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="827bf-127">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="827bf-127">**PATCH**</span></span> | <span data-ttu-id="827bf-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="827bf-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="827bf-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="827bf-129">URI parameter</span></span>

<span data-ttu-id="827bf-130">K identifikaci správného zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="827bf-130">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="827bf-131">Název</span><span class="sxs-lookup"><span data-stu-id="827bf-131">Name</span></span>                   | <span data-ttu-id="827bf-132">Typ</span><span class="sxs-lookup"><span data-stu-id="827bf-132">Type</span></span>     | <span data-ttu-id="827bf-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="827bf-133">Required</span></span> | <span data-ttu-id="827bf-134">Popis</span><span class="sxs-lookup"><span data-stu-id="827bf-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="827bf-135">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="827bf-135">**customer-tenant-id**</span></span> | <span data-ttu-id="827bf-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="827bf-136">**guid**</span></span> | <span data-ttu-id="827bf-137">Y</span><span class="sxs-lookup"><span data-stu-id="827bf-137">Y</span></span>        | <span data-ttu-id="827bf-138">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="827bf-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="827bf-139">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="827bf-139">**user-id**</span></span>            | <span data-ttu-id="827bf-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="827bf-140">**guid**</span></span> | <span data-ttu-id="827bf-141">Y</span><span class="sxs-lookup"><span data-stu-id="827bf-141">Y</span></span>        | <span data-ttu-id="827bf-142">Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="827bf-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="827bf-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="827bf-143">Request headers</span></span>

<span data-ttu-id="827bf-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="827bf-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="827bf-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="827bf-145">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="827bf-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="827bf-146">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
     "passwordProfile":{
        password: "Renew456*",
        forceChangePassword: true
      },

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="827bf-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="827bf-147">REST response</span></span>

<span data-ttu-id="827bf-148">V případě úspěchu vrátí tato metoda informace o uživateli společně s aktualizovanými informacemi o hesle.</span><span class="sxs-lookup"><span data-stu-id="827bf-148">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="827bf-149">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="827bf-149">Response success and error codes</span></span>

<span data-ttu-id="827bf-150">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="827bf-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="827bf-151">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="827bf-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="827bf-152">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="827bf-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="827bf-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="827bf-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "AX",
  "id": "95794928-9abe-4548-8b43-50ffc20b9404",
  "userPrincipalName": "aaaa4@abcdefgh1234.ccsctp.net",
  "firstName": "aaaa4",
  "lastName": "aaaa4",
  "displayName": "aaaa4",
  "passwordProfile": {
    "forceChangePassword": false,
    "password": "Renew456*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/95794928-9abe-4548-8b43-50ffc20b9404",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
