---
title: Prostředky předplatného
description: Prostředky předplatného můžou poskytovat další informace o předplatných v průběhu životního cyklu, jako je podpora, refundace, nároky na Azure.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c898f9673525cf0ba32619b7c7b16f91311a81c7
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456804"
---
# <a name="subscription-resources"></a>Prostředky předplatného

**Platí pro**: partnerské Centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Německo | Partnerské centrum pro Microsoft Cloud for US Government

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
| status               | řetězec                                                        | Stav předplatného: "žádná", "aktivní", "čeká", "pozastaveno", "prošlo" nebo "odstraněno".                                                                                                         |
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
| termDuration         | řetězec                                                        | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc), **P1Y** (1 rok) a **P3Y** (3 roky).                                                        |
| atributy           | [Atributy prostředků](utility-resources.md#resourceattributes) | Atributy metadat odpovídající předplatnému.                                                                                                                    |
| renewalTermDuration  | řetězec                                                        | Reprezentace doby trvání období podle STANDARDu ISO 8601. Aktuální podporované hodnoty jsou **P1M (1** měsíc) a **P1Y** (1 rok).                                                        |
| Typ produktu  | [Itemtype](product-resources.md#itemtype)                             | Jen pro čtení. Typ produktu, pro který se předplatné používá.     |

## <a name="subscriptionlinks"></a>Odkazy na předplatné

Prostředek **SubscriptionLinks** popisuje kolekci odkazů připojených k prostředku předplatného.

| Vlastnost           | Typ                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Odkaz](utility-resources.md#link) | Získá nebo nastaví nabídku.               |
| parentSubscription (nadřazenépředřazení) | [Odkaz](utility-resources.md#link) | Získá nebo nastaví nadřazené předplatné. |
| product            | [Odkaz](utility-resources.md#link) | Získá produkt přidružený k předplatnému. |
| Sku                | [Odkaz](utility-resources.md#link) | Získá SKU produktu přidružené k předplatnému. |
| dostupnosti       | [Odkaz](utility-resources.md#link) | Získá dostupnost SKU produktu přidruženou k předplatnému. |
| aktivační odkazy    | [Odkaz](utility-resources.md#link) | Získá seznam aktivačních odkazů přidružených k předplatnému. |
| Vlastní               | [Odkaz](utility-resources.md#link) | Identifikátor URI sebe sama.                         |
| Další               | [Odkaz](utility-resources.md#link) | Další stránka položek               |
| Předchozí           | [Odkaz](utility-resources.md#link) | Předchozí stránka položek           |

## <a name="subscriptionprovisioningstatus"></a>Stav zřizování předplatného

Prostředek **SubscriptionProvisioningStatus** poskytuje informace o stavu zřizování předplatného.

| Vlastnost   | Typ                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| ID SKU      | řetězec                                                         | Řetězec ve formátu GUID, který identifikuje SKU produktu.             |
| status     | řetězec                                                         | Označuje stav zřizování: "success", "pending" nebo "failed". |
| quantity   | číslo                                                         | Poskytuje množství předplatných po zřízení.               |
| Enddate    | řetězec ve formátu data a času UTC                                 | Koncové datum odběru.                                    |
| atributy | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat.                                             |

## <a name="subscriptionregistrationstatus"></a>Stav registrace předplatného

Prostředek **SubscriptionRegistrationStatus** popisuje kolekci odkazů připojených k prostředku předplatného.

| Vlastnost           | Typ                               | Description                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | řetězec                             | Identifikátor předplatného.                                                          |
| status             | řetězec                             | Označuje stav registrace: "registered", "registering" nebo "notregistered".    |

## <a name="supportcontact"></a>PodporaKontakt

Prostředek **SupportContact** představuje kontakt podpory pro předplatné zákazníka.

| Vlastnost        | Typ                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | řetězec                                                         | Řetězec ve formátu GUID, který označuje identifikátor tenanta kontaktu podpory. |
| supportMpnId    | řetězec                                                         | Identifikátor MPN (Microsoft Partner Network) kontaktu.                       |
| name            | řetězec                                                         | Název kontaktu podpory.                                                |
| Odkazy           | [Odkazy na prostředky](utility-resources.md#resourcelinks)            | Odkazy související s kontaktem podpory.                                              |
| atributy      | [Atributy prostředků](utility-resources.md#resourceattributes)  | Atributy metadat. Obsahuje objectType: SupportContact.              |

## <a name="registersubscription"></a>RegisterSubscription

Prostředek **RegisterSubscription** vrátí odkaz, který můžete použít k dotazování stavu registrace předplatného. Stav registrace se vrátí v textu odpovědi úspěšného přijatého požadavku na registraci předplatného Azure.

| Vlastnost                | Typ                               | Description                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Vrátí stavový kód HTTP 202 Přijato s hlavičkou Location obsahující odkaz na dotaz na stav registrace. Například `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"`. |

## <a name="refundoption"></a>RefundOption

Prostředek **RefundOption** představuje možnou možnost refundace pro předplatné.

| Vlastnost          | Typ | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| typ | řetězec | Typ refundace Podporované hodnoty jsou Partial (Částečná) a Full (Úplné). |
| expiresAfter      | řetězec ve formátu data a času UTC | Časové razítko, kdy vyprší platnost této možnosti. Pokud má hodnotu null, znamená to, že nemá žádné vypršení platnosti. |

## <a name="azureentitlement"></a>AzureEnti pro správu

Prostředek **AzureEnti pro předplatné** představuje nároky Azure.

| Vlastnost          | Typ | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | řetězec | Identifikátor nároku |
| Friendlyname      | řetězec | Popisný název nároku. |
| status | řetězec | Stav nároku |
| subscriptionId | řetězec | Identifikátor předplatného, do které nárok patří. |
