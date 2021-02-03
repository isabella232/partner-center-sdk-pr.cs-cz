---
title: Získání stavu registrace předplatných
description: Získejte stav předplatného, které je zaregistrované pro použití s Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767034"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="47689-103">Získání stavu registrace předplatných</span><span class="sxs-lookup"><span data-stu-id="47689-103">Get subscription registration status</span></span>

<span data-ttu-id="47689-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="47689-104">**Applies To**</span></span>

- <span data-ttu-id="47689-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="47689-105">Partner Center</span></span>

<span data-ttu-id="47689-106">Jak získat stav registrace předplatného u zákaznického předplatného, u kterého je povolené nakupování Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="47689-106">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="47689-107">K zakoupení rezervované instance virtuálního počítače Azure pomocí rozhraní API partnerského centra musíte mít aspoň jedno stávající předplatné Azure CSP.</span><span class="sxs-lookup"><span data-stu-id="47689-107">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="47689-108">Metoda [Register a Subscription](register-a-subscription.md) umožňuje zaregistrovat stávající předplatné Azure CSP a povolit ho pro nákup Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="47689-108">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="47689-109">Tato metoda umožňuje načíst stav této registrace.</span><span class="sxs-lookup"><span data-stu-id="47689-109">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47689-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="47689-110">Prerequisites</span></span>

- <span data-ttu-id="47689-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="47689-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="47689-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="47689-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="47689-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="47689-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="47689-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="47689-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="47689-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="47689-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="47689-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="47689-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="47689-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="47689-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="47689-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="47689-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="47689-119">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="47689-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="47689-120">C\#</span><span class="sxs-lookup"><span data-stu-id="47689-120">C\#</span></span>

<span data-ttu-id="47689-121">Pokud chcete získat stav registrace předplatného, začněte tím, že k identifikaci zákazníka použijete metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="47689-121">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="47689-122">Potom Získejte rozhraní k operacím předplatného voláním metody [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) s ID předplatného k identifikaci předplatného.</span><span class="sxs-lookup"><span data-stu-id="47689-122">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="47689-123">Dále pomocí vlastnosti RegistrationStatus Získejte rozhraní pro operace stavu registrace aktuálního předplatného a zavolejte metodu **Get** nebo **GetAsync** pro načtení objektu **SubscriptionRegistrationStatus** .</span><span class="sxs-lookup"><span data-stu-id="47689-123">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="47689-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="47689-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="47689-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="47689-125">Request syntax</span></span>

| <span data-ttu-id="47689-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="47689-126">Method</span></span>    | <span data-ttu-id="47689-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="47689-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="47689-128">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="47689-128">**GET**</span></span>  | <span data-ttu-id="47689-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrationstatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="47689-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="47689-130">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="47689-130">URI parameters</span></span>

<span data-ttu-id="47689-131">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="47689-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="47689-132">Název</span><span class="sxs-lookup"><span data-stu-id="47689-132">Name</span></span>                    | <span data-ttu-id="47689-133">Typ</span><span class="sxs-lookup"><span data-stu-id="47689-133">Type</span></span>       | <span data-ttu-id="47689-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="47689-134">Required</span></span> | <span data-ttu-id="47689-135">Popis</span><span class="sxs-lookup"><span data-stu-id="47689-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="47689-136">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="47689-136">customer-id</span></span>             | <span data-ttu-id="47689-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="47689-137">string</span></span>     | <span data-ttu-id="47689-138">Yes</span><span class="sxs-lookup"><span data-stu-id="47689-138">Yes</span></span>      | <span data-ttu-id="47689-139">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="47689-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="47689-140">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="47689-140">subscription-id</span></span>         | <span data-ttu-id="47689-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="47689-141">string</span></span>     | <span data-ttu-id="47689-142">Yes</span><span class="sxs-lookup"><span data-stu-id="47689-142">Yes</span></span>      | <span data-ttu-id="47689-143">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="47689-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="47689-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="47689-144">Request headers</span></span>

<span data-ttu-id="47689-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="47689-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="47689-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="47689-146">Request body</span></span>

<span data-ttu-id="47689-147">Žádné</span><span class="sxs-lookup"><span data-stu-id="47689-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="47689-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="47689-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="47689-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="47689-149">REST response</span></span>

<span data-ttu-id="47689-150">V případě úspěchu obsahuje tělo odpovědi prostředek [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) .</span><span class="sxs-lookup"><span data-stu-id="47689-150">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="47689-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="47689-151">Response success and error codes</span></span>

<span data-ttu-id="47689-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="47689-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="47689-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="47689-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="47689-154">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="47689-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="47689-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="47689-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
