---
title: Registrace předplatného
description: Zaregistrujte stávající předplatné, aby bylo povolené řazení rezervací Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766968"
---
# <a name="register-a-subscription"></a><span data-ttu-id="b04ce-103">Registrace předplatného</span><span class="sxs-lookup"><span data-stu-id="b04ce-103">Register a subscription</span></span>

<span data-ttu-id="b04ce-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="b04ce-104">**Applies To**</span></span>

- <span data-ttu-id="b04ce-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="b04ce-105">Partner Center</span></span>

<span data-ttu-id="b04ce-106">Zaregistrujte stávající [předplatné](subscription-resources.md) , aby bylo povolené řazení rezervací Azure.</span><span class="sxs-lookup"><span data-stu-id="b04ce-106">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="b04ce-107">Pokud si chcete koupit rezervaci Azure, musíte mít aspoň jedno stávající předplatné Azure CSP.</span><span class="sxs-lookup"><span data-stu-id="b04ce-107">To purchase an Azure reservation you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="b04ce-108">Tato metoda umožňuje zaregistrovat stávající předplatné Azure CSP a povolit ho k nákupu rezervací Azure.</span><span class="sxs-lookup"><span data-stu-id="b04ce-108">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b04ce-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b04ce-109">Prerequisites</span></span>

- <span data-ttu-id="b04ce-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b04ce-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b04ce-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="b04ce-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b04ce-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b04ce-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b04ce-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="b04ce-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b04ce-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="b04ce-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b04ce-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="b04ce-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b04ce-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="b04ce-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b04ce-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b04ce-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b04ce-118">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="b04ce-118">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="b04ce-119">C\#</span><span class="sxs-lookup"><span data-stu-id="b04ce-119">C\#</span></span>

<span data-ttu-id="b04ce-120">Pokud chcete zaregistrovat předplatné zákazníka, načtěte rozhraní k operacím předplatného tak, že zavoláte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka k identifikaci zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b04ce-120">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="b04ce-121">Pak zavolejte metodu [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) s ID předplatného k identifikaci předplatného, které zaregistrujete.</span><span class="sxs-lookup"><span data-stu-id="b04ce-121">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="b04ce-122">Nakonec zavolejte metodu Register **. Register ()** pro registraci předplatného a NAČTĚTE identifikátor URI, který se dá použít k získání stavu registrace předplatného.</span><span class="sxs-lookup"><span data-stu-id="b04ce-122">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="b04ce-123">Další informace najdete v tématu [získání stavu registrace předplatného](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="b04ce-123">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="b04ce-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="b04ce-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b04ce-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="b04ce-125">Request syntax</span></span>

| <span data-ttu-id="b04ce-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="b04ce-126">Method</span></span>    | <span data-ttu-id="b04ce-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="b04ce-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b04ce-128">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="b04ce-128">**POST**</span></span>  | <span data-ttu-id="b04ce-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b04ce-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b04ce-130">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="b04ce-130">URI parameters</span></span>

<span data-ttu-id="b04ce-131">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="b04ce-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="b04ce-132">Název</span><span class="sxs-lookup"><span data-stu-id="b04ce-132">Name</span></span>                    | <span data-ttu-id="b04ce-133">Typ</span><span class="sxs-lookup"><span data-stu-id="b04ce-133">Type</span></span>       | <span data-ttu-id="b04ce-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="b04ce-134">Required</span></span> | <span data-ttu-id="b04ce-135">Popis</span><span class="sxs-lookup"><span data-stu-id="b04ce-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="b04ce-136">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="b04ce-136">customer-id</span></span>             | <span data-ttu-id="b04ce-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="b04ce-137">string</span></span>     | <span data-ttu-id="b04ce-138">Yes</span><span class="sxs-lookup"><span data-stu-id="b04ce-138">Yes</span></span>      | <span data-ttu-id="b04ce-139">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="b04ce-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="b04ce-140">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="b04ce-140">subscription-id</span></span>         | <span data-ttu-id="b04ce-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="b04ce-141">string</span></span>     | <span data-ttu-id="b04ce-142">Yes</span><span class="sxs-lookup"><span data-stu-id="b04ce-142">Yes</span></span>      | <span data-ttu-id="b04ce-143">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="b04ce-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="b04ce-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="b04ce-144">Request headers</span></span>

<span data-ttu-id="b04ce-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b04ce-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b04ce-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="b04ce-146">Request body</span></span>

<span data-ttu-id="b04ce-147">Žádné</span><span class="sxs-lookup"><span data-stu-id="b04ce-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b04ce-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="b04ce-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b04ce-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="b04ce-149">REST response</span></span>

<span data-ttu-id="b04ce-150">V případě úspěchu odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který lze použít k načtení stavu registrace předplatného.</span><span class="sxs-lookup"><span data-stu-id="b04ce-150">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="b04ce-151">Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.</span><span class="sxs-lookup"><span data-stu-id="b04ce-151">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="b04ce-152">Příklad toho, jak načíst stav, najdete v tématu [získání stavu registrace předplatného](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="b04ce-152">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b04ce-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b04ce-153">Response success and error codes</span></span>

<span data-ttu-id="b04ce-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="b04ce-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b04ce-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="b04ce-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b04ce-156">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b04ce-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b04ce-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="b04ce-157">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
