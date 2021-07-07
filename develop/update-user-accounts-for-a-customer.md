---
title: Aktualizace uživatelských účtů pro zákazníka
description: Aktualizujte podrobnosti v existujícím uživatelském účtu pro zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ebfdbb5df1d56416835af771fd6b70190776012
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445268"
---
# <a name="update-user-accounts-for-a-customer"></a><span data-ttu-id="61452-103">Aktualizace uživatelských účtů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="61452-103">Update user accounts for a customer</span></span>

<span data-ttu-id="61452-104">Aktualizujte podrobnosti v existujícím uživatelském účtu pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="61452-104">Update details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61452-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="61452-105">Prerequisites</span></span>

- <span data-ttu-id="61452-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="61452-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="61452-107">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="61452-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="61452-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="61452-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="61452-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="61452-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="61452-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="61452-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="61452-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="61452-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="61452-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="61452-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="61452-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="61452-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="61452-114">C\#</span><span class="sxs-lookup"><span data-stu-id="61452-114">C\#</span></span>

<span data-ttu-id="61452-115">Chcete-li aktualizovat podrobnosti pro zadaného uživatele zákazníka, napřed si načtěte zadané ID zákazníka a uživatele, které chcete aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="61452-115">To update the details for a specified customer user, first retrieve the specified customer ID and user to update.</span></span> <span data-ttu-id="61452-116">Pak v novém objektu **CustomerUser** vytvořte aktualizovanou verzi uživatele.</span><span class="sxs-lookup"><span data-stu-id="61452-116">Then, create an updated version of the user in a new **CustomerUser** object.</span></span> <span data-ttu-id="61452-117">Pak použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="61452-117">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="61452-118">Pak zavolejte vlastnost **Users** , metodu **ById ()** následovanou metodou **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="61452-118">Then call the **Users** property, the **ById()** method, followed by the **Patch()** method.</span></span>

``` csharp
// string selectedCustomerId;
// customerUser specifiedUser;
// IAggregatePartner partnerOperations;

// Updated information
var userToUpdate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "testPw@!122B" },
    DisplayName = "DisplayNameChange",
    FirstName = "FirstNameChange",
    LastName = "LastNameChange",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

// Update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="61452-119">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="61452-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="61452-120">**Project**: PartnerSDK. FeatureSamples **třída**: CustomerUserUpdate. cs</span><span class="sxs-lookup"><span data-stu-id="61452-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="61452-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="61452-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="61452-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="61452-122">Request syntax</span></span>

| <span data-ttu-id="61452-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="61452-123">Method</span></span>    | <span data-ttu-id="61452-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="61452-124">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="61452-125">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="61452-125">**PATCH**</span></span> | <span data-ttu-id="61452-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="61452-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="61452-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="61452-127">URI parameter</span></span>

<span data-ttu-id="61452-128">K identifikaci správného zákazníka použijte následující parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="61452-128">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="61452-129">Název</span><span class="sxs-lookup"><span data-stu-id="61452-129">Name</span></span>                   | <span data-ttu-id="61452-130">Typ</span><span class="sxs-lookup"><span data-stu-id="61452-130">Type</span></span>     | <span data-ttu-id="61452-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="61452-131">Required</span></span> | <span data-ttu-id="61452-132">Popis</span><span class="sxs-lookup"><span data-stu-id="61452-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="61452-133">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="61452-133">**customer-tenant-id**</span></span> | <span data-ttu-id="61452-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="61452-134">**guid**</span></span> | <span data-ttu-id="61452-135">Y</span><span class="sxs-lookup"><span data-stu-id="61452-135">Y</span></span>        | <span data-ttu-id="61452-136">Hodnota je identifikátor **zákazníka** , který je ve formátu GUID, který umožňuje prodejci filtrovat výsledky pro daného zákazníka, kteří patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="61452-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="61452-137">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="61452-137">**user-id**</span></span>            | <span data-ttu-id="61452-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="61452-138">**guid**</span></span> | <span data-ttu-id="61452-139">Y</span><span class="sxs-lookup"><span data-stu-id="61452-139">Y</span></span>        | <span data-ttu-id="61452-140">Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="61452-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="61452-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="61452-141">Request headers</span></span>

<span data-ttu-id="61452-142">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="61452-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="61452-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="61452-143">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="61452-144">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="61452-144">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "new country/region code",

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="61452-145">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="61452-145">REST response</span></span>

<span data-ttu-id="61452-146">V případě úspěchu vrátí tato metoda uživatelský účet s aktualizovanými informacemi.</span><span class="sxs-lookup"><span data-stu-id="61452-146">If successful, this method returns a user account with the updated information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="61452-147">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="61452-147">Response success and error codes</span></span>

<span data-ttu-id="61452-148">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="61452-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="61452-149">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="61452-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="61452-150">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="61452-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="61452-151">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="61452-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "new country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "emailidchange@abcdefgh1234.ccsctp.net",
  "firstName": "FirstNameChange",
  "lastName": "LastNameChange",
  "displayName": "DisplayNameChange",
  "userDomainType": "none",
  "state": "active",
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/4b10bf41-ab11-40e3-8c53-cd67849b50de",
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
