---
title: Aktivace předplatného izolovaného prostoru pro produkty z komerčního tržiště
description: Naučte se používat rozhraní REST API pro C/# a partnerská centra k aktivaci předplatného pro komerční produkty z webu Marketplace.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/11/2020
ms.locfileid: "97767068"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Aktivace předplatného izolovaného prostoru (sandbox) pro SaaS produkty z webu Marketplace pro povolení fakturace

**Platí pro:**

- Partnerské centrum

Jak aktivovat předplatné pro produkty komerčního SaaS (software jako služba) z účtů izolovaného prostoru (sandbox) integrací pro povolení fakturace

> [!NOTE]
> Předplatné pro produkty SaaS na komerčním webu Marketplace je možné aktivovat z účtů karantény integrace. Pokud máte produkční předplatné, musíte navštívit web vydavatele, aby se dokončil proces instalace. Fakturace předplatného se zahájí až po dokončení instalace.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v [partnerském centru ověřování](partner-center-authentication.md). Tento scénář podporuje ověřování pomocí samostatné aplikace a přihlašovacích údajů uživatele a aplikace.

- Partnerský účet integrace izolovaného prostoru (sandbox) se zákazníkem s aktivním předplatným pro komerční SaaS produkty z webu Marketplace.

- Pro partnery, kteří používají Partnerská rozhraní .NET SDK, musíte pro přístup k této funkci použít sadu SDK verze 1.14.0 nebo vyšší.

## <a name="c"></a>C\#

K aktivaci předplatného pro komerční produkty SaaS na webu Marketplace použijte následující postup:

1. Zpřístupněte rozhraní k dostupným operacím předplatného. Musíte identifikovat zákazníka a zadat identifikátor předplatného zkušebního předplatného.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktivujte předplatné pomocí operace **aktivovat** .

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda     | Identifikátor URI žádosti                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **SPUŠTĚNÍ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Subscriptions/{Subscription-ID}/Activate HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

| Název                   | Typ     | Vyžadováno | Popis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer-tenant-ID** | **guid** | Y | Hodnota je identifikátor zákazníka ve formátu GUID (**Customer-tenant-ID**), který umožňuje zadat zákazníka. |
| **ID předplatného** | **guid** | Y | Hodnota je identifikátor předplatného ve formátu GUID (**ID předplatného**), který umožňuje zadat předplatné. |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v tématu [záhlaví REST partnerského centra](headers.md).

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

Tato metoda vrátí vlastnost **ID předplatného** a **stavu** .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb REST partnerského centra](error-codes.md).

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
