---
title: Vytvoření uživatelských účtů pro zákazníka
description: Vytvořte nový uživatelský účet pro zákazníka.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9131a1c4c37d07b1994b67379ec8361fda13a371
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766687"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="143fd-103">Vytvoření uživatelských účtů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="143fd-103">Create user accounts for a customer</span></span>

<span data-ttu-id="143fd-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="143fd-104">**Applies to:**</span></span>

- <span data-ttu-id="143fd-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="143fd-105">Partner Center</span></span>

<span data-ttu-id="143fd-106">Vytvořte nový uživatelský účet pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="143fd-106">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="143fd-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="143fd-107">Prerequisites</span></span>

- <span data-ttu-id="143fd-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="143fd-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="143fd-109">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="143fd-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="143fd-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="143fd-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="143fd-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="143fd-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="143fd-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="143fd-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="143fd-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="143fd-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="143fd-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="143fd-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="143fd-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="143fd-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="143fd-116">C\#</span><span class="sxs-lookup"><span data-stu-id="143fd-116">C\#</span></span>

<span data-ttu-id="143fd-117">Získání nového uživatelského účtu pro zákazníka:</span><span class="sxs-lookup"><span data-stu-id="143fd-117">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="143fd-118">Vytvořte nový objekt **CustomerUser** s informacemi o relevantním uživateli.</span><span class="sxs-lookup"><span data-stu-id="143fd-118">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="143fd-119">Použijte svou kolekci **IAggregatePartner. Customers** a zavolejte metodu **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="143fd-119">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="143fd-120">Zavolejte vlastnost **Users** a potom metodu **Create** .</span><span class="sxs-lookup"><span data-stu-id="143fd-120">Call the **Users** property, followed by the **Create** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// var SelectedCustomer;

var userToCreate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "Password!1" },
    DisplayName = "TestDisplayName",
    FirstName = "TestFirstName",
    LastName = "TestLastName",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

User createdUser = partnerOperations.Customers.ById(selectedCustomerId).Users.Create(userToCreate);
```

<span data-ttu-id="143fd-121">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="143fd-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="143fd-122">**Projekt**: PartnerSDK. FeatureSamples **Třída**: CustomerUserCreate.cs</span><span class="sxs-lookup"><span data-stu-id="143fd-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="143fd-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="143fd-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="143fd-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="143fd-124">Request syntax</span></span>

| <span data-ttu-id="143fd-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="143fd-125">Method</span></span>   | <span data-ttu-id="143fd-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="143fd-126">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="143fd-127">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="143fd-127">**POST**</span></span> | <span data-ttu-id="143fd-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="143fd-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="143fd-129">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="143fd-129">URI parameters</span></span>

<span data-ttu-id="143fd-130">K identifikaci správného zákazníka použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="143fd-130">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="143fd-131">Název</span><span class="sxs-lookup"><span data-stu-id="143fd-131">Name</span></span> | <span data-ttu-id="143fd-132">Typ</span><span class="sxs-lookup"><span data-stu-id="143fd-132">Type</span></span> | <span data-ttu-id="143fd-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="143fd-133">Required</span></span> | <span data-ttu-id="143fd-134">Popis</span><span class="sxs-lookup"><span data-stu-id="143fd-134">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="143fd-135">**Customer-tenant-ID**</span><span class="sxs-lookup"><span data-stu-id="143fd-135">**customer-tenant-id**</span></span> | <span data-ttu-id="143fd-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="143fd-136">**guid**</span></span> | <span data-ttu-id="143fd-137">Y</span><span class="sxs-lookup"><span data-stu-id="143fd-137">Y</span></span> | <span data-ttu-id="143fd-138">Hodnota je **ID zákazníka-tenanta** ve formátu GUID. Umožňuje prodejci filtrovat výsledky pro konkrétního zákazníka, který patří prodejci.</span><span class="sxs-lookup"><span data-stu-id="143fd-138">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="143fd-139">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="143fd-139">**user-id**</span></span> | <span data-ttu-id="143fd-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="143fd-140">**guid**</span></span> | <span data-ttu-id="143fd-141">N</span><span class="sxs-lookup"><span data-stu-id="143fd-141">N</span></span> | <span data-ttu-id="143fd-142">Hodnota je **ID uživatele** FORMÁTOVANÉho identifikátorem GUID, který patří k jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="143fd-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="143fd-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="143fd-143">Request headers</span></span>

<span data-ttu-id="143fd-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="143fd-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="143fd-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="143fd-145">Request body</span></span>

<span data-ttu-id="143fd-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="143fd-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="143fd-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="143fd-147">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "country/region code",
      "userPrincipalName": "userid@domain.onmicrosoft.com",
      "firstName": "First",
      "lastName": "Last",
      "displayName": "User name",
      "immutableId": "Some unique ID",
      "passwordProfile":{
                 password: "abCD123*",
                 forceChangePassword: true
      },
      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="143fd-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="143fd-148">REST response</span></span>

<span data-ttu-id="143fd-149">V případě úspěchu vrátí tato metoda uživatelský účet, včetně identifikátoru GUID.</span><span class="sxs-lookup"><span data-stu-id="143fd-149">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="143fd-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="143fd-150">Response success and error codes</span></span>

<span data-ttu-id="143fd-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="143fd-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="143fd-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="143fd-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="143fd-153">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="143fd-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="143fd-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="143fd-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
  "usageLocation": "country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "userid@domain.onmicrosoft.com",
  "firstName": "First",
  "lastName": "Last",
  "displayName": "User name",
  "immutableId": "Some unique ID",
  "passwordProfile": {
    "forceChangePassword": true,
    "password": "abCD123*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```