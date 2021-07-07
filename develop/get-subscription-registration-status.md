---
title: Získání stavu registrace předplatných
description: Získejte stav předplatného, které je zaregistrované pro použití s Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e39f94c0eac402a0be3afde84279aa637868f96
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445948"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="748f6-103">Získání stavu registrace předplatných</span><span class="sxs-lookup"><span data-stu-id="748f6-103">Get subscription registration status</span></span>

<span data-ttu-id="748f6-104">Jak získat stav registrace předplatného pro zákaznické předplatné, které bylo povoleno pro nákup Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="748f6-104">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="748f6-105">Pokud si chcete koupit rezervovanou instanci virtuálního počítače Azure pomocí rozhraní PARTNERSKÉ CENTRUM API, musíte mít alespoň jedno stávající předplatné Azure CSP.</span><span class="sxs-lookup"><span data-stu-id="748f6-105">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="748f6-106">Metoda [Registrace předplatného](register-a-subscription.md) vám umožní zaregistrovat stávající předplatné Azure CSP a povolit ho pro nákup Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="748f6-106">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="748f6-107">Tato metoda umožňuje načíst stav této registrace.</span><span class="sxs-lookup"><span data-stu-id="748f6-107">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="748f6-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="748f6-108">Prerequisites</span></span>

- <span data-ttu-id="748f6-109">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="748f6-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="748f6-110">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="748f6-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="748f6-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="748f6-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="748f6-112">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="748f6-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="748f6-113">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="748f6-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="748f6-114">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="748f6-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="748f6-115">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="748f6-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="748f6-116">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="748f6-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="748f6-117">ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="748f6-117">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="748f6-118">C\#</span><span class="sxs-lookup"><span data-stu-id="748f6-118">C\#</span></span>

<span data-ttu-id="748f6-119">Pokud chcete získat stav registrace předplatného, začněte tím, že k identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="748f6-119">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="748f6-120">Pak získejte rozhraní pro operace předplatného voláním metody [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) s ID předplatného pro identifikaci předplatného.</span><span class="sxs-lookup"><span data-stu-id="748f6-120">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="748f6-121">Dále pomocí vlastnosti RegistrationStatus získejte rozhraní pro operace stavu registrace aktuálního předplatného a zavolejte metodu **Get** nebo **GetAsync** pro načtení **objektu SubscriptionRegistrationStatus.**</span><span class="sxs-lookup"><span data-stu-id="748f6-121">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="748f6-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="748f6-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="748f6-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="748f6-123">Request syntax</span></span>

| <span data-ttu-id="748f6-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="748f6-124">Method</span></span>    | <span data-ttu-id="748f6-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="748f6-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="748f6-126">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="748f6-126">**GET**</span></span>  | <span data-ttu-id="748f6-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/stav registrace HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="748f6-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="748f6-128">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="748f6-128">URI parameters</span></span>

<span data-ttu-id="748f6-129">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="748f6-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="748f6-130">Název</span><span class="sxs-lookup"><span data-stu-id="748f6-130">Name</span></span>                    | <span data-ttu-id="748f6-131">Typ</span><span class="sxs-lookup"><span data-stu-id="748f6-131">Type</span></span>       | <span data-ttu-id="748f6-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="748f6-132">Required</span></span> | <span data-ttu-id="748f6-133">Popis</span><span class="sxs-lookup"><span data-stu-id="748f6-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="748f6-134">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="748f6-134">customer-id</span></span>             | <span data-ttu-id="748f6-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="748f6-135">string</span></span>     | <span data-ttu-id="748f6-136">Yes</span><span class="sxs-lookup"><span data-stu-id="748f6-136">Yes</span></span>      | <span data-ttu-id="748f6-137">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="748f6-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="748f6-138">id předplatného</span><span class="sxs-lookup"><span data-stu-id="748f6-138">subscription-id</span></span>         | <span data-ttu-id="748f6-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="748f6-139">string</span></span>     | <span data-ttu-id="748f6-140">Yes</span><span class="sxs-lookup"><span data-stu-id="748f6-140">Yes</span></span>      | <span data-ttu-id="748f6-141">Řetězec ve formátu GUID, který identifikuje odběr.</span><span class="sxs-lookup"><span data-stu-id="748f6-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="748f6-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="748f6-142">Request headers</span></span>

<span data-ttu-id="748f6-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="748f6-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="748f6-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="748f6-144">Request body</span></span>

<span data-ttu-id="748f6-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="748f6-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="748f6-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="748f6-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="748f6-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="748f6-147">REST response</span></span>

<span data-ttu-id="748f6-148">V případě úspěchu bude tělo odpovědi obsahovat [prostředek SubscriptionRegistrationStatus.](subscription-resources.md#subscriptionregistrationstatus)</span><span class="sxs-lookup"><span data-stu-id="748f6-148">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="748f6-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="748f6-149">Response success and error codes</span></span>

<span data-ttu-id="748f6-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="748f6-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="748f6-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="748f6-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="748f6-152">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="748f6-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="748f6-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="748f6-153">Response example</span></span>

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
