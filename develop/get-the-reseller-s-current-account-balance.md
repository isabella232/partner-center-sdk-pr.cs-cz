---
title: Získání aktuálního zůstatku na účtu partnera
description: Načte aktuální zůstatek účtu partnera. Souhrn zůstatku a celkové poplatky za fakturu pro periodické i jednorázové poplatky.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a04ab63482ec9d06e2fe47d2b6ce1bc6a5fd5f27
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548494"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="1cd9d-104">Získání aktuálního zůstatku na účtu partnera</span><span class="sxs-lookup"><span data-stu-id="1cd9d-104">Get the partner's current account balance</span></span>

<span data-ttu-id="1cd9d-105">**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1cd9d-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1cd9d-106">Načte aktuální zůstatek účtu partnera.</span><span class="sxs-lookup"><span data-stu-id="1cd9d-106">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="1cd9d-107">Souhrn zůstatku a celkové poplatky za fakturu pro periodické i jednorázové poplatky.</span><span class="sxs-lookup"><span data-stu-id="1cd9d-107">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1cd9d-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1cd9d-108">Prerequisites</span></span>

- <span data-ttu-id="1cd9d-109">Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1cd9d-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1cd9d-110">Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.</span><span class="sxs-lookup"><span data-stu-id="1cd9d-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="1cd9d-111">C\#</span><span class="sxs-lookup"><span data-stu-id="1cd9d-111">C\#</span></span>

<span data-ttu-id="1cd9d-112">Pokud chcete načíst zůstatek vašeho účtu, použijte svou kolekci **IAggregatePartner. faktur** a pak zavolejte vlastnost **summary** .</span><span class="sxs-lookup"><span data-stu-id="1cd9d-112">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="1cd9d-113">Pak zavolejte funkci **Get** a nakonec zavolejte vlastnost **BalanceAmount** .</span><span class="sxs-lookup"><span data-stu-id="1cd9d-113">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="1cd9d-114">**Ukázka**: [aplikace testů konzoly](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1cd9d-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1cd9d-115">**Project**: PartnerSDK. FeatureSample **třída**: GetInvoiceSummary. cs</span><span class="sxs-lookup"><span data-stu-id="1cd9d-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1cd9d-116">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="1cd9d-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1cd9d-117">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="1cd9d-117">Request syntax</span></span>

| <span data-ttu-id="1cd9d-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="1cd9d-118">Method</span></span>  | <span data-ttu-id="1cd9d-119">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="1cd9d-119">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="1cd9d-120">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="1cd9d-120">**GET**</span></span> | <span data-ttu-id="1cd9d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/Summary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1cd9d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="1cd9d-122">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="1cd9d-122">Request headers</span></span>

<span data-ttu-id="1cd9d-123">Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1cd9d-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1cd9d-124">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1cd9d-124">Request body</span></span>

<span data-ttu-id="1cd9d-125">Žádná</span><span class="sxs-lookup"><span data-stu-id="1cd9d-125">None</span></span>

### <a name="request-example"></a><span data-ttu-id="1cd9d-126">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="1cd9d-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="1cd9d-127">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="1cd9d-127">REST response</span></span>

<span data-ttu-id="1cd9d-128">V případě úspěchu tato metoda vrátí prostředek [InvoiceSummary](invoice-resources.md#invoicesummary) v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="1cd9d-128">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1cd9d-129">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="1cd9d-129">Response success and error codes</span></span>

<span data-ttu-id="1cd9d-130">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="1cd9d-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1cd9d-131">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="1cd9d-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1cd9d-132">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1cd9d-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1cd9d-133">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="1cd9d-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "balanceAmount": 751094.39,
    "currencyCode": "USD",
    "currencySymbol": "$",
    "accountingDate": "2018-03-16T00:00:00",
    "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
    "lastPaymentDate": "2017-01-01T12:00:00Z",
    "lastPaymentAmount": 1000,
    "latestInvoiceDate": "2018-03-16T00:00:00",
    "details": [
        {
            "invoiceType": "Recurring",
            "summary": {
                "balanceAmount": 202955.87,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "accountingDate": "2017-02-27T00:00:00Z",
                "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
                "lastPaymentDate": "2017-01-01T12:00:00Z",
                "lastPaymentAmount": 1000,
                "latestInvoiceDate": "0001-01-01T00:00:00",
                "attributes": {
                    "objectType": "InvoiceSummary"
                }
            }
        },
        {
            "invoiceType": "OneTime",
            "summary": {
                "balanceAmount": 548138.52,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "accountingDate": "2018-03-16T00:00:00",
                "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                "lastPaymentDate": "0001-01-01T00:00:00",
                "lastPaymentAmount": 0,
                "latestInvoiceDate": "2018-03-16T00:00:00",
                "attributes": {
                    "objectType": "InvoiceSummary"
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/summary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "InvoiceSummary"
    }
}
```
