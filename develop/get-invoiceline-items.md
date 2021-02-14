---
title: Získání řádkových položek faktury
description: Pomocí rozhraní API partnerského centra můžete získat podrobnosti o položce řádku faktury (s uzavřenou položkou fakturačního řádku) pro zadanou fakturu.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e797f549e1344268c8167259a231122e7c669a2e
ms.sourcegitcommit: 9f8ba784171ab4f980ed0c60ef6f2323849c4a98
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2021
ms.locfileid: "100499894"
---
# <a name="get-invoice-line-items"></a><span data-ttu-id="12216-103">Získání řádkových položek faktury</span><span class="sxs-lookup"><span data-stu-id="12216-103">Get invoice line items</span></span>

<span data-ttu-id="12216-104">**Platí pro:**</span><span class="sxs-lookup"><span data-stu-id="12216-104">**Applies to:**</span></span>

- <span data-ttu-id="12216-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="12216-105">Partner Center</span></span>
- <span data-ttu-id="12216-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="12216-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="12216-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="12216-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="12216-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="12216-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="12216-109">Následující metody můžete použít k získání podrobností kolekce pro položky řádku faktury (známé také jako řádky s uzavřenými fakturačními položkami) pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="12216-109">You can use the following methods to get a collection details for of invoice line items (also known as closed billing line items) for a specified invoice.</span></span>

<span data-ttu-id="12216-110">*S výjimkou oprav chyb už toto rozhraní API není aktualizované.*</span><span class="sxs-lookup"><span data-stu-id="12216-110">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="12216-111">Své aplikace byste měli aktualizovat tak, aby místo **webu Marketplace** volala rozhraní **jednorázová** API.</span><span class="sxs-lookup"><span data-stu-id="12216-111">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="12216-112">Rozhraní **jednorázová** API poskytuje další funkce a bude se dál aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="12216-112">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="12216-113">**Jednorázová** byste měli použít k dotazování na všechny položky řádkové spotřeby místo na **webu Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="12216-113">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="12216-114">Případně můžete postupovat podle odkazů ve voláních odkazů na odhad.</span><span class="sxs-lookup"><span data-stu-id="12216-114">Or, you can follow the links in the estimate links call.</span></span>

<span data-ttu-id="12216-115">Toto rozhraní API podporuje také **poskytovatele služeb** **Azure** a **Office** for Microsoft Azure (MS-AZR-0145P) a nabídky pro Office, které zpřístupňuje funkci rozhraní API zpětně kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="12216-115">This API also supports the **provider** types of **azure** and **office** for Microsoft Azure (MS-AZR-0145P) subscriptions and Office offers, which makes the API feature backward compatible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12216-116">Požadavky</span><span class="sxs-lookup"><span data-stu-id="12216-116">Prerequisites</span></span>

- <span data-ttu-id="12216-117">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="12216-117">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="12216-118">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="12216-118">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="12216-119">Identifikátor faktury</span><span class="sxs-lookup"><span data-stu-id="12216-119">An invoice identifier.</span></span> <span data-ttu-id="12216-120">Určuje fakturu, pro kterou se mají načíst položky řádku.</span><span class="sxs-lookup"><span data-stu-id="12216-120">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="12216-121">C\#</span><span class="sxs-lookup"><span data-stu-id="12216-121">C\#</span></span>

