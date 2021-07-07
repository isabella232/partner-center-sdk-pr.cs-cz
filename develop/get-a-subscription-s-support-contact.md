---
title: Získání kontaktu podpory pro předplatné
description: Jak získat kontakt podpory předplatného
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b6c98e5ed96f2ca4787e93504c9e094bd46ae783
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760755"
---
# <a name="get-a-subscriptions-support-contact"></a><span data-ttu-id="6895b-103">Získání kontaktu podpory pro předplatné</span><span class="sxs-lookup"><span data-stu-id="6895b-103">Get a subscription's support contact</span></span>

<span data-ttu-id="6895b-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6895b-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6895b-105">Jak získat kontakt podpory předplatného</span><span class="sxs-lookup"><span data-stu-id="6895b-105">How to get a subscription's support contact.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6895b-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6895b-106">Prerequisites</span></span>

- <span data-ttu-id="6895b-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6895b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6895b-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="6895b-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6895b-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6895b-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6895b-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6895b-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6895b-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="6895b-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6895b-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="6895b-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6895b-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="6895b-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6895b-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6895b-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6895b-115">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="6895b-115">A subscription identifier.</span></span>

## <a name="c"></a><span data-ttu-id="6895b-116">C\#</span><span class="sxs-lookup"><span data-stu-id="6895b-116">C\#</span></span>

<span data-ttu-id="6895b-117">Pokud chcete získat kontakt podpory předplatného, začněte tím, že k identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="6895b-117">To get a subscription's support contact, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="6895b-118">Pak získejte rozhraní pro operace předplatného voláním metody [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="6895b-118">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="6895b-119">Dále pomocí vlastnosti [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) získejte rozhraní pro podporu kontaktních operací a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) nebo [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) která načte objekt [**SupportContact.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact)</span><span class="sxs-lookup"><span data-stu-id="6895b-119">Next, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

<span data-ttu-id="6895b-120">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6895b-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6895b-121">**Project:** SDK pro Partnerské centrum Samples **Class**: GetSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="6895b-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6895b-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="6895b-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6895b-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="6895b-123">Request syntax</span></span>

| <span data-ttu-id="6895b-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="6895b-124">Method</span></span>  | <span data-ttu-id="6895b-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="6895b-125">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6895b-126">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="6895b-126">**GET**</span></span> | <span data-ttu-id="6895b-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/podporaContact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6895b-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6895b-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="6895b-128">URI parameter</span></span>

<span data-ttu-id="6895b-129">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="6895b-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="6895b-130">Název</span><span class="sxs-lookup"><span data-stu-id="6895b-130">Name</span></span>            | <span data-ttu-id="6895b-131">Typ</span><span class="sxs-lookup"><span data-stu-id="6895b-131">Type</span></span>   | <span data-ttu-id="6895b-132">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="6895b-132">Required</span></span> | <span data-ttu-id="6895b-133">Popis</span><span class="sxs-lookup"><span data-stu-id="6895b-133">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="6895b-134">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="6895b-134">customer-id</span></span>     | <span data-ttu-id="6895b-135">řetězec</span><span class="sxs-lookup"><span data-stu-id="6895b-135">string</span></span> | <span data-ttu-id="6895b-136">Yes</span><span class="sxs-lookup"><span data-stu-id="6895b-136">Yes</span></span>      | <span data-ttu-id="6895b-137">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="6895b-137">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="6895b-138">id předplatného</span><span class="sxs-lookup"><span data-stu-id="6895b-138">subscription-id</span></span> | <span data-ttu-id="6895b-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="6895b-139">string</span></span> | <span data-ttu-id="6895b-140">Yes</span><span class="sxs-lookup"><span data-stu-id="6895b-140">Yes</span></span>      | <span data-ttu-id="6895b-141">Řetězec formátovaný identifikátorem GUID, který identifikuje zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="6895b-141">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6895b-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="6895b-142">Request headers</span></span>

<span data-ttu-id="6895b-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6895b-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6895b-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="6895b-144">Request body</span></span>

<span data-ttu-id="6895b-145">Žádné</span><span class="sxs-lookup"><span data-stu-id="6895b-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6895b-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="6895b-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6895b-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="6895b-147">REST response</span></span>

<span data-ttu-id="6895b-148">V případě úspěchu bude tělo odpovědi obsahovat prostředek [SupportContact.](subscription-resources.md#supportcontact)</span><span class="sxs-lookup"><span data-stu-id="6895b-148">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6895b-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="6895b-149">Response success and error codes</span></span>

<span data-ttu-id="6895b-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="6895b-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6895b-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="6895b-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6895b-152">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6895b-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6895b-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="6895b-153">Response example</span></span>

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
