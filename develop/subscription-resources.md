---
title: Prostředky předplatného
description: Prostředky předplatného mohou poskytovat další informace o předplatných v průběhu životního cyklu, jako jsou podpora, refundace nebo nároky Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35d8c86ab061797109b3c152eff02f354b7ea23a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547445"
---
# <a name="subscription-resources"></a>Prostředky předplatného

**Platí pro**: Partnerské centrum | Partnerské centrum provozovaný společností 21Vianet | Partnerské centrum pro Microsoft Cloud Germany | Partnerské centrum pro Microsoft Cloud for US Government

Předplatné umožňuje zákazníkovi používat službu po určitou dobu. Ne všechna pole se použijí pro všechna předplatná. Mnoho polí se používá pouze v určitých bodech životního cyklu, například v případě, že je předplatné pozastavené nebo zrušené.

## <a name="subscription"></a>Předplatné

>[!NOTE]
>U **prostředku předplatného** platí omezení rychlosti 500 požadavků za minutu na identifikátor tenanta.

Prostředek **Předplatné** představuje životní cyklus předplatného a zahrnuje vlastnosti, které definují stavy v průběhu životního cyklu předplatného.

| Vlastnost             | Typ                                                          | Description                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | řetězec                                                        | Identifikátor předplatného.                                                                                                                                                  |
| ID nabídky              | řetězec                                                        | Identifikátor nabídky.                                                                                                                                                         |
| entitlementId (ID nároku)        | řetězec                                                        | Identifikátor nároku (ID předplatného Azure).                                                                                                                        |
| název_nabídky            | řetězec                                                        | Název nabídky                                                                                                                                                               |
| Friendlyname         | řetězec                                                        | Popisný název předplatného definovaného partnerem, který pomáhá jednoznačně rozpoznat.                                                                                           |
| quantity             | číslo                                                        | Množství Například v případě fakturace na základě licencí je tato vlastnost nastavená na počet licencí.                                                            |
| Unittype             | řetězec                                                        | Jednotky definující množství pro předplatné.                                                                                                                             |
| PARENTSubscriptionId | řetězec                                                        | Získá nebo nastaví identifikátor nadřazeného předplatného.                                                                                                                              |
| datum vytvoření         | řetězec                                                        | Získá nebo nastaví datum vytvoření ve formátu data a času.                                                                                                                          |
| effectiveStartDate   | řetězec ve formátu data a času UTC                                | Získá nebo nastaví efektivní počáteční datum pro toto předplatné ve formátu data a času. Slouží k obnovení data migrovaných předplatných nebo k jeho sladění s jiným.                |
| datum ukončení závazku    | řetězec ve formátu data a času UTC                                | Koncové datum závazku pro toto předplatné ve formátu data a času. U předplatných, která není možné automaticky obnovit, představuje datum daleko do budoucna.       |
| status               | řetězec                                                        | Stav předplatného: žádné, Aktivní, Čekající, Pozastaveno nebo Odstraněno.                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Získá hodnotu určující, jestli se odběr obnovil automaticky.                                                                                                    |
| typ fakturace          | řetězec                                                        | Určuje, jak se předplatné účtuje: "žádné", "využití" nebo "licence".                                                                                                      |
| billingCycle         | řetězec                                                        | Určuje frekvenci, s jakou se partner účtuje za tuto objednávku. Podporované hodnoty jsou názvy členů, které najdete v [**části BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Získá nebo nastaví hodnotu určující, jestli má předplatné doplňky, které je možné koupit.                                                                                             |
| isTrial (aplikace isTrial)              | boolean                                                       | Hodnota určující, jestli se jedná o zkušební předplatné.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Hodnota, která určuje, jestli se jedná o produkt Microsoftu.                                                                                                                       |
| publisherName        | řetězec                                                        | Název vydavatele.                                                                                                                                                           |
| akce              | pole řetězců                                              | Získá nebo nastaví akce, které jsou povoleny. Možné hodnoty: edit (upravit), cancel (zrušit).                                                                                                  |
| ID partnera            | řetězec                                                        | ID MPN záznamu prodejce použitého v modelu nepřímého partnera.                                                                                                     |
| suspensionReasons    | pole řetězců                                              | Jen pro čtení. Pokud bylo předplatné pozastavené, indikuje důvod.                                                                                                                  |
| contractType (Typ kontraktu)         | řetězec                                                        | Jen pro čtení. Typ kontraktu: "subscription", "productKey" nebo "redemptionCode".                                                                                           |
| refundOptions        | pole prostředků [RefundOption](#refundoption)   | Jen pro čtení. Sada možností refundace, které jsou k dispozici pro toto předplatné.                                                                                              |
| Odkazy                | [Odkazy na předplatné](#subscriptionlinks)                       | Získá nebo nastaví odkazy na předplatné.                                                                                                                                          |
| Kódobjednávky              | řetězec                                                        | ID objednávky, která byla umístěna za účelem zahájení odběru.                                                                                                                |
| termDuration         | řetězec                                                        | ISO 8601 reprezentace doby trvání období. Aktuální podporované hodnoty jsou **P1M** (1 měsíc), **P1Y** (1 rok) a **P3Y** (3 roky).                                                        |
| atributy           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atributy metadat odpovídající předplatnému.                                                                                                                    |
| renewalTermDuration  | řetězec                                                        | ISO 8601 reprezentace doby trvání období. Aktuální podporované hodnoty jsou **P1M** (1 měsíc) a **P1Y** (1 rok).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

Prostředek **SubscriptionLinks** popisuje kolekci odkazů připojených k prostředku předplatného.

| Vlastnost           | Typ                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Propojit](utility-resources.md#link) | Získá nebo nastaví nabídku.               |
| parentSubscription | [Propojit](utility-resources.md#link) | Získá nebo nastaví nadřazený odběr. |
| product            | [Propojit](utility-resources.md#link) | Získá produkt přidružený k předplatnému. |
| skladové                | [Propojit](utility-resources.md#link) | Získá skladovou položku produktu přidruženou k předplatnému. |
| dostupnosti       | [Propojit](utility-resources.md#link) | Získá dostupnost SKU produktu přidružená k předplatnému. |
| activationLinks    | [Propojit](utility-resources.md#link) | Získá seznam aktivačních odkazů přidružených k předplatnému. |
| samorozbalující               | [Propojit](utility-resources.md#link) | Identifikátor URI pro sebe.                         |
| generace               | [Propojit](utility-resources.md#link) | Další stránka položek               |
| předchozí           | [Propojit](utility-resources.md#link) | Předchozí stránka položek           |

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
| status             | řetězec                             | Určuje stav registrace: "registrované", "registrace" nebo "notregistered".    |

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
