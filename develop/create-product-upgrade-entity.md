---
title: Vytvoření entity upgradu produktu pro zákazníka
description: Pomocí prostředku ProductUpgradeRequest můžete vytvořit entitu upgradu produktu a upgradovat zákazníka na danou produktové rodinu.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4e346b7f5294a8847047c85115d8c80f34eaca84
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973397"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="937e5-103">Vytvoření entity upgradu produktu pro zákazníka</span><span class="sxs-lookup"><span data-stu-id="937e5-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="937e5-104">Pokud chcete upgradovat zákazníka na danou produktové rodinu (například plán Azure), můžete vytvořit entitu upgradu produktu pomocí prostředku **ProductUpgradeRequest.**</span><span class="sxs-lookup"><span data-stu-id="937e5-104">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="937e5-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="937e5-105">Prerequisites</span></span>

- <span data-ttu-id="937e5-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="937e5-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="937e5-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="937e5-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="937e5-108">Při použití [ověřování aplikací a uživatelů](enable-secure-app-model.md) s využitím rozhraní API pro Partnerské centrum aplikací postupujte podle modelu zabezpečené aplikace.</span><span class="sxs-lookup"><span data-stu-id="937e5-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="937e5-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="937e5-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="937e5-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="937e5-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="937e5-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="937e5-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="937e5-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="937e5-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="937e5-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="937e5-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="937e5-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="937e5-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="937e5-115">Produktová skupina, na kterou chcete upgradovat zákazníka.</span><span class="sxs-lookup"><span data-stu-id="937e5-115">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="937e5-116">C\#</span><span class="sxs-lookup"><span data-stu-id="937e5-116">C\#</span></span>

<span data-ttu-id="937e5-117">Upgrade zákazníka na plán Azure:</span><span class="sxs-lookup"><span data-stu-id="937e5-117">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="937e5-118">Vytvořte objekt **ProductUpgradesRequest** a jako produktové skupiny zadejte identifikátor zákazníka a "Azure".</span><span class="sxs-lookup"><span data-stu-id="937e5-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="937e5-119">Použijte **kolekci IAggregatePartner.ProductUpgrades.**</span><span class="sxs-lookup"><span data-stu-id="937e5-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="937e5-120">Zavolejte **metodu Create** a předejte objekt **ProductUpgradesRequest,** který vrátí **řetězec hlavičky** umístění.</span><span class="sxs-lookup"><span data-stu-id="937e5-120">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="937e5-121">**Extrahujte id upgradu** z řetězce hlavičky umístění, který můžete použít k [dotazování na stav upgradu.](get-product-upgrade-status.md)</span><span class="sxs-lookup"><span data-stu-id="937e5-121">Extract the **upgrade-id** from the location header string that can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="937e5-122">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="937e5-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="937e5-123">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="937e5-123">Request syntax</span></span>

| <span data-ttu-id="937e5-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="937e5-124">Method</span></span>   | <span data-ttu-id="937e5-125">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="937e5-125">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="937e5-126">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="937e5-126">**POST**</span></span> | <span data-ttu-id="937e5-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="937e5-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="937e5-128">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="937e5-128">Request headers</span></span>

<span data-ttu-id="937e5-129">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="937e5-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="937e5-130">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="937e5-130">Request body</span></span>

<span data-ttu-id="937e5-131">Text požadavku musí obsahovat prostředek [ProductUpgradeRequest.](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="937e5-131">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="937e5-132">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="937e5-132">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="937e5-133">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="937e5-133">REST response</span></span>

<span data-ttu-id="937e5-134">V případě úspěchu odpověď obsahuje **hlavičku Location** s identifikátorem URI, který lze použít k načtení stavu upgradu produktu.</span><span class="sxs-lookup"><span data-stu-id="937e5-134">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="937e5-135">Uložte si tento identifikátor URI pro použití s dalšími souvisejícími rozhraními REST API.</span><span class="sxs-lookup"><span data-stu-id="937e5-135">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="937e5-136">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="937e5-136">Response success and error codes</span></span>

<span data-ttu-id="937e5-137">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="937e5-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="937e5-138">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="937e5-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="937e5-139">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="937e5-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="937e5-140">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="937e5-140">Response example</span></span>

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
