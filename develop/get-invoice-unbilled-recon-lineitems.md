---
title: Získat neúčtované položky řádku odsouhlasení faktury
description: Pomocí rozhraní API partnerského centra můžete získat souhrn nefakturovaných podrobností o položkách řádků odsouhlasení pro zadané období.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: ff69798ddfd91fca817ec0d047bf407f326066c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2020
ms.locfileid: "97767035"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a><span data-ttu-id="2f692-103">Získat neúčtované položky řádku odsouhlasení faktury</span><span class="sxs-lookup"><span data-stu-id="2f692-103">Get invoice's unbilled reconciliation line items</span></span>

<span data-ttu-id="2f692-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="2f692-104">**Applies to:**</span></span>

- <span data-ttu-id="2f692-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="2f692-105">Partner Center</span></span>
- <span data-ttu-id="2f692-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="2f692-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2f692-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="2f692-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2f692-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2f692-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2f692-109">Následující metody můžete použít k získání kolekce podrobností pro nefakturovatelné položky řádku faktury (známé také jako otevřené položky fakturačního řádku).</span><span class="sxs-lookup"><span data-stu-id="2f692-109">You can use the following methods get a collection of details for unbilled invoice line items (also known as open billing line items).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f692-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2f692-110">Prerequisites</span></span>

- <span data-ttu-id="2f692-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2f692-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2f692-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="2f692-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2f692-113">Identifikátor faktury</span><span class="sxs-lookup"><span data-stu-id="2f692-113">An invoice identifier.</span></span> <span data-ttu-id="2f692-114">Určuje fakturu, pro kterou se mají načíst položky řádku.</span><span class="sxs-lookup"><span data-stu-id="2f692-114">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="2f692-115">C\#</span><span class="sxs-lookup"><span data-stu-id="2f692-115">C\#</span></span>

<span data-ttu-id="2f692-116">Chcete-li získat položky řádku pro určenou fakturu, načtěte objekt faktury:</span><span class="sxs-lookup"><span data-stu-id="2f692-116">To get the line items for the specified invoice, retrieve the invoice object:</span></span>

1. <span data-ttu-id="2f692-117">Zavolejte metodu [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , která získá rozhraní k fakturaci operace pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="2f692-117">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="2f692-118">Pro načtení objektu faktury zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) .</span><span class="sxs-lookup"><span data-stu-id="2f692-118">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="2f692-119">Objekt faktury obsahuje všechny informace o zadané faktuře:</span><span class="sxs-lookup"><span data-stu-id="2f692-119">The invoice object contains all of the information for the specified invoice:</span></span>

- <span data-ttu-id="2f692-120">**Zprostředkovatel** identifikuje zdroj nefakturovaných podrobných informací (například **jednorázová**).</span><span class="sxs-lookup"><span data-stu-id="2f692-120">**Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span>

- <span data-ttu-id="2f692-121">**InvoiceLineItemType** určuje typ (například **BillingLineItem**).</span><span class="sxs-lookup"><span data-stu-id="2f692-121">**InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="2f692-122">Získání kolekce položek řádků, které odpovídají instanci **InvoiceDetail** :</span><span class="sxs-lookup"><span data-stu-id="2f692-122">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="2f692-123">Předejte BillingProvider a InvoiceLineItemType instance do metody [**podle**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .</span><span class="sxs-lookup"><span data-stu-id="2f692-123">Pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="2f692-124">Zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) pro načtení přidružených položek řádků.</span><span class="sxs-lookup"><span data-stu-id="2f692-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>

3. <span data-ttu-id="2f692-125">Vytvořte enumerátor pro procházení kolekce.</span><span class="sxs-lookup"><span data-stu-id="2f692-125">Create an enumerator to traverse the collection.</span></span> <span data-ttu-id="2f692-126">Příklad naleznete v následujícím ukázkovém kódu.</span><span class="sxs-lookup"><span data-stu-id="2f692-126">For an example, see the following sample code.</span></span>

