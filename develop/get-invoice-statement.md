---
title: Získání výkazů faktur
description: Načte výpis faktury pomocí ID faktury.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 97a0ee60b2cb57d3413d341ceea10e267fc1660c83fccbbc20353c3ad6bfc8c2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994485"
---
# <a name="get-invoice-statement"></a>Získání výkazů faktur

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- Platné ID faktury.

## <a name="c"></a>C\#

Pokud chcete získat výpis faktury podle ID, použijte kolekci **IPartner.Invoices,** zavolejte metodu **ById()** pomocí ID faktury a potom zavolejte metody **Documents()** a **Statement()** pro přístup k výpisu faktury. Nakonec zavolejte **metody Get()** nebo **GetAsync().**

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**Ukázka:** [Konzolová testovací aplikace](console-test-app.md). **Project:** PartnerSDK.FeatureSample **– třída:** GetInvoiceStatement.cs

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda  | Identifikátor URI žádosti                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **Dostat** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{ID_faktury}/documents/statement HTTP/1.1  |

### <a name="uri-parameter"></a>Parametr URI

K získání výpisu faktury použijte následující parametr dotazu.

| Název       | Typ       | Vyžadováno | Popis                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| id faktury | řetězec     | Yes      | Hodnota je ID faktury, které prodejci umožňuje filtrovat výsledky pro danou fakturu. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádná

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v textu odpovědi prostředek [InvoiceStatement.](invoice-resources.md#invoicestatement)

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
