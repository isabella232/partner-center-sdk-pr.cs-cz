---
title: Získání kontaktu podpory pro předplatné
description: Jak získat kontakt na podporu pro předplatné.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df3bce48902d95dc541c4a45e4e633569fc4406e
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766842"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="0260f-103">Získání kontaktu podpory pro předplatné</span><span class="sxs-lookup"><span data-stu-id="0260f-103">Get a subscription's support contact</span></span>

<span data-ttu-id="0260f-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="0260f-104">**Applies To**</span></span>

- <span data-ttu-id="0260f-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0260f-105">Partner Center</span></span>
- <span data-ttu-id="0260f-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="0260f-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0260f-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0260f-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0260f-108">Jak získat kontakt na podporu pro předplatné.</span><span class="sxs-lookup"><span data-stu-id="0260f-108">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0260f-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0260f-109">Prerequisites</span></span>

- <span data-ttu-id="0260f-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0260f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0260f-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="0260f-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0260f-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0260f-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0260f-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="0260f-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0260f-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="0260f-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0260f-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="0260f-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0260f-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="0260f-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0260f-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0260f-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0260f-118">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="0260f-118">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="0260f-119">C\#</span><span class="sxs-lookup"><span data-stu-id="0260f-119">C\#</span></span>

<span data-ttu-id="0260f-120">Pokud chcete získat kontakt na podporu pro předplatné, začněte tím, že k identifikaci zákazníka použijete metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0260f-120">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="0260f-121">Pak můžete získat rozhraní k operacím předplatného voláním metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="0260f-121">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="0260f-122">Dále pomocí vlastnosti [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) Získejte rozhraní pro podporu operací kontaktů a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) pro načtení objektu [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) .</span><span class="sxs-lookup"><span data-stu-id="0260f-122">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="0260f-123">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0260f-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0260f-124">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="0260f-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0260f-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="0260f-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0260f-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="0260f-126">Request syntax</span></span>

| <span data-ttu-id="0260f-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="0260f-127">Method</span></span>  | <span data-ttu-id="0260f-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0260f-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0260f-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="0260f-129">**GET**</span></span> | <span data-ttu-id="0260f-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/supportcontact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0260f-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0260f-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0260f-131">URI parameter</span></span>

<span data-ttu-id="0260f-132">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="0260f-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="0260f-133">Název</span><span class="sxs-lookup"><span data-stu-id="0260f-133">Name</span></span>            | <span data-ttu-id="0260f-134">Typ</span><span class="sxs-lookup"><span data-stu-id="0260f-134">Type</span></span>   | <span data-ttu-id="0260f-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0260f-135">Required</span></span> | <span data-ttu-id="0260f-136">Popis</span><span class="sxs-lookup"><span data-stu-id="0260f-136">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="0260f-137">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="0260f-137">customer-id</span></span>     | <span data-ttu-id="0260f-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="0260f-138">string</span></span> | <span data-ttu-id="0260f-139">Yes</span><span class="sxs-lookup"><span data-stu-id="0260f-139">Yes</span></span>      | <span data-ttu-id="0260f-140">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0260f-140">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="0260f-141">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="0260f-141">subscription-id</span></span> | <span data-ttu-id="0260f-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="0260f-142">string</span></span> | <span data-ttu-id="0260f-143">Yes</span><span class="sxs-lookup"><span data-stu-id="0260f-143">Yes</span></span>      | <span data-ttu-id="0260f-144">Řetězec ve formátu GUID, který identifikuje zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="0260f-144">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0260f-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0260f-145">Request headers</span></span>

<span data-ttu-id="0260f-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0260f-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0260f-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0260f-147">Request body</span></span>

<span data-ttu-id="0260f-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="0260f-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0260f-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0260f-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0260f-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0260f-150">REST response</span></span>

<span data-ttu-id="0260f-151">V případě úspěchu obsahuje tělo odpovědi prostředek [SupportContact](subscription-resources.md#supportcontact) .</span><span class="sxs-lookup"><span data-stu-id="0260f-151">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0260f-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0260f-152">Response success and error codes</span></span>

<span data-ttu-id="0260f-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0260f-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0260f-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0260f-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0260f-155">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0260f-155">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0260f-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0260f-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CV: bLbUhqy0+ESOX1v4.0
MS-ServerId: 201022015
Date: Tue, 20 Jun 2017 19:30:19 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
