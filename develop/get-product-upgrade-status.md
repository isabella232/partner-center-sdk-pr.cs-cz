---
title: Získat stav upgradu produktu pro zákazníka
description: Pomocí prostředku ProductUpgradeRequest můžete určit stav upgradu produktu pro zákazníka na novou produktovou řadu, jako je například z předplatného služby Microsoft Azure (MS-AZR-0145P) k plánu Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1819887d459ec72a48ea2b7a5a4121dc56718313
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766771"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="3a5a9-103">Získat stav upgradu produktu pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="3a5a9-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="3a5a9-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="3a5a9-104">**Applies to:**</span></span>

- <span data-ttu-id="3a5a9-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="3a5a9-105">Partner Center</span></span>

<span data-ttu-id="3a5a9-106">Pomocí prostředku [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) můžete získat stav upgradu na novou produktovou řadu.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="3a5a9-107">Tento prostředek se používá, když upgradujete zákazníka z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-107">This resource applies when you're upgrading a customer from an Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="3a5a9-108">Úspěšná žádost vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) .</span><span class="sxs-lookup"><span data-stu-id="3a5a9-108">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a5a9-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3a5a9-109">Prerequisites</span></span>

- <span data-ttu-id="3a5a9-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a9-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3a5a9-111">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-111">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="3a5a9-112">Použijte [zabezpečený model aplikace](enable-secure-app-model.md) při použití ověřování aplikací a uživatelů s rozhraními API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-112">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="3a5a9-113">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3a5a9-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3a5a9-114">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3a5a9-115">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3a5a9-116">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3a5a9-117">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="3a5a9-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3a5a9-118">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3a5a9-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3a5a9-119">Produktová řada.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-119">The product family.</span></span>

- <span data-ttu-id="3a5a9-120">ID upgradu žádosti o upgrade.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-120">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="3a5a9-121">C\#</span><span class="sxs-lookup"><span data-stu-id="3a5a9-121">C\#</span></span>

<span data-ttu-id="3a5a9-122">Pokud chcete zjistit, jestli má zákazník nárok na upgrade na plán Azure, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="3a5a9-122">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="3a5a9-123">Vytvořte objekt **ProductUpgradesRequest** a zadejte identifikátor zákazníka a "Azure" jako produktovou řadu.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-123">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="3a5a9-124">Použijte kolekci **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="3a5a9-124">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="3a5a9-125">Zavolejte metodu **ById** a předejte ji do **ID upgradu**.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-125">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="3a5a9-126">Zavolejte metodu **CheckStatus** a předejte ji do objektu **ProductUpgradesRequest** , který vrátí objekt **ProductUpgradeStatus** .</span><span class="sxs-lookup"><span data-stu-id="3a5a9-126">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="3a5a9-127">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="3a5a9-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3a5a9-128">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="3a5a9-128">Request syntax</span></span>

| <span data-ttu-id="3a5a9-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="3a5a9-129">Method</span></span>   | <span data-ttu-id="3a5a9-130">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3a5a9-130">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="3a5a9-131">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="3a5a9-131">**POST**</span></span> | <span data-ttu-id="3a5a9-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-ID}/status HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3a5a9-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3a5a9-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="3a5a9-133">URI parameter</span></span>

<span data-ttu-id="3a5a9-134">Použijte následující parametr dotazu k určení zákazníka, pro kterého se vám zobrazuje stav upgradu produktu.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-134">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="3a5a9-135">Název</span><span class="sxs-lookup"><span data-stu-id="3a5a9-135">Name</span></span>               | <span data-ttu-id="3a5a9-136">Typ</span><span class="sxs-lookup"><span data-stu-id="3a5a9-136">Type</span></span> | <span data-ttu-id="3a5a9-137">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3a5a9-137">Required</span></span> | <span data-ttu-id="3a5a9-138">Popis</span><span class="sxs-lookup"><span data-stu-id="3a5a9-138">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="3a5a9-139">**upgrade – ID**</span><span class="sxs-lookup"><span data-stu-id="3a5a9-139">**upgrade-id**</span></span> | <span data-ttu-id="3a5a9-140">Identifikátor GUID</span><span class="sxs-lookup"><span data-stu-id="3a5a9-140">GUID</span></span> | <span data-ttu-id="3a5a9-141">Yes</span><span class="sxs-lookup"><span data-stu-id="3a5a9-141">Yes</span></span> | <span data-ttu-id="3a5a9-142">Hodnota je identifikátor upgradu ve formátu GUID.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-142">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="3a5a9-143">Pomocí tohoto identifikátoru můžete zadat upgrade, který se má sledovat.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-143">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3a5a9-144">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="3a5a9-144">Request headers</span></span>

<span data-ttu-id="3a5a9-145">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a9-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3a5a9-146">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="3a5a9-146">Request body</span></span>

<span data-ttu-id="3a5a9-147">Tělo žádosti musí obsahovat prostředek [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .</span><span class="sxs-lookup"><span data-stu-id="3a5a9-147">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="3a5a9-148">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="3a5a9-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="3a5a9-149">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3a5a9-149">REST response</span></span>

<span data-ttu-id="3a5a9-150">V případě úspěchu tato metoda vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) v těle.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-150">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3a5a9-151">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="3a5a9-151">Response success and error codes</span></span>

<span data-ttu-id="3a5a9-152">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3a5a9-153">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="3a5a9-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3a5a9-154">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a9-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3a5a9-155">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="3a5a9-155">Response example</span></span>

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
