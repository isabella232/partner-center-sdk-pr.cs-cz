---
title: Přijetí převodu předplatných
description: Zjistěte, jak pomocí Partnerské centrum REST API přijmout převod předplatných pro zákazníka. Zahrnuje syntaxi požadavku REST, hlavičky a odpovědi REST.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 762f2106d6173e352bec11936c96bc3a9c9f89cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025747"
---
# <a name="accept-a-transfer-of-subscriptions-for-a-customer-using-partner-center-rest-apis"></a><span data-ttu-id="5f9d4-104">Přijetí převodu předplatných pro zákazníka pomocí Partnerské centrum rozhraní REST API</span><span class="sxs-lookup"><span data-stu-id="5f9d4-104">Accept a transfer of subscriptions for a customer using Partner Center REST APIs</span></span>

<span data-ttu-id="5f9d4-105">Tento článek popisuje, jak pomocí REST API v Partnerské centrum přijmout převod předplatných pro zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-105">This article covers how to use the REST API in Partner Center to accept the transfer of subscriptions for a customer.</span></span> <span data-ttu-id="5f9d4-106">Příklad obsahuje syntaxi REST, hlavičky a odpovědi REST.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-106">The example includes REST syntax, headers, and REST responses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f9d4-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5f9d4-107">Prerequisites</span></span>

- <span data-ttu-id="5f9d4-108">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5f9d4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5f9d4-109">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5f9d4-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5f9d4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5f9d4-111">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="5f9d4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5f9d4-112">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5f9d4-113">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5f9d4-114">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5f9d4-115">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5f9d4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5f9d4-116">Identifikátor přenosu pro existující přenos.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-116">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5f9d4-117">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="5f9d4-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5f9d4-118">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="5f9d4-118">Request syntax</span></span>

| <span data-ttu-id="5f9d4-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="5f9d4-119">Method</span></span>   | <span data-ttu-id="5f9d4-120">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5f9d4-120">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5f9d4-121">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-121">**POST**</span></span> | <span data-ttu-id="5f9d4-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_zákazníka}/transfers/{ID_přenosu}/přijmout HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5f9d4-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id}/accept HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="5f9d4-123">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5f9d4-123">URI parameter</span></span>

<span data-ttu-id="5f9d4-124">Pomocí následujícího parametru cesty identifikujte zákazníka a určete přenos, který se má přijmout.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-124">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="5f9d4-125">Název</span><span class="sxs-lookup"><span data-stu-id="5f9d4-125">Name</span></span>            | <span data-ttu-id="5f9d4-126">Typ</span><span class="sxs-lookup"><span data-stu-id="5f9d4-126">Type</span></span>     | <span data-ttu-id="5f9d4-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="5f9d4-127">Required</span></span> | <span data-ttu-id="5f9d4-128">Popis</span><span class="sxs-lookup"><span data-stu-id="5f9d4-128">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="5f9d4-129">**id zákazníka**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-129">**customer-id**</span></span> | <span data-ttu-id="5f9d4-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="5f9d4-130">string</span></span>   | <span data-ttu-id="5f9d4-131">Yes</span><span class="sxs-lookup"><span data-stu-id="5f9d4-131">Yes</span></span>      | <span data-ttu-id="5f9d4-132">Identifikátor GUID naformátovaný jako customer-id, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-132">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="5f9d4-133">**id přenosu**</span><span class="sxs-lookup"><span data-stu-id="5f9d4-133">**transfer-id**</span></span> | <span data-ttu-id="5f9d4-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="5f9d4-134">string</span></span>   | <span data-ttu-id="5f9d4-135">Yes</span><span class="sxs-lookup"><span data-stu-id="5f9d4-135">Yes</span></span>      | <span data-ttu-id="5f9d4-136">Identifikátor GUID formátovaný jako transfer-id, který identifikuje přenos.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-136">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="5f9d4-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5f9d4-137">Request headers</span></span>

<span data-ttu-id="5f9d4-138">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5f9d4-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="5f9d4-139">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="5f9d4-139">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/aa2bddb6-9cc8-4949-80fe-a37d5e0a13ba/accept HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0

```

## <a name="rest-response"></a><span data-ttu-id="5f9d4-140">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5f9d4-140">REST response</span></span>

<span data-ttu-id="5f9d4-141">V případě úspěchu tato metoda vrátí naplněný prostředek [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) v textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-141">If successful, this method returns the populated [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5f9d4-142">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="5f9d4-142">Response success and error codes</span></span>

<span data-ttu-id="5f9d4-143">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5f9d4-144">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="5f9d4-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5f9d4-145">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5f9d4-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5f9d4-146">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="5f9d4-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3389
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Date: Wed, 25 Mar 2020 19:13:06 GMT

{
  "orders": [
    {
      "id": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "alternateId": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "5344C201-3099-44E5-B333-C3EB0401EDE0",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Customer Engagement Plan (36 mo)",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:23.183+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6IjIxYjkyMzkzLWZmY2UtNGJjNy04N2M1LTYyY2ZhODk3ZDhmOSIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    },
    {
      "id": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "alternateId": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "1A90EE13-2CB4-4785-BB0F-542813F00A37",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Business Central Essential",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:34.59+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6Ijc0MTRiOGVhLWMxNjctNGNjNC1iYzhlLWI0M2VmYzE3N2E0NiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    }
  ],
  "transferErrors": [
    {
      "transferGroupId": "1",
      "lineItems": [
        {
          "id": 1,
          "subscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "entitlementId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "offerId": "A4179D30-CC09-49F0-977E-DC2CB70B874F",
          "friendlyName": "Project Online Essentials",
          "quantity": 1,
          "transferGroupId": "1",
          "addonItems": [ ],
          "partnerIdOnRecord": "5139005",
          "billingCycle": "annual",
          "sourceSubscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A"
        }
      ],
      "code": 900103,
      "description": "Subscription SyncState must be SyncComplete for the Subscription to be a source in a Subscription Ownership Transfer. Subscription: 637ff8f6-d842-4573-8da8-89765356cd1a, current state: None",
      "attributes": {
        "objectType": "TransferError"
      }
    }
  ],
  "attributes": {
    "objectType": "TransferSubmitResult"
  }
}
```
