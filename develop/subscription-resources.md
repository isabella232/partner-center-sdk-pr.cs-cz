---
title: Prostředky předplatného
description: Prostředky předplatného můžou poskytovat další informace o předplatných v průběhu životního cyklu, jako je podpora, refundace, nároky na Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd835e46e99b1fcb1e0b0e694ad73b1dca1240c9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/08/2020
ms.locfileid: "97766739"
---
# <a name="subscription-resources"></a>Prostředky předplatného

**Platí pro:**

- Partnerské centrum
- Partnerské centrum provozovaný společností 21Vianet
- Partnerské centrum pro Microsoft Cloud pro Německo
- Partnerské centrum pro Microsoft Cloud for US Government

Předplatné umožní zákazníkovi používat službu po určitou dobu. Ne všechna pole budou použita pro všechna předplatná. Mnoho polí se vztahuje pouze na určité body životního cyklu, jako je například pozastavení nebo zrušení odběru.

## <a name="subscription"></a>Předplatné

>[!NOTE]
>Prostředek **odběru** má omezení frekvence 500 požadavků za minutu na identifikátor tenanta.

Prostředek **předplatného** představuje životní cyklus předplatného a obsahuje vlastnosti definující stavy v rámci životního cyklu předplatného.

| Vlastnost             | Typ                                                          | Description                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | řetězec                                                        | Identifikátor předplatného.                                                                                                                                                  |
| Hodnotami OfferId              | řetězec                                                        | Identifikátor nabídky                                                                                                                                                         |
| entitlementId        | řetězec                                                        | Identifikátor nároku (ID předplatného Azure)                                                                                                                        |
| offerName            | řetězec                                                        | Název nabídky                                                                                                                                                               |
| friendlyName         | řetězec                                                        | Popisný název předplatného definovaného partnerem, který vám umožní určit nejednoznačnost.                                                                                           |
| quantity             | číslo                                                        | Množství. Například v případě fakturace na základě licence je tato vlastnost nastavena na počet licencí.                                                            |
| Jednotkách UnitType             | řetězec                                                        | Jednotky definující množství pro předplatné.                                                                                                                             |
| parentSubscriptionId | řetězec                                                        | Získá nebo nastaví nadřazený identifikátor předplatného.                                                                                                                              |
| creationDate         | řetězec                                                        | Získá nebo nastaví datum vytvoření ve formátu data a času.                                                                                                                          |
| effectiveStartDate   | řetězec ve formátu data a času UTC                                | Získá nebo nastaví platné počáteční datum pro toto předplatné ve formátu data a času. Používá se k datu zálohování migrovaného předplatného nebo k jeho zarovnávání jiným.                |
| commitmentEndDate    | řetězec ve formátu data a času UTC                                | Koncové datum závazku pro toto předplatné ve formátu data a času. U předplatných, která nejsou automaticky obnovitelné, představuje datum v budoucnosti.       |
| status               | řetězec                                                        | Stav předplatného: "none", "Active", "pending", "Suspended" nebo "Deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Načte hodnotu, která označuje, jestli se předplatné obnovuje automaticky.                                                                                                    |
| billingType          | řetězec                                                        | Určuje, jak se má předplatné fakturovat: "none", "Usage" nebo "License".                                                                                                      |
| billingCycle         | řetězec                                                        | Určuje četnost, s jakou se má partner fakturovat v této objednávce. Podporované hodnoty jsou názvy členů nalezené v [**BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Získává nebo nastavuje hodnotu, která indikuje, jestli má předplatné k možnost nákupu doplňků.                                                                                             |
| Zkušební verze              | boolean                                                       | Hodnota, která označuje, zda se jedná o zkušební předplatné.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Hodnota, která označuje, zda se jedná o produkt společnosti Microsoft.                                                                                                                       |
| publisherName        | řetězec                                                        | Název vydavatele                                                                                                                                                           |
| akce              | pole řetězců                                              | Získá nebo nastaví akce, které jsou povoleny. Možné hodnoty: "Upravit", "Storno"                                                                                                  |
| partnerId            | řetězec                                                        | ID MPN prodejce záznamu používaného v modelu nepřímých partnerů.                                                                                                     |
| suspensionReasons    | pole řetězců                                              | Jen pro čtení. Pokud se předplatné pozastavilo, indikuje, proč.                                                                                                                  |
| contractType         | řetězec                                                        | Jen pro čtení. Typ kontraktu: "Subscription", "productKey" nebo "redemptionCode".                                                                                           |
| refundOptions        | pole prostředků [RefundOption](#refundoption)   | Jen pro čtení. Sada možností refundace dostupných pro toto předplatné.                                                                                              |
| odkazy                | [SubscriptionLinks](#subscriptionlinks)                       | Získá nebo nastaví odkazy na odběr.                                                                                                                                          |
| Seskup              | řetězec                                                        | ID pořadí, ve kterém bylo zahájeno předplatné.                                                                                                                |
| termDuration         | řetězec                                                        | ISO 8601 reprezentace doby trvání období. Aktuální podporované hodnoty jsou **P1M** (1 měsíc), **P1Y** (1 rok) a **P3Y** (3 roky).                                                        |
| atributy           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající předplatnému.                                                                                                                    |
| renewalTermDuration  | řetězec                                                        | ISO 8601 reprezentace doby trvání období. Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

Prostředek **SubscriptionLinks** popisuje kolekci odkazů připojených k prostředku předplatného.

| Vlastnost           | Typ                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Odkaz](utility-resources.md#link) | Získá nebo nastaví nabídku.               |
| parentSubscription | [Odkaz](utility-resources.md#link) | Získá nebo nastaví nadřazený odběr. |
| product            | [Odkaz](utility-resources.md#link) | Získá produkt přidružený k předplatnému. |
| skladové                | [Odkaz](utility-resources.md#link) | Získá skladovou položku produktu přidruženou k předplatnému. |
| dostupnosti       | [Odkaz](utility-resources.md#link) | Získá dostupnost SKU produktu přidružená k předplatnému. |
| activationLinks    | [Odkaz](utility-resources.md#link) | Získá seznam aktivačních odkazů přidružených k předplatnému. |
| samorozbalující               | [Odkaz](utility-resources.md#link) | Identifikátor URI samostatného.                         |
| generace               | [Odkaz](utility-resources.md#link) | Další stránka položek               |
| předchozí           | [Odkaz](utility-resources.md#link) | Předchozí stránka položek           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

Prostředek **SubscriptionProvisioningStatus** poskytuje informace o stavu zřizování předplatného.

| Vlastnost   | Typ                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | řetězec                                                         | Řetězec ve formátu GUID, který identifikuje SKU produktu.             |
| status     | řetězec                                                         | Označuje stav zřizování: "úspěch", "čeká na vyřízení" nebo "neúspěšné". |
| quantity   | číslo                                                         | Poskytuje množství předplatného po zřízení.               |
| endDate    | řetězec ve formátu data a času UTC                                 | Koncové datum předplatného.                                    |
| atributy | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atributy metadat.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

Prostředek **SubscriptionRegistrationStatus** popisuje kolekci odkazů připojených k prostředku předplatného.

| Vlastnost           | Typ                               | Description                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | řetězec                             | Identifikátor předplatného.                                                          |
| status             | řetězec                             | Určuje stav registrace: "registrované", "Register" nebo "notregistered".    |

## <a name="supportcontact"></a>SupportContact

Prostředek **SupportContact** představuje kontakt podpory pro předplatné zákazníka.

| Vlastnost        | Typ                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | řetězec                                                         | Řetězec ve formátu GUID, který označuje identifikátor tenanta kontaktu podpory. |
| supportMpnId    | řetězec                                                         | Identifikátor Microsoft Partner Network kontaktu (MPN).                       |
| name            | řetězec                                                         | Název kontaktu podpory                                                |
| odkazy           | [ResourceLinks](utility-resources.md#resourcelinks)            | Odkazy související s kontaktem podpory.                                              |
| atributy      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atributy metadat. Obsahuje "objectType": "SupportContact".              |

## <a name="registersubscription"></a>RegisterSubscription

Prostředek **RegisterSubscription** vrátí odkaz, který se dá použít k dotazování na stav registrace předplatného. Stav registrace se vrátí v těle odpovědi úspěšně přijaté žádosti o registraci předplatného Azure.

| Vlastnost                | Typ                               | Description                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Vrátí stavový kód HTTP 202 "přijato" s hlavičkou umístění obsahující odkaz na dotaz na stav registrace. Například `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"`. |

## <a name="refundoption"></a>RefundOption

Prostředek **RefundOption** představuje možnou možnost refundace pro předplatné.

| Vlastnost          | Typ | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| typ | řetězec | Typ refundace. Podporované hodnoty jsou "částečné" a "úplné". |
| expiresAfter      | řetězec ve formátu data a času UTC | Časové razítko, kdy tato možnost vyprší Pokud má hodnotu null, znamená to, že nemá žádné vypršení platnosti. |

## <a name="azureentitlement"></a>AzureEntitlement

Prostředek **AzureEntitlement** představuje nároky Azure na předplatné.

| Vlastnost          | Typ | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | řetězec | Identifikátor nároku |
| friendlyName      | řetězec | Popisný název oprávnění |
| status | řetězec | Stav oprávnění. |
| subscriptionId | řetězec | Identifikátor předplatného, ke kterému oprávnění patří. |
