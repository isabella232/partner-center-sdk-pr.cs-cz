---
title: Získání fakturovaných řádkových položek komerční spotřeby na faktuře
description: Kolekci podrobností řádkových položek faktury ke komerční spotřebě (uzavřená položka řádku s denním hodnocením využití) pro zadanou fakturu můžete získat pomocí rozhraní API Partnerské centrum využití.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 285b6fbda774c9396dee8947550ed774d52bf901
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446220"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="95610-103">Získání fakturovaných řádkových položek komerční spotřeby na faktuře</span><span class="sxs-lookup"><span data-stu-id="95610-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="95610-104">Pomocí následujících metod můžete získat kolekci podrobností o řádkových položkách faktury ke komerční spotřebě (označované také jako uzavřené řádkové položky s denním hodnocením využití) pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="95610-104">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="95610-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="95610-105">Prerequisites</span></span>

- <span data-ttu-id="95610-106">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="95610-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95610-107">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="95610-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="95610-108">Identifikátor faktury.</span><span class="sxs-lookup"><span data-stu-id="95610-108">An invoice identifier.</span></span> <span data-ttu-id="95610-109">Tím se identifikuje faktura, pro kterou se mají načíst řádkové položky.</span><span class="sxs-lookup"><span data-stu-id="95610-109">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="95610-110">C\#</span><span class="sxs-lookup"><span data-stu-id="95610-110">C\#</span></span>

