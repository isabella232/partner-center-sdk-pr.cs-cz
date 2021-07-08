---
title: Získání souhrnu nákladů na služby zákazníka
description: Získá náklady na službu zákazníka za zadané fakturační období.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cab23238b5f62a02a5f7368f626648d5b1b5b7e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874903"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="ba45f-103">Získání souhrnu nákladů na služby zákazníka</span><span class="sxs-lookup"><span data-stu-id="ba45f-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="ba45f-104">Získá náklady na službu zákazníka za zadané fakturační období.</span><span class="sxs-lookup"><span data-stu-id="ba45f-104">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba45f-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ba45f-105">Prerequisites</span></span>

- <span data-ttu-id="ba45f-106">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ba45f-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ba45f-107">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="ba45f-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="ba45f-108">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ba45f-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ba45f-109">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="ba45f-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ba45f-110">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="ba45f-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ba45f-111">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="ba45f-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ba45f-112">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="ba45f-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ba45f-113">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ba45f-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ba45f-114">Indikátor fakturačního období ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="ba45f-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="ba45f-115">C\#</span><span class="sxs-lookup"><span data-stu-id="ba45f-115">C\#</span></span>

<span data-ttu-id="ba45f-116">Postup načtení souhrnu nákladů služby pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="ba45f-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="ba45f-117">Pro identifikaci zákazníka zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ba45f-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="ba45f-118">Pomocí vlastnosti [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) můžete získat rozhraní operací shromažďování nákladů na služby zákazníkům.</span><span class="sxs-lookup"><span data-stu-id="ba45f-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="ba45f-119">Voláním metody [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) s členem výčtu [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) se vrátí [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="ba45f-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="ba45f-120">K získání souhrnu nákladů na službu zákazníka použijte metodu [**IServiceCostsCollection. Summary. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) .</span><span class="sxs-lookup"><span data-stu-id="ba45f-120">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="ba45f-121">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="ba45f-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ba45f-122">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="ba45f-122">Request syntax</span></span>

| <span data-ttu-id="ba45f-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="ba45f-123">Method</span></span>  | <span data-ttu-id="ba45f-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ba45f-124">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ba45f-125">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="ba45f-125">**GET**</span></span> | <span data-ttu-id="ba45f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/servicecosts/{Billing-period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ba45f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="ba45f-127">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="ba45f-127">URI parameters</span></span>

<span data-ttu-id="ba45f-128">K identifikaci zákazníka a fakturačního období použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="ba45f-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="ba45f-129">Název</span><span class="sxs-lookup"><span data-stu-id="ba45f-129">Name</span></span>           | <span data-ttu-id="ba45f-130">Typ</span><span class="sxs-lookup"><span data-stu-id="ba45f-130">Type</span></span>   | <span data-ttu-id="ba45f-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ba45f-131">Required</span></span> | <span data-ttu-id="ba45f-132">Popis</span><span class="sxs-lookup"><span data-stu-id="ba45f-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ba45f-133">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="ba45f-133">customer-id</span></span>    | <span data-ttu-id="ba45f-134">guid</span><span class="sxs-lookup"><span data-stu-id="ba45f-134">guid</span></span>   | <span data-ttu-id="ba45f-135">Yes</span><span class="sxs-lookup"><span data-stu-id="ba45f-135">Yes</span></span>      | <span data-ttu-id="ba45f-136">Identifikátor zákazníka formátovaného identifikátorem GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="ba45f-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="ba45f-137">fakturace – období</span><span class="sxs-lookup"><span data-stu-id="ba45f-137">billing-period</span></span> | <span data-ttu-id="ba45f-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="ba45f-138">string</span></span> | <span data-ttu-id="ba45f-139">Yes</span><span class="sxs-lookup"><span data-stu-id="ba45f-139">Yes</span></span>      | <span data-ttu-id="ba45f-140">Indikátor, který představuje fakturační období.</span><span class="sxs-lookup"><span data-stu-id="ba45f-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="ba45f-141">Jediná podporovaná hodnota je MostRecent.</span><span class="sxs-lookup"><span data-stu-id="ba45f-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="ba45f-142">Případ řetězce nezáleží.</span><span class="sxs-lookup"><span data-stu-id="ba45f-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ba45f-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ba45f-143">Request headers</span></span>

<span data-ttu-id="ba45f-144">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ba45f-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ba45f-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="ba45f-145">Request body</span></span>

<span data-ttu-id="ba45f-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="ba45f-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ba45f-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ba45f-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ba45f-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ba45f-148">REST response</span></span>

<span data-ttu-id="ba45f-149">V případě úspěchu obsahuje tělo odpovědi prostředek [ServiceCostsSummary](service-costs-resources.md) , který poskytuje informace o nákladech služby.</span><span class="sxs-lookup"><span data-stu-id="ba45f-149">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ba45f-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="ba45f-150">Response success and error codes</span></span>

<span data-ttu-id="ba45f-151">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ba45f-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ba45f-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="ba45f-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ba45f-153">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ba45f-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ba45f-154">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ba45f-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 766
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "billingStartDate": "2015-12-12T00:00:00Z",
    "billingEndDate": "2016-01-11T00:00:00Z",
    "pretaxTotal": 17.22,
    "tax": 0.0,
    "afterTaxTotal": 17.22,
    "currencySymbol": "$",
    "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
    "details":
     [
        {
            "invoiceType": "Recurring",
            "summary": {
                "billingStartDate": "2015-12-12T00:00:00Z",
                "billingEndDate": "2016-01-11T00:00:00Z",
                "pretaxTotal": 17.22,
                "tax": 0.0,
                "afterTaxTotal": 17.22,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        },
        {
            "invoiceType": "OneTime",
            "summary": {
                "billingStartDate": "2019-04-01T00:00:00Z",
                "billingEndDate": "2019-04-30T23:59:59.9999999Z",
                "pretaxTotal": 2,
                "tax": 0.2,
                "afterTaxTotal": 2.2,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        }
    ],
    "links": {
        "serviceCostLineItems": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "ServiceCostsSummary"
    }
}
```
