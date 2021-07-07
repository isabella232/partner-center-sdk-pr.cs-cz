---
title: Resetování uživatelského hesla pro zákazníka
description: Resetování hesla se podobá aktualizaci dalších podrobností v existujícím uživatelském účtu pro vašeho zákazníka.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: f3661a588f566485cbd58035c63ae9f8e5d383af
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445676"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="6fff7-103">Resetování uživatelského hesla pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="6fff7-103">Reset user password for a customer</span></span>

<span data-ttu-id="6fff7-104">Resetování hesla se podobá aktualizaci dalších podrobností v existujícím uživatelském účtu pro vašeho zákazníka.</span><span class="sxs-lookup"><span data-stu-id="6fff7-104">Resetting a password is similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fff7-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6fff7-105">Prerequisites</span></span>

- <span data-ttu-id="6fff7-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6fff7-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6fff7-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="6fff7-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6fff7-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6fff7-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6fff7-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6fff7-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6fff7-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="6fff7-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6fff7-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="6fff7-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6fff7-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="6fff7-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6fff7-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6fff7-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6fff7-114">C\#</span><span class="sxs-lookup"><span data-stu-id="6fff7-114">C\#</span></span>

<span data-ttu-id="6fff7-115">Pokud chcete resetovat heslo pro zadaného uživatele zákazníka, nejprve načtěte zadané ID zákazníka a cílového uživatele.</span><span class="sxs-lookup"><span data-stu-id="6fff7-115">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="6fff7-116">Pak vytvořte nový objekt **CustomerUser,** který obsahuje informace o existujícím zákazníkovi, ale s novým objektem **PasswordProfile.**</span><span class="sxs-lookup"><span data-stu-id="6fff7-116">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="6fff7-117">Pak použijte kolekci **IAggregatePartner.Customers** a zavolejte **metodu ById().**</span><span class="sxs-lookup"><span data-stu-id="6fff7-117">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="6fff7-118">Potom **zavolejte vlastnost Users,** **metodu ById()** a pak **metodu Patch.**</span><span class="sxs-lookup"><span data-stu-id="6fff7-118">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

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

<span data-ttu-id="6fff7-119">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6fff7-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6fff7-120">**Project:** PartnerSDK.FeatureSamples **– třída:** CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="6fff7-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6fff7-121">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="6fff7-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6fff7-122">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="6fff7-122">Request syntax</span></span>

| <span data-ttu-id="6fff7-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="6fff7-123">Method</span></span>    | <span data-ttu-id="6fff7-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="6fff7-124">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="6fff7-125">**Oprava**</span><span class="sxs-lookup"><span data-stu-id="6fff7-125">**PATCH**</span></span> | <span data-ttu-id="6fff7-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/uživatelé HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6fff7-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6fff7-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="6fff7-127">URI parameter</span></span>

<span data-ttu-id="6fff7-128">Pomocí následujícího parametru dotazu identifikujte správného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="6fff7-128">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="6fff7-129">Název</span><span class="sxs-lookup"><span data-stu-id="6fff7-129">Name</span></span>                   | <span data-ttu-id="6fff7-130">Typ</span><span class="sxs-lookup"><span data-stu-id="6fff7-130">Type</span></span>     | <span data-ttu-id="6fff7-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="6fff7-131">Required</span></span> | <span data-ttu-id="6fff7-132">Popis</span><span class="sxs-lookup"><span data-stu-id="6fff7-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6fff7-133">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="6fff7-133">**customer-tenant-id**</span></span> | <span data-ttu-id="6fff7-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="6fff7-134">**guid**</span></span> | <span data-ttu-id="6fff7-135">Y</span><span class="sxs-lookup"><span data-stu-id="6fff7-135">Y</span></span>        | <span data-ttu-id="6fff7-136">Hodnota je IDENTIFIKÁTOR GUID naformátovaný jako **customer-tenant-id,** který umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="6fff7-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="6fff7-137">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="6fff7-137">**user-id**</span></span>            | <span data-ttu-id="6fff7-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="6fff7-138">**guid**</span></span> | <span data-ttu-id="6fff7-139">Y</span><span class="sxs-lookup"><span data-stu-id="6fff7-139">Y</span></span>        | <span data-ttu-id="6fff7-140">Hodnota je ID uživatele ve **formátu** GUID, které patří jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="6fff7-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="6fff7-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="6fff7-141">Request headers</span></span>

<span data-ttu-id="6fff7-142">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6fff7-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6fff7-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="6fff7-143">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="6fff7-144">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="6fff7-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6fff7-145">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="6fff7-145">REST response</span></span>

<span data-ttu-id="6fff7-146">V případě úspěchu tato metoda vrátí informace o uživateli spolu s aktualizovanými informacemi o hesle.</span><span class="sxs-lookup"><span data-stu-id="6fff7-146">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6fff7-147">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="6fff7-147">Response success and error codes</span></span>

<span data-ttu-id="6fff7-148">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="6fff7-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6fff7-149">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="6fff7-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6fff7-150">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6fff7-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6fff7-151">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="6fff7-151">Response example</span></span>

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
