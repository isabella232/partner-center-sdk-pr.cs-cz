---
title: Vytvoření uživatelských účtů pro zákazníka
description: Vytvořte pro zákazníka nový uživatelský účet.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d086d7ba72c9d9e42dc88684ddeafc9a597bfd7c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973379"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="0e4ce-103">Vytvoření uživatelských účtů pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="0e4ce-103">Create user accounts for a customer</span></span>

<span data-ttu-id="0e4ce-104">Vytvořte pro zákazníka nový uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-104">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e4ce-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0e4ce-105">Prerequisites</span></span>

- <span data-ttu-id="0e4ce-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0e4ce-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0e4ce-107">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0e4ce-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0e4ce-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0e4ce-109">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0e4ce-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0e4ce-110">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0e4ce-111">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0e4ce-112">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0e4ce-113">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0e4ce-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0e4ce-114">C\#</span><span class="sxs-lookup"><span data-stu-id="0e4ce-114">C\#</span></span>

<span data-ttu-id="0e4ce-115">Získání nového uživatelského účtu pro zákazníka:</span><span class="sxs-lookup"><span data-stu-id="0e4ce-115">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="0e4ce-116">Vytvořte nový objekt **CustomerUser** s příslušnými informacemi o uživateli.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-116">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="0e4ce-117">Použijte kolekci **IAggregatePartner.Customers** a zavolejte **metodu ById().**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-117">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="0e4ce-118">Zavolejte **vlastnost Users** a pak **metodu Create.**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-118">Call the **Users** property, followed by the **Create** method.</span></span>

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

<span data-ttu-id="0e4ce-119">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0e4ce-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0e4ce-120">**Project:** PartnerSDK.FeatureSamples **– třída:** CustomerUserCreate.cs</span><span class="sxs-lookup"><span data-stu-id="0e4ce-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0e4ce-121">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="0e4ce-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0e4ce-122">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="0e4ce-122">Request syntax</span></span>

| <span data-ttu-id="0e4ce-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="0e4ce-123">Method</span></span>   | <span data-ttu-id="0e4ce-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0e4ce-124">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0e4ce-125">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-125">**POST**</span></span> | <span data-ttu-id="0e4ce-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/uživatelé HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0e4ce-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="0e4ce-127">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="0e4ce-127">URI parameters</span></span>

<span data-ttu-id="0e4ce-128">Pomocí následujících parametrů dotazu identifikujte správného zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-128">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="0e4ce-129">Název</span><span class="sxs-lookup"><span data-stu-id="0e4ce-129">Name</span></span> | <span data-ttu-id="0e4ce-130">Typ</span><span class="sxs-lookup"><span data-stu-id="0e4ce-130">Type</span></span> | <span data-ttu-id="0e4ce-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0e4ce-131">Required</span></span> | <span data-ttu-id="0e4ce-132">Popis</span><span class="sxs-lookup"><span data-stu-id="0e4ce-132">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="0e4ce-133">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-133">**customer-tenant-id**</span></span> | <span data-ttu-id="0e4ce-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-134">**guid**</span></span> | <span data-ttu-id="0e4ce-135">Y</span><span class="sxs-lookup"><span data-stu-id="0e4ce-135">Y</span></span> | <span data-ttu-id="0e4ce-136">Hodnota je IDENTIFIKÁTOR GUID naformátovaný **jako customer-tenant-id**. Umožňuje prodejci filtrovat výsledky pro daného zákazníka, který patří k prodejci.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-136">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="0e4ce-137">**ID uživatele**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-137">**user-id**</span></span> | <span data-ttu-id="0e4ce-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="0e4ce-138">**guid**</span></span> | <span data-ttu-id="0e4ce-139">N</span><span class="sxs-lookup"><span data-stu-id="0e4ce-139">N</span></span> | <span data-ttu-id="0e4ce-140">Hodnota je ID uživatele ve **formátu** GUID, které patří jednomu uživatelskému účtu.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0e4ce-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0e4ce-141">Request headers</span></span>

<span data-ttu-id="0e4ce-142">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0e4ce-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0e4ce-143">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0e4ce-143">Request body</span></span>

<span data-ttu-id="0e4ce-144">Žádné</span><span class="sxs-lookup"><span data-stu-id="0e4ce-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0e4ce-145">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0e4ce-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0e4ce-146">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0e4ce-146">REST response</span></span>

<span data-ttu-id="0e4ce-147">V případě úspěchu tato metoda vrátí uživatelský účet včetně identifikátoru GUID.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-147">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0e4ce-148">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="0e4ce-148">Response success and error codes</span></span>

<span data-ttu-id="0e4ce-149">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0e4ce-150">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="0e4ce-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0e4ce-151">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0e4ce-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0e4ce-152">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0e4ce-152">Response example</span></span>

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