<span data-ttu-id="2f692-127">Následující vzorový kód používá smyčku **foreach** ke zpracování kolekce **InvoiceLineItems** .</span><span class="sxs-lookup"><span data-stu-id="2f692-127">The following sample code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="2f692-128">Pro každou **InvoiceLineItemType** se načte samostatná kolekce položek čáry.</span><span class="sxs-lookup"><span data-stu-id="2f692-128">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string currencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type OneTimeInvoiceLineItem
        if (item is OneTimeInvoiceLineItem)
        {
            Type t = typeof(OneTimeInvoiceLineItem);
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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="2f692-129">Podobný příklad najdete v těchto tématech:</span><span class="sxs-lookup"><span data-stu-id="2f692-129">For a similar example, see:</span></span>

- <span data-ttu-id="2f692-130">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2f692-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="2f692-131">Projekt: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="2f692-131">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="2f692-132">Třída: **GetUnBilledReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="2f692-132">Class: **GetUnBilledReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="2f692-133">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="2f692-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2f692-134">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="2f692-134">Request syntax</span></span>

<span data-ttu-id="2f692-135">V závislosti na vašem případu použití můžete pro požadavek REST použít následující syntaxe.</span><span class="sxs-lookup"><span data-stu-id="2f692-135">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="2f692-136">Další informace najdete v popisech jednotlivých syntaxí.</span><span class="sxs-lookup"><span data-stu-id="2f692-136">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="2f692-137">Metoda</span><span class="sxs-lookup"><span data-stu-id="2f692-137">Method</span></span>  | <span data-ttu-id="2f692-138">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="2f692-138">Request URI</span></span>            | <span data-ttu-id="2f692-139">Popis případu použití syntaxe</span><span class="sxs-lookup"><span data-stu-id="2f692-139">Description of syntax use case</span></span>                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2f692-140">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="2f692-140">**GET**</span></span> | <span data-ttu-id="2f692-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = jednorázová&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &perioda = {period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2f692-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="2f692-142">Pomocí této syntaxe vrátíte úplný seznam všech položek řádku pro danou fakturu.</span><span class="sxs-lookup"><span data-stu-id="2f692-142">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="2f692-143">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="2f692-143">**GET**</span></span> | <span data-ttu-id="2f692-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = jednorázová&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2f692-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="2f692-145">Pro velké faktury použijte tuto syntaxi se zadanou velikostí a 0 posunem na základě posunutí stránkovaného seznamu položek řádků.</span><span class="sxs-lookup"><span data-stu-id="2f692-145">For large invoices, use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="2f692-146">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="2f692-146">**GET**</span></span> | <span data-ttu-id="2f692-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = jednorázová&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} &SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="2f692-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="2f692-148">Tuto syntaxi použijte k získání další stránky položek řádku odsouhlasení pomocí `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="2f692-148">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2f692-149">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="2f692-149">URI parameters</span></span>

<span data-ttu-id="2f692-150">Při vytváření žádosti použijte následující identifikátor URI a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="2f692-150">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="2f692-151">Název</span><span class="sxs-lookup"><span data-stu-id="2f692-151">Name</span></span>                   | <span data-ttu-id="2f692-152">Typ</span><span class="sxs-lookup"><span data-stu-id="2f692-152">Type</span></span>   | <span data-ttu-id="2f692-153">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="2f692-153">Required</span></span> | <span data-ttu-id="2f692-154">Popis</span><span class="sxs-lookup"><span data-stu-id="2f692-154">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="2f692-155">ID faktury</span><span class="sxs-lookup"><span data-stu-id="2f692-155">invoice-id</span></span>             | <span data-ttu-id="2f692-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="2f692-156">string</span></span> | <span data-ttu-id="2f692-157">Yes</span><span class="sxs-lookup"><span data-stu-id="2f692-157">Yes</span></span>      | <span data-ttu-id="2f692-158">Řetězec, který identifikuje fakturu.</span><span class="sxs-lookup"><span data-stu-id="2f692-158">A string that identifies the invoice.</span></span> <span data-ttu-id="2f692-159">K získání nefakturovaných odhadů použijte příkaz unfakturováno.</span><span class="sxs-lookup"><span data-stu-id="2f692-159">Use 'unbilled' to get unbilled estimates.</span></span> |
| <span data-ttu-id="2f692-160">Zprostředkovatel</span><span class="sxs-lookup"><span data-stu-id="2f692-160">provider</span></span>               | <span data-ttu-id="2f692-161">řetězec</span><span class="sxs-lookup"><span data-stu-id="2f692-161">string</span></span> | <span data-ttu-id="2f692-162">Yes</span><span class="sxs-lookup"><span data-stu-id="2f692-162">Yes</span></span>      | <span data-ttu-id="2f692-163">Zprostředkovatel: "jednorázová".</span><span class="sxs-lookup"><span data-stu-id="2f692-163">The provider: "OneTime".</span></span>                                                |
| <span data-ttu-id="2f692-164">faktura-line-Item-Type</span><span class="sxs-lookup"><span data-stu-id="2f692-164">invoice-line-item-type</span></span> | <span data-ttu-id="2f692-165">řetězec</span><span class="sxs-lookup"><span data-stu-id="2f692-165">string</span></span> | <span data-ttu-id="2f692-166">Yes</span><span class="sxs-lookup"><span data-stu-id="2f692-166">Yes</span></span>      | <span data-ttu-id="2f692-167">Typ podrobností o faktuře: "BillingLineItems".</span><span class="sxs-lookup"><span data-stu-id="2f692-167">The type of invoice detail: "BillingLineItems".</span></span>               |
| <span data-ttu-id="2f692-168">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="2f692-168">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="2f692-169">bool</span><span class="sxs-lookup"><span data-stu-id="2f692-169">bool</span></span>   | <span data-ttu-id="2f692-170">No</span><span class="sxs-lookup"><span data-stu-id="2f692-170">No</span></span>       | <span data-ttu-id="2f692-171">Hodnota, která označuje, zda se mají vracet položky řádku s použitím realizovaného kreditu.</span><span class="sxs-lookup"><span data-stu-id="2f692-171">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="2f692-172">Poznámka: Tento parametr bude použit pouze v případě, že typ zprostředkovatele je jednorázová a InvoiceLineItemType je UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="2f692-172">Note: this parameter will be only applied when provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span>
| <span data-ttu-id="2f692-173">currencyCode</span><span class="sxs-lookup"><span data-stu-id="2f692-173">currencyCode</span></span>           | <span data-ttu-id="2f692-174">řetězec</span><span class="sxs-lookup"><span data-stu-id="2f692-174">string</span></span> | <span data-ttu-id="2f692-175">Yes</span><span class="sxs-lookup"><span data-stu-id="2f692-175">Yes</span></span>      | <span data-ttu-id="2f692-176">Kód měny pro nefakturovatelné položky řádku</span><span class="sxs-lookup"><span data-stu-id="2f692-176">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="2f692-177">period</span><span class="sxs-lookup"><span data-stu-id="2f692-177">period</span></span>                 | <span data-ttu-id="2f692-178">řetězec</span><span class="sxs-lookup"><span data-stu-id="2f692-178">string</span></span> | <span data-ttu-id="2f692-179">Yes</span><span class="sxs-lookup"><span data-stu-id="2f692-179">Yes</span></span>      | <span data-ttu-id="2f692-180">Období pro nefakturované rekognoskaci.</span><span class="sxs-lookup"><span data-stu-id="2f692-180">The period for unbilled recon.</span></span> <span data-ttu-id="2f692-181">Příklad: Current, Previous.</span><span class="sxs-lookup"><span data-stu-id="2f692-181">example: current, previous.</span></span>                      |
| <span data-ttu-id="2f692-182">size</span><span class="sxs-lookup"><span data-stu-id="2f692-182">size</span></span>                   | <span data-ttu-id="2f692-183">číslo</span><span class="sxs-lookup"><span data-stu-id="2f692-183">number</span></span> | <span data-ttu-id="2f692-184">No</span><span class="sxs-lookup"><span data-stu-id="2f692-184">No</span></span>       | <span data-ttu-id="2f692-185">Maximální počet položek, které se mají vrátit.</span><span class="sxs-lookup"><span data-stu-id="2f692-185">The maximum number of items to return.</span></span> <span data-ttu-id="2f692-186">Výchozí velikost je 2000.</span><span class="sxs-lookup"><span data-stu-id="2f692-186">Default size is 2000</span></span>                     |
| <span data-ttu-id="2f692-187">seekOperation</span><span class="sxs-lookup"><span data-stu-id="2f692-187">seekOperation</span></span>          | <span data-ttu-id="2f692-188">řetězec</span><span class="sxs-lookup"><span data-stu-id="2f692-188">string</span></span> | <span data-ttu-id="2f692-189">No</span><span class="sxs-lookup"><span data-stu-id="2f692-189">No</span></span>       | <span data-ttu-id="2f692-190">Nastavte seekOperation = Next pro získání další stránky rekognoskaci položek řádků.</span><span class="sxs-lookup"><span data-stu-id="2f692-190">Set seekOperation=Next to get the next page of recon line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="2f692-191">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="2f692-191">Request headers</span></span>

<span data-ttu-id="2f692-192">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2f692-192">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2f692-193">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="2f692-193">Request body</span></span>

<span data-ttu-id="2f692-194">Žádné</span><span class="sxs-lookup"><span data-stu-id="2f692-194">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="2f692-195">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="2f692-195">REST response</span></span>

<span data-ttu-id="2f692-196">V případě úspěchu obsahuje odpověď kolekci podrobností položky řádku.</span><span class="sxs-lookup"><span data-stu-id="2f692-196">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="2f692-197">*Pro položku řádku **ChargeType** je hodnota **Nákup** namapována na hodnotu **New** a **náhrada** hodnoty je namapována na **Canceled**.*</span><span class="sxs-lookup"><span data-stu-id="2f692-197">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2f692-198">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="2f692-198">Response success and error codes</span></span>

<span data-ttu-id="2f692-199">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="2f692-199">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2f692-200">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="2f692-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2f692-201">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2f692-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="request-response-examples"></a><span data-ttu-id="2f692-202">Příklady požadavků a odpovědí</span><span class="sxs-lookup"><span data-stu-id="2f692-202">Request-response examples</span></span>

#### <a name="request-response-example-1"></a><span data-ttu-id="2f692-203">Požadavek-odpověď – příklad 1</span><span class="sxs-lookup"><span data-stu-id="2f692-203">Request-response example 1</span></span>

<span data-ttu-id="2f692-204">Následující podrobnosti se vztahují na tento příklad:</span><span class="sxs-lookup"><span data-stu-id="2f692-204">The following details apply to this example:</span></span>

- <span data-ttu-id="2f692-205">Zprostředkovatel: **jednorázová**</span><span class="sxs-lookup"><span data-stu-id="2f692-205">Provider: **OneTime**</span></span>
- <span data-ttu-id="2f692-206">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="2f692-206">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="2f692-207">Období: **Předchozí**</span><span class="sxs-lookup"><span data-stu-id="2f692-207">Period: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="2f692-208">Příklad žádosti 1</span><span class="sxs-lookup"><span data-stu-id="2f692-208">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="2f692-209">Příklad odpovědi 1</span><span class="sxs-lookup"><span data-stu-id="2f692-209">Response example 1</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "HJVtMZMkgQ2miuCiNv0RSr51zQDans0m1",
            "orderDate": "2019-02-04T17:59:52.9460102Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0002",
            "availabilityId": "DZH318Z0BP8B",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Medium Plan",
            "chargeType": "New",
            "unitPrice": 820,
            "effectiveUnitPrice": 820,
            "unitType": "",
            "quantity": 1,
            "subtotal": 820,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-9cf0-4a1f-9514-7fcc7fe9d1fe",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 3.1618,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "883d475b-0000-1234-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="2f692-210">Požadavek-odpověď – příklad 2</span><span class="sxs-lookup"><span data-stu-id="2f692-210">Request-response example 2</span></span>

<span data-ttu-id="2f692-211">Následující podrobnosti se vztahují na tento příklad:</span><span class="sxs-lookup"><span data-stu-id="2f692-211">The following details apply to this example:</span></span>

- <span data-ttu-id="2f692-212">Zprostředkovatel: **jednorázová**</span><span class="sxs-lookup"><span data-stu-id="2f692-212">Provider: **OneTime**</span></span>
- <span data-ttu-id="2f692-213">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="2f692-213">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="2f692-214">Období: **Předchozí**</span><span class="sxs-lookup"><span data-stu-id="2f692-214">Period: **Previous**</span></span>
- <span data-ttu-id="2f692-215">SeekOperation: **Další**</span><span class="sxs-lookup"><span data-stu-id="2f692-215">SeekOperation: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="2f692-216">Příklad žádosti 2</span><span class="sxs-lookup"><span data-stu-id="2f692-216">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=billinglineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="2f692-217">Příklad odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="2f692-217">Response example 2</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": ""
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

#### <a name="request-example-3"></a><span data-ttu-id="2f692-218">Příklad žádosti 3</span><span class="sxs-lookup"><span data-stu-id="2f692-218">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=OneTime&invoiceLineItemType=UsageLineItems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="2f692-219">Příklad odpovědi 3</span><span class="sxs-lookup"><span data-stu-id="2f692-219">Response example 3</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "PartnerName": "testPartner",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "invoiceNumber": "T11ETHHDDD",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "publisherId": "21223810",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "subscriptionDescription": "sub description",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "UsageDate": "2019-02-07T09:22:34.6455294-08:00",
            "MeterType": "type",
            "MeterCategory": "category",
            "MeterId": "21312312312-fdsfsd",
            "MeterSubCategory": "subcategory",
            "MeterName": "meter name",
            "MeterRegion": "meter region",
            "UnitOfMeasure": "11",
            "skuName": "Test WaaS - Large Plan",
            "publisherName": "Test Networks, Inc.",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "discountDetails": "",
            "providerSource": "All",
            "RateOfPartnerEarnedCredit": 0.15,
            "IsPartnerEarnedCreditApplied": true,
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
