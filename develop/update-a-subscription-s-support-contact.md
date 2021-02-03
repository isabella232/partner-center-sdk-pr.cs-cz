---
title: Aktualizace kontaktu podpory pro předplatné
description: Jak aktualizovat kontakt na podporu pro předplatné na jednu z hodnot partnera, který přidal prodejce.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8c6b658cfe6e14c75b0c06b177920ce3eb1b4ed
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766947"
---
# <a name="update-a-subscriptions-support-contact"></a><span data-ttu-id="ddff4-103">Aktualizace kontaktu podpory pro předplatné</span><span class="sxs-lookup"><span data-stu-id="ddff4-103">Update a subscription's support contact</span></span>

<span data-ttu-id="ddff4-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="ddff4-104">**Applies To**</span></span>

- <span data-ttu-id="ddff4-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="ddff4-105">Partner Center</span></span>
- <span data-ttu-id="ddff4-106">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="ddff4-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ddff4-107">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ddff4-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ddff4-108">Jak aktualizovat kontakt na podporu pro předplatné na jednu z hodnot partnera, který přidal prodejce.</span><span class="sxs-lookup"><span data-stu-id="ddff4-108">How to update a subscription's support contact to one of the partner's value added resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddff4-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ddff4-109">Prerequisites</span></span>

- <span data-ttu-id="ddff4-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ddff4-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ddff4-111">Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ddff4-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="ddff4-112">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ddff4-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ddff4-113">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="ddff4-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ddff4-114">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="ddff4-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ddff4-115">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="ddff4-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ddff4-116">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="ddff4-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ddff4-117">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ddff4-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ddff4-118">Identifikátor předplatného.</span><span class="sxs-lookup"><span data-stu-id="ddff4-118">A subscription identifier.</span></span>

- <span data-ttu-id="ddff4-119">Informace o novém kontaktu podpory: identifikátor tenanta, identifikátor Microsoft Partner Network a název.</span><span class="sxs-lookup"><span data-stu-id="ddff4-119">Information about the new support contact: tenant identifier, Microsoft Partner Network identifier, and name.</span></span> <span data-ttu-id="ddff4-120">Kontakt na podporu musí být jednou z hodnot partnera, který přidal prodejce.</span><span class="sxs-lookup"><span data-stu-id="ddff4-120">The support contact must be one of the partner's value added resellers.</span></span>

## <a name="c"></a><span data-ttu-id="ddff4-121">C\#</span><span class="sxs-lookup"><span data-stu-id="ddff4-121">C\#</span></span>

<span data-ttu-id="ddff4-122">Chcete-li aktualizovat kontakt podpory předplatného, nejprve vytvořte instanci a naplňte objekt [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) novými hodnotami.</span><span class="sxs-lookup"><span data-stu-id="ddff4-122">To update a subscription's support contact, first instantiate and populate a [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) object with the new values.</span></span> <span data-ttu-id="ddff4-123">Potom k identifikaci zákazníka použijte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ddff4-123">Then use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ddff4-124">Dále Získejte rozhraní pro operace předplatného voláním metody [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) s ID předplatného.</span><span class="sxs-lookup"><span data-stu-id="ddff4-124">Next, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="ddff4-125">Pak pomocí vlastnosti [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) Získejte rozhraní pro podporu operací kontaktů.</span><span class="sxs-lookup"><span data-stu-id="ddff4-125">Then, use the [**SupportContact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) property to obtain an interface to support contact operations.</span></span> <span data-ttu-id="ddff4-126">Nakonec zavolejte metodu [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) nebo [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) s naplněným objektem SupportContact, abyste aktualizovali kontakt na podporu.</span><span class="sxs-lookup"><span data-stu-id="ddff4-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) method with the populated SupportContact object to update the support contact.</span></span>

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

<span data-ttu-id="ddff4-127">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ddff4-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ddff4-128">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: UpdateSubscriptionSupportContact.cs</span><span class="sxs-lookup"><span data-stu-id="ddff4-128">**Project**: Partner Center SDK Samples **Class**: UpdateSubscriptionSupportContact.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ddff4-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ddff4-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ddff4-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ddff4-130">Request syntax</span></span>

| <span data-ttu-id="ddff4-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="ddff4-131">Method</span></span>  | <span data-ttu-id="ddff4-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ddff4-132">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ddff4-133">**PUT**</span><span class="sxs-lookup"><span data-stu-id="ddff4-133">**PUT**</span></span> | <span data-ttu-id="ddff4-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/supportcontact HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ddff4-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ddff4-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="ddff4-135">URI parameter</span></span>

<span data-ttu-id="ddff4-136">K identifikaci zákazníka a předplatného použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="ddff4-136">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="ddff4-137">Název</span><span class="sxs-lookup"><span data-stu-id="ddff4-137">Name</span></span>            | <span data-ttu-id="ddff4-138">Typ</span><span class="sxs-lookup"><span data-stu-id="ddff4-138">Type</span></span>   | <span data-ttu-id="ddff4-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ddff4-139">Required</span></span> | <span data-ttu-id="ddff4-140">Popis</span><span class="sxs-lookup"><span data-stu-id="ddff4-140">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="ddff4-141">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="ddff4-141">customer-id</span></span>     | <span data-ttu-id="ddff4-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="ddff4-142">string</span></span> | <span data-ttu-id="ddff4-143">Yes</span><span class="sxs-lookup"><span data-stu-id="ddff4-143">Yes</span></span>      | <span data-ttu-id="ddff4-144">Řetězec ve formátu GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ddff4-144">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="ddff4-145">ID předplatného</span><span class="sxs-lookup"><span data-stu-id="ddff4-145">subscription-id</span></span> | <span data-ttu-id="ddff4-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="ddff4-146">string</span></span> | <span data-ttu-id="ddff4-147">Yes</span><span class="sxs-lookup"><span data-stu-id="ddff4-147">Yes</span></span>      | <span data-ttu-id="ddff4-148">Řetězec ve formátu GUID, který identifikuje zkušební předplatné.</span><span class="sxs-lookup"><span data-stu-id="ddff4-148">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ddff4-149">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ddff4-149">Request headers</span></span>

<span data-ttu-id="ddff4-150">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ddff4-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ddff4-151">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ddff4-151">Request body</span></span>

<span data-ttu-id="ddff4-152">Do textu žádosti musíte zahrnout naplněný prostředek [SupportContact](subscription-resources.md#supportcontact) .</span><span class="sxs-lookup"><span data-stu-id="ddff4-152">You must include a populated [SupportContact](subscription-resources.md#supportcontact) resource in the request body.</span></span> <span data-ttu-id="ddff4-153">Kontakt na podporu musí být stávající prodejce s vztahem k partnerovi.</span><span class="sxs-lookup"><span data-stu-id="ddff4-153">The support contact must be an existing reseller with a relationship to the partner.</span></span>

### <a name="request-example"></a><span data-ttu-id="ddff4-154">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ddff4-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ddff4-155">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ddff4-155">REST response</span></span>

<span data-ttu-id="ddff4-156">V případě úspěchu obsahuje tělo odpovědi prostředek [SupportContact](subscription-resources.md#supportcontact) .</span><span class="sxs-lookup"><span data-stu-id="ddff4-156">If successful, the response body contains the [SupportContact](subscription-resources.md#supportcontact) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ddff4-157">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ddff4-157">Response success and error codes</span></span>

<span data-ttu-id="ddff4-158">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ddff4-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ddff4-159">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ddff4-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ddff4-160">Úplný seznam najdete v tématu [kódy chyb partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ddff4-160">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ddff4-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ddff4-161">Response example</span></span>

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
