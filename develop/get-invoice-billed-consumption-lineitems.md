---
title: Získat položky řádku komerčního vyúčtování faktury
description: Pomocí rozhraní API partnerského centra můžete získat podrobnosti o položce řádku faktury pro komerční spotřebu (uzavřenou položku řádku s údaji o denním hodnocení) pro zadanou fakturu.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1406938b16e5a363a73c36ef0338eb5fc4305279
ms.sourcegitcommit: 89aefbff6dbe740b6f27a888492ffc2e5f98b1e9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/24/2021
ms.locfileid: "110325441"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="0b813-103">Získat položky řádku komerčního vyúčtování faktury</span><span class="sxs-lookup"><span data-stu-id="0b813-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="0b813-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="0b813-104">**Applies to:**</span></span>

- <span data-ttu-id="0b813-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="0b813-105">Partner Center</span></span>

<span data-ttu-id="0b813-106">Následující metody můžete použít k získání shromažďování podrobností o položkách řádků faktury pro komerční spotřebu (označované také jako uzavřené položky řádku s vyhodnoceným řádkem využití) pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="0b813-106">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0b813-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0b813-107">Prerequisites</span></span>

- <span data-ttu-id="0b813-108">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0b813-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0b813-109">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="0b813-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0b813-110">Identifikátor faktury</span><span class="sxs-lookup"><span data-stu-id="0b813-110">An invoice identifier.</span></span> <span data-ttu-id="0b813-111">Určuje fakturu, pro kterou se mají načíst položky řádku.</span><span class="sxs-lookup"><span data-stu-id="0b813-111">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="0b813-112">C\#</span><span class="sxs-lookup"><span data-stu-id="0b813-112">C\#</span></span>

