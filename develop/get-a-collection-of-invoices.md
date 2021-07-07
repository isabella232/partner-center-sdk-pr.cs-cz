---
title: Získání kolekce faktur
description: Jak načíst kolekci faktur partnera
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 7698d85df3341ae4cbff0377bd0a1bb47cd36740
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906433"
---
# <a name="get-a-collection-of-invoices"></a><span data-ttu-id="f3db1-103">Získání kolekce faktur</span><span class="sxs-lookup"><span data-stu-id="f3db1-103">Get a collection of invoices</span></span>

<span data-ttu-id="f3db1-104">**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f3db1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f3db1-105">Jak načíst kolekci faktur partnera</span><span class="sxs-lookup"><span data-stu-id="f3db1-105">How to retrieve a collection of the partner's invoices.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3db1-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f3db1-106">Prerequisites</span></span>

- <span data-ttu-id="f3db1-107">Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f3db1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f3db1-108">Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="f3db1-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="f3db1-109">C\#</span><span class="sxs-lookup"><span data-stu-id="f3db1-109">C\#</span></span>

<span data-ttu-id="f3db1-110">Pokud chcete získat kolekci všech dostupných faktur, pomocí vlastnosti [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) získejte rozhraní pro operace s fakturami a potom zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) nebo [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) která kolekci načte.</span><span class="sxs-lookup"><span data-stu-id="f3db1-110">To get a collection of all available invoices, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.</span></span>

<span data-ttu-id="f3db1-111">Pokud chcete získat stránkované kolekce faktur, nejprve zavolejte metodu [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) a předejte jí velikost stránky pro vytvoření [**objektu IQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery)</span><span class="sxs-lookup"><span data-stu-id="f3db1-111">To get a paged collection of invoices, first call the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object.</span></span> <span data-ttu-id="f3db1-112">Dále pomocí vlastnosti [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) získejte rozhraní pro operace s fakturami a pak předejte objekt IQuery metodě [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) nebo [**QueryAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) která odešle požadavek a získá první stránku.</span><span class="sxs-lookup"><span data-stu-id="f3db1-112">Next, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.</span></span>

<span data-ttu-id="f3db1-113">Dále pomocí vlastnosti [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) získejte rozhraní pro kolekci podporovaných enumerátorů kolekce prostředků a potom zavolejte [**metodu Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) a vytvořte enumerátor pro procházení kolekce faktur.</span><span class="sxs-lookup"><span data-stu-id="f3db1-113">Next, use the [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices.</span></span> <span data-ttu-id="f3db1-114">Nakonec pomocí enumerátoru načtěte a pracujte s každou stránkou faktur, jak je znázorněno v následujícím příkladu kódu.</span><span class="sxs-lookup"><span data-stu-id="f3db1-114">Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example.</span></span> <span data-ttu-id="f3db1-115">Každé volání metody [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) odešle požadavek na další stránku faktur na základě velikosti stránky.</span><span class="sxs-lookup"><span data-stu-id="f3db1-115">Each call to the [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged)
                 ? partnerOperations.Invoices.Get()
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;

    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}",
            lineCounter++,
            i.Id,
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

