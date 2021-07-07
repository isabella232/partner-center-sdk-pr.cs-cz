---
title: Partnerské centrum události webhooku
description: Naučte se testovat a používat události webhooku k poznámce, kdy se odběry a další události v Partnerské centrum.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: e5e363a2f928dd38304887547bdc0e5d652728d6
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547736"
---
# <a name="partner-center-webhook-events"></a>Partnerské centrum události webhooku

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Partnerské centrum webhooku jsou události změny prostředků doručené ve formě HTTP POST na zaregistrovanou adresu URL. Pokud chcete přijímat události z Partnerské centrum, hostíte zpětné volání, Partnerské centrum může událost POST. Událost je digitálně podepsaná, abyste mohli ověřit, že se odeslala z Partnerské centrum.

Informace o tom, jak přijímat události, ověřovat zpětné volání a používat rozhraní API webhooku Partnerské centrum k vytvoření, zobrazení a aktualizaci registrace události, najdete v [tématu Partnerské centrum Webhooky.](partner-center-webhooks.md)

## <a name="supported-events"></a>Podporované události

Následující události webhooku jsou podporovány Partnerské centrum.

### <a name="test-event"></a>Testovací událost

Tato událost vám umožní registraci sama onboardovat a otestovat tak, že si vyžádáte testovací událost a pak budete sledovat její průběh. Uvidíte zprávy o selhání, které microsoft přijímá při pokusu o doručení události. To platí jenom pro události vytvořené testem a data starší než sedm dnů se vyprázdní.

>[!NOTE]
>Při odesílání události vytvořené testem platí limit 2 požadavků za minutu.

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve tvaru {resource}-{action}. Pro tuto událost je hodnota "test-created".                                          |
| Identifikátor URI prostředku               | Identifikátor URI                                | Identifikátor URI pro získání prostředku. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | řetězec                             | Název prostředku, který aktivuje událost. Pro tuto událost je hodnota "test".                                  |
| AuditUri                  | Identifikátor URI                                | (Volitelné) Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | řetězec ve formátu data a času UTC | Datum a čas, kdy došlo ke změně prostředku                                                         |

#### <a name="example"></a>Příklad

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="subscription-updated-event"></a>Událost aktualizace předplatného

Tato událost se vyvolala při změně zadaného předplatného. Událost Aktualizace předplatného se vygeneruje v případě, že dojde k interní změně kromě toho, kdy se změny provádí prostřednictvím Partnerské centrum API.  Tato událost se vygeneruje jenom v případě, že dojde ke změnám na úrovni obchodu, například když se změní počet licencí a stav předplatného. Při vytváření prostředků v rámci předplatného se nevygeneruje.

>[!NOTE]
>Mezi změnou předplatného a aktivací události Aktualizace předplatného je zpoždění až 48 hodin.

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve tvaru {resource}-{action}. Pro tuto událost je hodnota subscription-updated.                                  |
| Identifikátor URI prostředku               | Identifikátor URI                                | Identifikátor URI pro získání prostředku. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | řetězec                             | Název prostředku, který aktivuje událost. Pro tuto událost je hodnota "subscription".                          |
| AuditUri                  | Identifikátor URI                                | (Volitelné) Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | řetězec ve formátu data a času UTC | Datum a čas, kdy došlo ke změně prostředku                                                         |

#### <a name="example"></a>Příklad

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="threshold-exceeded-event"></a>Prahová hodnota překročena – událost

Tato událost se nastane, když výše Microsoft Azure využití u všech zákazníků překročí rozpočet útraty za využití (jejich prahovou hodnotu). Další informace najdete v tématu [Nastavení rozpočtu útraty Azure pro zákazníky/partnerské centrum/set-an-azure-spending-budget-for-your-customers).

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve tvaru {resource}-{action}. Pro tuto událost je hodnota usagerecords-thresholdExceeded.                                  |
| Identifikátor URI prostředku               | Identifikátor URI                                | Identifikátor URI pro získání prostředku. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords |
| ResourceName              | řetězec                             | Název prostředku, který aktivuje událost. Pro tuto událost je hodnota "usagerecords".                          |
| AuditUri                  | Identifikátor URI                                | (Volitelné) Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | řetězec ve formátu data a času UTC | Datum a čas, kdy došlo ke změně prostředku                                                         |

#### <a name="example"></a>Příklad

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>Událost vytvoření referenčního odkazu

Tato událost se vyvolala při vytvoření referenčního odkazu.

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve tvaru {resource}-{action}. Pro tuto událost je hodnota "referral-created" (vytvoření referenčního seznamu).                                  |
| Identifikátor URI prostředku               | Identifikátor URI                                | Identifikátor URI pro získání prostředku. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | řetězec                             | Název prostředku, který aktivuje událost. Pro tuto událost je hodnota referenčního seznamu.                          |
| AuditUri                  | Identifikátor URI                                | (Volitelné) Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | řetězec ve formátu data a času UTC | Datum a čas, kdy došlo ke změně prostředku                                                         |

#### <a name="example"></a>Příklad

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>Aktualizovaná událost referenčního odkazu

Tato událost se vyvolala při aktualizaci referenčního odkazu.

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve tvaru {resource}-{action}. Pro tuto událost je hodnota "referenční seznam aktualizován".                                  |
| Identifikátor URI prostředku               | Identifikátor URI                                | Identifikátor URI pro získání prostředku. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | řetězec                             | Název prostředku, který aktivuje událost. Pro tuto událost je hodnota referenčního seznamu.                          |
| AuditUri                  | Identifikátor URI                                | (Volitelné) Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | řetězec ve formátu data a času UTC | Datum a čas, kdy došlo ke změně prostředku                                                         |

#### <a name="example"></a>Příklad

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>Událost připravenou na fakturu

Tato událost se vyvolala, když je nová faktura připravená.

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | řetězec | Název události. Ve tvaru {resource}-{action}. Pro tuto událost je hodnota "invoice-ready" (připraveno na fakturu). |
| Identifikátor URI prostředku | Identifikátor URI | Identifikátor URI pro získání prostředku. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" |
| ResourceName | řetězec | Název prostředku, který aktivuje událost. Pro tuto událost je hodnotou "invoice". |
| AuditUri |  Identifikátor URI | (Volitelné) Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}") |
| ResourceChangeUtcDate | řetězec ve formátu data a času UTC | Datum a čas, kdy došlo ke změně prostředku |

#### <a name="example"></a>Příklad

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```
