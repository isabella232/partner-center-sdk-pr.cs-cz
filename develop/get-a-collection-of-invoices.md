---
title: Získání kolekce faktur
description: Jak načíst kolekci faktur partnera.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: f56c3de8dd227f573921e5b969c2217c2f743a21
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "97766847"
---
# <a name="get-a-collection-of-invoices"></a><span data-ttu-id="86a69-103">Získání kolekce faktur</span><span class="sxs-lookup"><span data-stu-id="86a69-103">Get a collection of invoices</span></span>

<span data-ttu-id="86a69-104">**Platí pro**</span><span class="sxs-lookup"><span data-stu-id="86a69-104">**Applies To**</span></span>

- <span data-ttu-id="86a69-105">Partnerské centrum</span><span class="sxs-lookup"><span data-stu-id="86a69-105">Partner Center</span></span>
- <span data-ttu-id="86a69-106">Partnerské centrum provozovaný společností 21Vianet</span><span class="sxs-lookup"><span data-stu-id="86a69-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="86a69-107">Partnerské centrum pro Microsoft Cloud pro Německo</span><span class="sxs-lookup"><span data-stu-id="86a69-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="86a69-108">Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="86a69-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="86a69-109">Jak načíst kolekci faktur partnera.</span><span class="sxs-lookup"><span data-stu-id="86a69-109">How to retrieve a collection of the partner's invoices.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86a69-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="86a69-110">Prerequisites</span></span>

- <span data-ttu-id="86a69-111">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="86a69-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="86a69-112">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="86a69-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="86a69-113">C\#</span><span class="sxs-lookup"><span data-stu-id="86a69-113">C\#</span></span>

<span data-ttu-id="86a69-114">Chcete-li získat kolekci všech dostupných faktur, použijte vlastnost [**faktur**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) k získání rozhraní k fakturaci operace a poté zavolejte metodu [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) nebo [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) pro načtení kolekce.</span><span class="sxs-lookup"><span data-stu-id="86a69-114">To get a collection of all available invoices, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.</span></span>

<span data-ttu-id="86a69-115">Chcete-li získat stránkované kolekce faktur, nejprve zavolejte metodu [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) a předejte jí velikost stránky pro vytvoření objektu [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) .</span><span class="sxs-lookup"><span data-stu-id="86a69-115">To get a paged collection of invoices, first call the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object.</span></span> <span data-ttu-id="86a69-116">Dále pomocí vlastnosti [**faktury**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) Získejte rozhraní k fakturaci operací a pak předejte objekt IQuery do [**dotazu**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) nebo metody [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) k odeslání požadavku a získání první stránky.</span><span class="sxs-lookup"><span data-stu-id="86a69-116">Next, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.</span></span>

