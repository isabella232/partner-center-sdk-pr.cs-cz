---
title: Kontrola způsobilosti zákazníka k upgradu na plán Azure
description: Pomocí prostředku ProductUpgradeRequest můžete vrátit prostředek ProductUpgradesEligibility a zjistit, jestli má zákazník nárok na upgrade z předplatného Microsoft Azure (MS-AZR-0145P) na plán Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 34a20611c7d92042b5432c5ffb3ba4702d77e0c2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446254"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="0379e-103">Kontrola způsobilosti zákazníka k upgradu na plán Azure</span><span class="sxs-lookup"><span data-stu-id="0379e-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="0379e-104">Pomocí prostředku [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) můžete zkontrolovat, jestli má zákazník nárok na upgrade na plán Azure z předplatného Microsoft Azure (MS-AZR-0145P). Tato metoda vrátí prostředek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) s nárokem zákazníka na upgrade produktu.</span><span class="sxs-lookup"><span data-stu-id="0379e-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0379e-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0379e-105">Prerequisites</span></span>

- <span data-ttu-id="0379e-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0379e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0379e-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="0379e-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="0379e-108">Při použití [ověřování aplikací a uživatelů](enable-secure-app-model.md) s využitím rozhraní API pro Partnerské centrum aplikací postupujte podle modelu zabezpečené aplikace.</span><span class="sxs-lookup"><span data-stu-id="0379e-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="0379e-109">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0379e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0379e-110">Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0379e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0379e-111">V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.**</span><span class="sxs-lookup"><span data-stu-id="0379e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0379e-112">V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.**</span><span class="sxs-lookup"><span data-stu-id="0379e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0379e-113">Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka.</span><span class="sxs-lookup"><span data-stu-id="0379e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0379e-114">Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0379e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0379e-115">Produktová skupina.</span><span class="sxs-lookup"><span data-stu-id="0379e-115">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="0379e-116">C\#</span><span class="sxs-lookup"><span data-stu-id="0379e-116">C\#</span></span>

<span data-ttu-id="0379e-117">Pokud chcete zkontrolovat, jestli má zákazník nárok na upgrade na plán Azure:</span><span class="sxs-lookup"><span data-stu-id="0379e-117">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="0379e-118">Vytvořte objekt **ProductUpgradesRequest** a jako produktové skupiny zadejte identifikátor zákazníka a "Azure".</span><span class="sxs-lookup"><span data-stu-id="0379e-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="0379e-119">Použijte **kolekci IAggregatePartner.ProductUpgrades.**</span><span class="sxs-lookup"><span data-stu-id="0379e-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="0379e-120">Zavolejte **metodu CheckEligibility** a předejte objekt **ProductUpgradesRequest,** který vrátí objekt **ProductUpgradesEligibility.**</span><span class="sxs-lookup"><span data-stu-id="0379e-120">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="0379e-121">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="0379e-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0379e-122">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="0379e-122">Request syntax</span></span>

| <span data-ttu-id="0379e-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="0379e-123">Method</span></span>   | <span data-ttu-id="0379e-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0379e-124">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0379e-125">**Příspěvek**</span><span class="sxs-lookup"><span data-stu-id="0379e-125">**POST**</span></span> | <span data-ttu-id="0379e-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0379e-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0379e-127">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0379e-127">Request headers</span></span>

<span data-ttu-id="0379e-128">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0379e-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0379e-129">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0379e-129">Request body</span></span>

<span data-ttu-id="0379e-130">Text požadavku musí obsahovat prostředek [**ProductUpgradeRequest.**](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="0379e-130">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="0379e-131">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="0379e-131">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0379e-132">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0379e-132">REST response</span></span>

<span data-ttu-id="0379e-133">V případě úspěchu vrátí tato metoda v těle prostředek [**ProductUpgradesEligibility.**](product-upgrade-resources.md#productupgradeseligibility)</span><span class="sxs-lookup"><span data-stu-id="0379e-133">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0379e-134">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="0379e-134">Response success and error codes</span></span>

<span data-ttu-id="0379e-135">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0379e-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0379e-136">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="0379e-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0379e-137">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0379e-137">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0379e-138">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="0379e-138">Response example</span></span>

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
