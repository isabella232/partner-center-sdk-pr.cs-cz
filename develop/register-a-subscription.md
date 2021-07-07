---
title: Registrace předplatného
description: Zaregistrujte stávající předplatné, aby bylo povolené pro objednávání rezervací Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d26a7c77f60e6ef817cde80b9e97c88bd8bdc786
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446611"
---
# <a name="register-a-subscription"></a><span data-ttu-id="9548d-103">Registrace předplatného</span><span class="sxs-lookup"><span data-stu-id="9548d-103">Register a subscription</span></span>

<span data-ttu-id="9548d-104">Zaregistrujte stávající [předplatné,](subscription-resources.md) aby bylo povolené pro objednávání rezervací Azure.</span><span class="sxs-lookup"><span data-stu-id="9548d-104">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="9548d-105">Pokud si chcete koupit rezervaci Azure, musíte mít alespoň jedno stávající předplatné Azure CSP.</span><span class="sxs-lookup"><span data-stu-id="9548d-105">To purchase an Azure reservation, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="9548d-106">Tato metoda vám umožní zaregistrovat stávající předplatné Azure CSP a umožnit mu nákup rezervací Azure.</span><span class="sxs-lookup"><span data-stu-id="9548d-106">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9548d-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9548d-107">Prerequisites</span></span>

- <span data-ttu-id="9548d-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9548d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9548d-109">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="9548d-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9548d-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9548d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9548d-111">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="9548d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9548d-112">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="9548d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9548d-113">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="9548d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9548d-114">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9548d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9548d-115">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9548d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9548d-116">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="9548d-116">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="9548d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="9548d-117">C\#</span></span>

<span data-ttu-id="9548d-118">Pokud chcete zaregistrovat předplatné zákazníka, načtěte rozhraní pro operace předplatného voláním metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka a identifikujte zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9548d-118">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="9548d-119">Potom zavolejte [**metodu Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) s ID předplatného a identifikujte předplatné, které registrujete.</span><span class="sxs-lookup"><span data-stu-id="9548d-119">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="9548d-120">Nakonec zavolejte **metodu Registration.Register()** pro registraci předplatného a načtěte identifikátor URI, který lze použít k získání stavu registrace předplatného.</span><span class="sxs-lookup"><span data-stu-id="9548d-120">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="9548d-121">Další informace najdete v tématu [Získání stavu registrace předplatného.](get-subscription-registration-status.md)</span><span class="sxs-lookup"><span data-stu-id="9548d-121">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="9548d-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="9548d-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9548d-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="9548d-123">Request syntax</span></span>

| <span data-ttu-id="9548d-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="9548d-124">Method</span></span>    | <span data-ttu-id="9548d-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="9548d-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9548d-126">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="9548d-126">**POST**</span></span>  | <span data-ttu-id="9548d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/registrace HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9548d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="9548d-128">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="9548d-128">URI parameters</span></span>

<span data-ttu-id="9548d-129">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="9548d-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="9548d-130">Název</span><span class="sxs-lookup"><span data-stu-id="9548d-130">Name</span></span>                    | <span data-ttu-id="9548d-131">Typ</span><span class="sxs-lookup"><span data-stu-id="9548d-131">Type</span></span>       | <span data-ttu-id="9548d-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="9548d-132">Required</span></span> | <span data-ttu-id="9548d-133">Popis</span><span class="sxs-lookup"><span data-stu-id="9548d-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="9548d-134">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="9548d-134">customer-id</span></span>             | <span data-ttu-id="9548d-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="9548d-135">string</span></span>     | <span data-ttu-id="9548d-136">Yes</span><span class="sxs-lookup"><span data-stu-id="9548d-136">Yes</span></span>      | <span data-ttu-id="9548d-137">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="9548d-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="9548d-138">id předplatného</span><span class="sxs-lookup"><span data-stu-id="9548d-138">subscription-id</span></span>         | <span data-ttu-id="9548d-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="9548d-139">string</span></span>     | <span data-ttu-id="9548d-140">Yes</span><span class="sxs-lookup"><span data-stu-id="9548d-140">Yes</span></span>      | <span data-ttu-id="9548d-141">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="9548d-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="9548d-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="9548d-142">Request headers</span></span>

<span data-ttu-id="9548d-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9548d-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9548d-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="9548d-144">Request body</span></span>

<span data-ttu-id="9548d-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="9548d-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9548d-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="9548d-146">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9548d-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="9548d-147">REST response</span></span>

<span data-ttu-id="9548d-148">V případě úspěchu odpověď obsahuje **hlavičku Location** s identifikátorem URI, který lze použít k načtení stavu registrace předplatného.</span><span class="sxs-lookup"><span data-stu-id="9548d-148">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="9548d-149">Uložte si tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.</span><span class="sxs-lookup"><span data-stu-id="9548d-149">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="9548d-150">Příklad načtení stavu najdete v tématu Získání [stavu registrace předplatného.](get-subscription-registration-status.md)</span><span class="sxs-lookup"><span data-stu-id="9548d-150">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9548d-151">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="9548d-151">Response success and error codes</span></span>

<span data-ttu-id="9548d-152">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="9548d-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9548d-153">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="9548d-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9548d-154">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9548d-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9548d-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="9548d-155">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