<span data-ttu-id="12216-122">Získání položek řádků pro určenou fakturu:</span><span class="sxs-lookup"><span data-stu-id="12216-122">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="12216-123">Zavolejte metodu [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , která získá rozhraní k fakturaci operace pro zadanou fakturu.</span><span class="sxs-lookup"><span data-stu-id="12216-123">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="12216-124">Pro načtení objektu faktury zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) .</span><span class="sxs-lookup"><span data-stu-id="12216-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="12216-125">Objekt faktury obsahuje všechny informace o zadané faktuře.</span><span class="sxs-lookup"><span data-stu-id="12216-125">The invoice object contains all of the information for the specified invoice.</span></span>
3. <span data-ttu-id="12216-126">Pomocí vlastnosti [**uzlu InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) objektu faktury získáte přístup ke kolekci objektů [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) , z nichž každá obsahuje [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) a [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span><span class="sxs-lookup"><span data-stu-id="12216-126">Use the invoice object's [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) property to get access to a collection of [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) objects, each of which contains a [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) and an [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span></span> <span data-ttu-id="12216-127">**BillingProvider** identifikuje zdroj informací o podrobnostech faktury (například **Office**, **Azure**, **jednorázová**) a **InvoiceLineItemType** určuje typ (například **BillingLineItem**).</span><span class="sxs-lookup"><span data-stu-id="12216-127">The **BillingProvider** identifies the source of the invoice detail information (such as **Office**, **Azure**, **OneTime**), and the **InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="12216-128">Následující příklad kódu používá smyčku **foreach** ke zpracování kolekce **uzlu InvoiceDetails** .</span><span class="sxs-lookup"><span data-stu-id="12216-128">The following example code uses a **foreach** loop to process the **InvoiceDetails** collection.</span></span> <span data-ttu-id="12216-129">Pro každou instanci **InvoiceDetail** se načtou samostatné kolekce položek řádků.</span><span class="sxs-lookup"><span data-stu-id="12216-129">A separate collection of line items is retrieved for each **InvoiceDetail** instance.</span></span>

<span data-ttu-id="12216-130">Získání kolekce položek řádků, které odpovídají instanci **InvoiceDetail** :</span><span class="sxs-lookup"><span data-stu-id="12216-130">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="12216-131">Předejte **BillingProvider** a **InvoiceLineItemType** instance do metody [**podle**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .</span><span class="sxs-lookup"><span data-stu-id="12216-131">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="12216-132">Zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) pro načtení přidružených položek řádků.</span><span class="sxs-lookup"><span data-stu-id="12216-132">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="12216-133">Vytvořte enumerátor pro procházení kolekce, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="12216-133">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;
// string invoiceId;

// Retrieve the invoice.
var invoiceOperations = partnerOperations.Invoices.ById(invoiceId);
var invoice = invoiceOperations.Get();

foreach (var invoiceDetail in invoice.InvoiceDetails)
{
    Console.WriteLine(string.Format("Getting invoice line item for product {0} and line item type {1}",
        invoiceDetail.BillingProvider,
        invoiceDetail.InvoiceLineItemType));

    // Is this an unpaged or paged request?
    bool isUnPaged = (this.invoicePageSize <= 0);

    // If the scenario is unpaged, get all the invoice line items, otherwise get the first page.
    var invoiceLineItemsCollection =
        (isUnPaged)
        ? invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get()
        : invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get(this.invoicePageSize, 0);

    // Create an enumerator for traversing the line items collection.
    var invoiceLineItemEnumerator =
        partnerOperations.Enumerators.InvoiceLineItems.Create(invoiceLineItemsCollection);

    while (invoiceLineItemEnumerator.HasValue)
    {
        // invoiceLineItemEnumerator.Current contains a collection
        // of line items.
        Console.WriteLine(String.Format("invoiceLineItemEnumerator.Current has {0} line items.",
            invoiceLineItemEnumerator.Current.TotalCount));
        //
        // Insert code here to work with the line items.
        //
        Console.WriteLine();
        Console.Write("Press any key to retrieve the next invoice line items page");
        Console.ReadKey();

        // Get the next list of invoice line items.
        invoiceLineItemEnumerator.Next();
    }
}
```

<span data-ttu-id="12216-134">Podobný příklad naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="12216-134">For a similar example, see the following:</span></span>

- <span data-ttu-id="12216-135">Ukázka: [aplikace testů konzoly](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="12216-135">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="12216-136">Projekt: **ukázky sady SDK pro partnerských Center**</span><span class="sxs-lookup"><span data-stu-id="12216-136">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="12216-137">Třída: **GetInvoiceLineItems.cs**</span><span class="sxs-lookup"><span data-stu-id="12216-137">Class: **GetInvoiceLineItems.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="12216-138">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="12216-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="12216-139">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="12216-139">Request syntax</span></span>

<span data-ttu-id="12216-140">Ve svém scénáři proveďte požadavek pomocí vhodné syntaxe pro poskytovatele fakturace.</span><span class="sxs-lookup"><span data-stu-id="12216-140">Make your request using the appropriate syntax for the billing provider in your scenario.</span></span>

#### <a name="office"></a><span data-ttu-id="12216-141">Office</span><span class="sxs-lookup"><span data-stu-id="12216-141">Office</span></span>

<span data-ttu-id="12216-142">Následující syntaxe platí v případě, že je poskytovatel fakturace **Office**.</span><span class="sxs-lookup"><span data-stu-id="12216-142">The following syntax applies when the billing provider is **Office**.</span></span>

| <span data-ttu-id="12216-143">Metoda</span><span class="sxs-lookup"><span data-stu-id="12216-143">Method</span></span>  | <span data-ttu-id="12216-144">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="12216-144">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="12216-145">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="12216-145">**GET**</span></span> | <span data-ttu-id="12216-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = Office&invoicelineitemtype = billinglineitems&size = {size} &posun = {offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="12216-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=office&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>                               |

#### <a name="microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="12216-147">Předplatné Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="12216-147">Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="12216-148">Následující syntaxe Microsoft Azure se použijí, pokud má poskytovatel fakturace předplatné AZR (MS--0145P).</span><span class="sxs-lookup"><span data-stu-id="12216-148">The following syntaxes apply when the billing provider has a Microsoft Azure (MS-AZR-0145P) subscription.</span></span>

| <span data-ttu-id="12216-149">Metoda</span><span class="sxs-lookup"><span data-stu-id="12216-149">Method</span></span>  | <span data-ttu-id="12216-150">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="12216-150">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="12216-151">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="12216-151">**GET**</span></span> | <span data-ttu-id="12216-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = Azure&invoicelineitemtype = billinglineitems&size = {size} &posun = {offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="12216-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |
| <span data-ttu-id="12216-153">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="12216-153">**GET**</span></span> | <span data-ttu-id="12216-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = Azure&invoicelineitemtype = usagelineitems&size = {size} &posun = {offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="12216-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=usagelineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |

##### <a name="onetime"></a><span data-ttu-id="12216-155">Jednorázová</span><span class="sxs-lookup"><span data-stu-id="12216-155">OneTime</span></span>

<span data-ttu-id="12216-156">Následující syntaxe se použijí, když je poskytovatel fakturace **jednorázová**.</span><span class="sxs-lookup"><span data-stu-id="12216-156">The following syntaxes apply when the billing provider is **OneTime**.</span></span> <span data-ttu-id="12216-157">Zahrnuje to i poplatky za rezervace Azure, software, plány Azure a produkty z komerčního tržiště.</span><span class="sxs-lookup"><span data-stu-id="12216-157">This includes charges for Azure reservations, software, Azure plans, and commercial marketplace products.</span></span>

| <span data-ttu-id="12216-158">Metoda</span><span class="sxs-lookup"><span data-stu-id="12216-158">Method</span></span>  | <span data-ttu-id="12216-159">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="12216-159">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="12216-160">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="12216-160">**GET**</span></span> | <span data-ttu-id="12216-161">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems? Provider = jednorázová&invoicelineitemtype = billinglineitems&velikost = {Size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="12216-161">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="12216-162">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="12216-162">**GET**</span></span> | <span data-ttu-id="12216-163">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems/Onetime/billinglineitems&velikost = {Size}? SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="12216-163">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/onetime/billinglineitems&size={size}?seekOperation=Next</span></span>                           |

#### <a name="previous-syntaxes"></a><span data-ttu-id="12216-164">Předchozí syntaxe</span><span class="sxs-lookup"><span data-stu-id="12216-164">Previous syntaxes</span></span>

<span data-ttu-id="12216-165">Pokud používáte následující syntaxe, nezapomeňte použít příslušnou syntaxi pro váš případ použití.</span><span class="sxs-lookup"><span data-stu-id="12216-165">If you are using the following syntaxes, be sure to use the appropriate syntax for your use case.</span></span>

<span data-ttu-id="12216-166">*S výjimkou oprav chyb už toto rozhraní API není aktualizované.*</span><span class="sxs-lookup"><span data-stu-id="12216-166">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="12216-167">Své aplikace byste měli aktualizovat tak, aby místo **webu Marketplace** volala rozhraní **jednorázová** API.</span><span class="sxs-lookup"><span data-stu-id="12216-167">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="12216-168">Rozhraní **jednorázová** API poskytuje další funkce a bude se dál aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="12216-168">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="12216-169">**Jednorázová** byste měli použít k dotazování na všechny položky řádkové spotřeby místo na **webu Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="12216-169">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="12216-170">Případně můžete postupovat podle odkazů ve voláních odkazů na odhad.</span><span class="sxs-lookup"><span data-stu-id="12216-170">Or, you can follow the links in the estimate links call.</span></span>

| <span data-ttu-id="12216-171">Metoda</span><span class="sxs-lookup"><span data-stu-id="12216-171">Method</span></span> | <span data-ttu-id="12216-172">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="12216-172">Request URI</span></span> | <span data-ttu-id="12216-173">Popis případu použití syntaxe</span><span class="sxs-lookup"><span data-stu-id="12216-173">Description of syntax use case</span></span> |
| ------ | ----------- | -------------------------------- |
| <span data-ttu-id="12216-174">GET</span><span class="sxs-lookup"><span data-stu-id="12216-174">GET</span></span> | <span data-ttu-id="12216-175">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems/{Billing-Provider}/{Invoice-line-Item-Type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="12216-175">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type} HTTP/1.1</span></span>                              | <span data-ttu-id="12216-176">Tuto syntaxi můžete použít k vrácení úplného seznamu každé položky řádku pro danou fakturu.</span><span class="sxs-lookup"><span data-stu-id="12216-176">You can use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="12216-177">GET</span><span class="sxs-lookup"><span data-stu-id="12216-177">GET</span></span> | <span data-ttu-id="12216-178">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems/{Billing-Provider}/{Invoice-line-Item-Type}? size = {size} &posun = {offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="12216-178">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type}?size={size}&offset={offset} HTTP/1.1</span></span>  | <span data-ttu-id="12216-179">Pro velké faktury můžete použít tuto syntaxi se zadanou velikostí a 0 posunutím k vrácení stránkovaného seznamu položek řádků.</span><span class="sxs-lookup"><span data-stu-id="12216-179">For large invoices, you can use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="12216-180">GET</span><span class="sxs-lookup"><span data-stu-id="12216-180">GET</span></span> | <span data-ttu-id="12216-181">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems/OneTime/{Invoice-line-Item-Type}? SeekOperation = další</span><span class="sxs-lookup"><span data-stu-id="12216-181">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/OneTime/{invoice-line-item-type}?seekOperation=Next</span></span>                               | <span data-ttu-id="12216-182">Tuto syntaxi můžete použít pro fakturu s hodnotou poskytovatele fakturace **jednorázová** a nastavením **seekOperation** na **Další** pro získání další stránky položek řádků faktury.</span><span class="sxs-lookup"><span data-stu-id="12216-182">You can use this syntax for an invoice with a billing-provider value of **OneTime** and set **seekOperation** to **Next** to get the next page of invoice line items.</span></span> |

##### <a name="uri-parameters"></a><span data-ttu-id="12216-183">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="12216-183">URI parameters</span></span>

<span data-ttu-id="12216-184">Při vytváření žádosti použijte následující identifikátor URI a parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="12216-184">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="12216-185">Název</span><span class="sxs-lookup"><span data-stu-id="12216-185">Name</span></span>                   | <span data-ttu-id="12216-186">Typ</span><span class="sxs-lookup"><span data-stu-id="12216-186">Type</span></span>   | <span data-ttu-id="12216-187">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="12216-187">Required</span></span> | <span data-ttu-id="12216-188">Popis</span><span class="sxs-lookup"><span data-stu-id="12216-188">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="12216-189">ID faktury</span><span class="sxs-lookup"><span data-stu-id="12216-189">invoice-id</span></span>             | <span data-ttu-id="12216-190">řetězec</span><span class="sxs-lookup"><span data-stu-id="12216-190">string</span></span> | <span data-ttu-id="12216-191">Yes</span><span class="sxs-lookup"><span data-stu-id="12216-191">Yes</span></span>      | <span data-ttu-id="12216-192">Řetězec, který identifikuje fakturu.</span><span class="sxs-lookup"><span data-stu-id="12216-192">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="12216-193">fakturace – poskytovatel</span><span class="sxs-lookup"><span data-stu-id="12216-193">billing-provider</span></span>       | <span data-ttu-id="12216-194">řetězec</span><span class="sxs-lookup"><span data-stu-id="12216-194">string</span></span> | <span data-ttu-id="12216-195">Yes</span><span class="sxs-lookup"><span data-stu-id="12216-195">Yes</span></span>      | <span data-ttu-id="12216-196">Zprostředkovatel fakturace: "Office", "Azure", "jednorázová".</span><span class="sxs-lookup"><span data-stu-id="12216-196">The billing provider: "Office", "Azure", "OneTime".</span></span> <span data-ttu-id="12216-197">Ve starší verzi máme pro Office & transakcí Azure samostatné datové modely.</span><span class="sxs-lookup"><span data-stu-id="12216-197">In the legacy, we have separate data models for Office & Azure transactions.</span></span> <span data-ttu-id="12216-198">Moderní ale má jeden jeden datový model ve všech transakcích filtrovaných pomocí hodnoty "jednorázová".</span><span class="sxs-lookup"><span data-stu-id="12216-198">However, the modern has one single data model across all transactions filtered through the "OneTime" value.</span></span>            |
| <span data-ttu-id="12216-199">faktura-line-Item-Type</span><span class="sxs-lookup"><span data-stu-id="12216-199">invoice-line-item-type</span></span> | <span data-ttu-id="12216-200">řetězec</span><span class="sxs-lookup"><span data-stu-id="12216-200">string</span></span> | <span data-ttu-id="12216-201">Yes</span><span class="sxs-lookup"><span data-stu-id="12216-201">Yes</span></span>      | <span data-ttu-id="12216-202">Typ podrobností o faktuře: "BillingLineItems", "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="12216-202">The type of invoice detail: "BillingLineItems", "UsageLineItems".</span></span> |
| <span data-ttu-id="12216-203">size</span><span class="sxs-lookup"><span data-stu-id="12216-203">size</span></span>                   | <span data-ttu-id="12216-204">číslo</span><span class="sxs-lookup"><span data-stu-id="12216-204">number</span></span> | <span data-ttu-id="12216-205">No</span><span class="sxs-lookup"><span data-stu-id="12216-205">No</span></span>       | <span data-ttu-id="12216-206">Maximální počet položek, které se mají vrátit.</span><span class="sxs-lookup"><span data-stu-id="12216-206">The maximum number of items to return.</span></span> <span data-ttu-id="12216-207">Výchozí maximální velikost = 2000</span><span class="sxs-lookup"><span data-stu-id="12216-207">Default max size = 2000</span></span>    |
| <span data-ttu-id="12216-208">posun</span><span class="sxs-lookup"><span data-stu-id="12216-208">offset</span></span>                 | <span data-ttu-id="12216-209">číslo</span><span class="sxs-lookup"><span data-stu-id="12216-209">number</span></span> | <span data-ttu-id="12216-210">No</span><span class="sxs-lookup"><span data-stu-id="12216-210">No</span></span>       | <span data-ttu-id="12216-211">Index založený na nule první položky řádku, který se má vrátit.</span><span class="sxs-lookup"><span data-stu-id="12216-211">The zero-based index of the first line item to return.</span></span>            |
| <span data-ttu-id="12216-212">seekOperation</span><span class="sxs-lookup"><span data-stu-id="12216-212">seekOperation</span></span>          | <span data-ttu-id="12216-213">řetězec</span><span class="sxs-lookup"><span data-stu-id="12216-213">string</span></span> | <span data-ttu-id="12216-214">No</span><span class="sxs-lookup"><span data-stu-id="12216-214">No</span></span>       | <span data-ttu-id="12216-215">Pokud se pro **fakturaci** rovná **jednorázová**, nastavte **seekOperation** na hodnotu **Další** a získejte další stránku položek řádků faktury.</span><span class="sxs-lookup"><span data-stu-id="12216-215">If **billing-provider** equals **OneTime**, set **seekOperation** equal to **Next** to get the next page of invoice line items.</span></span> |
| <span data-ttu-id="12216-216">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="12216-216">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="12216-217">bool</span><span class="sxs-lookup"><span data-stu-id="12216-217">bool</span></span> | <span data-ttu-id="12216-218">No</span><span class="sxs-lookup"><span data-stu-id="12216-218">No</span></span> | <span data-ttu-id="12216-219">Hodnota, která označuje, zda se mají vracet položky řádku s použitím realizovaného kreditu.</span><span class="sxs-lookup"><span data-stu-id="12216-219">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="12216-220">Poznámka: Tento parametr bude použit, pouze pokud je typ poskytovatele fakturace jednorázová a InvoiceLineItemType je UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="12216-220">Note: this parameter will be only applied when billing provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="12216-221">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="12216-221">Request headers</span></span>

<span data-ttu-id="12216-222">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="12216-222">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="12216-223">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="12216-223">Request body</span></span>

<span data-ttu-id="12216-224">Žádné</span><span class="sxs-lookup"><span data-stu-id="12216-224">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="12216-225">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="12216-225">REST response</span></span>

<span data-ttu-id="12216-226">V případě úspěchu obsahuje odpověď kolekci podrobností položky řádku.</span><span class="sxs-lookup"><span data-stu-id="12216-226">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="12216-227">*Pro položku řádku **ChargeType** je hodnota **Nákup** namapována na **New (nový**). **Náhrada** hodnoty je namapována na **Zrušit**.*</span><span class="sxs-lookup"><span data-stu-id="12216-227">*For the line item **ChargeType**, the value **Purchase** is mapped to **New**. The value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="12216-228">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="12216-228">Response success and error codes</span></span>

<span data-ttu-id="12216-229">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="12216-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="12216-230">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="12216-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="12216-231">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="12216-231">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="rest-request-response-examples"></a><span data-ttu-id="12216-232">Příklady požadavků REST – odpověď</span><span class="sxs-lookup"><span data-stu-id="12216-232">REST request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="12216-233">Požadavek-odpověď – příklad 1</span><span class="sxs-lookup"><span data-stu-id="12216-233">Request-response example 1</span></span>

<span data-ttu-id="12216-234">V tomto příkladu jsou podrobnosti následující:</span><span class="sxs-lookup"><span data-stu-id="12216-234">In this example, the details are as follows:</span></span>

- <span data-ttu-id="12216-235">**BillingProvider**: **Office**</span><span class="sxs-lookup"><span data-stu-id="12216-235">**BillingProvider**: **Office**</span></span>
- <span data-ttu-id="12216-236">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="12216-236">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="12216-237">Příklad žádosti 1</span><span class="sxs-lookup"><span data-stu-id="12216-237">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="12216-238">Příklad odpovědi 1</span><span class="sxs-lookup"><span data-stu-id="12216-238">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045559164136",
            "subscriptionId": "4KIKawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "1F58ACD7-FE51-4705-9567-D009C9ADA150",
            "offerId": "AAA5B3F0-0EE2-431B-A42F-3F18F3C6D540",
            "durableOfferId": "2F707C7C-2433-49A5-A437-9CA7CF40D3EB",
            "offerName": "EXCHANGE ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionDescription": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-12T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-12T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 3,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045564795186",
            "subscriptionId": "Ik4YawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "D8A8F773-9D3E-4244-8797-3182075F09FA",
            "offerId": "618B53FE-9B99-428B-9745-F706AEAF3979",
            "durableOfferId": "69C67983-CF78-4102-83F6-3E5FD246864F",
            "offerName": "SHAREPOINT ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionDescription": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-13T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-13T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 1,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="12216-239">Požadavek-odpověď – příklad 2</span><span class="sxs-lookup"><span data-stu-id="12216-239">Request-response example 2</span></span>

<span data-ttu-id="12216-240">V následujícím příkladu jsou podrobnosti následující:</span><span class="sxs-lookup"><span data-stu-id="12216-240">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="12216-241">**BillingProvider**: **Azure**</span><span class="sxs-lookup"><span data-stu-id="12216-241">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="12216-242">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="12216-242">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="12216-243">Příklad žádosti 2</span><span class="sxs-lookup"><span data-stu-id="12216-243">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="12216-244">Příklad odpovědi 2</span><span class="sxs-lookup"><span data-stu-id="12216-244">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 745,
            "listPrice": 0.085,
            "currency": "USD",
            "pretaxCharges": 63.33,
            "taxAmount": 6.34,
            "postTaxTotal": 69.67,
            "pretaxEffectiveRate": 0.08500671,
            "postTaxEffectiveRate": 0.09351677,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac000000",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Azure App Service",
            "serviceType": "Standard Plan",
            "resourceGuid": "505db374-df8a-44df-9d8c-13c14b61dee1",
            "resourceName": "S1",
            "region": "",
            "consumedQuantity": 745,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 Hour",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        },
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 0.000882,
            "listPrice": 0.0383,
            "currency": "USD",
            "pretaxCharges": 0,
            "taxAmount": 0,
            "postTaxTotal": 0,
            "pretaxEffectiveRate": 0,
            "postTaxEffectiveRate": 0,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E87E26A",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac9cac68",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Storage",
            "serviceType": "Standard Page Blob",
            "resourceGuid": "d23a5753-ff85-4ddf-af28-8cc5cf2d3882",
            "resourceName": "LRS Data Stored",
            "region": "",
            "consumedQuantity": 0.000882,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 GB/Month",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-3"></a><span data-ttu-id="12216-245">Příklad odpovědi na požadavek 3</span><span class="sxs-lookup"><span data-stu-id="12216-245">Request-response example 3</span></span>

<span data-ttu-id="12216-246">V následujícím příkladu jsou podrobnosti následující:</span><span class="sxs-lookup"><span data-stu-id="12216-246">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="12216-247">**BillingProvider**: **Azure**</span><span class="sxs-lookup"><span data-stu-id="12216-247">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="12216-248">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="12216-248">**InvoiceLineItemType**: **UsageLineItems**</span></span>

#### <a name="request-example-3"></a><span data-ttu-id="12216-249">Příklad žádosti 3</span><span class="sxs-lookup"><span data-stu-id="12216-249">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="12216-250">Příklad odpovědi 3</span><span class="sxs-lookup"><span data-stu-id="12216-250">Response example 3</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "customerBillableAccount": "1439508127",
            "usageDate": "2019-08-05T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "9E9B71BA-3442-458B-B519-E1CCF72FBB54",
            "domainName": "test600.onmicrosoft.com",
            "customerCompanyName": "600 TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "F9BA6DA0-6DAC-4F88-B623-313C9B9C117A",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985577171353",
            "serviceName": "STORAGE",
            "serviceType": "STANDARD PAGE BLOB",
            "resourceGuid": "9CC63CF8-6593-410A-B0E7-26A4EF71E8B3",
            "resourceName": "DISK DELETE OPERATIONS",
            "region": "",
            "consumedQuantity": 2.9616,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "10K",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        },
        {
            "customerBillableAccount": "1307536861",
            "usageDate": "2019-08-10T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "EB53B7BD-267E-440E-B3C0-8F0B40000000",
            "domainName": "brandontest.onmicrosoft.com",
            "customerCompanyName": "BRANDON'S TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "62D22561-AB15-41E5-AD59-99025C000000",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985605838583",
            "serviceName": "VIRTUAL MACHINES",
            "serviceType": "D/DS SERIES WINDOWS",
            "resourceGuid": "62C64B6C-4033-4E20-AB33-9E81271AC12A",
            "resourceName": "D1/DS1",
            "region": "US WEST",
            "consumedQuantity": 24,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "1 HOUR",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-4"></a><span data-ttu-id="12216-251">Požadavek-odpověď – příklad 4</span><span class="sxs-lookup"><span data-stu-id="12216-251">Request-response example 4</span></span>

<span data-ttu-id="12216-252">V následujícím příkladu jsou podrobnosti následující:</span><span class="sxs-lookup"><span data-stu-id="12216-252">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="12216-253">**BillingProvider**: **jednorázová**</span><span class="sxs-lookup"><span data-stu-id="12216-253">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="12216-254">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="12216-254">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-4"></a><span data-ttu-id="12216-255">Příklad žádosti 4</span><span class="sxs-lookup"><span data-stu-id="12216-255">Request example 4</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-4"></a><span data-ttu-id="12216-256">Příklad odpovědi 4</span><span class="sxs-lookup"><span data-stu-id="12216-256">Response example 4</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

 {
    "continuationToken": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7",
    "totalCount": 2,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 431.8,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 431.8,
            "taxTotal": 38.87,
            "totalForCustomer": 470.67,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234278124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0159369774,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "billingFrequency": "Monthly",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f4badc2",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38cbb28e",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 26.35,
            "effectiveUnitPrice": 496.07,
            "unitType": "1 Hour",
            "quantity": 1,
            "subtotal": 26.35,
            "taxTotal": 2.37,
            "totalForCustomer": 28.72,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232ea904a",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234578124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2?seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7"
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-5"></a><span data-ttu-id="12216-257">Příklad odpovědi Request-response 5</span><span class="sxs-lookup"><span data-stu-id="12216-257">Request-response example 5</span></span>

<span data-ttu-id="12216-258">V následujícím příkladu je stránkování pomocí tokenu pro pokračování.</span><span class="sxs-lookup"><span data-stu-id="12216-258">In the following example, there is paging using a continuation token.</span></span> <span data-ttu-id="12216-259">Podrobnosti jsou následující:</span><span class="sxs-lookup"><span data-stu-id="12216-259">The details are as follows:</span></span>

- <span data-ttu-id="12216-260">**BillingProvider**: **jednorázová**</span><span class="sxs-lookup"><span data-stu-id="12216-260">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="12216-261">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="12216-261">**InvoiceLineItemType**: **BillingLineItems**</span></span>
- <span data-ttu-id="12216-262">**SeekOperation**: **Další**</span><span class="sxs-lookup"><span data-stu-id="12216-262">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-5"></a><span data-ttu-id="12216-263">Příklad žádosti 5</span><span class="sxs-lookup"><span data-stu-id="12216-263">Request example 5</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?seekOperation=Next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-5"></a><span data-ttu-id="12216-264">Příklad odpovědi 5</span><span class="sxs-lookup"><span data-stu-id="12216-264">Response example 5</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "NeqT31Kziwf8gkCXM9YQToWTqU-9Jbm81",
            "orderDate": "2018-02-08T22:31:47.1751688Z",
            "productId": "DZH318Z0BQ3P",
            "skuId": "001F",
            "availabilityId": "DZH318Z0DR0H",
            "productName": "Reserved VM Instance, Standard_D1, AP East, 3 years",
            "skuName": "D Series",
            "chargeType": "New",
            "unitPrice": 1447,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 1447,
            "taxTotal": 130.24,
            "totalForCustomer": 1577.24,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234568124b8",
            "priceAdjustmentDescription": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "billingFrequency": "Monthly",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