<span data-ttu-id="f3db1-116">Trochu jiný příklad najdete v **tématu** Ukázka: [Konzolová testovací aplikace](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f3db1-116">For a slightly different example, see **Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f3db1-117">**Project:** SDK pro Partnerské centrum Samples **:** GetPagedInvoices.cs</span><span class="sxs-lookup"><span data-stu-id="f3db1-117">**Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs</span></span>

> [!NOTE] 
> <span data-ttu-id="f3db1-118">Stejné rozhraní API se používá pro všechny moderní komerční nákupy a také pro 145p a Office licence.</span><span class="sxs-lookup"><span data-stu-id="f3db1-118">The same API is used for all modern commercial purchases as well as 145p and Office licenses.</span></span> <span data-ttu-id="f3db1-119">Velikost a posun se zvažuje pouze u starších faktur.</span><span class="sxs-lookup"><span data-stu-id="f3db1-119">Size and offset are only considered for legacy invoices.</span></span> <span data-ttu-id="f3db1-120">U všech moderních komerčních nákupů se velikost & bude ignorovat.</span><span class="sxs-lookup"><span data-stu-id="f3db1-120">For all modern commercial purchases, pagesize & offset will be ignored.</span></span>

## <a name="rest-request"></a><span data-ttu-id="f3db1-121">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="f3db1-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f3db1-122">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="f3db1-122">Request syntax</span></span>

| <span data-ttu-id="f3db1-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="f3db1-123">Method</span></span>  | <span data-ttu-id="f3db1-124">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="f3db1-124">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f3db1-125">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="f3db1-125">**GET**</span></span> | <span data-ttu-id="f3db1-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f3db1-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span></span>  |

### <a name="uri-parameters"></a><span data-ttu-id="f3db1-127">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="f3db1-127">URI parameters</span></span>

<span data-ttu-id="f3db1-128">Při vytváření požadavku použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="f3db1-128">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="f3db1-129">Název</span><span class="sxs-lookup"><span data-stu-id="f3db1-129">Name</span></span>   | <span data-ttu-id="f3db1-130">Typ</span><span class="sxs-lookup"><span data-stu-id="f3db1-130">Type</span></span> | <span data-ttu-id="f3db1-131">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="f3db1-131">Required</span></span> | <span data-ttu-id="f3db1-132">Popis</span><span class="sxs-lookup"><span data-stu-id="f3db1-132">Description</span></span>                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="f3db1-133">size</span><span class="sxs-lookup"><span data-stu-id="f3db1-133">size</span></span>   | <span data-ttu-id="f3db1-134">int</span><span class="sxs-lookup"><span data-stu-id="f3db1-134">int</span></span>  | <span data-ttu-id="f3db1-135">No</span><span class="sxs-lookup"><span data-stu-id="f3db1-135">No</span></span>       | <span data-ttu-id="f3db1-136">Počet prostředků faktury, které se v odpovědi vrátí.</span><span class="sxs-lookup"><span data-stu-id="f3db1-136">The number of invoice resources to return in the response.</span></span> <span data-ttu-id="f3db1-137">Tento parametr je volitelný.</span><span class="sxs-lookup"><span data-stu-id="f3db1-137">This parameter is optional.</span></span> |
| <span data-ttu-id="f3db1-138">posun</span><span class="sxs-lookup"><span data-stu-id="f3db1-138">offset</span></span> | <span data-ttu-id="f3db1-139">int</span><span class="sxs-lookup"><span data-stu-id="f3db1-139">int</span></span>  | <span data-ttu-id="f3db1-140">No</span><span class="sxs-lookup"><span data-stu-id="f3db1-140">No</span></span>       | <span data-ttu-id="f3db1-141">Index první faktury, která se má vrátit, založený na nule.</span><span class="sxs-lookup"><span data-stu-id="f3db1-141">The zero-based index of the first invoice to return.</span></span>                                   |

### <a name="request-headers"></a><span data-ttu-id="f3db1-142">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="f3db1-142">Request headers</span></span>

<span data-ttu-id="f3db1-143">Další informace najdete v Partnerské centrum [REST.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f3db1-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f3db1-144">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="f3db1-144">Request body</span></span>

<span data-ttu-id="f3db1-145">Žádná</span><span class="sxs-lookup"><span data-stu-id="f3db1-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f3db1-146">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="f3db1-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f3db1-147">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="f3db1-147">REST response</span></span>

<span data-ttu-id="f3db1-148">V případě úspěchu bude text odpovědi obsahovat kolekci prostředků [faktury.](invoice-resources.md#invoice)</span><span class="sxs-lookup"><span data-stu-id="f3db1-148">If successful, the response body contains the collection of [Invoice](invoice-resources.md#invoice) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f3db1-149">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="f3db1-149">Response success and error codes</span></span>

<span data-ttu-id="f3db1-150">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="f3db1-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f3db1-151">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="f3db1-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f3db1-152">Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f3db1-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f3db1-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="f3db1-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "taxReceipts": [
                {
                    "id": "123456",
                    "taxReceiptPdfDownloadLink": "/invoices/D02005YFHI/receipts/123456/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "documentType": "invoice",
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "taxReceipts": [
                {
                    "id": "234567",
                    "taxReceiptPdfDownloadLink": "/invoices/G000024130/receipts/234567/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
