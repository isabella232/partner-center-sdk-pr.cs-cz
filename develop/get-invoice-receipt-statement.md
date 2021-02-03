---
title: Získání příjmových výkazů faktur
description: Načte výpis účtenky faktury pomocí ID faktury a ID účtenky.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766655"
---
# <a name="get-invoice-receipt-statement"></a>Získání příjmových výkazů faktur

**Platí pro**

- Partnerské centrum

Načte výpis účtenky faktury pomocí ID faktury a ID účtenky.

> [!IMPORTANT]
> Tato funkce se vztahuje pouze na příjem daně z Tchaj-wanu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování jenom pomocí přihlašovacích údajů pro aplikace a uživatele.

- Platné ID faktury a odpovídající ID účtenky.

## <a name="c"></a>C\#

Chcete-li získat příkaz pro příjem faktury podle ID počínaje partnerským centrem SDK v 1.12.0, použijte svou kolekci **IPartner.** Invoices a zavolejte metodu **ById ()** s použitím ID faktury, potom zavolejte shromažďování **příjemek** a zavolejte **ById ()** a zavolejte metody **Documents ()** a **Statement ()** pro přístup k příkazu pro příjem faktury. Nakonec zavolejte metody **Get ()** nebo **GetAsync ()** .

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Ukázka**: [aplikace testů konzoly](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample **Třída**: GetInvoiceReceiptStatement.cs

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Čtěte** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Receipts/{Receipt-ID}/Documents/Statement HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

K získání příkazu pro příjem faktury použijte následující parametr dotazu.

| Název       | Typ   | Vyžadováno | Popis                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| ID faktury | řetězec | Yes      | Hodnota je ID faktury, které prodejci umožňuje filtrovat výsledky dané faktury. |
| ID účtenky | řetězec | Yes      | Hodnota je ID příjemky, které umožňuje prodejci filtrovat účtenky pro danou fakturu. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí datový proud PDF v těle odpovědi.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
