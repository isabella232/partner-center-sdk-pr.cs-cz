---
title: Vytvoření entity upgradu produktu pro zákazníka
description: Pomocí prostředku ProductUpgradeRequest můžete vytvořit entitu upgrade produktu pro upgrade zákazníka na danou produktovou řadu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45830033d93e0906eafc169cf04b997e2ff7c3d8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766689"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="6342e-103">Vytvoření entity upgradu produktu pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="6342e-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="6342e-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="6342e-104">**Applies to:**</span></span>

- <span data-ttu-id="6342e-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="6342e-105">Partner Center</span></span>

<span data-ttu-id="6342e-106">Můžete vytvořit entitu upgrade produktu pro upgrade zákazníka na určitou produktovou řadu (například plán Azure) pomocí prostředku **ProductUpgradeRequest** .</span><span class="sxs-lookup"><span data-stu-id="6342e-106">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6342e-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6342e-107">Prerequisites</span></span>

- <span data-ttu-id="6342e-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6342e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6342e-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="6342e-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="6342e-110">Použijte [zabezpečený model aplikace](enable-secure-app-model.md) při použití ověřování aplikací a uživatelů s rozhraními API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="6342e-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="6342e-111">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6342e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6342e-112">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="6342e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6342e-113">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="6342e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6342e-114">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="6342e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6342e-115">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="6342e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6342e-116">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6342e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6342e-117">Produktová řada, na kterou chcete provést upgrade zákazníka.</span><span class="sxs-lookup"><span data-stu-id="6342e-117">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="6342e-118">C\#</span><span class="sxs-lookup"><span data-stu-id="6342e-118">C\#</span></span>

<span data-ttu-id="6342e-119">Upgrade zákazníka na plán Azure:</span><span class="sxs-lookup"><span data-stu-id="6342e-119">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="6342e-120">Vytvořte objekt **ProductUpgradesRequest** a zadejte identifikátor zákazníka a "Azure" jako produktovou řadu.</span><span class="sxs-lookup"><span data-stu-id="6342e-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="6342e-121">Použijte kolekci **IAggregatePartner. ProductUpgrades** .</span><span class="sxs-lookup"><span data-stu-id="6342e-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="6342e-122">Zavolejte metodu **Create** a předejte objekt **ProductUpgradesRequest** , který vrátí řetězec **hlavičky umístění** .</span><span class="sxs-lookup"><span data-stu-id="6342e-122">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="6342e-123">Extrahujte **ID upgradu** z řetězce hlavičky umístění, který lze použít k [dotazování na stav upgradu](get-product-upgrade-status.md).</span><span class="sxs-lookup"><span data-stu-id="6342e-123">Extract the **upgrade-id** from the location header string which can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a><span data-ttu-id="6342e-124">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="6342e-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6342e-125">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="6342e-125">Request syntax</span></span>

| <span data-ttu-id="6342e-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="6342e-126">Method</span></span>   | <span data-ttu-id="6342e-127">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="6342e-127">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="6342e-128">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="6342e-128">**POST**</span></span> | <span data-ttu-id="6342e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6342e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="6342e-130">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="6342e-130">Request headers</span></span>

<span data-ttu-id="6342e-131">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6342e-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="6342e-132">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="6342e-132">Request body</span></span>

<span data-ttu-id="6342e-133">Tělo žádosti musí obsahovat prostředek [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) .</span><span class="sxs-lookup"><span data-stu-id="6342e-133">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="6342e-134">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="6342e-134">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a><span data-ttu-id="6342e-135">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="6342e-135">REST response</span></span>

<span data-ttu-id="6342e-136">V případě úspěchu odpověď obsahuje hlavičku **umístění** s identifikátorem URI, který lze použít k načtení stavu upgradu produktu.</span><span class="sxs-lookup"><span data-stu-id="6342e-136">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="6342e-137">Uložte tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.</span><span class="sxs-lookup"><span data-stu-id="6342e-137">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6342e-138">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="6342e-138">Response success and error codes</span></span>

<span data-ttu-id="6342e-139">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="6342e-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6342e-140">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="6342e-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6342e-141">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6342e-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6342e-142">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="6342e-142">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