<span data-ttu-id="95610-111">Pokud chcete získat komerční řádkové položky pro zadanou fakturu, musíte načíst objekt faktury:</span><span class="sxs-lookup"><span data-stu-id="95610-111">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="95610-112">Voláním [**metody ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) získáte rozhraní pro operace s fakturou pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="95610-112">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="95610-113">Voláním [**metody Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) načtěte objekt faktury.</span><span class="sxs-lookup"><span data-stu-id="95610-113">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="95610-114">Objekt faktury obsahuje všechny informace pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="95610-114">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="95610-115">**Zprostředkovatel** identifikuje zdroj fakturovaných podrobných informací (například **jednou).**</span><span class="sxs-lookup"><span data-stu-id="95610-115">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="95610-116">**InvoiceLineItemType** určuje typ (například **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="95610-116">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="95610-117">Následující příklad kódu používá smyčku **foreach** ke zpracování kolekce položek řádku.</span><span class="sxs-lookup"><span data-stu-id="95610-117">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="95610-118">Pro každý typ InvoiceLineItemType se načte samostatná kolekce **řádových položek.**</span><span class="sxs-lookup"><span data-stu-id="95610-118">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="95610-119">Získání kolekce řádových položek, které odpovídají instanci **InvoiceDetail:**</span><span class="sxs-lookup"><span data-stu-id="95610-119">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="95610-120">Do metody [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) předejte **vlastnosti BillingProvider** a **InvoiceLineItemType** instance.</span><span class="sxs-lookup"><span data-stu-id="95610-120">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="95610-121">Voláním [**metody Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) načtěte přidružené řádkové položky.</span><span class="sxs-lookup"><span data-stu-id="95610-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="95610-122">Vytvořte enumerátor pro přechod kolekce, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="95610-122">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="95610-123">Podobný příklad najdete v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="95610-123">For a similar example, see the following:</span></span>

- <span data-ttu-id="95610-124">Ukázka: [Konzolová testovací aplikace](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="95610-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="95610-125">Project: **SDK pro Partnerské centrum ukázky**</span><span class="sxs-lookup"><span data-stu-id="95610-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="95610-126">Třída: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="95610-126">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="95610-127">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="95610-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95610-128">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="95610-128">Request syntax</span></span>

<span data-ttu-id="95610-129">První syntaxí můžete vrátit úplný seznam všech řádových položek pro danou fakturu.</span><span class="sxs-lookup"><span data-stu-id="95610-129">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="95610-130">Pro velké faktury použijte druhou syntaxi se zadanou velikostí a posunem založeným na 0, abyste vrátili stránkovaný seznam řádových položek.</span><span class="sxs-lookup"><span data-stu-id="95610-130">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="95610-131">Třetí syntaxi použijte k získání další stránky řádových položek odsoustavy pomocí `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="95610-131">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="95610-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="95610-132">Method</span></span>  | <span data-ttu-id="95610-133">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="95610-133">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95610-134">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="95610-134">**GET**</span></span> | <span data-ttu-id="95610-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{id_faktury}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="95610-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="95610-136">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="95610-136">**GET**</span></span> | <span data-ttu-id="95610-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{id_faktury}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="95610-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="95610-138">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="95610-138">**GET**</span></span> | <span data-ttu-id="95610-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{id_faktury}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="95610-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="95610-140">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="95610-140">URI parameters</span></span>

<span data-ttu-id="95610-141">Při vytváření požadavku použijte následující identifikátor URI a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="95610-141">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="95610-142">Název</span><span class="sxs-lookup"><span data-stu-id="95610-142">Name</span></span>                   | <span data-ttu-id="95610-143">Typ</span><span class="sxs-lookup"><span data-stu-id="95610-143">Type</span></span>   | <span data-ttu-id="95610-144">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="95610-144">Required</span></span> | <span data-ttu-id="95610-145">Popis</span><span class="sxs-lookup"><span data-stu-id="95610-145">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="95610-146">id faktury</span><span class="sxs-lookup"><span data-stu-id="95610-146">invoice-id</span></span>             | <span data-ttu-id="95610-147">řetězec</span><span class="sxs-lookup"><span data-stu-id="95610-147">string</span></span> | <span data-ttu-id="95610-148">Yes</span><span class="sxs-lookup"><span data-stu-id="95610-148">Yes</span></span>      | <span data-ttu-id="95610-149">Řetězec, který identifikuje fakturu.</span><span class="sxs-lookup"><span data-stu-id="95610-149">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="95610-150">Zprostředkovatel</span><span class="sxs-lookup"><span data-stu-id="95610-150">provider</span></span>               | <span data-ttu-id="95610-151">řetězec</span><span class="sxs-lookup"><span data-stu-id="95610-151">string</span></span> | <span data-ttu-id="95610-152">Yes</span><span class="sxs-lookup"><span data-stu-id="95610-152">Yes</span></span>      | <span data-ttu-id="95610-153">Poskytovatel: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="95610-153">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="95610-154">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="95610-154">invoice-line-item-type</span></span> | <span data-ttu-id="95610-155">řetězec</span><span class="sxs-lookup"><span data-stu-id="95610-155">string</span></span> | <span data-ttu-id="95610-156">Yes</span><span class="sxs-lookup"><span data-stu-id="95610-156">Yes</span></span>      | <span data-ttu-id="95610-157">Podrobnosti o typu faktury: UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="95610-157">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="95610-158">currencyCode</span><span class="sxs-lookup"><span data-stu-id="95610-158">currencyCode</span></span>           | <span data-ttu-id="95610-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="95610-159">string</span></span> | <span data-ttu-id="95610-160">Yes</span><span class="sxs-lookup"><span data-stu-id="95610-160">Yes</span></span>      | <span data-ttu-id="95610-161">Kód měny pro fakturované řádkové položky.</span><span class="sxs-lookup"><span data-stu-id="95610-161">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="95610-162">period</span><span class="sxs-lookup"><span data-stu-id="95610-162">period</span></span>                 | <span data-ttu-id="95610-163">řetězec</span><span class="sxs-lookup"><span data-stu-id="95610-163">string</span></span> | <span data-ttu-id="95610-164">Yes</span><span class="sxs-lookup"><span data-stu-id="95610-164">Yes</span></span>      | <span data-ttu-id="95610-165">Období pro fakturované odsoustavy</span><span class="sxs-lookup"><span data-stu-id="95610-165">The period for billed recon.</span></span> <span data-ttu-id="95610-166">example: current, previous.</span><span class="sxs-lookup"><span data-stu-id="95610-166">example: current, previous.</span></span>        |
| <span data-ttu-id="95610-167">size</span><span class="sxs-lookup"><span data-stu-id="95610-167">size</span></span>                   | <span data-ttu-id="95610-168">číslo</span><span class="sxs-lookup"><span data-stu-id="95610-168">number</span></span> | <span data-ttu-id="95610-169">No</span><span class="sxs-lookup"><span data-stu-id="95610-169">No</span></span>       | <span data-ttu-id="95610-170">Maximální počet položek, které se budou vracet.</span><span class="sxs-lookup"><span data-stu-id="95610-170">The maximum number of items to return.</span></span> <span data-ttu-id="95610-171">Výchozí velikost je 2 000.</span><span class="sxs-lookup"><span data-stu-id="95610-171">Default size is 2000</span></span>       |
| <span data-ttu-id="95610-172">seekOperation</span><span class="sxs-lookup"><span data-stu-id="95610-172">seekOperation</span></span>          | <span data-ttu-id="95610-173">řetězec</span><span class="sxs-lookup"><span data-stu-id="95610-173">string</span></span> | <span data-ttu-id="95610-174">No</span><span class="sxs-lookup"><span data-stu-id="95610-174">No</span></span>       | <span data-ttu-id="95610-175">Pokud chcete získat další stránku řádových položek odsouváte, nastavte seekOperation=Next.</span><span class="sxs-lookup"><span data-stu-id="95610-175">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="95610-176">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="95610-176">Request headers</span></span>

<span data-ttu-id="95610-177">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="95610-177">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95610-178">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="95610-178">Request body</span></span>

<span data-ttu-id="95610-179">Žádné</span><span class="sxs-lookup"><span data-stu-id="95610-179">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="95610-180">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="95610-180">REST response</span></span>

<span data-ttu-id="95610-181">V případě úspěchu odpověď obsahuje kolekci podrobností řádkové položky.</span><span class="sxs-lookup"><span data-stu-id="95610-181">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="95610-182">Pro položku řádku **ChargeType** se hodnota **Purchase** namapuje na **New**.</span><span class="sxs-lookup"><span data-stu-id="95610-182">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="95610-183">Hodnota **Refundace se mapuje** na **Hodnotu Zrušit.**</span><span class="sxs-lookup"><span data-stu-id="95610-183">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95610-184">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="95610-184">Response success and error codes</span></span>

<span data-ttu-id="95610-185">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="95610-185">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95610-186">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="95610-186">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="95610-187">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="95610-187">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="95610-188">Příklady REST</span><span class="sxs-lookup"><span data-stu-id="95610-188">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="95610-189">Příklad požadavku a odpovědi 1</span><span class="sxs-lookup"><span data-stu-id="95610-189">Request-response example 1</span></span>

<span data-ttu-id="95610-190">Podrobnosti pro tento příklad požadavku a odpovědi REST jsou následující:</span><span class="sxs-lookup"><span data-stu-id="95610-190">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="95610-191">**Poskytovatel:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="95610-191">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="95610-192">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="95610-192">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="95610-193">**Period**: **Previous**</span><span class="sxs-lookup"><span data-stu-id="95610-193">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="95610-194">Příklad požadavku 1</span><span class="sxs-lookup"><span data-stu-id="95610-194">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="95610-195">Příklad odpovědi 1</span><span class="sxs-lookup"><span data-stu-id="95610-195">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="95610-196">Příklad požadavku a odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="95610-196">Request-response example 2</span></span>

<span data-ttu-id="95610-197">Podrobnosti pro tento příklad požadavku a odpovědi REST jsou následující:</span><span class="sxs-lookup"><span data-stu-id="95610-197">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="95610-198">**Poskytovatel:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="95610-198">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="95610-199">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="95610-199">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="95610-200">**Period**: **Previous**</span><span class="sxs-lookup"><span data-stu-id="95610-200">**Period**: **Previous**</span></span>
- <span data-ttu-id="95610-201">**SeekOperation**: **Další**</span><span class="sxs-lookup"><span data-stu-id="95610-201">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="95610-202">Příklad žádosti 2</span><span class="sxs-lookup"><span data-stu-id="95610-202">Request example 2</span></span>

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

## <a name="response-example-2"></a><span data-ttu-id="95610-203">Příklad odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="95610-203">Response example 2</span></span>

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
