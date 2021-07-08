---
title: Získání řádkových položek nákladů na služby zákazníka
description: Získá položky řádku s náklady na službu zákazníka za zadané fakturační období.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1bc2914d7c8d41c6d806131444fdc241aa1feb90
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874937"
---
# <a name="get-a-customers-service-costs-line-items"></a><span data-ttu-id="3a7e5-103">Získání řádkových položek nákladů na služby zákazníka</span><span class="sxs-lookup"><span data-stu-id="3a7e5-103">Get a customer's service costs line items</span></span>

<span data-ttu-id="3a7e5-104">Získá položky řádku s náklady na službu zákazníka za zadané fakturační období.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-104">Gets a customer's service cost line items for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a7e5-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3a7e5-105">Prerequisites</span></span>

- <span data-ttu-id="3a7e5-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3a7e5-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3a7e5-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="3a7e5-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3a7e5-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3a7e5-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3a7e5-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3a7e5-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3a7e5-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="3a7e5-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3a7e5-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3a7e5-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3a7e5-114">Indikátor fakturačního období ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="3a7e5-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="3a7e5-115">C\#</span><span class="sxs-lookup"><span data-stu-id="3a7e5-115">C\#</span></span>

<span data-ttu-id="3a7e5-116">Postup načtení souhrnu nákladů služby pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="3a7e5-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="3a7e5-117">Pro identifikaci zákazníka zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="3a7e5-118">Pomocí vlastnosti [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) můžete získat rozhraní operací shromažďování nákladů na služby zákazníkům.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="3a7e5-119">Voláním metody [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) s členem výčtu [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) se vrátí [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="3a7e5-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="3a7e5-120">Použijte metodu [**IServiceCostsCollection. položky řádku. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) k získání nákladů na službu na řádku zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-120">Use the [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) method to get the customer's service costs line items.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a><span data-ttu-id="3a7e5-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="3a7e5-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3a7e5-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="3a7e5-122">Request syntax</span></span>

| <span data-ttu-id="3a7e5-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="3a7e5-123">Method</span></span>  | <span data-ttu-id="3a7e5-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="3a7e5-124">Request URI</span></span>                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3a7e5-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="3a7e5-125">**GET**</span></span> | <span data-ttu-id="3a7e5-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/servicecosts/{Billing-period}/LineItems HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3a7e5-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3a7e5-127">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="3a7e5-127">URI parameters</span></span>

<span data-ttu-id="3a7e5-128">K identifikaci zákazníka a fakturačního období použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="3a7e5-129">Název</span><span class="sxs-lookup"><span data-stu-id="3a7e5-129">Name</span></span>           | <span data-ttu-id="3a7e5-130">Typ</span><span class="sxs-lookup"><span data-stu-id="3a7e5-130">Type</span></span>   | <span data-ttu-id="3a7e5-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="3a7e5-131">Required</span></span> | <span data-ttu-id="3a7e5-132">Popis</span><span class="sxs-lookup"><span data-stu-id="3a7e5-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3a7e5-133">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="3a7e5-133">customer-id</span></span>    | <span data-ttu-id="3a7e5-134">guid</span><span class="sxs-lookup"><span data-stu-id="3a7e5-134">guid</span></span>   | <span data-ttu-id="3a7e5-135">Yes</span><span class="sxs-lookup"><span data-stu-id="3a7e5-135">Yes</span></span>      | <span data-ttu-id="3a7e5-136">Identifikátor zákazníka formátovaného identifikátorem GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="3a7e5-137">fakturace – období</span><span class="sxs-lookup"><span data-stu-id="3a7e5-137">billing-period</span></span> | <span data-ttu-id="3a7e5-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="3a7e5-138">string</span></span> | <span data-ttu-id="3a7e5-139">Yes</span><span class="sxs-lookup"><span data-stu-id="3a7e5-139">Yes</span></span>      | <span data-ttu-id="3a7e5-140">Indikátor, který představuje fakturační období.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="3a7e5-141">Jediná podporovaná hodnota je MostRecent.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="3a7e5-142">Případ řetězce nezáleží.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3a7e5-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="3a7e5-143">Request headers</span></span>

<span data-ttu-id="3a7e5-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3a7e5-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3a7e5-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="3a7e5-145">Request body</span></span>

<span data-ttu-id="3a7e5-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="3a7e5-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3a7e5-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="3a7e5-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3a7e5-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="3a7e5-148">REST response</span></span>

<span data-ttu-id="3a7e5-149">V případě úspěchu obsahuje tělo odpovědi prostředek [ServiceCostLineItem](service-costs-resources.md) , který poskytuje informace o nákladech služby.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-149">If successful, the response body contains a [ServiceCostLineItem](service-costs-resources.md) resource that provides information about the service costs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a7e5-150">Následující vlastnosti *platí jenom pro položky s náklady na* službu, u kterých je produkt *jednorázové nákupy*: **ProductID**, **ProductName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **Publisher**, **termAndBillingCycle**, **discountDetails**.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-150">The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span></span> <span data-ttu-id="3a7e5-151">Tyto vlastnosti se *nevztahují na* položky řádku služby, ve kterých je produkt *opakovaný nákup*.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-151">These properties *don't apply to* service line items where the product is a *recurring purchase*.</span></span> <span data-ttu-id="3a7e5-152">tyto vlastnosti se například *nevztahují* na Office 365 a Azure na základě předplatného.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-152">For example, these properties *don't apply* to subscription-based Office 365 and Azure.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3a7e5-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="3a7e5-153">Response success and error codes</span></span>

<span data-ttu-id="3a7e5-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3a7e5-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="3a7e5-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3a7e5-156">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3a7e5-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3a7e5-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="3a7e5-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2148
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "attributes": {
        "objectType": "Collection"
    },
    "items":
    [{
            "afterTaxTotal": 0.0,
            "chargeType": "PURCHASE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-01-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 0.0,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2015-12-15T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 0.0,
            "invoiceNumber": "T000003163",
            "invoiceType": "OneTime",
            "productId": "DZH318Z0BJR6",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BMFK",
            "productName": "Azure Managed Experience",
            "skuName": "Azure Managed Experience - Optimize",
            "publisherName": "Microsoft",
            "publisherId": "01323244",
            "termAndBillingCycle": "",
            "discountDetails": "N/A"
        }, {
            "afterTaxTotal": 17.219999999999999,
            "chargeType": "CYCLE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-02-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 17.219999999999999,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2016-01-12T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 17.219999999999999,
            "invoiceNumber": "D000003163",
            "invoiceType": "Recurring",
            "productId": "DZH318Z0BJR7",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BTTTT",
            "productName": "NGINX Plus",
            "skuName": "NGINX Plus (Ubuntu 14.04)",
            "publisherName": "Nginx, Inc.",
            "publisherId": "212336222",
            "termAndBillingCycle": "30 Days Trial",
            "discountDetails": "20%"
        }
    ],
    "links": {
        "self": {
            "headers": [],
            "method": "GET",
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems"
        }
    },
    "totalCount": 2
}
```
