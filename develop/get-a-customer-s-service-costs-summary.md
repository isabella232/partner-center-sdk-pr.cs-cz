---
title: Získání souhrnu nákladů na služby zákazníka
description: Získá náklady na službu zákazníka za zadané fakturační období.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 635e61342e13c3676120ec0df02f1e8bffda64ac
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766867"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="162c4-103">Získání souhrnu nákladů na služby zákazníka</span><span class="sxs-lookup"><span data-stu-id="162c4-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="162c4-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="162c4-104">**Applies to:**</span></span>

- <span data-ttu-id="162c4-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="162c4-105">Partner Center</span></span>

<span data-ttu-id="162c4-106">Získá náklady na službu zákazníka za zadané fakturační období.</span><span class="sxs-lookup"><span data-stu-id="162c4-106">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="162c4-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="162c4-107">Prerequisites</span></span>

- <span data-ttu-id="162c4-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="162c4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="162c4-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="162c4-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="162c4-110">ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="162c4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="162c4-111">Pokud ID zákazníka neznáte, můžete ho vyhledat na [řídicím panelu](https://partner.microsoft.com/dashboard)partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="162c4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="162c4-112">V nabídce partnerského centra klikněte na **CSP** a potom na **zákazníci**.</span><span class="sxs-lookup"><span data-stu-id="162c4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="162c4-113">Vyberte zákazníka ze seznamu Zákazník a pak vyberte možnost **účet**.</span><span class="sxs-lookup"><span data-stu-id="162c4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="162c4-114">Na stránce účet zákazníka vyhledejte v části **informace o účtu zákazníka** **ID Microsoftu** .</span><span class="sxs-lookup"><span data-stu-id="162c4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="162c4-115">ID společnosti Microsoft je stejné jako ID zákazníka ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="162c4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="162c4-116">Indikátor fakturačního období ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="162c4-116">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="162c4-117">C\#</span><span class="sxs-lookup"><span data-stu-id="162c4-117">C\#</span></span>

<span data-ttu-id="162c4-118">Postup načtení souhrnu nákladů služby pro zadaného zákazníka:</span><span class="sxs-lookup"><span data-stu-id="162c4-118">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="162c4-119">Pro identifikaci zákazníka zavolejte metodu [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s ID zákazníka.</span><span class="sxs-lookup"><span data-stu-id="162c4-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="162c4-120">Pomocí vlastnosti [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) můžete získat rozhraní operací shromažďování nákladů na služby zákazníkům.</span><span class="sxs-lookup"><span data-stu-id="162c4-120">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="162c4-121">Voláním metody [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) s členem výčtu [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) se vrátí [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="162c4-121">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="162c4-122">K získání souhrnu nákladů na službu zákazníka použijte metodu [**IServiceCostsCollection. Summary. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) .</span><span class="sxs-lookup"><span data-stu-id="162c4-122">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="162c4-123">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="162c4-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="162c4-124">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="162c4-124">Request syntax</span></span>

| <span data-ttu-id="162c4-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="162c4-125">Method</span></span>  | <span data-ttu-id="162c4-126">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="162c4-126">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="162c4-127">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="162c4-127">**GET**</span></span> | <span data-ttu-id="162c4-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/servicecosts/{Billing-period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="162c4-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="162c4-129">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="162c4-129">URI parameters</span></span>

<span data-ttu-id="162c4-130">K identifikaci zákazníka a fakturačního období použijte následující parametry cesty.</span><span class="sxs-lookup"><span data-stu-id="162c4-130">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="162c4-131">Název</span><span class="sxs-lookup"><span data-stu-id="162c4-131">Name</span></span>           | <span data-ttu-id="162c4-132">Typ</span><span class="sxs-lookup"><span data-stu-id="162c4-132">Type</span></span>   | <span data-ttu-id="162c4-133">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="162c4-133">Required</span></span> | <span data-ttu-id="162c4-134">Popis</span><span class="sxs-lookup"><span data-stu-id="162c4-134">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="162c4-135">ID zákazníka</span><span class="sxs-lookup"><span data-stu-id="162c4-135">customer-id</span></span>    | <span data-ttu-id="162c4-136">guid</span><span class="sxs-lookup"><span data-stu-id="162c4-136">guid</span></span>   | <span data-ttu-id="162c4-137">Yes</span><span class="sxs-lookup"><span data-stu-id="162c4-137">Yes</span></span>      | <span data-ttu-id="162c4-138">Identifikátor zákazníka formátovaného identifikátorem GUID, který identifikuje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="162c4-138">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="162c4-139">fakturace – období</span><span class="sxs-lookup"><span data-stu-id="162c4-139">billing-period</span></span> | <span data-ttu-id="162c4-140">řetězec</span><span class="sxs-lookup"><span data-stu-id="162c4-140">string</span></span> | <span data-ttu-id="162c4-141">Yes</span><span class="sxs-lookup"><span data-stu-id="162c4-141">Yes</span></span>      | <span data-ttu-id="162c4-142">Indikátor, který představuje fakturační období.</span><span class="sxs-lookup"><span data-stu-id="162c4-142">An indicator that represents the billing period.</span></span> <span data-ttu-id="162c4-143">Jediná podporovaná hodnota je MostRecent.</span><span class="sxs-lookup"><span data-stu-id="162c4-143">The only supported value is MostRecent.</span></span> <span data-ttu-id="162c4-144">Případ řetězce nezáleží.</span><span class="sxs-lookup"><span data-stu-id="162c4-144">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="162c4-145">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="162c4-145">Request headers</span></span>

<span data-ttu-id="162c4-146">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="162c4-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="162c4-147">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="162c4-147">Request body</span></span>

<span data-ttu-id="162c4-148">Žádné</span><span class="sxs-lookup"><span data-stu-id="162c4-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="162c4-149">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="162c4-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="162c4-150">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="162c4-150">REST response</span></span>

<span data-ttu-id="162c4-151">V případě úspěchu obsahuje tělo odpovědi prostředek [ServiceCostsSummary](service-costs-resources.md) , který poskytuje informace o nákladech služby.</span><span class="sxs-lookup"><span data-stu-id="162c4-151">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="162c4-152">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="162c4-152">Response success and error codes</span></span>

<span data-ttu-id="162c4-153">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="162c4-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="162c4-154">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="162c4-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="162c4-155">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="162c4-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="162c4-156">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="162c4-156">Response example</span></span>

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
