---
title: Odmítnout přenos
description: Způsob odmítnutí přenosu předplatných pro zákazníka.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e4a182ff92a21cf72ca1c2da9de7e211b433725f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766744"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="76844-103">Odmítnout přenos</span><span class="sxs-lookup"><span data-stu-id="76844-103">Reject a transfer</span></span>

<span data-ttu-id="76844-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="76844-104">**Applies to:**</span></span>

- <span data-ttu-id="76844-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="76844-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76844-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="76844-106">Prerequisites</span></span>

- <span data-ttu-id="76844-107">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="76844-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="76844-108">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="76844-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="76844-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="76844-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="76844-110">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="76844-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="76844-111">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="76844-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="76844-112">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="76844-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="76844-113">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="76844-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="76844-114">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="76844-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="76844-115">Identifikátor přenosu pro existující přenos.</span><span class="sxs-lookup"><span data-stu-id="76844-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="76844-116">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="76844-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="76844-117">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="76844-117">Request syntax</span></span>

| <span data-ttu-id="76844-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="76844-118">Method</span></span>   | <span data-ttu-id="76844-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="76844-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="76844-120">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="76844-120">**PATCH**</span></span> | <span data-ttu-id="76844-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers/{Transfer-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="76844-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="76844-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="76844-122">URI parameter</span></span>

<span data-ttu-id="76844-123">Použijte následující parametr cesty k identifikaci zákazníka a určení přenosu, který chcete přijmout.</span><span class="sxs-lookup"><span data-stu-id="76844-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="76844-124">Název</span><span class="sxs-lookup"><span data-stu-id="76844-124">Name</span></span>            | <span data-ttu-id="76844-125">Typ</span><span class="sxs-lookup"><span data-stu-id="76844-125">Type</span></span>     | <span data-ttu-id="76844-126">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="76844-126">Required</span></span> | <span data-ttu-id="76844-127">Popis</span><span class="sxs-lookup"><span data-stu-id="76844-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="76844-128">**ID zákazníka**</span><span class="sxs-lookup"><span data-stu-id="76844-128">**customer-id**</span></span> | <span data-ttu-id="76844-129">řetězec</span><span class="sxs-lookup"><span data-stu-id="76844-129">string</span></span>   | <span data-ttu-id="76844-130">Yes</span><span class="sxs-lookup"><span data-stu-id="76844-130">Yes</span></span>      | <span data-ttu-id="76844-131">Identifikátor zákazníka, který je ve formátu identifikátoru GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="76844-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="76844-132">**ID přenosu**</span><span class="sxs-lookup"><span data-stu-id="76844-132">**transfer-id**</span></span> | <span data-ttu-id="76844-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="76844-133">string</span></span>   | <span data-ttu-id="76844-134">Yes</span><span class="sxs-lookup"><span data-stu-id="76844-134">Yes</span></span>      | <span data-ttu-id="76844-135">Identifikátor ID přenosu, ve formátu GUID, který identifikuje přenos.</span><span class="sxs-lookup"><span data-stu-id="76844-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="76844-136">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="76844-136">Request headers</span></span>

<span data-ttu-id="76844-137">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="76844-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="76844-138">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="76844-138">Request body</span></span>

<span data-ttu-id="76844-139">Tato tabulka popisuje vlastnosti [TransferEntity](transfer-entity-resources.md) v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="76844-139">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="76844-140">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="76844-140">Property</span></span>              | <span data-ttu-id="76844-141">Typ</span><span class="sxs-lookup"><span data-stu-id="76844-141">Type</span></span>          | <span data-ttu-id="76844-142">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="76844-142">Required</span></span>  | <span data-ttu-id="76844-143">Popis</span><span class="sxs-lookup"><span data-stu-id="76844-143">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="76844-144">id</span><span class="sxs-lookup"><span data-stu-id="76844-144">id</span></span>                    | <span data-ttu-id="76844-145">řetězec</span><span class="sxs-lookup"><span data-stu-id="76844-145">string</span></span>        | <span data-ttu-id="76844-146">No</span><span class="sxs-lookup"><span data-stu-id="76844-146">No</span></span>    | <span data-ttu-id="76844-147">TransferEntity identifikátor, který je poskytnut po úspěšném vytvoření transferEntity.</span><span class="sxs-lookup"><span data-stu-id="76844-147">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="76844-148">status</span><span class="sxs-lookup"><span data-stu-id="76844-148">status</span></span>                | <span data-ttu-id="76844-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="76844-149">string</span></span>        | <span data-ttu-id="76844-150">No</span><span class="sxs-lookup"><span data-stu-id="76844-150">No</span></span>    | <span data-ttu-id="76844-151">Stav transferEntity.</span><span class="sxs-lookup"><span data-stu-id="76844-151">The status of the transferEntity.</span></span> <span data-ttu-id="76844-152">Pokud chcete přenos odmítnout, hodnota se nastaví jako zamítnout.</span><span class="sxs-lookup"><span data-stu-id="76844-152">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="76844-153">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="76844-153">Request example</span></span>

```http
PATCH /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
Connection: keep-alive
Content-Length: 63

{"id":"ac4a9d22-ba07-444e-890f-cfe084eed498","status":"reject"}

```

## <a name="rest-response"></a><span data-ttu-id="76844-154">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="76844-154">REST response</span></span>

<span data-ttu-id="76844-155">V případě úspěchu tato metoda vrátí naplněný prostředek [TransferEntity](transfer-entity-resources.md) v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="76844-155">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="76844-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="76844-156">Response success and error codes</span></span>

<span data-ttu-id="76844-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="76844-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="76844-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="76844-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="76844-159">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="76844-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="76844-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="76844-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1069
Content-Type: application/json; charset=utf-8
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
X-Locale: en-US
Date: Fri, 27 Mar 2020 17:50:33 GMT

{
  "id": "ac4a9d22-ba07-444e-890f-cfe084eed498",
  "status": "Reject",
  "createdTime": "2020-03-25T22:05:25.1057725Z",
  "lastModifiedTime": "2020-03-27T17:50:32Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "01a7548d-1136-4cf0-ba9a-300f921ffb22",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "1151B8CE-125C-49D7-8C48-E62FC9101B77",
      "offerId": "13D32E13-A1B0-400D-96C0-4EAAA14DCED5",
      "billingCycle": "monthly",
      "friendlyName": "Dynamics 365 for Supply Chain Management Attach to Qualifying Dynamics 365 Base Offer (Qualified Offer)",
      "quantity": 20,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "TransferEntity"
  }
}
```
