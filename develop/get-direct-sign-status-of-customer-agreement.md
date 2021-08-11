---
title: Získejte stav přímého podepsání zákazníka pro Smlouva se zákazníkem Microsoftu.
description: Pomocí prostředku DirectSignedCustomerAgreementStatus můžete získat stav přímého podepisování zákazníka (přímé přijetí) Smlouva se zákazníkem Microsoftu.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 544965ab05e3956aa5b7b6fa2ef9656ff33990ef9c8d91422797132a814b85f1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993345"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Získání stavu přímého podepsání zákazníka (přímé přijetí) Smlouva se zákazníkem Microsoftu

**Platí pro:** Partnerské centrum

**Nevztahuje se na**: Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Prostředek **DirectSignedCustomerAgreementStatus** je aktuálně podporován Partnerské centrum ve veřejném cloudu Microsoftu.

Tento článek vysvětluje, jak můžete načíst stav přímého přijetí služby zákazníkem Smlouva se zákazníkem Microsoftu.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pouze pomocí přihlašovacích údajů aplikace a uživatele.

- ID zákazníka ( `customer-tenant-id` ). Pokud ID zákazníka neznáme, můžete ho na řídicím panelu [Partnerské centrum.](https://partner.microsoft.com/dashboard) V nabídce Partnerské centrum vyberte **CSP** a pak **Zákazníci.** V seznamu zákazníků vyberte zákazníka a pak vyberte **Účet.** Na stránce Účtu zákazníka vyhledejte **ID Microsoftu** v části **Informace o účtu** zákazníka. Id Microsoftu je stejné jako ID zákazníka ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Pokud chcete načíst stav přímého přijetí požadavku zákazníkem, Smlouva se zákazníkem Microsoftu [**metodu IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) s identifikátorem zákazníka. Potom pomocí [**vlastnosti Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) načtěte rozhraní [**ICustomerAgreementCollection.**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) Nakonec zavolejte `GetDirectSignedCustomerAgreementStatus()` nebo `GetDirectSignedCustomerAgreementStatusAsync()` a načtěte stav.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Ukázka:** [Konzolová ukázková aplikace](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples **– třída:** GetDirectSignedCustomerAgreementStatus.cs

## <a name="rest-request"></a>Požadavek REST

Pokud chcete načíst stav přímého přijetí žádosti zákazníka Smlouva se zákazníkem Microsoftu, vytvořte požadavek REST pro načtení [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) pro zákazníka.

### <a name="request-syntax"></a>Syntaxe požadavku

Použijte následující syntaxi požadavku:

| Metoda | Identifikátor URI žádosti                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{id_tenanta_zákazníka}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1 |

### <a name="uri-parameters"></a>Parametry identifikátoru URI

S požadavkem můžete použít následující parametry identifikátoru URI:

| Název             | Typ | Vyžadováno | Popis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | Identifikátor GUID | Yes | Hodnota je **CustomerTenantId** ve formátu GUID, která umožňuje zadat ID tenanta zákazníka. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v textu odpovědi prostředek [ **DirectSignedCustomerAgreementStatus.**](./customer-agreement-direct-sign-status-resource.md)

Prostředek má vlastnost **isSigned,** která označuje stav přímého podepsání (přímého přijetí) zákazníka.

- Hodnota true **znamená,** že zákazník smlouvu podepsal (přijal) přímo.

- Hodnota false **znamená,** že  zákazník smlouvu přímo nepodepsal (nepřijal).

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.

K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
