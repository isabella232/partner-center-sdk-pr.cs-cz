---
title: Získat stav upgradu produktu pro zákazníka
description: pomocí prostředku ProductUpgradeRequest můžete určit stav upgradu produktu pro zákazníka na novou produktovou řadu, jako je například z předplatného služby Microsoft Azure (MS-AZR-0145P) k plánu Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 03d925dd0fae987226ad1f8e71fad380ba144b83
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445557"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="f5091-103">Získat stav upgradu produktu pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="f5091-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="f5091-104">Pomocí prostředku [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) můžete získat stav upgradu na novou produktovou řadu.</span><span class="sxs-lookup"><span data-stu-id="f5091-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="f5091-105">tento prostředek se použije, když upgradujete zákazníka z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure.</span><span class="sxs-lookup"><span data-stu-id="f5091-105">This resource applies when you're upgrading a customer from a Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="f5091-106">Úspěšná žádost vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) .</span><span class="sxs-lookup"><span data-stu-id="f5091-106">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5091-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f5091-107">Prerequisites</span></span>

- <span data-ttu-id="f5091-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f5091-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f5091-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="f5091-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="f5091-110">Použijte [zabezpečený model aplikace](enable-secure-app-model.md) při použití ověřování aplikací a uživatelů s rozhraními API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="f5091-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="f5091-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f5091-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f5091-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="f5091-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f5091-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="f5091-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f5091-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="f5091-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f5091-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="f5091-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f5091-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f5091-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f5091-117">Produktová řada.</span><span class="sxs-lookup"><span data-stu-id="f5091-117">The product family.</span></span>

- <span data-ttu-id="f5091-118">ID upgradu žádosti o upgrade.</span><span class="sxs-lookup"><span data-stu-id="f5091-118">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="f5091-119">C\#</span><span class="sxs-lookup"><span data-stu-id="f5091-119">C\#</span></span>

<span data-ttu-id="f5091-120">Pokud chcete zjistit, jestli má zákazník nárok na upgrade na plán Azure, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="f5091-120">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="f5091-121">Vytvořte objekt **ProductUpgradesRequest** a zadejte identifikátor zákazníka a "Azure" jako produktovou řadu.</span><span class="sxs-lookup"><span data-stu-id="f5091-121">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="f5091-122">Použijte kolekci **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="f5091-122">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="f5091-123">Zavolejte metodu **ById** a předejte ji do **ID upgradu**.</span><span class="sxs-lookup"><span data-stu-id="f5091-123">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="f5091-124">Zavolejte metodu **CheckStatus** a předejte ji do objektu **ProductUpgradesRequest** , který vrátí objekt **ProductUpgradeStatus** .</span><span class="sxs-lookup"><span data-stu-id="f5091-124">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a><span data-ttu-id="f5091-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="f5091-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f5091-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="f5091-126">Request syntax</span></span>

| <span data-ttu-id="f5091-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="f5091-127">Method</span></span>   | <span data-ttu-id="f5091-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f5091-128">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f5091-129">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="f5091-129">**POST**</span></span> | <span data-ttu-id="f5091-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-ID}/status HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f5091-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f5091-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f5091-131">URI parameter</span></span>

<span data-ttu-id="f5091-132">Použijte následující parametr dotazu k určení zákazníka, pro kterého se vám zobrazuje stav upgradu produktu.</span><span class="sxs-lookup"><span data-stu-id="f5091-132">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="f5091-133">Název</span><span class="sxs-lookup"><span data-stu-id="f5091-133">Name</span></span>               | <span data-ttu-id="f5091-134">Typ</span><span class="sxs-lookup"><span data-stu-id="f5091-134">Type</span></span> | <span data-ttu-id="f5091-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f5091-135">Required</span></span> | <span data-ttu-id="f5091-136">Popis</span><span class="sxs-lookup"><span data-stu-id="f5091-136">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="f5091-137">**upgrade – ID**</span><span class="sxs-lookup"><span data-stu-id="f5091-137">**upgrade-id**</span></span> | <span data-ttu-id="f5091-138">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="f5091-138">GUID</span></span> | <span data-ttu-id="f5091-139">Yes</span><span class="sxs-lookup"><span data-stu-id="f5091-139">Yes</span></span> | <span data-ttu-id="f5091-140">Hodnota je identifikátor upgradu ve formátu GUID.</span><span class="sxs-lookup"><span data-stu-id="f5091-140">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="f5091-141">Pomocí tohoto identifikátoru můžete zadat upgrade, který se má sledovat.</span><span class="sxs-lookup"><span data-stu-id="f5091-141">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f5091-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f5091-142">Request headers</span></span>

<span data-ttu-id="f5091-143">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f5091-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f5091-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f5091-144">Request body</span></span>

<span data-ttu-id="f5091-145">Tělo žádosti musí obsahovat prostředek [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .</span><span class="sxs-lookup"><span data-stu-id="f5091-145">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="f5091-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f5091-146">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a><span data-ttu-id="f5091-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f5091-147">REST response</span></span>

<span data-ttu-id="f5091-148">V případě úspěchu tato metoda vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) v těle.</span><span class="sxs-lookup"><span data-stu-id="f5091-148">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f5091-149">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="f5091-149">Response success and error codes</span></span>

<span data-ttu-id="f5091-150">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f5091-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f5091-151">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="f5091-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f5091-152">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f5091-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f5091-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f5091-153">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
