---
title: Aktualizace kontaktu podpory pro předplatné
description: Jak aktualizovat kontakt podpory předplatného na jednoho z prodejců s přidanou hodnotou partnera.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c89f91fc9e89384a7be1237c08d7a9a1cfe3164
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530357"
---
# <a name="update-a-subscriptions-support-contact"></a><span data-ttu-id="f76f5-103">Aktualizace kontaktu podpory pro předplatné</span><span class="sxs-lookup"><span data-stu-id="f76f5-103">Update a subscription's support contact</span></span>

<span data-ttu-id="f76f5-104">**Platí pro**: Partnerské centrum | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f76f5-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f76f5-105">Jak aktualizovat kontakt podpory předplatného na jednoho z prodejců s přidanou hodnotou partnera.</span><span class="sxs-lookup"><span data-stu-id="f76f5-105">How to update a subscription's support contact to one of the partner's value added resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f76f5-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f76f5-106">Prerequisites</span></span>

- <span data-ttu-id="f76f5-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f76f5-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f76f5-108">Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="f76f5-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f76f5-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f76f5-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f76f5-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="f76f5-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f76f5-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="f76f5-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f76f5-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="f76f5-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f76f5-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f76f5-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f76f5-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f76f5-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f76f5-115">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="f76f5-115">A subscription identifier.</span></span>

- <span data-ttu-id="f76f5-116">Informace o novém kontaktu podpory: identifikátor tenanta, Microsoft Partner Network identifikátor a název.</span><span class="sxs-lookup"><span data-stu-id="f76f5-116">Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name.</span></span> <span data-ttu-id="f76f5-117">Kontakt podpory musí být jedním z prodejců s přidanou hodnotou partnera.</span><span class="sxs-lookup"><span data-stu-id="f76f5-117">The support contact must be one of the partner's value added resellers.</span></span>

## <a name="c"></a><span data-ttu-id="f76f5-118">C\#</span><span class="sxs-lookup"><span data-stu-id="f76f5-118">C\#</span></span>

<span data-ttu-id="f76f5-119">Pokud chcete aktualizovat kontakt podpory předplatného, nejprve vytvořte instanci objektu [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) a naplňte ho novými hodnotami.</span><span class="sxs-lookup"><span data-stu-id="f76f5-119">To update a subscription's support contact, first instantiate and populate a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values.</span></span> <span data-ttu-id="f76f5-120">Pak k identifikaci zákazníka použijte metodu [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f76f5-120">Then use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="f76f5-121">Dále získejte rozhraní pro operace předplatného voláním metody [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="f76f5-121">Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="f76f5-122">Potom pomocí vlastnosti [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) získejte rozhraní pro podporu kontaktních operací.</span><span class="sxs-lookup"><span data-stu-id="f76f5-122">Then, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations.</span></span> <span data-ttu-id="f76f5-123">Nakonec zavolejte [**metodu Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) nebo [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) s vyplněnou objektem SupportContact a aktualizujte kontakt podpory.</span><span class="sxs-lookup"><span data-stu-id="f76f5-123">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

<span data-ttu-id="f76f5-124">**Ukázka:** [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f76f5-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f76f5-125">**Project:** SDK pro Partnerské centrum Samples **Class:** UpdateSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="f76f5-125">**Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f76f5-126">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="f76f5-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f76f5-127">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="f76f5-127">Request syntax</span></span>

| <span data-ttu-id="f76f5-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="f76f5-128">Method</span></span>  | <span data-ttu-id="f76f5-129">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f76f5-129">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f76f5-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="f76f5-130">**PUT**</span></span> | <span data-ttu-id="f76f5-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/subscriptions/{ID_předplatného}/podporaContact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f76f5-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f76f5-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f76f5-132">URI parameter</span></span>

<span data-ttu-id="f76f5-133">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="f76f5-133">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="f76f5-134">Název</span><span class="sxs-lookup"><span data-stu-id="f76f5-134">Name</span></span>            | <span data-ttu-id="f76f5-135">Typ</span><span class="sxs-lookup"><span data-stu-id="f76f5-135">Type</span></span>   | <span data-ttu-id="f76f5-136">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f76f5-136">Required</span></span> | <span data-ttu-id="f76f5-137">Popis</span><span class="sxs-lookup"><span data-stu-id="f76f5-137">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="f76f5-138">id zákazníka</span><span class="sxs-lookup"><span data-stu-id="f76f5-138">customer-id</span></span>     | <span data-ttu-id="f76f5-139">řetězec</span><span class="sxs-lookup"><span data-stu-id="f76f5-139">string</span></span> | <span data-ttu-id="f76f5-140">Yes</span><span class="sxs-lookup"><span data-stu-id="f76f5-140">Yes</span></span>      | <span data-ttu-id="f76f5-141">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="f76f5-141">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="f76f5-142">id předplatného</span><span class="sxs-lookup"><span data-stu-id="f76f5-142">subscription-id</span></span> | <span data-ttu-id="f76f5-143">řetězec</span><span class="sxs-lookup"><span data-stu-id="f76f5-143">string</span></span> | <span data-ttu-id="f76f5-144">Yes</span><span class="sxs-lookup"><span data-stu-id="f76f5-144">Yes</span></span>      | <span data-ttu-id="f76f5-145">Řetězec formátovaný identifikátorem GUID, který identifikuje zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="f76f5-145">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f76f5-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f76f5-146">Request headers</span></span>

<span data-ttu-id="f76f5-147">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f76f5-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f76f5-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f76f5-148">Request body</span></span>

<span data-ttu-id="f76f5-149">Do textu požadavku musíte zahrnout vyplněný prostředek [SupportContact.](subscription-resources.md#supportcontact)</span><span class="sxs-lookup"><span data-stu-id="f76f5-149">You must include a populated [SupportContact](subscription-resources.md#supportcontact) resource in the request body.</span></span> <span data-ttu-id="f76f5-150">Kontakt podpory musí být stávajícím prodejcem se vztahem k partnerovi.</span><span class="sxs-lookup"><span data-stu-id="f76f5-150">The support contact must be an existing reseller with a relationship to the partner.</span></span>

### <a name="request-example"></a><span data-ttu-id="f76f5-151">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f76f5-151">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="f76f5-152">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f76f5-152">REST response</span></span>

<span data-ttu-id="f76f5-153">V případě úspěchu bude tělo odpovědi obsahovat prostředek [SupportContact.](subscription-resources.md#supportcontact)</span><span class="sxs-lookup"><span data-stu-id="f76f5-153">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f76f5-154">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="f76f5-154">Response success and error codes</span></span>

<span data-ttu-id="f76f5-155">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f76f5-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f76f5-156">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="f76f5-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f76f5-157">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f76f5-157">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f76f5-158">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f76f5-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

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
