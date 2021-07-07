---
title: Aktivace předplatného sandboxu pro produkty komerčního marketplace
description: Naučte se používat C/# a Partnerské centrum ROZHRANÍ REST API k aktivaci předplatného sandboxu pro produkty komerčního marketplace.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b32c3e87462f58218771fc5da7da56ed177489cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025696"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Aktivace předplatného sandboxu pro produkty SaaS komerčního marketplace a povolení fakturace

Postup aktivace předplatného pro produkty SaaS (Software jako služba) na komerčním marketplace z účtů sandboxu integrace a povolení fakturace

> [!NOTE]
> Předplatné pro produkty SaaS komerčního marketplace je možné aktivovat jenom z účtů sandboxu pro integraci. Pokud máte produkční předplatné, musíte navštívit web vydavatele a dokončit proces nastavení. Fakturace předplatného začne až po dokončení nastavení.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partnerské centrum ověřování.](partner-center-authentication.md) Tento scénář podporuje ověřování pomocí samostatných přihlašovacích údajů aplikace i aplikace a uživatele.

- Partnerský účet sandboxu pro integraci se zákazníkem, který má aktivní předplatné pro komerční marketplace produktů SaaS.

- Pro partnery, kteří Partnerské centrum .NET SDK, musíte pro přístup k této funkci použít sadu SDK verze 1.14.0 nebo vyšší.

## <a name="c"></a>C\#

K aktivaci předplatného pro produkty SaaS na komerčním marketplace použijte následující postup:

1. Zdělte rozhraní operací předplatného. Musíte identifikovat zákazníka a zadat identifikátor předplatného zkušebního předplatného.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktivujte předplatné pomocí **operace Aktivovat.**

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda     | Identifikátor URI žádosti                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Příspěvek** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ID_tenanta_zákazníka}/subscriptions/{ID_předplatného}/aktivace HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y | Hodnota je identifikátor tenanta zákazníka ve formátu GUID **(customer-tenant-id),** který umožňuje zadat zákazníka. |
| **id předplatného** | **guid** | Y | Hodnota je identifikátor předplatného ve formátu GUID **(id_předplatného),** který umožňuje zadat předplatné. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v Partnerské centrum [REST.](headers.md)

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>Odpověď REST

Tato metoda vrátí **vlastnosti subscription-id** **a status.**

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Partnerské centrum kódy chyb REST.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
