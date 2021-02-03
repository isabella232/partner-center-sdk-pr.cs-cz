---
title: Získat fakturovatelné položky řádkové spotřeby pro komerční spotřebu
description: Pomocí rozhraní API partnerského centra můžete získat informace o neúčtovaných podrobnostech o položkách na řádcích komerční spotřeby pro zadanou fakturu.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 594946db712c28983dd390207fb06c8d9f62f18b
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97766977"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="5138b-103">Získat fakturovatelné položky řádkové spotřeby pro komerční spotřebu</span><span class="sxs-lookup"><span data-stu-id="5138b-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="5138b-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="5138b-104">**Applies to:**</span></span>

- <span data-ttu-id="5138b-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="5138b-105">Partner Center</span></span>

<span data-ttu-id="5138b-106">Jak získat informace o nefakturovatelné položce komerčního řádku spotřeby.</span><span class="sxs-lookup"><span data-stu-id="5138b-106">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="5138b-107">Pomocí následujících metod můžete získat kolekci podrobností o neúčtovaných položkách na řádcích komerční spotřeby (označují se také jako otevřené položky řádků použití) prostřednictvím kódu programu.</span><span class="sxs-lookup"><span data-stu-id="5138b-107">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="5138b-108">Denní hodnocení využití obvykle trvá 24 hodin, než se zobrazí v partnerském centru nebo je k němu možné přistupovat prostřednictvím rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="5138b-108">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5138b-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5138b-109">Prerequisites</span></span>

- <span data-ttu-id="5138b-110">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5138b-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5138b-111">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="5138b-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5138b-112">Identifikátor faktury</span><span class="sxs-lookup"><span data-stu-id="5138b-112">An invoice identifier.</span></span> <span data-ttu-id="5138b-113">Určuje fakturu, pro kterou se mají načíst položky řádku.</span><span class="sxs-lookup"><span data-stu-id="5138b-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="5138b-114">C\#</span><span class="sxs-lookup"><span data-stu-id="5138b-114">C\#</span></span>