<span data-ttu-id="0b813-113">Chcete-li získat položky komerčních řádků pro určenou fakturu, je nutné načíst objekt faktury:</span><span class="sxs-lookup"><span data-stu-id="0b813-113">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="0b813-114">Zavolejte metodu [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , která získá rozhraní k fakturaci operace pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="0b813-114">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="0b813-115">Pro načtení objektu faktury zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) .</span><span class="sxs-lookup"><span data-stu-id="0b813-115">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="0b813-116">Objekt faktury obsahuje všechny informace o zadané faktuře.</span><span class="sxs-lookup"><span data-stu-id="0b813-116">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="0b813-117">**Poskytovatel** identifikuje zdroj fakturovaných podrobných informací (například **jednorázová**).</span><span class="sxs-lookup"><span data-stu-id="0b813-117">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="0b813-118">**InvoiceLineItemType** určuje typ (například **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="0b813-118">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="0b813-119">Následující příklad kódu používá smyčku **foreach** ke zpracování kolekce položek řádků.</span><span class="sxs-lookup"><span data-stu-id="0b813-119">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="0b813-120">Pro každou **InvoiceLineItemType** se načte samostatná kolekce položek čáry.</span><span class="sxs-lookup"><span data-stu-id="0b813-120">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="0b813-121">Získání kolekce položek řádků, které odpovídají instanci **InvoiceDetail** :</span><span class="sxs-lookup"><span data-stu-id="0b813-121">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="0b813-122">Předejte **BillingProvider** a **InvoiceLineItemType** instance do metody [**podle**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .</span><span class="sxs-lookup"><span data-stu-id="0b813-122">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="0b813-123">Zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) pro načtení přidružených položek řádků.</span><span class="sxs-lookup"><span data-stu-id="0b813-123">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="0b813-124">Vytvořte enumerátor pro přechod kolekce, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="0b813-124">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string invoiceId;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="0b813-125">Podobný příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="0b813-125">For a similar example, see the following:</span></span>

- <span data-ttu-id="0b813-126">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="0b813-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="0b813-127">Projekt: **SDK pro Partnerské centrum ukázky**</span><span class="sxs-lookup"><span data-stu-id="0b813-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="0b813-128">Třída: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="0b813-128">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="0b813-129">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="0b813-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0b813-130">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="0b813-130">Request syntax</span></span>

<span data-ttu-id="0b813-131">První syntaxí můžete vrátit úplný seznam všech řádových položek pro danou fakturu.</span><span class="sxs-lookup"><span data-stu-id="0b813-131">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="0b813-132">Pro velké faktury použijte druhou syntaxi se zadanou velikostí a posunem založeným na 0, abyste vrátili stránkovaný seznam řádových položek.</span><span class="sxs-lookup"><span data-stu-id="0b813-132">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="0b813-133">Třetí syntaxi použijte k získání další stránky řádových položek odsoustavy pomocí `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="0b813-133">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="0b813-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="0b813-134">Method</span></span>  | <span data-ttu-id="0b813-135">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="0b813-135">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0b813-136">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="0b813-136">**GET**</span></span> | <span data-ttu-id="0b813-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{id_faktury}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0b813-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="0b813-138">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="0b813-138">**GET**</span></span> | <span data-ttu-id="0b813-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{id_faktury}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0b813-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="0b813-140">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="0b813-140">**GET**</span></span> | <span data-ttu-id="0b813-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{id_faktury}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="0b813-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="0b813-142">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="0b813-142">URI parameters</span></span>

<span data-ttu-id="0b813-143">Při vytváření požadavku použijte následující identifikátor URI a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="0b813-143">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="0b813-144">Název</span><span class="sxs-lookup"><span data-stu-id="0b813-144">Name</span></span>                   | <span data-ttu-id="0b813-145">Typ</span><span class="sxs-lookup"><span data-stu-id="0b813-145">Type</span></span>   | <span data-ttu-id="0b813-146">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="0b813-146">Required</span></span> | <span data-ttu-id="0b813-147">Popis</span><span class="sxs-lookup"><span data-stu-id="0b813-147">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="0b813-148">id faktury</span><span class="sxs-lookup"><span data-stu-id="0b813-148">invoice-id</span></span>             | <span data-ttu-id="0b813-149">řetězec</span><span class="sxs-lookup"><span data-stu-id="0b813-149">string</span></span> | <span data-ttu-id="0b813-150">Yes</span><span class="sxs-lookup"><span data-stu-id="0b813-150">Yes</span></span>      | <span data-ttu-id="0b813-151">Řetězec, který identifikuje fakturu.</span><span class="sxs-lookup"><span data-stu-id="0b813-151">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="0b813-152">Zprostředkovatel</span><span class="sxs-lookup"><span data-stu-id="0b813-152">provider</span></span>               | <span data-ttu-id="0b813-153">řetězec</span><span class="sxs-lookup"><span data-stu-id="0b813-153">string</span></span> | <span data-ttu-id="0b813-154">Yes</span><span class="sxs-lookup"><span data-stu-id="0b813-154">Yes</span></span>      | <span data-ttu-id="0b813-155">Zprostředkovatel: "jednorázová".</span><span class="sxs-lookup"><span data-stu-id="0b813-155">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="0b813-156">faktura-line-Item-Type</span><span class="sxs-lookup"><span data-stu-id="0b813-156">invoice-line-item-type</span></span> | <span data-ttu-id="0b813-157">řetězec</span><span class="sxs-lookup"><span data-stu-id="0b813-157">string</span></span> | <span data-ttu-id="0b813-158">Yes</span><span class="sxs-lookup"><span data-stu-id="0b813-158">Yes</span></span>      | <span data-ttu-id="0b813-159">Typ podrobností o faktuře: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="0b813-159">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="0b813-160">currencyCode</span><span class="sxs-lookup"><span data-stu-id="0b813-160">currencyCode</span></span>           | <span data-ttu-id="0b813-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="0b813-161">string</span></span> | <span data-ttu-id="0b813-162">Yes</span><span class="sxs-lookup"><span data-stu-id="0b813-162">Yes</span></span>      | <span data-ttu-id="0b813-163">Kód měny pro účtované řádkové položky.</span><span class="sxs-lookup"><span data-stu-id="0b813-163">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="0b813-164">period</span><span class="sxs-lookup"><span data-stu-id="0b813-164">period</span></span>                 | <span data-ttu-id="0b813-165">řetězec</span><span class="sxs-lookup"><span data-stu-id="0b813-165">string</span></span> | <span data-ttu-id="0b813-166">Yes</span><span class="sxs-lookup"><span data-stu-id="0b813-166">Yes</span></span>      | <span data-ttu-id="0b813-167">Období pro fakturované rekognoskaci</span><span class="sxs-lookup"><span data-stu-id="0b813-167">The period for billed recon.</span></span> <span data-ttu-id="0b813-168">Příklad: Current, Previous.</span><span class="sxs-lookup"><span data-stu-id="0b813-168">example: current, previous.</span></span>        |
| <span data-ttu-id="0b813-169">size</span><span class="sxs-lookup"><span data-stu-id="0b813-169">size</span></span>                   | <span data-ttu-id="0b813-170">číslo</span><span class="sxs-lookup"><span data-stu-id="0b813-170">number</span></span> | <span data-ttu-id="0b813-171">No</span><span class="sxs-lookup"><span data-stu-id="0b813-171">No</span></span>       | <span data-ttu-id="0b813-172">Maximální počet položek, které se mají vrátit.</span><span class="sxs-lookup"><span data-stu-id="0b813-172">The maximum number of items to return.</span></span> <span data-ttu-id="0b813-173">Výchozí velikost je 2000.</span><span class="sxs-lookup"><span data-stu-id="0b813-173">Default size is 2000</span></span>       |
| <span data-ttu-id="0b813-174">seekOperation</span><span class="sxs-lookup"><span data-stu-id="0b813-174">seekOperation</span></span>          | <span data-ttu-id="0b813-175">řetězec</span><span class="sxs-lookup"><span data-stu-id="0b813-175">string</span></span> | <span data-ttu-id="0b813-176">No</span><span class="sxs-lookup"><span data-stu-id="0b813-176">No</span></span>       | <span data-ttu-id="0b813-177">Nastavte seekOperation = Next pro získání další stránky rekognoskaci položek řádků.</span><span class="sxs-lookup"><span data-stu-id="0b813-177">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0b813-178">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="0b813-178">Request headers</span></span>

<span data-ttu-id="0b813-179">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0b813-179">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0b813-180">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="0b813-180">Request body</span></span>

<span data-ttu-id="0b813-181">Žádné</span><span class="sxs-lookup"><span data-stu-id="0b813-181">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="0b813-182">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="0b813-182">REST response</span></span>

<span data-ttu-id="0b813-183">V případě úspěchu obsahuje odpověď kolekci podrobností položky řádku.</span><span class="sxs-lookup"><span data-stu-id="0b813-183">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="0b813-184">Pro položku řádku **ChargeType** je hodnota **Nákup** namapována na **New (nový**).</span><span class="sxs-lookup"><span data-stu-id="0b813-184">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="0b813-185">**Náhrada** hodnoty je namapována na **Zrušit**.</span><span class="sxs-lookup"><span data-stu-id="0b813-185">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0b813-186">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="0b813-186">Response success and error codes</span></span>

<span data-ttu-id="0b813-187">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="0b813-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0b813-188">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="0b813-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0b813-189">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0b813-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="0b813-190">Příklady REST</span><span class="sxs-lookup"><span data-stu-id="0b813-190">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="0b813-191">Požadavek-odpověď – příklad 1</span><span class="sxs-lookup"><span data-stu-id="0b813-191">Request-response example 1</span></span>

<span data-ttu-id="0b813-192">Podrobnosti pro tento příklad požadavku a odpovědi REST jsou následující:</span><span class="sxs-lookup"><span data-stu-id="0b813-192">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="0b813-193">**Poskytovatel:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="0b813-193">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="0b813-194">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="0b813-194">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="0b813-195">**Period**: **Previous**</span><span class="sxs-lookup"><span data-stu-id="0b813-195">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="0b813-196">Příklad požadavku 1</span><span class="sxs-lookup"><span data-stu-id="0b813-196">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="0b813-197">Příklad odpovědi 1</span><span class="sxs-lookup"><span data-stu-id="0b813-197">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        },
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Ubuntu 16.04 (WebHost)",
            "productName": "Test Test on Linux",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Linux",
            "meterName": "Test Test on Linux - Test Test on Ubuntu 16.04 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TESTRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/testUbuntuTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209951014286867,
            "quantity": 23.350007,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.490235765325545,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.490235765325545,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1999968000511991808131,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="0b813-198">Příklad požadavku a odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="0b813-198">Request-response example 2</span></span>

<span data-ttu-id="0b813-199">Podrobnosti pro tento příklad požadavku a odpovědi REST jsou následující:</span><span class="sxs-lookup"><span data-stu-id="0b813-199">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="0b813-200">**Poskytovatel:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="0b813-200">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="0b813-201">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="0b813-201">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="0b813-202">**Period**: **Previous**</span><span class="sxs-lookup"><span data-stu-id="0b813-202">**Period**: **Previous**</span></span>
- <span data-ttu-id="0b813-203">**SeekOperation:** **Next**</span><span class="sxs-lookup"><span data-stu-id="0b813-203">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="0b813-204">Příklad požadavku 2</span><span class="sxs-lookup"><span data-stu-id="0b813-204">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="response-example-2"></a><span data-ttu-id="0b813-205">Příklad odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="0b813-205">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
          {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1835431430074643112595,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
