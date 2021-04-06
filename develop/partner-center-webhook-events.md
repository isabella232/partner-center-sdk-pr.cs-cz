---
title: Události Webhooku partnerského centra
description: Naučte se testovat a používat události Webhooku, abyste poznamenali, kdy se předplatné a další události mění v partnerském centru.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 03ee1d4e74408b8cf69e2971054bf9060650cb77
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500035"
---
# <a name="partner-center-webhook-events"></a>Události Webhooku partnerského centra

**Platí pro**

- Partnerské centrum
- Partnerské centrum provozované společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Události Webhooku partnerského centra jsou události změny prostředků doručené ve formě příspěvků HTTP na registrovanou adresu URL. Pokud chcete získat událost z partnerského centra, můžete hostovat zpětné volání, které může partnerské Centrum publikovat událost. Událost je digitálně podepsaná, abyste mohli ověřit, že byla odeslána z partnerského centra.

Informace o tom, jak přijímat události, ověřovat zpětné volání a používat rozhraní API Webhooku partnerského centra k vytvoření, zobrazení a aktualizaci registrace události, najdete v tématu [Webhooky partnerského centra](partner-center-webhooks.md).

## <a name="supported-events"></a>Podporované události

Partnerské centrum podporuje následující události Webhooku.

### <a name="test-event"></a>Testovací událost

Tato událost umožňuje samoobslužné zprovoznění a testování registrace tím, že požaduje testovací událost a pak sleduje jeho průběh. Při pokusu o doručení události budete moci zobrazit zprávy o chybách, které jsou přijímány od společnosti Microsoft. Tato možnost bude platit jenom pro události "vytvořené testem" a data starší než 7 dní se vyprázdní.

>[!NOTE]
>Při odesílání události vytvořené testem je omezení dvou požadavků za minutu.

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve formátu {Resource} – {Action}. Pro tuto událost je hodnota "test-Created".                                          |
| ResourceUri               | Identifikátor URI                                | Identifikátor URI pro získání prostředku Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Registration/validationEvents/{{CorrelationId}}. |
| ResourceName              | řetězec                             | Název prostředku, který spustí událost. Pro tuto událost je hodnota "test".                                  |
| AuditUri                  | Identifikátor URI                                | Volitelné Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}}. |
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

Tato událost se vyvolá, když se změní zadané předplatné. Událost aktualizace předplatného se vygeneruje, když se kromě změn provedených prostřednictvím rozhraní API partnerského centra provede nějaká interní změna.  Tato událost bude vygenerována pouze v případě, že dojde ke změně úrovně Commerce, například při změně počtu licencí a změně stavu předplatného. Při vytváření prostředků v rámci předplatného nebude vygenerována.

>[!NOTE]
>Mezi časem změny předplatného a aktivací události aktualizace předplatného dojde k prodlevě až 48 hodin.

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve formátu {Resource} – {Action}. Pro tuto událost je hodnota "předplatné-aktualizováno".                                  |
| ResourceUri               | Identifikátor URI                                | Identifikátor URI pro získání prostředku Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Customers/{{CustomerID}}/Subscriptions/{{SubscriptionId}}. |
| ResourceName              | řetězec                             | Název prostředku, který spustí událost. Pro tuto událost je hodnota "předplatné".                          |
| AuditUri                  | Identifikátor URI                                | Volitelné Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}}. |
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

### <a name="threshold-exceeded-event"></a>Událost překročení prahové hodnoty

Tato událost se vyvolá v případě, že množství využití Microsoft Azure pro každého zákazníka přesáhne rozpočet výdajů na využití (jejich prahovou hodnotu). Další informace najdete v tématu [nastavení rozpočtu útraty Azure pro vaše zákazníky/partnery – Center/set-a-Azure-útraty-rozpočet-pro zákazníky).

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve formátu {Resource} – {Action}. Pro tuto událost je hodnota "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | Identifikátor URI                                | Identifikátor URI pro získání prostředku Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Customers/usagerecords. |
| ResourceName              | řetězec                             | Název prostředku, který spustí událost. Pro tuto událost je hodnota "usagerecords".                          |
| AuditUri                  | Identifikátor URI                                | Volitelné Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}}. |
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

### <a name="referral-created-event"></a>Událost vytvořená odkazem

Tato událost je aktivována při vytvoření odkazu.

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve formátu {Resource} – {Action}. Pro tuto událost je hodnota "odkaz-vytvořeno".                                  |
| ResourceUri               | Identifikátor URI                                | Identifikátor URI pro získání prostředku Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/Engagements/v1/Referrals/{{ReferralID}}. |
| ResourceName              | řetězec                             | Název prostředku, který spustí událost. Pro tuto událost je tato hodnota "Reference".                          |
| AuditUri                  | Identifikátor URI                                | Volitelné Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}}. |
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

### <a name="referral-updated-event"></a>Událost aktualizovaného odkazu

Tato událost je aktivována při aktualizaci odkazu.

#### <a name="properties"></a>Vlastnosti

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | řetězec                             | Název události. Ve formátu {Resource} – {Action}. Pro tuto událost je hodnota "odkaz-aktualizováno".                                  |
| ResourceUri               | Identifikátor URI                                | Identifikátor URI pro získání prostředku Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/Engagements/v1/Referrals/{{ReferralID}}. |
| ResourceName              | řetězec                             | Název prostředku, který spustí událost. Pro tuto událost je tato hodnota "Reference".                          |
| AuditUri                  | Identifikátor URI                                | Volitelné Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}}. |
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

### <a name="invoice-ready-event"></a>Událost připravena k faktuře

Tato událost se vyvolá, když je nová faktura připravena.

| Vlastnost                  | Typ                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | řetězec | Název události. Ve formátu {Resource} – {Action}. Pro tuto událost je hodnota "faktura-připravena". |
| ResourceUri | Identifikátor URI | Identifikátor URI pro získání prostředku Používá syntaxi [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{{InvoiceId}}. |
| ResourceName | řetězec | Název prostředku, který spustí událost. Pro tuto událost je hodnota "Invoice". |
| AuditUri |  Identifikátor URI | Volitelné Identifikátor URI pro získání záznamu auditu, pokud existuje. Používá syntaxi:[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} ") |
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
