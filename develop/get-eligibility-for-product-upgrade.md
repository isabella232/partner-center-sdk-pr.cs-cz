---
title: Projděte si nárok zákazníka na upgrade na plán Azure
description: Prostředek ProductUpgradeRequest můžete použít k vrácení prostředku ProductUpgradesEligibility, abyste zjistili, jestli má zákazník nárok na upgrade z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766659"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="4e86c-103">Projděte si nárok zákazníka na upgrade na plán Azure</span><span class="sxs-lookup"><span data-stu-id="4e86c-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="4e86c-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="4e86c-104">**Applies to:**</span></span>

- <span data-ttu-id="4e86c-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="4e86c-105">Partner Center</span></span>

<span data-ttu-id="4e86c-106">Pomocí prostředku [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) můžete ověřit, jestli má zákazník nárok na upgrade na plán Azure z předplatného služby Microsoft Azure (MS-AZR-0145P). Tato metoda vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) s nárokem na upgrade produktu zákazníka.</span><span class="sxs-lookup"><span data-stu-id="4e86c-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e86c-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4e86c-107">Prerequisites</span></span>

- <span data-ttu-id="4e86c-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4e86c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4e86c-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="4e86c-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="4e86c-110">Použijte [zabezpečený model aplikace](enable-secure-app-model.md) při použití ověřování aplikací a uživatelů s rozhraními API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="4e86c-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="4e86c-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4e86c-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4e86c-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="4e86c-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4e86c-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="4e86c-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4e86c-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="4e86c-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4e86c-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="4e86c-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4e86c-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4e86c-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4e86c-117">Produktová řada.</span><span class="sxs-lookup"><span data-stu-id="4e86c-117">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="4e86c-118">C\#</span><span class="sxs-lookup"><span data-stu-id="4e86c-118">C\#</span></span>

<span data-ttu-id="4e86c-119">Pokud chcete zjistit, jestli má zákazník nárok na upgrade na plán Azure, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="4e86c-119">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="4e86c-120">Vytvořte objekt **ProductUpgradesRequest** a zadejte identifikátor zákazníka a "Azure" jako produktovou řadu.</span><span class="sxs-lookup"><span data-stu-id="4e86c-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="4e86c-121">Použijte kolekci **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="4e86c-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="4e86c-122">Zavolejte metodu **CheckEligibility** a předejte ji do objektu **ProductUpgradesRequest** , který vrátí objekt **ProductUpgradesEligibility** .</span><span class="sxs-lookup"><span data-stu-id="4e86c-122">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a><span data-ttu-id="4e86c-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="4e86c-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4e86c-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="4e86c-124">Request syntax</span></span>

| <span data-ttu-id="4e86c-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="4e86c-125">Method</span></span>   | <span data-ttu-id="4e86c-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="4e86c-126">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="4e86c-127">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="4e86c-127">**POST**</span></span> | <span data-ttu-id="4e86c-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4e86c-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4e86c-129">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="4e86c-129">Request headers</span></span>

<span data-ttu-id="4e86c-130">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4e86c-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4e86c-131">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="4e86c-131">Request body</span></span>

<span data-ttu-id="4e86c-132">Tělo žádosti musí obsahovat prostředek [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .</span><span class="sxs-lookup"><span data-stu-id="4e86c-132">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="4e86c-133">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="4e86c-133">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
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
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
}
```

## <a name="rest-response"></a><span data-ttu-id="4e86c-134">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="4e86c-134">REST response</span></span>

<span data-ttu-id="4e86c-135">V případě úspěchu tato metoda vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) v těle.</span><span class="sxs-lookup"><span data-stu-id="4e86c-135">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4e86c-136">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="4e86c-136">Response success and error codes</span></span>

<span data-ttu-id="4e86c-137">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="4e86c-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4e86c-138">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="4e86c-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4e86c-139">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4e86c-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4e86c-140">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="4e86c-140">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