<span data-ttu-id="5138b-115">Získání položek řádků pro určenou fakturu:</span><span class="sxs-lookup"><span data-stu-id="5138b-115">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="5138b-116">Zavolejte metodu [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , která získá rozhraní k fakturaci operace pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="5138b-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="5138b-117">Pro načtení objektu faktury zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) .</span><span class="sxs-lookup"><span data-stu-id="5138b-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="5138b-118">**Objekt faktury** obsahuje všechny informace o zadané faktuře.</span><span class="sxs-lookup"><span data-stu-id="5138b-118">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="5138b-119">**Zprostředkovatel** identifikuje zdroj nefakturovaných podrobných informací (například **jednorázová**).</span><span class="sxs-lookup"><span data-stu-id="5138b-119">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="5138b-120">**InvoiceLineItemType** určuje typ (například **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="5138b-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="5138b-121">Následující příklad kódu používá smyčku **foreach** ke zpracování kolekce **InvoiceLineItems** .</span><span class="sxs-lookup"><span data-stu-id="5138b-121">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="5138b-122">Pro každou **InvoiceLineItemType** se načte samostatná kolekce položek čáry.</span><span class="sxs-lookup"><span data-stu-id="5138b-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="5138b-123">Získání kolekce položek řádků, které odpovídají instanci **InvoiceDetail** :</span><span class="sxs-lookup"><span data-stu-id="5138b-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="5138b-124">Předejte **BillingProvider** a **InvoiceLineItemType** instance do metody [**podle**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .</span><span class="sxs-lookup"><span data-stu-id="5138b-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="5138b-125">Zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) pro načtení přidružených položek řádků.</span><span class="sxs-lookup"><span data-stu-id="5138b-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="5138b-126">Vytvořte enumerátor pro procházení kolekce, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="5138b-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine items count: " + seekBasedResourceCollection.Items.Count());

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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="5138b-127">Podobný příklad najdete v těchto tématech:</span><span class="sxs-lookup"><span data-stu-id="5138b-127">For a similar example, see:</span></span>

- <span data-ttu-id="5138b-128">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5138b-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="5138b-129">Projekt: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="5138b-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="5138b-130">Třída: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="5138b-130">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="5138b-131">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="5138b-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5138b-132">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="5138b-132">Request syntax</span></span>

<span data-ttu-id="5138b-133">V závislosti na vašem případu použití můžete pro požadavek REST použít následující syntaxe.</span><span class="sxs-lookup"><span data-stu-id="5138b-133">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="5138b-134">Další informace najdete v popisech jednotlivých syntaxí.</span><span class="sxs-lookup"><span data-stu-id="5138b-134">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="5138b-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="5138b-135">Method</span></span>  | <span data-ttu-id="5138b-136">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="5138b-136">Request URI</span></span>         | <span data-ttu-id="5138b-137">Popis případu použití syntaxe</span><span class="sxs-lookup"><span data-stu-id="5138b-137">Description of syntax use case</span></span> |                                                                                                                                            |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5138b-138">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="5138b-138">**GET**</span></span> | <span data-ttu-id="5138b-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/unbilled/LineItems? Provider = jednorázová&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &perioda = {period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5138b-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="5138b-140">Pomocí této syntaxe vrátíte úplný seznam všech položek řádku pro danou fakturu.</span><span class="sxs-lookup"><span data-stu-id="5138b-140">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="5138b-141">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="5138b-141">**GET**</span></span> | <span data-ttu-id="5138b-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/unbilled/LineItems? Provider = jednorázová&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5138b-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="5138b-143">Použijte tuto syntaxi pro velké faktury.</span><span class="sxs-lookup"><span data-stu-id="5138b-143">Use this syntax for large invoices.</span></span> <span data-ttu-id="5138b-144">Tuto syntaxi použijte se zadanou velikostí a 0 posunutím pro vrácení stránkovaného seznamu položek řádků.</span><span class="sxs-lookup"><span data-stu-id="5138b-144">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="5138b-145">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="5138b-145">**GET**</span></span> | <span data-ttu-id="5138b-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/unbilled/LineItems? Provider = jednorázová&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} &SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="5138b-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="5138b-147">Tuto syntaxi použijte k získání další stránky položek řádku odsouhlasení pomocí `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="5138b-147">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="5138b-148">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="5138b-148">URI parameters</span></span>

<span data-ttu-id="5138b-149">Při vytváření žádosti použijte následující identifikátor URI a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="5138b-149">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="5138b-150">Název</span><span class="sxs-lookup"><span data-stu-id="5138b-150">Name</span></span>                   | <span data-ttu-id="5138b-151">Typ</span><span class="sxs-lookup"><span data-stu-id="5138b-151">Type</span></span>   | <span data-ttu-id="5138b-152">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="5138b-152">Required</span></span> | <span data-ttu-id="5138b-153">Popis</span><span class="sxs-lookup"><span data-stu-id="5138b-153">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="5138b-154">Zprostředkovatel</span><span class="sxs-lookup"><span data-stu-id="5138b-154">provider</span></span>               | <span data-ttu-id="5138b-155">řetězec</span><span class="sxs-lookup"><span data-stu-id="5138b-155">string</span></span> | <span data-ttu-id="5138b-156">Yes</span><span class="sxs-lookup"><span data-stu-id="5138b-156">Yes</span></span>      | <span data-ttu-id="5138b-157">Zprostředkovatel: "**jednorázová**".</span><span class="sxs-lookup"><span data-stu-id="5138b-157">The provider: "**OneTime**".</span></span>                                                |
| <span data-ttu-id="5138b-158">faktura-line-Item-Type</span><span class="sxs-lookup"><span data-stu-id="5138b-158">invoice-line-item-type</span></span> | <span data-ttu-id="5138b-159">řetězec</span><span class="sxs-lookup"><span data-stu-id="5138b-159">string</span></span> | <span data-ttu-id="5138b-160">Yes</span><span class="sxs-lookup"><span data-stu-id="5138b-160">Yes</span></span>      | <span data-ttu-id="5138b-161">Typ podrobností o faktuře: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="5138b-161">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>               |
| <span data-ttu-id="5138b-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="5138b-162">currencyCode</span></span>           | <span data-ttu-id="5138b-163">řetězec</span><span class="sxs-lookup"><span data-stu-id="5138b-163">string</span></span> | <span data-ttu-id="5138b-164">Yes</span><span class="sxs-lookup"><span data-stu-id="5138b-164">Yes</span></span>      | <span data-ttu-id="5138b-165">Kód měny pro nefakturovatelné položky řádku</span><span class="sxs-lookup"><span data-stu-id="5138b-165">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="5138b-166">period</span><span class="sxs-lookup"><span data-stu-id="5138b-166">period</span></span>                 | <span data-ttu-id="5138b-167">řetězec</span><span class="sxs-lookup"><span data-stu-id="5138b-167">string</span></span> | <span data-ttu-id="5138b-168">Yes</span><span class="sxs-lookup"><span data-stu-id="5138b-168">Yes</span></span>      | <span data-ttu-id="5138b-169">Období pro nefakturované rekognoskaci (například: **Current**, **Previous**).</span><span class="sxs-lookup"><span data-stu-id="5138b-169">The period for unbilled recon (for example: **current**, **previous**).</span></span><br/><br/><span data-ttu-id="5138b-170">**Předchozí** – Pokud je fakturační cyklus 01/01/2020 – 01/31/2020 a pak s největší pravděpodobnější, že se vaše faktura vygenerovala mezi 02/06/2020 a časem 02/08/2020 UTC.</span><span class="sxs-lookup"><span data-stu-id="5138b-170">**Previous** – if the billing cycle is 01/01/2020 – 01/31/2020 then, most likely that your invoice is generated between 02/06/2020 and 02/08/2020 UTC time.</span></span> <span data-ttu-id="5138b-171">Pokud potřebujete zadat dotaz na data o neúčtovaném využití fakturačního cyklu (01/01/2020 – 01/31/2020) kdykoli mezi 02/01/2020 a datem vygenerování faktury (mezi 02/06/2020 a 02/08/2020 času UTC), pak musíte zvolit perioda jako "předchozí".</span><span class="sxs-lookup"><span data-stu-id="5138b-171">If you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) on any time between 02/01/2020 and the invoice-generated date (which is between 02/06/2020 and 02/08/2020 UTC time), then, you need to choose Period as "Previous".</span></span><br/><br/><span data-ttu-id="5138b-172">**Current** – Pokud je fakturační cyklus 01/01/2020 – 01/31/2020 02/08/2020 a pak je pravděpodobně vygenerována vaše faktura mezi 02/06/2020 a časem UTC.</span><span class="sxs-lookup"><span data-stu-id="5138b-172">**Current** – if the billing cycle is 01/01/2020 – 01/31/2020 then, most likely that your invoice is generated between 02/06/2020 and 02/08/2020 UTC time.</span></span> <span data-ttu-id="5138b-173">Pokud potřebujete zadat dotaz na nefakturovaná data o využití fakturačního cyklu (01/01/2020 – 01/31/2020), kdykoli mezi 01/01/2020 a 01/31/2020, která jsou v rámci fakturačního cyklu, musíte zvolit perioda jako "aktuální".</span><span class="sxs-lookup"><span data-stu-id="5138b-173">If you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) on any time between 01/01/2020 and 01/31/2020 which is within your billing cycle, then, you need to choose Period as "Current".</span></span> |
| <span data-ttu-id="5138b-174">size</span><span class="sxs-lookup"><span data-stu-id="5138b-174">size</span></span>                   | <span data-ttu-id="5138b-175">číslo</span><span class="sxs-lookup"><span data-stu-id="5138b-175">number</span></span> | <span data-ttu-id="5138b-176">No</span><span class="sxs-lookup"><span data-stu-id="5138b-176">No</span></span>       | <span data-ttu-id="5138b-177">Maximální počet položek, které se mají vrátit.</span><span class="sxs-lookup"><span data-stu-id="5138b-177">The maximum number of items to return.</span></span> <span data-ttu-id="5138b-178">Výchozí velikost je 2000.</span><span class="sxs-lookup"><span data-stu-id="5138b-178">The default size is 2000.</span></span>                    |
| <span data-ttu-id="5138b-179">seekOperation</span><span class="sxs-lookup"><span data-stu-id="5138b-179">seekOperation</span></span>          | <span data-ttu-id="5138b-180">řetězec</span><span class="sxs-lookup"><span data-stu-id="5138b-180">string</span></span> | <span data-ttu-id="5138b-181">No</span><span class="sxs-lookup"><span data-stu-id="5138b-181">No</span></span>       | <span data-ttu-id="5138b-182">Nastavte `seekOperation=Next` , aby se získala další stránka položek řádku odsouhlasení.</span><span class="sxs-lookup"><span data-stu-id="5138b-182">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="5138b-183">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="5138b-183">Request headers</span></span>

<span data-ttu-id="5138b-184">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5138b-184">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5138b-185">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="5138b-185">Request body</span></span>

<span data-ttu-id="5138b-186">Žádné</span><span class="sxs-lookup"><span data-stu-id="5138b-186">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="5138b-187">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="5138b-187">REST response</span></span>

<span data-ttu-id="5138b-188">V případě úspěchu obsahuje odpověď kolekci podrobností položky řádku.</span><span class="sxs-lookup"><span data-stu-id="5138b-188">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="5138b-189">*Pro položku řádku **ChargeType** je hodnota **Nákup** namapována na hodnotu **New** a **náhrada** hodnoty je namapována na **Canceled**.*</span><span class="sxs-lookup"><span data-stu-id="5138b-189">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5138b-190">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="5138b-190">Response success and error codes</span></span>

<span data-ttu-id="5138b-191">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="5138b-191">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5138b-192">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="5138b-192">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5138b-193">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5138b-193">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="5138b-194">Příklady požadavků a odpovědí</span><span class="sxs-lookup"><span data-stu-id="5138b-194">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="5138b-195">Požadavek-odpověď – příklad 1</span><span class="sxs-lookup"><span data-stu-id="5138b-195">Request-response example 1</span></span>

<span data-ttu-id="5138b-196">Následující podrobnosti se vztahují na tento příklad:</span><span class="sxs-lookup"><span data-stu-id="5138b-196">The following details apply to this example:</span></span>

- <span data-ttu-id="5138b-197">**Zprostředkovatel**: **jednorázová**</span><span class="sxs-lookup"><span data-stu-id="5138b-197">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="5138b-198">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="5138b-198">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="5138b-199">**Období**: **předchozí**</span><span class="sxs-lookup"><span data-stu-id="5138b-199">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="5138b-200">Příklad žádosti 1</span><span class="sxs-lookup"><span data-stu-id="5138b-200">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

### <a name="response-example-1"></a><span data-ttu-id="5138b-201">Příklad odpovědi 1</span><span class="sxs-lookup"><span data-stu-id="5138b-201">Response example 1</span></span>

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-01T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "1234547f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
         },
         {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d12345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="5138b-202">Požadavek-odpověď – příklad 2</span><span class="sxs-lookup"><span data-stu-id="5138b-202">Request-response example 2</span></span>

<span data-ttu-id="5138b-203">Následující podrobnosti se vztahují na tento příklad:</span><span class="sxs-lookup"><span data-stu-id="5138b-203">The following details apply to this example:</span></span>

- <span data-ttu-id="5138b-204">**Zprostředkovatel**: **jednorázová**</span><span class="sxs-lookup"><span data-stu-id="5138b-204">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="5138b-205">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="5138b-205">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="5138b-206">**Období**: **předchozí**</span><span class="sxs-lookup"><span data-stu-id="5138b-206">**Period**: **Previous**</span></span>
- <span data-ttu-id="5138b-207">**SeekOperation**: **Další**</span><span class="sxs-lookup"><span data-stu-id="5138b-207">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="5138b-208">Příklad žádosti 2</span><span class="sxs-lookup"><span data-stu-id="5138b-208">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="5138b-209">Příklad odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="5138b-209">Response example 2</span></span>

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