<span data-ttu-id="86a69-117">Dále pomocí vlastnosti [**enumerátory**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) Získejte rozhraní pro kolekci podporovaných enumerátorů kolekcí prostředků a potom zavolejte [**faktury. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) k vytvoření enumerátoru pro procházení kolekce faktur.</span><span class="sxs-lookup"><span data-stu-id="86a69-117">Next, use the [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices.</span></span> <span data-ttu-id="86a69-118">Nakonec použijte enumerátor pro načtení a práci s každou stránkou faktury, jak je znázorněno v následujícím příkladu kódu.</span><span class="sxs-lookup"><span data-stu-id="86a69-118">Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example.</span></span> <span data-ttu-id="86a69-119">Každé volání metody [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) pošle požadavek na další stránku faktury na základě velikosti stránky.</span><span class="sxs-lookup"><span data-stu-id="86a69-119">Each call to the [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.</span></span>

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

<span data-ttu-id="86a69-120">Trochu odlišný příklad naleznete v tématu **Ukázka**: [aplikace test Console](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="86a69-120">For a slightly different example, see **Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="86a69-121">**Projekt**: ukázkové **třídy** SDK pro partnerských Center: GetPagedInvoices.cs</span><span class="sxs-lookup"><span data-stu-id="86a69-121">**Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs</span></span>

> [!NOTE] 
> <span data-ttu-id="86a69-122">Stejné rozhraní API se používá pro všechny moderní komerční nákupy i pro licence na 145p a Office.</span><span class="sxs-lookup"><span data-stu-id="86a69-122">The same API is used for all modern commercial purchases as well as 145p and Office licenses.</span></span> <span data-ttu-id="86a69-123">Velikost a posun se považují jenom za starší faktury.</span><span class="sxs-lookup"><span data-stu-id="86a69-123">Size and offset are only considered for legacy invoices.</span></span> <span data-ttu-id="86a69-124">U všech moderních komerčních nákupů se hodnota PageSize & posunu bude ignorovat.</span><span class="sxs-lookup"><span data-stu-id="86a69-124">For all modern commercial purchases, pagesize & offset will be ignored.</span></span>

## <a name="rest-request"></a><span data-ttu-id="86a69-125">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="86a69-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="86a69-126">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="86a69-126">Request syntax</span></span>

| <span data-ttu-id="86a69-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="86a69-127">Method</span></span>  | <span data-ttu-id="86a69-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="86a69-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="86a69-129">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="86a69-129">**GET**</span></span> | <span data-ttu-id="86a69-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices? size = {size} &posun = {offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="86a69-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span></span>  |

### <a name="uri-parameters"></a><span data-ttu-id="86a69-131">Parametry identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="86a69-131">URI parameters</span></span>

<span data-ttu-id="86a69-132">Při vytváření žádosti použijte následující parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="86a69-132">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="86a69-133">Název</span><span class="sxs-lookup"><span data-stu-id="86a69-133">Name</span></span>   | <span data-ttu-id="86a69-134">Typ</span><span class="sxs-lookup"><span data-stu-id="86a69-134">Type</span></span> | <span data-ttu-id="86a69-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="86a69-135">Required</span></span> | <span data-ttu-id="86a69-136">Popis</span><span class="sxs-lookup"><span data-stu-id="86a69-136">Description</span></span>                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="86a69-137">size</span><span class="sxs-lookup"><span data-stu-id="86a69-137">size</span></span>   | <span data-ttu-id="86a69-138">int</span><span class="sxs-lookup"><span data-stu-id="86a69-138">int</span></span>  | <span data-ttu-id="86a69-139">No</span><span class="sxs-lookup"><span data-stu-id="86a69-139">No</span></span>       | <span data-ttu-id="86a69-140">Počet fakturovaných prostředků, které se mají vrátit v odpovědi</span><span class="sxs-lookup"><span data-stu-id="86a69-140">The number of invoice resources to return in the response.</span></span> <span data-ttu-id="86a69-141">Tento parametr je volitelný.</span><span class="sxs-lookup"><span data-stu-id="86a69-141">This parameter is optional.</span></span> |
| <span data-ttu-id="86a69-142">posun</span><span class="sxs-lookup"><span data-stu-id="86a69-142">offset</span></span> | <span data-ttu-id="86a69-143">int</span><span class="sxs-lookup"><span data-stu-id="86a69-143">int</span></span>  | <span data-ttu-id="86a69-144">No</span><span class="sxs-lookup"><span data-stu-id="86a69-144">No</span></span>       | <span data-ttu-id="86a69-145">Index založený na nule první faktury, která se má vrátit</span><span class="sxs-lookup"><span data-stu-id="86a69-145">The zero-based index of the first invoice to return.</span></span>                                   |

### <a name="request-headers"></a><span data-ttu-id="86a69-146">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="86a69-146">Request headers</span></span>

<span data-ttu-id="86a69-147">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="86a69-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="86a69-148">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="86a69-148">Request body</span></span>

<span data-ttu-id="86a69-149">Žádné</span><span class="sxs-lookup"><span data-stu-id="86a69-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="86a69-150">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="86a69-150">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="86a69-151">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="86a69-151">REST response</span></span>

<span data-ttu-id="86a69-152">V případě úspěchu obsahuje tělo odpovědi kolekci zdrojů [faktury](invoice-resources.md#invoice) .</span><span class="sxs-lookup"><span data-stu-id="86a69-152">If successful, the response body contains the collection of [Invoice](invoice-resources.md#invoice) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="86a69-153">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="86a69-153">Response success and error codes</span></span>

<span data-ttu-id="86a69-154">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="86a69-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="86a69-155">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="86a69-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="86a69-156">Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="86a69-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="86a69-157">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="86a69-157">Response example</span></span>

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
